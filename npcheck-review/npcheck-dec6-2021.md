# npcheck review - Dec 6 - 2021

## Results

```shell
PCheck Report
(1): The "cldr-localenames-full" seems that is lacking appropriate testing (https://www.github.com/unicode-cldr/cldr-json)
(2): The module "cldr-localenames-full" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(3): The module "cldr-localenames-full" seems to have no available TypeScript typings.
(4): The module "cldr-localenames-full" is not tested by community CITGM runs.
(5): The module "eslint" is not tested (skipped) by community CITGM runs.
(6): The module "eslint" has "86" dependencies (including sub-dependencies) which is more than the default "20".
(7): The latest release of "express" was over 1 year ago
(8): The module "express" has "48" dependencies (including sub-dependencies) which is more than the default "20".
(9): The module "express-prom-bundle" is not tested by community CITGM runs.
(10): The latest release of "helmet" was 7 months ago
(11): The module "helmet" is not tested by community CITGM runs.
(12): The module "ibmcloud-appid" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(13): The module "ibmcloud-appid" seems to have no available TypeScript typings.
(14): The module "ibmcloud-appid" is not tested by community CITGM runs.
(15): The module "ibmcloud-appid" has "117" dependencies (including sub-dependencies) which is more than the default "20".
(16): The module "i18next" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(17): The module "i18next" is not tested by community CITGM runs.
(18): The latest release of "i18next-icu" was 8 months ago
(19): The module "i18next-icu" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(20): The module "i18next-icu" seems to have no available TypeScript typings.
(21): The module "i18next-icu" is not tested by community CITGM runs.
(22): The module "i18next-http-middleware" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(23): The module "i18next-http-middleware" is not tested by community CITGM runs.
(24): The module "i18next-fs-backend" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(25): The module "i18next-fs-backend" seems to have no available TypeScript typings.
(26): The module "i18next-fs-backend" is not tested by community CITGM runs.
(27): The module "ioredis" is not tested by community CITGM runs.
(28): The module "node-rdkafka" seems to have no available TypeScript typings.
(29): The module "node-rdkafka" is not tested by community CITGM runs.
(30): The module "opossum" is not tested by community CITGM runs.
(31): The module "passport" is not tested by community CITGM runs.
(32): The module "pino" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(33): The module "pino" has "23" dependencies (including sub-dependencies) which is more than the default "20".
(34): The module "rhea" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(35): The module "rhea" is not tested by community CITGM runs.
(36): The latest release of "lru-cache" was over 1 year ago
(37): The module "lru-cache" is not tested by community CITGM runs.
(38): The module "mocha" is not tested (skipped) by community CITGM runs.
(39): The module "mocha" has "76" dependencies (including sub-dependencies) which is more than the default "20".
(40): The "jest" seems that is lacking appropriate testing (https://www.github.com/facebook/jest)
(41): The module "jest" has "307" dependencies (including sub-dependencies) which is more than the default "20".
(42): The module "@ibm-cloud/cloudant" is not tested by community CITGM runs.
(43): The module "@ibm-cloud/cloudant" has "85" dependencies (including sub-dependencies) which is more than the default "20".
(44): The module "nano" is not tested by community CITGM runs.
(45): The module "@elastic/elasticsearch" is not tested by community CITGM runs.
(46): The module "odbc" is not tested by community CITGM runs.
(47): The module "odbc" has "56" dependencies (including sub-dependencies) which is more than the default "20".
(48): The module "ibm_db" is not tested by community CITGM runs.
(49): The module "ibm_db" has "56" dependencies (including sub-dependencies) which is more than the default "20".
(50): The module "mongodb" is not tested by community CITGM runs.
(51): The module "pg" is not tested by community CITGM runs.
(52): The module "kafkajs" is not tested by community CITGM runs.
(53): The "@openapitools/openapi-generator-cli" seems that is lacking appropriate testing (https://www.github.com/OpenAPITools/openapi-generator-cli)
(54): The module "@openapitools/openapi-generator-cli" seems to have no available TypeScript typings.
(55): The module "@openapitools/openapi-generator-cli" is not tested by community CITGM runs.
(56): The module "@openapitools/openapi-generator-cli" has "97" dependencies (including sub-dependencies) which is more than the default "20".
(57): The module "openapi-backend" is not tested by community CITGM runs.
(58): The module "openapi-backend" has "28" dependencies (including sub-dependencies) which is more than the default "20".
(59): The module "@stoplight/prism-http" is not tested by community CITGM runs.
(60): The module "@stoplight/prism-http" has "57" dependencies (including sub-dependencies) which is more than the default "20".
(61): The module "express-openapi-validator" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(62): The module "express-openapi-validator" seems to have no available TypeScript typings.
(63): The module "express-openapi-validator" is not tested by community CITGM runs.
(64): The module "express-openapi-validator" has "56" dependencies (including sub-dependencies) which is more than the default "20".
(65): The module "swagger-editor" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(66): The module "swagger-editor" seems to have no available TypeScript typings.
(67): The module "swagger-editor" is not tested by community CITGM runs.
(68): 0 medium risk vulnerabilities found.

-> minimist - CVE-2020-7598 - https://github.com/advisories/GHSA-vh95-rmgr-6w4m
(69): The module "swagger-editor" has "227" dependencies (including sub-dependencies) which is more than the default "20".
(70): The latest release of "openapi-editor" was 12 months ago
(71): The module "openapi-editor" is not tested by community CITGM runs.
(72): The module "openapi-editor" has "192" dependencies (including sub-dependencies) which is more than the default "20".
(73): The latest release of "nyc" was over 1 year ago
(74): The module "nyc" seems to have no available TypeScript typings.
(75): The module "nyc" is not tested by community CITGM runs.
(76): The module "nyc" has "140" dependencies (including sub-dependencies) which is more than the default "20".

problems: 76 (errors: 0 - warnings: 76)
```

## Notes
* We have added a number of new checks, which has resulted in a larger number of warnings. We plan
  to work these down.
* With respect to (7) we are looking at web frameworks but the concensus is still the current recommendations
* With respect to (10),(18), (36), (70), (73) we don't see a concern with those not having done a recent release.
* With respect to (1), after review it seems that being a data delivery package no testing is needed
* With respect to the 10 warmings about "no support", those indicate that the package does not include
  an engines field or package-support.json file. We have no reason to believe any of those
  flagged don't support the current LTS Node.js versions.
* With respect to (14), (42), (30), (48) we don't believe they would be accepted into CITGM. We plan
  to supress these warnings.
* With respect to (4), cldr-localenames-full has no tests which makes sense for what it is and therefore
  does not belong in CIGGM.
* With respect to the 26 other CITGM warnings we plan to review and see which packages make sense to be
  part of CITGM in the community.
* With respect to the 16 warnings (which is 16/27 modules) about modules with more than 20 dependencies, we are still working out how we should review/check dependencies. None of the warnings reported make us think we should re-look at the packages reported.
* With respect to (3) as a data delivery module, typings do not make sense.
* With respect to (20), (25) as plugins/backends for i18next typings do not make sense.
* With respect to (54) as a generator tool, typings do not make sense.
* With respect to (62) as express middleware typings do not make sense.
* With respect to (66) as an editor typings do not make sense.
* With respect to (74) as a test module typings do not make sense.
* With respect to (13) as a passport plug-in strategy typings are not as important as they might be for some modules. 
* With respect to (40) we think this is most likely an issue with npcheck as we believe JEST has tests
* With respect to (53) openapi-generator-cli has a "test" script in package.json so this seems to be an error. 
the CVE has been fixed in 1.2.3 or later. It's due to swagger-editor@4.0.2 pulling in an older version in its dependencies. Our investigation shows that its due to the use of the opencollective library and then react-ace which
uses the older version of minimist.  The opencollective library says it will not get updates. This seems like a minimal risk.
