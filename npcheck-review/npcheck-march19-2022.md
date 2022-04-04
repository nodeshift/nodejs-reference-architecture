# npcheck review - Dec 6 - 2021

## Results

```shell
NPCheck Report
(1): The "cldr-localenames-full" seems that is lacking appropriate testing (https://www.github.com/unicode-cldr/cldr-json)
(2): The module "cldr-localenames-full" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(3): The module "cldr-localenames-full" seems to have no available TypeScript typings.
(4): The module "eslint" is not tested (skipped) by community CITGM runs.
(5): The module "eslint" has "80" dependencies (including sub-dependencies) which is more than the default "20".
(6): The module "express" has "48" dependencies (including sub-dependencies) which is more than the default "20".
(7): The latest release of "express-prom-bundle" was 7 months ago
(8): The module "express-prom-bundle" is not tested by community CITGM runs.
(9): The module "helmet" is not tested by community CITGM runs.
(10): The module "ibmcloud-appid" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(11): The module "ibmcloud-appid" seems to have no available TypeScript typings.
(12): The module "ibmcloud-appid" has "117" dependencies (including sub-dependencies) which is more than the default "20".
(13): The module "i18next" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(14): The module "i18next" is not tested by community CITGM runs.
(15): The latest release of "i18next-icu" was 12 months ago
(16): The module "i18next-icu" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(17): The module "i18next-icu" seems to have no available TypeScript typings.
(18): The module "i18next-icu" is not tested by community CITGM runs.
(19): The module "i18next-http-middleware" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(20): The module "i18next-http-middleware" is not tested by community CITGM runs.
(21): The module "i18next-fs-backend" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(22): The module "i18next-fs-backend" seems to have no available TypeScript typings.
(23): The module "i18next-fs-backend" is not tested by community CITGM runs.
(24): The module "ioredis" is not tested by community CITGM runs.
(25): The module "node-rdkafka" seems to have no available TypeScript typings.
(26): The module "node-rdkafka" is not tested by community CITGM runs.
(27): The module "passport" is not tested by community CITGM runs.
(28): The module "pino" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(29): The module "pino" has "22" dependencies (including sub-dependencies) which is more than the default "20".
(30): The module "rhea" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(31): The module "rhea" is not tested by community CITGM runs.
(32): The module "lru-cache" is not tested by community CITGM runs.
(33): The module "mocha" is not tested (skipped) by community CITGM runs.
(34): The module "mocha" has "76" dependencies (including sub-dependencies) which is more than the default "20".
(35): The "jest" seems that is lacking appropriate testing (https://www.github.com/facebook/jest)
(36): The module "jest" has "315" dependencies (including sub-dependencies) which is more than the default "20".
(37): The module "@ibm-cloud/cloudant" has "85" dependencies (including sub-dependencies) which is more than the default "20".
(38): The latest release of "nano" was 6 months ago
(39): The module "nano" is not tested by community CITGM runs.
(40): The module "@elastic/elasticsearch" is not tested by community CITGM runs.
(41): The module "odbc" is not tested by community CITGM runs.
(42): The module "odbc" has "57" dependencies (including sub-dependencies) which is more than the default "20".
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
(53): The module "@stoplight/prism-cli" is not tested by community CITGM runs.
(54): 1 medium risk vulnerability found that are older than 4 months.

-> minimist - CVE-2020-7598 - https://github.com/advisories/GHSA-vh95-rmgr-6w4m
(55): The module "@stoplight/prism-cli" has "212" dependencies (including sub-dependencies) which is more than the default "20".
(56): The module "express-openapi-validator" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(57): The module "express-openapi-validator" seems to have no available TypeScript typings.
(58): The module "express-openapi-validator" is not tested by community CITGM runs.
(59): The module "express-openapi-validator" has "56" dependencies (including sub-dependencies) which is more than the default "20".
(60): The module "swagger-editor" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(61): The module "swagger-editor" seems to have no available TypeScript typings.
(62): The module "swagger-editor" is not tested by community CITGM runs.
(63): 2 medium risk vulnerabilities found that are older than 4 months.

-> ansi-regex - CVE-2021-3807 - https://github.com/advisories/GHSA-93q8-gq69-wqmw
-> minimist - CVE-2020-7598 - https://github.com/advisories/GHSA-vh95-rmgr-6w4m
(64): The module "swagger-editor" has "220" dependencies (including sub-dependencies) which is more than the default "20".
(65): The latest release of "openapi-editor" was about 1 year ago
(66): The module "openapi-editor" is not tested by community CITGM runs.
(67): The module "openapi-editor" has "195" dependencies (including sub-dependencies) which is more than the default "20".
(68): The latest release of "nyc" was almost 2 years ago
(69): The module "nyc" seems to have no available TypeScript typings.
(70): The module "nyc" is not tested by community CITGM runs.
(71): The module "nyc" has "142" dependencies (including sub-dependencies) which is more than the default "20".
(72): The module "dotenv" is not tested by community CITGM runs.
(73): The latest release of "node-vault" was 9 months ago
(74): The module "node-vault" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(75): The module "node-vault" is not tested by community CITGM runs.
(76): The module "node-vault" has "55" dependencies (including sub-dependencies) which is more than the default "20".
(77): The module "@ibm-cloud/secrets-manager" seems to have no available TypeScript typings.
(78): The module "@ibm-cloud/secrets-manager" is not tested by community CITGM runs.
(79): The module "@ibm-cloud/secrets-manager" has "85" dependencies (including sub-dependencies) which is more than the default "20".

problems: 79 (errors: 0 - warnings: 79)
```

New since last review:

```
(7): The latest release of "express-prom-bundle" was 7 months ago
(15): The latest release of "i18next-icu" was 12 months ago
(36): The module "jest" has "315" dependencies (including sub-dependencies) which is more than the default "20".
(42): The module "odbc" has "57" dependencies (including sub-dependencies) which is more than the default "20".
(43): The module "ibm_db" has "57" dependencies (including sub-dependencies) which is more than the default "20".
(53): The module "@stoplight/prism-cli" is not tested by community CITGM runs.
(54): 1 medium risk vulnerability found that are older than 4 months. "@stoplight/prims-cli"
-> minimist - CVE-2020-7598 - https://github.com/advisories/GHSA-vh95-rmgr-6w4m
(55): The module "@stoplight/prism-cli" has "212" dependencies (including sub-dependencies) which is more than the default "20".
(56): The module "express-openapi-validator" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(63): 2 medium risk vulnerabilities found that are older than 4 months. "swagger-editor"
-> ansi-regex - CVE-2021-3807 - https://github.com/advisories/GHSA-93q8-gq69-wqmw
-> minimist - CVE-2020-7598 - https://github.com/advisories/GHSA-vh95-rmgr-6w4m
(64): The module "swagger-editor" has "220" dependencies (including sub-dependencies) which is more than the default "20".
(65): The latest release of "openapi-editor" was about 1 year ago
(67): The module "openapi-editor" has "195" dependencies (including sub-dependencies) which is more than the default "20".
(68): The latest release of "nyc" was almost 2 years ago
(71): The module "nyc" has "142" dependencies (including sub-dependencies) which is more than the default "20".
(72): The module "dotenv" is not tested by community CITGM runs.
(73): The latest release of "node-vault" was 9 months ago
(74): The module "node-vault" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(75): The module "node-vault" is not tested by community CITGM runs.
(76): The module "node-vault" has "55" dependencies (including sub-dependencies) which is more than the default "20".
(77): The module "@ibm-cloud/secrets-manager" seems to have no available TypeScript typings.
(78): The module "@ibm-cloud/secrets-manager" is not tested by community CITGM runs.
(79): The module "@ibm-cloud/secrets-manager" has "85" dependencies (including sub-dependencies) which is more than the default "20".

```

## Notes
* These notes only cover the deltas from the last report.
* We have added some new modules which has resulted in a larger number of warnings. We plan
  to work these down.
* With respect to (7) express had a release and no longer shows up in the warnings We are
  no concerned with expres-prom-bundle not having a recent release
* With respect to (36), (42), (43), (55), (64), (67), (71), (76), (79) the number of dependencies for modules that
  were in the last report either went up or down by a few from the last report. These changes nor the
  numbers for the new modules make us think we should re-look at the packages reported although we
  still need to figure out a good way to evaluate how to best use the number of dependents.
* In respect to (15), (65), (68), (73) we don't see a concern with those not having done a recent release.
* In respect to (78) we don't believe it will be possible to get the module tested in CITGM.
* In respect to (53), (72), (75) we plan to review to see which ones make sense to be
  part of CITGM in the community.
* In respect to (56), (74) those indicate that the package does not include
  an engines field or package-support.json file. We have no reason to believe any of those
  flagged don't support the current LTS Node.js versions.
* In respect to (63) the medium vulnerabilities flagged in "swagger-editor" we'll keep an eye on wether they
  are still present in the next review
* In respect to (77) as an IBM module it would be good to have TypeScript typings, we should contact the
  team to see if they have plans in that respect.
* In respect to (54) we'll keep an eye on the medium vulnerabilties reported and see if they are still
  present in the next review
