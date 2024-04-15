# npcheck review - April 15 2024

No major concerns were noted in this review.

## Diff in npcheck.json since last review 

Only change was to move the location of node-rdkafka in the file, no 
material change.

diff --git a/npcheck.json b/npcheck.json
index d220594..1f65eff 100644
--- a/npcheck.json
+++ b/npcheck.json
@@ -1,5 +1,15 @@
 {
   "modules": [
+    {
+      "name": "node-rdkafka",
+      "npmlink": "https://www.npmjs.com/package/node-rdkafka",
+      "reviewlevel": "Active Watch",
+      "activitycurrent": "None",
+      "activitytarget": "Tested and Verified",
+      "section": [
+        "Message Queuing"
+      ]
+    },
     {
       "name": "cldr-localenames-full",
       "npmLink": "https://npmjs.com/package/cldr-localenames-full",
@@ -115,16 +125,6 @@
         "Message Queuing"
       ]
     },
-    {
-      "name": "node-rdkafka",
-      "npmlink": "https://www.npmjs.com/package/node-rdkafka",
-      "reviewlevel": "Active Watch",
-      "activitycurrent": "None",
-      "activitytarget": "Tested and Verified",
-      "section": [
-        "Message Queuing"
-      ]
-    },
     {
       "name": "opossum",
       "npmlink": "https://www.npmjs.com/package/opossum",


## Results

https://github.com/nodeshift/nodejs-reference-architecture/actions/runs/8695409976

npcheck report

```shell
(1): The module "node-rdkafka" seems to have no available TypeScript typings.
(2): The "cldr-localenames-full" seems that is lacking appropriate testing (https://www.github.com/unicode-cldr/cldr-json)
(3): The module "cldr-localenames-full" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(4): The module "cldr-localenames-full" seems to have no available TypeScript typings.
(5): The module "eslint" seems to have no available TypeScript typings.
(6): The module "eslint" has "87" dependencies (including sub-dependencies) which is more than the default "20".
(7): The module "express" seems to have no available TypeScript typings.
(8): The module "express" has "62" dependencies (including sub-dependencies) which is more than the default "20".
(9): The module "express-prom-bundle" has "80" dependencies (including sub-dependencies) which is more than the default "20".
(10): The latest release of "ibmcloud-appid" was about 1 year ago
(11): The module "ibmcloud-appid" has "227" dependencies (including sub-dependencies) which is more than the default "20".
(12): The module "i18next" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(13): The module "i18next" is not tested by community CITGM runs.
(14): The latest release of "i18next-icu" was about 1 year ago
(15): The module "i18next-icu" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(16): The module "i18next-http-middleware" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(17): The module "i18next-fs-backend" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(18): The latest release of "ioredis" was about 1 year ago
(19): The module "ioredis" is not tested by community CITGM runs.
(20): The module "opossum" seems to have no available TypeScript typings.
(21): The module "passport" seems to have no available TypeScript typings.
(22): The module "pino" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(23): The module "pino" has "22" dependencies (including sub-dependencies) which is more than the default "20".
(24): The latest release of "rhea" was about 1 year ago
(25): The module "rhea" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(26): The module "mocha" seems to have no available TypeScript typings.
(27): The module "mocha" has "69" dependencies (including sub-dependencies) which is more than the default "20".
(28): The "jest" seems that is lacking appropriate testing (https://www.github.com/jestjs/jest)
(29): The module "jest" has "261" dependencies (including sub-dependencies) which is more than the default "20".
(30): The module "@ibm-cloud/cloudant" has "97" dependencies (including sub-dependencies) which is more than the default "20".
(31): The module "nano" has "25" dependencies (including sub-dependencies) which is more than the default "20".
(32): The latest release of "odbc" was 11 months ago
(33): The module "odbc" has "57" dependencies (including sub-dependencies) which is more than the default "20".
(34): The module "ibm_db" seems to have no available TypeScript typings.
(35): The module "ibm_db" has "45" dependencies (including sub-dependencies) which is more than the default "20".
(36): The module "mongodb" is not tested by community CITGM runs.
(37): The module "pg" seems to have no available TypeScript typings.
(38): The module "pg" is not tested by community CITGM runs.
(39): The latest release of "kafkajs" was about 1 year ago
(40): The "@openapitools/openapi-generator-cli" seems that is lacking appropriate testing (https://www.github.com/OpenAPITools/openapi-generator-cli)
(41): The module "@openapitools/openapi-generator-cli" seems to have no available TypeScript typings.
(42): The module "@openapitools/openapi-generator-cli" has "107" dependencies (including sub-dependencies) which is more than the default "20".
(43): The module "openapi-backend" has "35" dependencies (including sub-dependencies) which is more than the default "20".
(44): The module "@stoplight/prism-cli" is not tested by community CITGM runs.
(45): The module "@stoplight/prism-cli" has "176" dependencies (including sub-dependencies) which is more than the default "20".
(46): The module "express-openapi-validator" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(47): The module "express-openapi-validator" has "55" dependencies (including sub-dependencies) which is more than the default "20".
(48): The module "swagger-editor" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(49): The module "swagger-editor" seems to have no available TypeScript typings.
(50): The module "swagger-editor" has "375" dependencies (including sub-dependencies) which is more than the default "20".
(51): The latest release of "openapi-editor" was over 3 years ago
(52): The module "openapi-editor" has "200" dependencies (including sub-dependencies) which is more than the default "20".
(53): The latest release of "nyc" was almost 4 years ago
(54): The module "nyc" seems to have no available TypeScript typings.
(55): The module "nyc" is not tested by community CITGM runs.
(56): The module "nyc" has "145" dependencies (including sub-dependencies) which is more than the default "20".
(57): The module "dotenv" is not tested by community CITGM runs.
(58): The latest release of "node-vault" was 9 months ago
(59): The module "node-vault" seems to have no available TypeScript typings.
(60): The module "node-vault" is not tested by community CITGM runs.
(61): The module "node-vault" has "59" dependencies (including sub-dependencies) which is more than the default "20".
(62): The module "@ibm-cloud/secrets-manager" seems to have no available TypeScript typings.
(63): The module "@ibm-cloud/secrets-manager" is not tested by community CITGM runs.
(64): The module "@ibm-cloud/secrets-manager" has "96" dependencies (including sub-dependencies) which is more than the default "20".
(65): The module "@opentelemetry/sdk-trace-base" is not tested by community CITGM runs.
(66): The module "@opentelemetry/sdk-trace-node" is not tested by community CITGM runs.
(67): The module "axios" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(68): The module "axios" is not tested by community CITGM runs.
(69): The latest release of "node-fetch" was 8 months ago
(70): The module "node-fetch" is not tested by community CITGM runs.
(71): The latest release of "cors" was over 5 years ago
(72): The module "cors" seems to have no available TypeScript typings.
(73): The module "cors" is not tested by community CITGM runs.

problems: 73 (errors: 0 - warnings: 73)
```

New (materially) since last review (excluding ones were # deps was already over limit and changed):
```
None
```
## Notes

There were releases of both express and mocha in the last 3 months with these from the last report
no longer being reported
* (6): The latest release of "express" was over 1 year ago
* (28): The latest release of "mocha" was about 1 year ago

A few modules are `aging` in terms of the last release. Not necessariliy something to worry about
yet but worth keeping an eye on (ioredis and kafkajs in particular).

Aging
(14): The latest release of "i18next-icu" was about 1 year ago
(18): The latest release of "ioredis" was about 1 year ago
(32): The latest release of "odbc" was 11 months ago
(39): The latest release of "kafkajs" was about 1 year ago
(53): The latest release of "nyc" was almost 4 years ago
