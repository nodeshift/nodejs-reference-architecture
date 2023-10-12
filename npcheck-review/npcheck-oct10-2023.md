# npcheck review - Oct 10 2023

No major concerns were noted in this review.

## Diff in npcheck.json since last review 

```shell
diff --git a/npcheck.json b/npcheck.json
index 4a9bb4b..d220594 100644
--- a/npcheck.json
+++ b/npcheck.json
@@ -495,7 +495,8 @@
       },
       "swagger-editor": {
         "note": "Multiple dependencies use licenses",
-        "allow": ["Python-2.0","0BSD"]
+        "note": "depends on jsonify which is under Public Domain",
+        "allow": ["Python-2.0","0BSD", "Public Domain"]
       },
       "@stoplight/prism-cli":{
         "note": "dependency tslib@2.3.1 reports 0BSD which is less restrictive than BSD",
```

## Results

```shell
https://github.com/nodeshift/nodejs-reference-architecture/actions/runs/6474140742

NPCheck Report

(1): The "cldr-localenames-full" seems that is lacking appropriate testing (https://www.github.com/unicode-cldr/cldr-json)
(2): The module "cldr-localenames-full" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(3): The module "cldr-localenames-full" seems to have no available TypeScript typings.
(4): The module "eslint" seems to have no available TypeScript typings.
(5): The module "eslint" has "97" dependencies (including sub-dependencies) which is more than the default "20".
(6): The latest release of "express" was about 1 year ago
(7): The module "express" seems to have no available TypeScript typings.
(8): The module "express" is not tested by community CITGM runs.
(9): The module "express" has "56" dependencies (including sub-dependencies) which is more than the default "20".
(10): The latest release of "express-prom-bundle" was 10 months ago
(11): The latest release of "ibmcloud-appid" was 8 months ago
(12): The module "ibmcloud-appid" has "220" dependencies (including sub-dependencies) which is more than the default "20".
(13): The module "i18next" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(14): The module "i18next" is not tested by community CITGM runs.
(15): The latest release of "i18next-icu" was 6 months ago
(16): The module "i18next-icu" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(17): The module "i18next-http-middleware" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(18): The module "i18next-fs-backend" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(19): The module "ioredis" is not tested by community CITGM runs.
(20): The module "node-rdkafka" seems to have no available TypeScript typings.
(21): The module "opossum" seems to have no available TypeScript typings.
(22): The latest release of "passport" was over 1 year ago
(23): The module "passport" seems to have no available TypeScript typings.
(24): The module "pino" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(25): The module "pino" has "22" dependencies (including sub-dependencies) which is more than the default "20".
(26): The latest release of "rhea" was 9 months ago
(27): The module "rhea" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(28): The latest release of "mocha" was 10 months ago
(29): The module "mocha" seems to have no available TypeScript typings.
(30): The module "mocha" has "72" dependencies (including sub-dependencies) which is more than the default "20".
(31): The "jest" seems that is lacking appropriate testing (https://www.github.com/jestjs/jest)
(32): The module "jest" has "260" dependencies (including sub-dependencies) which is more than the default "20".
(33): The module "@ibm-cloud/cloudant" has "93" dependencies (including sub-dependencies) which is more than the default "20".
(34): The latest release of "nano" was 9 months ago
(35): The module "odbc" has "57" dependencies (including sub-dependencies) which is more than the default "20".
(36): The module "ibm_db" seems to have no available TypeScript typings.
(37): The module "ibm_db" has "45" dependencies (including sub-dependencies) which is more than the default "20".
(38): The module "mongodb" is not tested by community CITGM runs.
(39): The module "pg" seems to have no available TypeScript typings.
(40): The module "pg" is not tested by community CITGM runs.
(41): The latest release of "kafkajs" was 8 months ago
(42): The "@openapitools/openapi-generator-cli" seems that is lacking appropriate testing (https://www.github.com/OpenAPITools/openapi-generator-cli)
(43): The module "@openapitools/openapi-generator-cli" seems to have no available TypeScript typings.
(44): The module "@openapitools/openapi-generator-cli" has "106" dependencies (including sub-dependencies) which is more than the default "20".
(45): The module "openapi-backend" has "32" dependencies (including sub-dependencies) which is more than the default "20".
(46): The module "@stoplight/prism-cli" is not tested by community CITGM runs.
(47): The module "@stoplight/prism-cli" has "179" dependencies (including sub-dependencies) which is more than the default "20".
(48): The module "express-openapi-validator" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(49): The module "express-openapi-validator" has "57" dependencies (including sub-dependencies) which is more than the default "20".
(50): The module "swagger-editor" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(51): The module "swagger-editor" seems to have no available TypeScript typings.
(52): The module "swagger-editor" has "318" dependencies (including sub-dependencies) which is more than the default "20".
(53): The latest release of "openapi-editor" was almost 3 years ago
(54): The module "openapi-editor" has "200" dependencies (including sub-dependencies) which is more than the default "20".
(55): The latest release of "nyc" was over 3 years ago
(56): The module "nyc" seems to have no available TypeScript typings.
(57): The module "nyc" is not tested by community CITGM runs.
(58): The module "nyc" has "145" dependencies (including sub-dependencies) which is more than the default "20".
(59): The module "dotenv" is not tested by community CITGM runs.
(60): The module "node-vault" seems to have no available TypeScript typings.
(61): The module "node-vault" is not tested by community CITGM runs.
(62): The module "node-vault" has "59" dependencies (including sub-dependencies) which is more than the default "20".
(63): The module "@ibm-cloud/secrets-manager" seems to have no available TypeScript typings.
(64): The module "@ibm-cloud/secrets-manager" is not tested by community CITGM runs.
(65): The module "@ibm-cloud/secrets-manager" has "93" dependencies (including sub-dependencies) which is more than the default "20".
(66): The module "@opentelemetry/sdk-trace-base" is not tested by community CITGM runs.
(67): The module "@opentelemetry/sdk-trace-node" is not tested by community CITGM runs.
(68): The module "axios" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(69): The module "axios" is not tested by community CITGM runs.
(70): The module "node-fetch" is not tested by community CITGM runs.
(71): The latest release of "cors" was almost 5 years ago
(72): The module "cors" seems to have no available TypeScript typings.
(73): The module "cors" is not tested by community CITGM runs.

```

New (materially) since last review (excluding ones were # deps was already over limit and changed):
```
(8): The module "express" is not tested by community CITGM runs.
(11): The latest release of "ibmcloud-appid" was 8 months ago
(15): The latest release of "i18next-icu" was 6 months ago
(26): The latest release of "rhea" was 9 months ago
(28): The latest release of "mocha" was 10 months ago
(34): The latest release of "nano" was 9 months ago
(41): The latest release of "kafkajs" was 8 months ago
(53): The latest release of "openapi-editor" was almost 3 years ago
(55): The latest release of "nyc" was over 3 years ago
(71): The latest release of "cors" was almost 5 years ago
```
## Notes
- some modules have been removed from CITGM in a community attempt to get it to
  a green state, hopefully express will make it back in at some point in the next
  quarter
- none of the last release which is still less than 1 year is a concern
- the last releases of 'openapit-editor', 'nyc' and 'cors' are worth discussing
  in a future Reference architecture team meeting.
