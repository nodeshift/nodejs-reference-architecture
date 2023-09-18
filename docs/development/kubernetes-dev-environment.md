# Kubernetes-based Development Environment Recommendations

Development and local-testing flows should ideally be the same for all the developers of a project, but its
common for developers on a team to have heterogenous development platforms (i.e. Linux, Intel-based MacOS, M1-based MacOS, Windows).
Using kubernetes as a homogenized execution/configuration layer can be key to ensure testing/deployment
use the same configuration settings for all developers.  Building a docker image is the same "docker build ..." command
regardless of development platform, and kubernetes configuration settings, ideally built through yaml configuration files and 
helm charts, are platform independent.

In the past the most common approach for building/running containers on Windows and MacOS
was docker desktop. Now that docker desktop is no longer free, development teams are exploring other
options which include:
* Virtualbox with a linux VM (the disadvantage is that this requires developers to become more
  familiar with Linux). Docker client is still free and it can connect to a remove virtual
  machine.  However, this has not worked well with recent versions of MacOS Ventura.
* podman and podman desktop which provides similar functionality to docker desktop but is
  open source and free.  The podman virtual machine does have two stability issues (it doesn't resync its
  clock after a sleep) and sometimes the minikube client on it becomes unresponsive, but usually it can run for multiple
  days before that happens.  Often, is fastest to just delete/rebuild the podman virtual machine, which can take 5-10 minutes.

# Sharing development-zone configurations
When developing microservices within a multi-microservice app, its ideal for the microservice architecture to not require all the
microservices to be deployed locally, just the microservices and databases/queues a specific microservice depends upon.  When it comes to
supporting a local kubernetes running your development/tests, having a microservice only needing to rely upon a 3-6 pods vs. 15+ is key to
fitting within a 8Gb memory footprint for your kubernetes deployment.  Another powerful trick is to identify those dependent services that
provide stateless support, in that functional calls to them are stateless where they are deployed, such as identity-lookup/token-exchange
APIs, and utilize the deployments in your shared development-zone cluster (what is deployed to when your Git PRs are merged) for your
local-microservice needs.  If your microservice APIs have to support multiple tenants/organizations, it is recommended that your 
development-zone cluster and local cluster share definitions of test users and organizations, but DO NOT share them with other CI pipeline
clusters. Specifically, test org display-names can still be the same in other clusters, but the guids and credentials for them should be
different.

We've had good success with defining our configurations for microservices in a hierarchical set of yaml files where the overrides
work in ascending order:
1. cross-zone app-generic settings,
2. cross-zone app-specific settings,
3. zone-specific app-generic settings,
4. zone-specific app-specific settings,
5. **local development settings (if local)**

This structure helps avoid redundancy of configuration settings and also allows our local development yaml to just override a few settings
like external hostnames and references to local databases/queues but otherwise inherit our 'development' zone settings.  Typically, this
hierarchy above is established by the order of yaml includes into the helm template (or helm deploy) command.  Example command:
```
helm template ../helm-charts/app1 --name-template app1-dev --output-dir ../kubectl-specs/dev --namespace dev -f ../k8s-yamls/common.yaml -f ../k8s-yamls/app1.common.yaml -f ../k8s-yamls/dev/common.yaml -f ../k8s-yamls/dev/app1.yaml -f ../k8s-yamls/local/common.yaml -f ../k8s-yamls/local/app1.yaml
```

# Replicating non-stateless DBs/queues locally
If possible, avoid using shared databases and use local k8s deployments of the databases/queues to avoid test case collision between 
developers. As long as you are careful to make sure your development zone does not contain customer data, then making backups of your 
development databases and loading those backups in local development copies can help speed up your testcase creation process and 
leverage "end to end" tests that may use such data.  It's common to use public helm charts (or make a copy of them) to deploy these
databases in your local or CI/CD environments.  Example charts:
 * Minio to locally replicate S3 APIs and storage: https://github.com/minio/minio/tree/master/helm/minio
 * A huge selection of others can be found from Bitnami's collection at https://github.com/bitnami/charts/tree/main/bitnami

# Doing interactive nodejs debugging in containers
The kubernetes pod's spec.containers.args field can be configured in a helm chart to conditionally override of the primary command the 
container uses when starting up.  This can be used to then override the regular node (my-app-entry).js command to also pass in the 
--inspect-brk flag, making the node (or nodemon) process wait for a remote debugger connection after starting up.  Remember, the same 
yaml-config value used to turn on this debugging mode should also be used to disable liveness/readiness checks in the pod, or else the pod 
will get restarted by such checks.  One can then use the "kubectl port-forward" command to establish a tunnel to the remote-debug port the 
nodejs process is listening to.  IDE's like Visual Studio Code can then connect to that tunnel-port to reach the backend nodejs process you 
want to interactively debug.

# Using nodemon in local containers
Similar to changing the startup command to set the --inspect-brk flag, local containers can also replace node with 'nodemon'.  Nodemon is
like node, but watches if any of the source .js files change and restart after second or two after changes have stabilized.  This can 
allow developers to modify the js code running on a container without having to rebuild and redeploy the container.  Docker build caching 
helps to accelerate the re-build process, but just copying over a few changed files can save 30 seconds or so in the iteration process.
Nodemon should NEVER be used in production but it's fine to be installed but unused in a production image.

Here is a sample bash shell script to copy over the updated .ts file and re-run 'tsc' in the deployed container, which often only takes 
about 5 seconds to run:
```
updatePod(){
  POD_NAME="$1"
  echo "*****UPDATING POD: $POD_NAME******"
  LAST_BUILD_TIMESTAMP=`kubectl exec -n $NAME_SPACE $POD_NAME -- ls --full-time $DOCKER_WORKDIR/$MAIN_BUILT_FILE | awk '{ print \$6, \$7 }'`
  echo "LAST_BUILD_TIMESTAMP = $LAST_BUILD_TIMESTAMP"
  LAST_BUILD_IN_SECONDS=`kubectl exec -n $NAME_SPACE $POD_NAME -- date +%s -d"$LAST_BUILD_TIMESTAMP"`
  echo "LAST_BUILD_IN_SECONDS = $LAST_BUILD_IN_SECONDS"
  NOW_IN_SECONDS=`kubectl exec -n $NAME_SPACE $POD_NAME -- date +%s`
  echo "NOW_IN_SECONDS = $NOW_IN_SECONDS"
  SECONDS_SINCE_LAST_BUILD=$(( $NOW_IN_SECONDS - $LAST_BUILD_IN_SECONDS ))
  echo "Last build was $SECONDS_SINCE_LAST_BUILD seconds ago"

  # now iterate through source dirs
  export UPDATES_MADE=false
  declare -a SOURCE_DIRS_ARRAY=($SOURCE_DIRS)
  for SOURCE_DIR in "${SOURCE_DIRS_ARRAY[@]}"
  do
    UPDATED_FILES=`find ${SOURCE_DIR} -type f -newerct "${SECONDS_SINCE_LAST_BUILD} seconds ago"`
    echo "UPDATED_FILES = $UPDATED_FILES"
    if [[ "$UPDATED_FILES" ]]; then
      export UPDATES_MADE=true
      declare -a UPDATED_FILES_ARRAY=($UPDATED_FILES)
      for UPDATED_FILE in "${UPDATED_FILES_ARRAY[@]}"
      do
        echo "copying in $UPDATED_FILE into ${POD_NAME}..."
        kubectl cp $UPDATED_FILE $NAME_SPACE/$POD_NAME:$DOCKER_WORKDIR/$UPDATED_FILE
      done
    fi
  done

  if [[ "$UPDATES_MADE" == "true" ]]; then
    kubectl exec -n $NAME_SPACE $POD_NAME -- npm run build
    kubectl exec -n $NAME_SPACE $POD_NAME -- touch $MAIN_BUILT_FILE
    echo "npm run build  - finished inside $POD_NAME"
  else
    echo "No updates found, npm run build not executed in $POD_NAME"
  fi
}
```

# Extracting test results from Kubernetes pods
So just like how debugger flags and nodemon can be conditionally turned on in a pod deployment, the same goes for starting a unit + 
integration test run.  When doing this, one should run nyc around the execution of the unit + integration tests to capture the code 
coverage from the combination of the two types of tests.  However, one can't have the pod test-script immediately finish once the test 
finishes, or else the test results will disappear when the test pod shuts down.  Normally, local developer testing can then just look at 
the logs of the shutdown pod to see if it was successful or not, but when debugging failures in a CI/CD pipeline like Travis/Jenkins, its 
very useful to run the same logic locally on one's development system, and those flows will typically need the full test result files.

There are two general solutions for this:
* For tests run in a non-production environment like minikube, a kubernetes Physical Volume (PV) can be created and
and mounted in the test container for the post-test script to copy its result files into.  The higher level test-logic flow on one's
development system (or CI/CD engine like Travis/Jenkins) can then copy out the test result and coverage files. 

* Utilize a state-handshake between the high level test scripting (eg. Travis/Jenkins/laptop shell) and the process in the
test pod.  This can be done with a file in the pod, where the test scripting writes the process return-code from the tests to that file and
loops (i.e. stays alive) until the file is deleted.  Example post-test script logic in the test-pod:
  ```
  ; TEST_RESULT=$?; echo $TEST_RESULT > /tmp/test.report.generated.semaphore; echo 'Waiting for test reports to be fetched...'; (while [ -f /tmp/test.report.generated.semaphore ]; do sleep 2; done); echo 'Test reports pulled!'; exit $TEST_RESULT
  ```
  The parent layer can then use "kubectl exec ... -- ls /tmp/test.report.generated.semaphore" to check for the presence of the semaphore file 
  that tells when tests finished.  It can then copy out the results with "kubectl cp ...", and delete the semaphore file with "kubectl exec 
  ... -- rm /tmp/test.report.generated.semaphore"
