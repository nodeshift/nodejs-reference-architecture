---
sidebar_position: 7
---
# Choosing and vetting dependencies

Node.js applications and modules often use a number of third party
dependencies. It is important that you choose those dependencies
carefully and regularly validate that they continue to be good
choices.

## Recommended Components

N/A

## Guidance

Based on the teams experience we recommend the following:

* Check what is already being used within your organization. Your
  organization may already have a reference architecture or something
  similar that can help you find modules that your organization has
  already had a good experience with or decided are good choices.
* Limit dependencies to the minimum required
  * prefer dependencies with limited or no dependencies of their own
  * avoid one-liners, is using the modules really saving you time 
    development/maintenance time versus incorporating your own code?
* Prefer dependencies that already have a reasonable level of usage 
  based on github star count and npm usage count. Compare usage
  to other possible options.
* Prefer dependencies with an active, open, and inclusive community. 
  Note that in some cases a dependency may be "done" but open and 
  inclusive is still important in those cases. Some
  indicators to consider include:
  * Number of active contributors since inception
  * If you needed to contribute a fix would it be accepted?
  * How long does it take for CVEs to get addressed?
  * Do you have to move up to a new Major release to get security fixes?
  * What is the cadence of releases?
  * Is the project part of a larger project or Foundation?
* Prefer dependencies aligned with the Node.js project releases
  * Does it support the current Node.js LTS releases
  * Is the dependency tested by the Node.js project's
    [Canary in the Gold Mine](https://github.com/nodejs/citgm)?
  * If the dependency is a native module does it use Node-API (use
    of Node-API means that packages can work across Node.js major versions)
* Only use dependencies with licenses acceptable to your organization
* When choosing to use dependencies with a lower level of use in the 
  ecosystem doing a code review to look for red flags can be useful.

When evaluating dependencies, the teams typically evaluate the top level
dependencies versus the full tree **EXCEPT** for the following in which
we evaluate the full tree:
* License Checks
* Security vulnerabilities (CVEs)
Total number of sub-dependencies

The Red Hat Node.js team is currently using
[npcheck](https://github.com/nodeshift/npcheck)
to help review packages based on some of the suggestions above.
