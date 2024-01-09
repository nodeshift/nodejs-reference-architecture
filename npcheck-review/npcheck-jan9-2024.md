# npcheck review - Jan 9 2023

No major concerns were noted in this review.

## Diff in npcheck.json since last review 

None

## Results

run locally due to automation issues

npcheck report

```shell
1): The "cldr-localenames-full" seems that is lacking appropriate testing (https://www.github.com/unicode-cldr/cldr-json)
(2): The module "cldr-localenames-full" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(3): The module "cldr-localenames-full" seems to have no available TypeScript typings.
(4): The module "eslint" seems to have no available TypeScript typings.
(5): The module "eslint" has "98" dependencies (including sub-dependencies) which is more than the default "20".
(6): The latest release of "express" was over 1 year ago
(7): The module "express" seems to have no available TypeScript typings.
(8): The module "express" is not tested by community CITGM runs.
(9): The module "express" has "60" dependencies (including sub-dependencies) which is more than the default "20".
(10): The module "express-prom-bundle" has "78" dependencies (including sub-dependencies) which is more than the default "20".
(11): The latest release of "ibmcloud-appid" was 11 months ago
(12): The module "ibmcloud-appid" has "224" dependencies (including sub-dependencies) which is more than the default "20".
(13): The module "i18next" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(14): The module "i18next" is not tested by community CITGM runs.
(15): The latest release of "i18next-icu" was 9 months ago
(16): The module "i18next-icu" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(17): The module "i18next-http-middleware" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(18): The module "i18next-fs-backend" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(19): The latest release of "ioredis" was 9 months ago
(20): The module "ioredis" is not tested by community CITGM runs.
(21): The module "node-rdkafka" seems to have no available TypeScript typings.
(22): The module "opossum" seems to have no available TypeScript typings.
(23): The module "passport" seems to have no available TypeScript typings.
(24): The module "pino" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(25): The module "pino" has "22" dependencies (including sub-dependencies) which is more than the default "20".
(26): The latest release of "rhea" was 12 months ago
(27): The module "rhea" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(28): The latest release of "mocha" was about 1 year ago
(29): The module "mocha" seems to have no available TypeScript typings.
(30): The module "mocha" has "72" dependencies (including sub-dependencies) which is more than the default "20".
(31): The "jest" seems that is lacking appropriate testing (https://www.github.com/jestjs/jest)
(32): The module "jest" has "261" dependencies (including sub-dependencies) which is more than the default "20".
(33): The module "@ibm-cloud/cloudant" has "96" dependencies (including sub-dependencies) which is more than the default "20".
(34): The module "nano" has "23" dependencies (including sub-dependencies) which is more than the default "20".
(35): The latest release of "odbc" was 8 months ago
(36): The module "odbc" has "57" dependencies (including sub-dependencies) which is more than the default "20".
(37): The module "ibm_db" seems to have no available TypeScript typings.
(38): The module "ibm_db" has "45" dependencies (including sub-dependencies) which is more than the default "20".
(39): The module "mongodb" is not tested by community CITGM runs.
(40): The module "pg" seems to have no available TypeScript typings.
(41): The module "pg" is not tested by community CITGM runs.
(42): The latest release of "kafkajs" was 11 months ago
(43): The "@openapitools/openapi-generator-cli" seems that is lacking appropriate testing (https://www.github.com/OpenAPITools/openapi-generator-cli)
(44): The module "@openapitools/openapi-generator-cli" seems to have no available TypeScript typings.
(45): The module "@openapitools/openapi-generator-cli" has "106" dependencies (including sub-dependencies) which is more than the default "20".
(46): The module "openapi-backend" has "36" dependencies (including sub-dependencies) which is more than the default "20".
(47): The module "@stoplight/prism-cli" is not tested by community CITGM runs.
(48): The module "@stoplight/prism-cli" has "179" dependencies (including sub-dependencies) which is more than the default "20".
(49): The module "express-openapi-validator" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(50): The module "express-openapi-validator" has "57" dependencies (including sub-dependencies) which is more than the default "20".
(51): The module "swagger-editor" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(52): The module "swagger-editor" seems to have no available TypeScript typings.
(53): The module "swagger-editor" has "330" dependencies (including sub-dependencies) which is more than the default "20".
(54): The latest release of "openapi-editor" was about 3 years ago
(55): The module "openapi-editor" has "200" dependencies (including sub-dependencies) which is more than the default "20".
(56): The latest release of "nyc" was over 3 years ago
(57): The module "nyc" seems to have no available TypeScript typings.
(58): The module "nyc" is not tested by community CITGM runs.
(59): The module "nyc" has "145" dependencies (including sub-dependencies) which is more than the default "20".
(60): The latest release of "dotenv" was 7 months ago
(61): The module "dotenv" is not tested by community CITGM runs.
(62): The module "node-vault" seems to have no available TypeScript typings.
(63): The module "node-vault" is not tested by community CITGM runs.
(64): The module "node-vault" has "59" dependencies (including sub-dependencies) which is more than the default "20".
(65): The module "@ibm-cloud/secrets-manager" seems to have no available TypeScript typings.
(66): The module "@ibm-cloud/secrets-manager" is not tested by community CITGM runs.
(67): The module "@ibm-cloud/secrets-manager" has "95" dependencies (including sub-dependencies) which is more than the default "20".
(68): The module "@opentelemetry/sdk-trace-base" is not tested by community CITGM runs.
(69): The module "@opentelemetry/sdk-trace-node" is not tested by community CITGM runs.
(70): The module "axios" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(71): The module "axios" is not tested by community CITGM runs.
(72): The module "node-fetch" is not tested by community CITGM runs.
(73): The latest release of "cors" was about 5 years ago
(74): The module "cors" seems to have no available TypeScript typings.
(75): The module "cors" is not tested by community CITGM runs.
```

New (materially) since last review (excluding ones were # deps was already over limit and changed):
```
(10): The module "express-prom-bundle" has "78" dependencies (including sub-dependencies) which is more than the default "20".
(19): The latest release of "ioredis" was 9 months ago
(35): The latest release of "odbc" was 8 months ago
(60): The latest release of "dotenv" was 7 months ago
```
## Notes
- the increase in deps in express-prom-bundle is noted but not a reason to drop from ref arch
- the increased times since a release of ioredis, odbc and dotenv is noted, will continue to see if time since last release
  continues to strech out.

