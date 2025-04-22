# npcheck review - April 07 2025



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
(5): The module "eslint" has "83" dependencies (including sub-dependencies) which is more than the default "20".
(6): The module "express" seems to have no available TypeScript typings.
(7): The module "express" has "65" dependencies (including sub-dependencies) which is more than the default "20".
(8): The latest release of "ibmcloud-appid" was about 2 years ago
(9): The module "ibmcloud-appid" has "230" dependencies (including sub-dependencies) which is more than the default "20".
(10): The module "i18next" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(11): The module "i18next" is not tested by community CITGM runs.
(12): The latest release of "i18next-icu" was about 2 years ago
(13): The module "i18next-icu" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(14): The module "i18next-http-middleware" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(15): The module "i18next-fs-backend" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(16): The module "ioredis" is not tested by community CITGM runs.
(17): The module "opossum" seems to have no available TypeScript typings.
(18): The latest release of "passport" was over 1 year ago
(19): The module "passport" seems to have no available TypeScript typings.
(20): The module "pino" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(21): The latest release of "prom-client" was 9 months ago
(22): The module "rhea" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(23): The module "lru-cache" has no support for the LTS version(s) 18.20.8 of Node.js.
(24): The module "mocha" seems to have no available TypeScript typings.
(25): The module "mocha" has "83" dependencies (including sub-dependencies) which is more than the default "20".
(26): The "jest" seems that is lacking appropriate testing (https://www.github.com/jestjs/jest)
(27): The module "jest" has "257" dependencies (including sub-dependencies) which is more than the default "20".
(28): The module "@ibm-cloud/cloudant" has "58" dependencies (including sub-dependencies) which is more than the default "20".
(29): The latest release of "nano" was 8 months ago
(30): The module "nano" has "31" dependencies (including sub-dependencies) which is more than the default "20".
(31): The module "@elastic/elasticsearch" has "31" dependencies (including sub-dependencies) which is more than the default "20".
(32): The latest release of "odbc" was 8 months ago
(33): The module "odbc" has "56" dependencies (including sub-dependencies) which is more than the default "20".
(34): The module "ibm_db" seems to have no available TypeScript typings.
(35): The module "ibm_db" has "59" dependencies (including sub-dependencies) which is more than the default "20".
(36): The module "mongodb" is not tested by community CITGM runs.
(37): The module "pg" seems to have no available TypeScript typings.
(38): The module "pg" is not tested by community CITGM runs.
(39): The latest release of "kafkajs" was about 2 years ago
(40): The "@openapitools/openapi-generator-cli" seems that is lacking appropriate testing (https://www.github.com/OpenAPITools/openapi-generator-cli)
(41): The module "@openapitools/openapi-generator-cli" seems to have no available TypeScript typings.
(42): The module "@openapitools/openapi-generator-cli" has "145" dependencies (including sub-dependencies) which is more than the default "20".
(43): The module "openapi-backend" has "38" dependencies (including sub-dependencies) which is more than the default "20".
(44): The module "@stoplight/prism-cli" is not tested by community CITGM runs.
(45): The module "@stoplight/prism-cli" has "178" dependencies (including sub-dependencies) which is more than the default "20".
(46): The module "express-openapi-validator" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(47): The module "express-openapi-validator" has "111" dependencies (including sub-dependencies) which is more than the default "20".
(48): The module "swagger-editor" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(49): The module "swagger-editor" seems to have no available TypeScript typings.
(50): The module "swagger-editor" has "377" dependencies (including sub-dependencies) which is more than the default "20".
(51): The latest release of "openapi-editor" was over 4 years ago
(52): The module "openapi-editor" has "191" dependencies (including sub-dependencies) which is more than the default "20".
(53): The latest release of "nyc" was 7 months ago
(54): The module "nyc" seems to have no available TypeScript typings.
(55): The module "nyc" is not tested by community CITGM runs.
(56): The module "nyc" has "136" dependencies (including sub-dependencies) which is more than the default "20".
(57): The module "dotenv" is not tested by community CITGM runs.
(58): The latest release of "node-vault" was over 1 year ago
(59): The module "node-vault" seems to have no available TypeScript typings.
(60): The module "node-vault" is not tested by community CITGM runs.
(61): The module "node-vault" has "49" dependencies (including sub-dependencies) which is more than the default "20".
(62): The module "@ibm-cloud/secrets-manager" seems to have no available TypeScript typings.
(63): The module "@ibm-cloud/secrets-manager" is not tested by community CITGM runs.
(64): The module "@ibm-cloud/secrets-manager" has "58" dependencies (including sub-dependencies) which is more than the default "20".
(65): The module "@opentelemetry/sdk-trace-base" is not tested by community CITGM runs.
(66): The module "@opentelemetry/sdk-trace-node" is not tested by community CITGM runs.
(67): The module "axios" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(68): The module "axios" is not tested by community CITGM runs.
(69): The module "axios" has "22" dependencies (including sub-dependencies) which is more than the default "20".
(70): The latest release of "node-fetch" was over 1 year ago
(71): The module "node-fetch" is not tested by community CITGM runs.
(72): The latest release of "cors" was over 6 years ago
(73): The module "cors" seems to have no available TypeScript typings.
(74): The module "cors" is not tested by community CITGM runs.

problems: 74 (errors: 0 - warnings: 74)
```


New (materially) since last review (excluding ones were # deps was already over limit and changed):
```
None
```
## Notes

Since the last report Axios has increased its dependencies to 22

A few modules are `aging` in terms of the last release. Not necessariliy something to worry about yet but worth keeping an eye on

Aging

The latest release of "nano" was 8 months ago
The latest release of "odbc" was 8 months ago
The latest release of "nyc" was 7 months ago

