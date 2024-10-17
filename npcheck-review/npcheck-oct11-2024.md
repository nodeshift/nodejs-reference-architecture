# npcheck review - October 11 2024



## Diff in npcheck.json since last review

```shell
@@ -498,7 +498,7 @@
diff --git a/npcheck.json b/npcheck.json
index 1f65eff..761845b 100644
--- a/npcheck.json
+++ b/npcheck.json
@@ -450,7 +450,9 @@
       "BSD-3-Clause",
       "Unlicense",
       "WTFPL",
-      "Unicode-DFS-2016"
+      "Unicode-DFS-2016",
+      "Unicode-3.0",
+      "BlueOak-1.0.0"
     ],
     "rules": {
       "ioredis": {
@@ -496,7 +498,7 @@
       "swagger-editor": {
         "note": "Multiple dependencies use licenses",
         "note": "depends on jsonify which is under Public Domain",
-        "allow": ["Python-2.0","0BSD", "Public Domain"]
+        "allow": ["Python-2.0","0BSD", "Public Domain", "CC0-1.0"]
       },
       "@stoplight/prism-cli":{
         "note": "dependency tslib@2.3.1 reports 0BSD which is less restrictive than BSD",
```

## Results

https://github.com/nodeshift/nodejs-reference-architecture/actions/runs/11197720660


NPCheck Report

```shell
NPCheck Report
(1): The module "node-rdkafka" seems to have no available TypeScript typings.
(2): The "cldr-localenames-full" seems that is lacking appropriate testing (https://www.github.com/unicode-cldr/cldr-json)
(3): The module "cldr-localenames-full" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(4): The module "cldr-localenames-full" seems to have no available TypeScript typings.
(5): The module "eslint" has "83" dependencies (including sub-dependencies) which is more than the default "20".
(6): The module "express" seems to have no available TypeScript typings.
(7): The module "express" has "62" dependencies (including sub-dependencies) which is more than the default "20".
(8): The latest release of "express-prom-bundle" was 9 months ago
(9): The module "express-prom-bundle" has "80" dependencies (including sub-dependencies) which is more than the default "20".
(10): The latest release of "ibmcloud-appid" was over 1 year ago
(11): The module "ibmcloud-appid" has "226" dependencies (including sub-dependencies) which is more than the default "20".
(12): The module "i18next" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(13): The module "i18next" is not tested by community CITGM runs.
(14): The latest release of "i18next-icu" was over 1 year ago
(15): The module "i18next-icu" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(16): The module "i18next-http-middleware" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(17): The module "i18next-fs-backend" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(18): The module "ioredis" is not tested by community CITGM runs.
(19): The module "opossum" seems to have no available TypeScript typings.
(20): The latest release of "passport" was 11 months ago
(21): The module "passport" seems to have no available TypeScript typings.
(22): The module "pino" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(23): The module "pino" has "22" dependencies (including sub-dependencies) which is more than the default "20".
(24): The module "rhea" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(25): The module "lru-cache" has no support for the LTS version(s) 18.20.4 of Node.js.
(26): The module "mocha" seems to have no available TypeScript typings.
(27): The module "mocha" has "69" dependencies (including sub-dependencies) which is more than the default "20".
(28): The "jest" seems that is lacking appropriate testing (https://www.github.com/jestjs/jest)
(29): The module "jest" has "260" dependencies (including sub-dependencies) which is more than the default "20".
(30): The module "@ibm-cloud/cloudant" has "54" dependencies (including sub-dependencies) which is more than the default "20".
(31): The module "nano" has "25" dependencies (including sub-dependencies) which is more than the default "20".
(32): The module "odbc" has "56" dependencies (including sub-dependencies) which is more than the default "20".
(33): The latest release of "ibm_db" was 6 months ago
(34): The module "ibm_db" seems to have no available TypeScript typings.
(35): The module "ibm_db" has "45" dependencies (including sub-dependencies) which is more than the default "20".
(36): The module "mongodb" is not tested by community CITGM runs.
(37): The module "pg" seems to have no available TypeScript typings.
(38): The module "pg" is not tested by community CITGM runs.
(39): The latest release of "kafkajs" was over 1 year ago
(40): The module "@openapitools/openapi-generator-cli" depends on the "path-scurry@1.11.1" package which is under the non-acceptable license "BlueOak-1.0.0". - ERROR
(41): The "@openapitools/openapi-generator-cli" seems that is lacking appropriate testing (https://www.github.com/OpenAPITools/openapi-generator-cli)
(42): The module "@openapitools/openapi-generator-cli" seems to have no available TypeScript typings.
(43): The module "@openapitools/openapi-generator-cli" has "109" dependencies (including sub-dependencies) which is more than the default "20".
(44): The module "openapi-backend" has "34" dependencies (including sub-dependencies) which is more than the default "20".
(45): The module "@stoplight/prism-cli" is not tested by community CITGM runs.
(46): The module "@stoplight/prism-cli" has "174" dependencies (including sub-dependencies) which is more than the default "20".
(47): The module "express-openapi-validator" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(48): The module "express-openapi-validator" has "108" dependencies (including sub-dependencies) which is more than the default "20".
(49): The module "swagger-editor" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(50): The module "swagger-editor" seems to have no available TypeScript typings.
(51): The module "swagger-editor" has "375" dependencies (including sub-dependencies) which is more than the default "20".
(52): The latest release of "openapi-editor" was almost 4 years ago
(53): The module "openapi-editor" has "196" dependencies (including sub-dependencies) which is more than the default "20".
(54): The module "nyc" seems to have no available TypeScript typings.
(55): The module "nyc" is not tested by community CITGM runs.
(56): The module "nyc" has "141" dependencies (including sub-dependencies) which is more than the default "20".
(57): The latest release of "dotenv" was 8 months ago
(58): The module "dotenv" is not tested by community CITGM runs.
(59): The latest release of "node-vault" was about 1 year ago
(60): The module "node-vault" seems to have no available TypeScript typings.
(61): The module "node-vault" is not tested by community CITGM runs.
(62): The module "node-vault" has "59" dependencies (including sub-dependencies) which is more than the default "20".
(63): The module "@ibm-cloud/secrets-manager" seems to have no available TypeScript typings.
(64): The module "@ibm-cloud/secrets-manager" is not tested by community CITGM runs.
(65): The module "@ibm-cloud/secrets-manager" has "53" dependencies (including sub-dependencies) which is more than the default "20".
(66): The module "@opentelemetry/sdk-trace-base" is not tested by community CITGM runs.
(67): The module "@opentelemetry/sdk-trace-node" is not tested by community CITGM runs.
(68): The module "axios" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(69): The module "axios" is not tested by community CITGM runs.
(70): The latest release of "node-fetch" was about 1 year ago
(71): The module "node-fetch" is not tested by community CITGM runs.
(72): The latest release of "cors" was almost 6 years ago
(73): The module "cors" seems to have no available TypeScript typings.
(74): The module "cors" is not tested by community CITGM runs.

problems: 74 (errors: 1 - warnings: 73)
```


New (materially) since last review (excluding ones were # deps was already over limit and changed):
```
None
```
## Notes

There was a release of Helmet since the last report.  It had been 8 months since the last one

There was a release of Helmet since the last report.  It had been 7 months since the last one

There was a release of Helmet since the last report.  It had been 8 months since the last one

(40): The module "@openapitools/openapi-generator-cli" depends on the "path-scurry@1.11.1" package which is under the non-acceptable license "BlueOak-1.0.0". - ERROR

The latest release of `@openapitools/openapi-generator-cli` added the `glob` module which includes `path-scurry` which had a license(BlueOak-1.0.0) that was not in the list.  It has now been added to the list.  The "Due Dilligence" action is now green after adding this in.

The latest release of swagger-editor depends on react-syntax-highlighter, which just added a new dependecy, highlightjs-vue, which has a license that was not previously in the list(CC0-1.0)

A few modules are `aging` in terms of the last release. Not necessariliy something to worry about yet but worth keeping an eye on

Aging
((20): The latest release of "passport" was 11 months ago
(59): The latest release of "node-vault" was about 1 year ago
(70): The latest release of "node-fetch" was about 1 year ago

