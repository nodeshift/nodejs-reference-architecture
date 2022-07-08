# npcheck review - July 7 - 2022

## Results

```shell
https://github.com/nodeshift/nodejs-reference-architecture/runs/7238817532?check_suite_focus=true

NPCheck Report
(1): The "cldr-localenames-full" seems that is lacking appropriate testing (https://www.github.com/unicode-cldr/cldr-json)
(2): The module "cldr-localenames-full" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(3): The module "cldr-localenames-full" seems to have no available TypeScript typings.
(4): The module "eslint" is not tested (skipped) by community CITGM runs.
(5): The module "eslint" has "80" dependencies (including sub-dependencies) which is more than the default "20".
(6): The module "express" has "55" dependencies (including sub-dependencies) which is more than the default "20".
(7): The module "express-prom-bundle" is not tested by community CITGM runs.
(8): The module "helmet" is not tested by community CITGM runs.
(9): The module "ibmcloud-appid" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(10): The module "ibmcloud-appid" seems to have no available TypeScript typings.
(11): The module "ibmcloud-appid" has "127" dependencies (including sub-dependencies) which is more than the default "20".
(12): The module "i18next" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(13): The module "i18next" is not tested by community CITGM runs.
(14): The latest release of "i18next-icu" was over 1 year ago
(15): The module "i18next-icu" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(16): The module "i18next-icu" seems to have no available TypeScript typings.
(17): The module "i18next-icu" is not tested by community CITGM runs.
(18): The module "i18next-http-middleware" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(19): The module "i18next-http-middleware" is not tested by community CITGM runs.
(20): The latest release of "i18next-fs-backend" was 8 months ago
(21): The module "i18next-fs-backend" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(22): The module "i18next-fs-backend" seems to have no available TypeScript typings.
(23): The module "i18next-fs-backend" is not tested by community CITGM runs.
(24): The module "ioredis" is not tested by community CITGM runs.
(25): The module "node-rdkafka" seems to have no available TypeScript typings.
(26): The module "node-rdkafka" is not tested by community CITGM runs.
(27): The module "passport" is not tested by community CITGM runs.
(28): The module "pino" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(29): The latest release of "prom-client" was 8 months ago
(30): The module "rhea" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(31): The module "rhea" is not tested by community CITGM runs.
(32): The module "lru-cache" is not tested by community CITGM runs.
(33): The module "mocha" is not tested (skipped) by community CITGM runs.
(34): The module "mocha" has "73" dependencies (including sub-dependencies) which is more than the default "20".
(35): The "jest" seems that is lacking appropriate testing (https://www.github.com/facebook/jest)
(36): The module "jest" has "261" dependencies (including sub-dependencies) which is more than the default "20".
(37): The module "@ibm-cloud/cloudant" has "85" dependencies (including sub-dependencies) which is more than the default "20".
(38): The module "nano" is not tested by community CITGM runs.
(39): The module "@elastic/elasticsearch" is not tested by community CITGM runs.
(40): The module "odbc" is not tested by community CITGM runs.
(41): The module "odbc" has "57" dependencies (including sub-dependencies) which is more than the default "20".
(42): The latest release of "ibm_db" was 7 months ago
(43): The module "ibm_db" has "57" dependencies (including sub-dependencies) which is more than the default "20".
(44): The module "mongodb" is not tested by community CITGM runs.
(45): The module "pg" is not tested by community CITGM runs.
(46): The module "kafkajs" is not tested by community CITGM runs.
(47): The "@openapitools/openapi-generator-cli" seems that is lacking appropriate testing (https://www.github.com/OpenAPITools/openapi-generator-cli)
(48): The module "@openapitools/openapi-generator-cli" seems to have no available TypeScript typings.
(49): The module "@openapitools/openapi-generator-cli" is not tested by community CITGM runs.
(50): The module "@openapitools/openapi-generator-cli" has "97" dependencies (including sub-dependencies) which is more than the default "20".
(51): The module "openapi-backend" is not tested by community CITGM runs.
(52): The module "openapi-backend" has "28" dependencies (including sub-dependencies) which is more than the default "20".
(53): The module "@stoplight/prism-cli" has no support for the LTS version(s) 14.20.0 of Node.js.
(54): The module "@stoplight/prism-cli" is not tested by community CITGM runs.
(55): The module "@stoplight/prism-cli" has "212" dependencies (including sub-dependencies) which is more than the default "20".
(56): The module "express-openapi-validator" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(57): The module "express-openapi-validator" seems to have no available TypeScript typings.
(58): The module "express-openapi-validator" is not tested by community CITGM runs.
(59): The module "express-openapi-validator" has "53" dependencies (including sub-dependencies) which is more than the default "20".
(60): The module "swagger-editor" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(61): The module "swagger-editor" seems to have no available TypeScript typings.
(62): The module "swagger-editor" is not tested by community CITGM runs.
(63): The module "swagger-editor" has "223" dependencies (including sub-dependencies) which is more than the default "20".
(64): The latest release of "openapi-editor" was over 1 year ago
(65): The module "openapi-editor" is not tested by community CITGM runs.
(66): The module "openapi-editor" has "195" dependencies (including sub-dependencies) which is more than the default "20".
(67): The latest release of "nyc" was about 2 years ago
(68): The module "nyc" seems to have no available TypeScript typings.
(69): The module "nyc" is not tested by community CITGM runs.
(70): The module "nyc" has "143" dependencies (including sub-dependencies) which is more than the default "20".
(71): The module "dotenv" is not tested by community CITGM runs.
(72): The latest release of "node-vault" was about 1 year ago
(73): The module "node-vault" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(74): The module "node-vault" is not tested by community CITGM runs.
(75): The module "node-vault" has "55" dependencies (including sub-dependencies) which is more than the default "20".
(76): The module "@ibm-cloud/secrets-manager" seems to have no available TypeScript typings.
(77): The module "@ibm-cloud/secrets-manager" is not tested by community CITGM runs.
(78): The module "@ibm-cloud/secrets-manager" has "85" dependencies (including sub-dependencies) which is more than the default "20".
(79): The module "@opentelemetry/sdk-trace-node" is not tested by community CITGM runs.
problems: 79 (errors: 0 - warnings: 79)



```

New since last review:

```
(20): The latest release of "i18next-fs-backend" was 8 months ago
(29): The latest release of "prom-client" was 8 months ago
(42): The latest release of "ibm_db" was 7 months ago
(53): The module "@stoplight/prism-cli" has no support for the LTS version(s) 14.20.0 of Node.js.
(79): The module "@opentelemetry/sdk-trace-node" is not tested by community CITGM runs.

```

## Notes
* These notes only cover the deltas from the last report.
* Not listed in the deltas, some warnings have gone away
* We have not mentioned modules where the number of deps has increased/decreased this time
  none of the deltas affect our thoughts on these modules
* With respect to (20) we are not concerned that there has been no release
  in "i18next-fs-backend". Seems to be a case of module being largely done. There has
  been a commit landed in the last few months and there is only one open issue in the repo.
* With respect to (29) there have not been many PRs landed recently (Last was Feb 27), seems
  like there are some open PRs without responses. Worth keeping an eye on, if this persists
  into the next report we should add to our active watch list.
* With respect to (53) looks like the minimum supported version was updated to 16 3 months
  ago. Support for all LTS versions would be better but this does not change
  our decision on including the reference in the architecture
* With respect to (79) we'd missed adding @opentelemetry/sdk-trace-node to the
  ref arch so not a concern that it now shows up. Is likely a good one to see if
  we can get into CITGM though.  

