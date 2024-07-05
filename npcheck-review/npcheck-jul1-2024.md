# npcheck review - July 1 2024



## Diff in npcheck.json since last review

```shell
diff --git a/npcheck.json b/npcheck.json
index 1f65eff..dba4bca 100644
--- a/npcheck.json
+++ b/npcheck.json
@@ -450,7 +450,8 @@
       "BSD-3-Clause",
       "Unlicense",
       "WTFPL",
-      "Unicode-DFS-2016"
+      "Unicode-DFS-2016",
+      "Unicode-3.0"
     ],
     "rules": {
       "ioredis": {
```

## Results

https://github.com/nodeshift/nodejs-reference-architecture/actions/runs/9746832658


NPCheck Report

```shell
(1): The module "node-rdkafka" seems to have no available TypeScript typings.
(2): The module "cldr-localenames-full" is under the non-acceptable license(s) "Unicode-3.0". - ERROR
(3): The module "cldr-localenames-full" depends on the "cldr-core@45.0.0" package which is under the non-acceptable license "Unicode-3.0". - ERROR
(4): The "cldr-localenames-full" seems that is lacking appropriate testing (https://www.github.com/unicode-cldr/cldr-json)
(5): The module "cldr-localenames-full" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(6): The module "cldr-localenames-full" seems to have no available TypeScript typings.
(7): The module "eslint" seems to have no available TypeScript typings.
(8): The module "eslint" has "87" dependencies (including sub-dependencies) which is more than the default "20".
(9): The module "express" seems to have no available TypeScript typings.
(10): The module "express" has "62" dependencies (including sub-dependencies) which is more than the default "20".
(11): The module "express-prom-bundle" has "80" dependencies (including sub-dependencies) which is more than the default "20".
(12): The latest release of "helmet" was 8 months ago
(13): The latest release of "ibmcloud-appid" was over 1 year ago
(14): The module "ibmcloud-appid" has "227" dependencies (including sub-dependencies) which is more than the default "20".
(15): The module "i18next" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(16): The module "i18next" is not tested by community CITGM runs.
(17): The latest release of "i18next-icu" was about 1 year ago
(18): The module "i18next-icu" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(19): The module "i18next-http-middleware" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(20): The latest release of "i18next-fs-backend" was 7 months ago
(21): The module "i18next-fs-backend" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(22): The module "ioredis" is not tested by community CITGM runs.
(23): The module "opossum" seems to have no available TypeScript typings.
(24): The latest release of "passport" was 7 months ago
(25): The module "passport" seems to have no available TypeScript typings.
(26): The module "pino" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(27): The module "pino" has "22" dependencies (including sub-dependencies) which is more than the default "20".
(28): The latest release of "rhea" was over 1 year ago
(29): The module "rhea" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(30): The module "mocha" seems to have no available TypeScript typings.
(31): The module "mocha" has "69" dependencies (including sub-dependencies) which is more than the default "20".
(32): The "jest" seems that is lacking appropriate testing (https://www.github.com/jestjs/jest)
(33): The module "jest" has "261" dependencies (including sub-dependencies) which is more than the default "20".
(34): The module "@ibm-cloud/cloudant" has "91" dependencies (including sub-dependencies) which is more than the default "20".
(35): The latest release of "nano" was 8 months ago
(36): The module "nano" has "25" dependencies (including sub-dependencies) which is more than the default "20".
(37): The latest release of "odbc" was about 1 year ago
(38): The module "odbc" has "56" dependencies (including sub-dependencies) which is more than the default "20".
(39): The module "ibm_db" seems to have no available TypeScript typings.
(40): The module "ibm_db" has "45" dependencies (including sub-dependencies) which is more than the default "20".
(41): The module "mongodb" is not tested by community CITGM runs.
(42): The module "pg" seems to have no available TypeScript typings.
(43): The module "pg" is not tested by community CITGM runs.
(44): The latest release of "kafkajs" was over 1 year ago
(45): The "@openapitools/openapi-generator-cli" seems that is lacking appropriate testing (https://www.github.com/OpenAPITools/openapi-generator-cli)
(46): The module "@openapitools/openapi-generator-cli" seems to have no available TypeScript typings.
(47): The module "@openapitools/openapi-generator-cli" has "111" dependencies (including sub-dependencies) which is more than the default "20".
(48): The module "openapi-backend" has "35" dependencies (including sub-dependencies) which is more than the default "20".
(49): The module "@stoplight/prism-cli" is not tested by community CITGM runs.
(50): The module "@stoplight/prism-cli" has "176" dependencies (including sub-dependencies) which is more than the default "20".
(51): The module "express-openapi-validator" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(52): The module "express-openapi-validator" has "109" dependencies (including sub-dependencies) which is more than the default "20".
(53): The module "swagger-editor" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(54): The module "swagger-editor" seems to have no available TypeScript typings.
(55): The module "swagger-editor" has "374" dependencies (including sub-dependencies) which is more than the default "20".
(56): The latest release of "openapi-editor" was over 3 years ago
(57): The module "openapi-editor" has "200" dependencies (including sub-dependencies) which is more than the default "20".
(58): The module "nyc" seems to have no available TypeScript typings.
(59): The module "nyc" is not tested by community CITGM runs.
(60): The module "nyc" has "145" dependencies (including sub-dependencies) which is more than the default "20".
(61): The module "dotenv" is not tested by community CITGM runs.
(62): The latest release of "node-vault" was 12 months ago
(63): The module "node-vault" seems to have no available TypeScript typings.
(64): The module "node-vault" is not tested by community CITGM runs.
(65): The module "node-vault" has "59" dependencies (including sub-dependencies) which is more than the default "20".
(66): The module "@ibm-cloud/secrets-manager" seems to have no available TypeScript typings.
(67): The module "@ibm-cloud/secrets-manager" is not tested by community CITGM runs.
(68): The module "@ibm-cloud/secrets-manager" has "90" dependencies (including sub-dependencies) which is more than the default "20".
(69): The module "@opentelemetry/sdk-trace-base" is not tested by community CITGM runs.
(70): The module "@opentelemetry/sdk-trace-node" is not tested by community CITGM runs.
(71): The module "axios" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(72): The module "axios" is not tested by community CITGM runs.
(73): The latest release of "node-fetch" was 10 months ago
(74): The module "node-fetch" is not tested by community CITGM runs.
(75): The latest release of "cors" was over 5 years ago
(76): The module "cors" seems to have no available TypeScript typings.
(77): The module "cors" is not tested by community CITGM runs.

problems: 77 (errors: 2 - warnings: 75)
```


New (materially) since last review (excluding ones were # deps was already over limit and changed):
```
None
```
## Notes

There was a release of NYC since the last report.  It had been 4 years since the last one

(2): The module "cldr-localenames-full" is under the non-acceptable license(s) "Unicode-3.0". - ERROR
(3): The module "cldr-localenames-full" depends on the "cldr-core@45.0.0" package which is under the non-acceptable license "Unicode-3.0". - ERROR

The `cldr-localenames-full` and `cldr-core` have changed their licenses from `Unicode-DFS-2016` to `Unicode-3.0` which is failing the checks.  I think we can just add the `Unicode-3.0` option to the list of valid licenses.

A few modules are `aging` in terms of the last release. Not necessariliy something to worry about yet but worth keeping an eye on

Aging
(12): The latest release of "helmet" was 8 months ago
(20): The latest release of "i18next-fs-backend" was 7 months ago
(24): The latest release of "passport" was 7 months ago
(35): The latest release of "nano" was 8 months ago