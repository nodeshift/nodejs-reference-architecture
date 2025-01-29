# npcheck review - January 29 2025



## Diff in npcheck.json since last review

```shell
```

## Results

https://github.com/nodeshift/nodejs-reference-architecture/actions/runs/12970009285/job/36174752220


NPCheck Report

```shell
NPCheck Report
(1): The module "node-rdkafka" seems to have no available TypeScript typings.
(2): The "cldr-localenames-full" seems that is lacking appropriate testing (https://www.github.com/unicode-cldr/cldr-json)
(3): The module "cldr-localenames-full" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(4): The module "cldr-localenames-full" seems to have no available TypeScript typings.
(5): The module "eslint" has "82" dependencies (including sub-dependencies) which is more than the default "20".
(6): The module "express" seems to have no available TypeScript typings.
(7): The module "express" has "66" dependencies (including sub-dependencies) which is more than the default "20".
(8): The latest release of "ibmcloud-appid" was almost 2 years ago
(9): The module "ibmcloud-appid" has "228" dependencies (including sub-dependencies) which is more than the default "20".
(10): The module "i18next" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(11): The module "i18next" is not tested by community CITGM runs.
(12): The latest release of "i18next-icu" was almost 2 years ago
(13): The module "i18next-icu" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(14): The module "i18next-http-middleware" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(15): The module "i18next-fs-backend" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(16): The module "ioredis" is not tested by community CITGM runs.
(17): The module "opossum" seems to have no available TypeScript typings.
(18): The latest release of "passport" was about 1 year ago
(19): The module "passport" seems to have no available TypeScript typings.
(20): The module "pino" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(21): The latest release of "prom-client" was 7 months ago
(22): The module "rhea" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(23): The module "lru-cache" has no support for the LTS version(s) 18.20.6 of Node.js.
(24): The module "mocha" seems to have no available TypeScript typings.
(25): The module "mocha" has "83" dependencies (including sub-dependencies) which is more than the default "20".
(26): The "jest" seems that is lacking appropriate testing (https://www.github.com/jestjs/jest)
(27): The module "jest" has "257" dependencies (including sub-dependencies) which is more than the default "20".
(28): The module "@ibm-cloud/cloudant" has "54" dependencies (including sub-dependencies) which is more than the default "20".
(29): The module "nano" has "29" dependencies (including sub-dependencies) which is more than the default "20".
(30): The module "@elastic/elasticsearch" has "31" dependencies (including sub-dependencies) which is more than the default "20".
(31): The module "odbc" has "56" dependencies (including sub-dependencies) which is more than the default "20".
(32): The module "ibm_db" seems to have no available TypeScript typings.
(33): The module "ibm_db" has "45" dependencies (including sub-dependencies) which is more than the default "20".
(34): The module "mongodb" is not tested by community CITGM runs.
(35): The module "pg" seems to have no available TypeScript typings.
(36): The module "pg" is not tested by community CITGM runs.
(37): The latest release of "kafkajs" was almost 2 years ago
(38): The "@openapitools/openapi-generator-cli" seems that is lacking appropriate testing (https://www.github.com/OpenAPITools/openapi-generator-cli)
(39): The module "@openapitools/openapi-generator-cli" seems to have no available TypeScript typings.
(40): The module "@openapitools/openapi-generator-cli" has "131" dependencies (including sub-dependencies) which is more than the default "20".
(41): The module "openapi-backend" has "38" dependencies (including sub-dependencies) which is more than the default "20".
(42): The module "@stoplight/prism-cli" is not tested by community CITGM runs.
(43): The module "@stoplight/prism-cli" has "178" dependencies (including sub-dependencies) which is more than the default "20".
(44): The module "express-openapi-validator" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(45): The module "express-openapi-validator" has "112" dependencies (including sub-dependencies) which is more than the default "20".
(46): The module "swagger-editor" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(47): The module "swagger-editor" seems to have no available TypeScript typings.
(48): The module "swagger-editor" has "375" dependencies (including sub-dependencies) which is more than the default "20".
(49): The latest release of "openapi-editor" was about 4 years ago
(50): The module "openapi-editor" has "191" dependencies (including sub-dependencies) which is more than the default "20".
(51): The module "nyc" seems to have no available TypeScript typings.
(52): The module "nyc" is not tested by community CITGM runs.
(53): The module "nyc" has "136" dependencies (including sub-dependencies) which is more than the default "20".
(54): The module "dotenv" is not tested by community CITGM runs.
(55): The latest release of "node-vault" was over 1 year ago
(56): The module "node-vault" seems to have no available TypeScript typings.
(57): The module "node-vault" is not tested by community CITGM runs.
(58): The module "node-vault" has "59" dependencies (including sub-dependencies) which is more than the default "20".
(59): The module "@ibm-cloud/secrets-manager" seems to have no available TypeScript typings.
(60): The module "@ibm-cloud/secrets-manager" is not tested by community CITGM runs.
(61): The module "@ibm-cloud/secrets-manager" has "53" dependencies (including sub-dependencies) which is more than the default "20".
(62): The module "@opentelemetry/sdk-trace-base" is not tested by community CITGM runs.
(63): The module "@opentelemetry/sdk-trace-node" is not tested by community CITGM runs.
(64): The module "axios" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(65): The module "axios" is not tested by community CITGM runs.
(66): The latest release of "node-fetch" was over 1 year ago
(67): The module "node-fetch" is not tested by community CITGM runs.
(68): The latest release of "cors" was about 6 years ago
(69): The module "cors" seems to have no available TypeScript typings.
(70): The module "cors" is not tested by community CITGM runs.

problems: 70 (errors: 0 - warnings: 70)
```


New (materially) since last review (excluding ones were # deps was already over limit and changed):
```
None
```
## Notes

There was a release of express-prom-bundle since the last report.  It had been 9 months since the last one

There was a release of dotenv since the last report.  It had been 8 months since the last one


A few modules are `aging` in terms of the last release. Not necessariliy something to worry about yet but worth keeping an eye on

Aging

The latest release of "passport" was 11 months ago
The latest release of "node-vault" was about 1 year ago
The latest release of "node-fetch" was about 1 year ago

