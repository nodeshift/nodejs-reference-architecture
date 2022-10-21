# npcheck review - July 7 - 2022

## Diff in npcheck.json since last review 

```shell
diff --git a/npcheck.json b/npcheck.json
index 7978fdf..2a320fa 100644
--- a/npcheck.json
+++ b/npcheck.json
@@ -152,9 +152,21 @@
       "name": "@ibm-cloud/secrets-manager",
       "npmlink": "https://www.npmjs.com/package/@ibm-cloud/secrets-manager"
     },
+    {
+      "name": "@opentelemetry/sdk-trace-base",
+      "npmlink": "https://www.npmjs.com/package/@opentelemetry/sdk-trace-base"
+    },
     {
       "name": "@opentelemetry/sdk-trace-node",
       "npmlink": "https://www.npmjs.com/package/@opentelemetry/sdk-trace-node"
+    },
+    {
+      "name": "axios",
+      "npmlink": "https://www.npmjs.com/package/axios"
+    },
+    {
+      "name": "node-fetch",
+      "npmlink": "https://www.npmjs.com/package/node-fetch"
     }
   ],
   "licenses": {
@@ -223,6 +235,13 @@
       "@elastic/elasticsearch": {
         "note": "dependency tslib@2.3.1 reports 0BSD which is less restrictive than BSD",
         "allow": ["0BSD"]
+      },
+      "node-rdkafka": {
+        "note": "dev depdency on domhandler, domutil and entities which are under BSD like reported as BSD*",
+        "note": "depends on argparse which is under Python-2.0",
+        "note": "dev dependency toolkit-jsdoc appears to be UNLICENCED (reports as Undefined) and shoujld not be installed, not required for non-dev use",
+        "note": "dependency taffydb reports an unknown licence but repo says it is BSD-2-Clause on npm",
+        "allow": ["BSD", "Python-2.0", "Undefined", "UNKNOWN"]
       }
     }
   },
@@ -241,13 +260,19 @@
       }],
       "CVE-2021-44906": [{
         "note": ["opencollective uses an old version of minimist. opencollective is used to ask for funding and the reported vulnerability is not a concern in that module"],
+	"note": ["mocha uses an old version of mkdirp. mocha is used for testing and the proptotype pollution vuln is not a concern in that module"],
         "name": "minimist",
-        "effects": ["opencollective"]
+        "effects": ["opencollective", "mkdirp"]
       }],
       "CVE-2020-7598": [{
         "note": ["opencollective uses an old version of minimist. opencollective is used to ask for funding and the reported vulnerability is not a concern in that module"],
         "name": "minimist",
         "effects": ["opencollective"]
+      }],
+      "CVE-2020-15168": [{
+        "note": ["swagger-editor isomorphic-fetch which uses node-fetch. The github and CVE list the severity as low/medium, while what is returned by the query to the github db says hight in one place and low in the other. This is unlikely to be an issue in use in swagger-editor and it seems like the rating should be low so just allow"],
+        "name": "node-fetch",
+        "effects": ["isomorphic-fetch"]
       }]
     }
   }
```

## Results

```shell
https://github.com/nodeshift/nodejs-reference-architecture/actions/runs/3292365882/jobs/5427642897

(1): The "cldr-localenames-full" seems that is lacking appropriate testing (https://www.github.com/unicode-cldr/cldr-json)
(2): The module "cldr-localenames-full" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(3): The module "cldr-localenames-full" seems to have no available TypeScript typings.
(4): The module "eslint" is not tested (skipped) by community CITGM runs.
(5): The module "eslint" has "107" dependencies (including sub-dependencies) which is more than the default "20".
(6): The module "express" has "55" dependencies (including sub-dependencies) which is more than the default "20".
(7): The module "express-prom-bundle" is not tested by community CITGM runs.
(8): The module "helmet" is not tested by community CITGM runs.
(9): The module "ibmcloud-appid" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(10): The module "ibmcloud-appid" seems to have no available TypeScript typings.
(11): The module "ibmcloud-appid" has "125" dependencies (including sub-dependencies) which is more than the default "20".
(12): The module "i18next" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(13): The module "i18next" is not tested by community CITGM runs.
(14): The latest release of "i18next-icu" was over 1 year ago
(15): The module "i18next-icu" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(16): The module "i18next-icu" seems to have no available TypeScript typings.
(17): The module "i18next-icu" is not tested by community CITGM runs.
(18): The module "i18next-http-middleware" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(19): The module "i18next-http-middleware" is not tested by community CITGM runs.
(20): The module "i18next-fs-backend" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(21): The module "i18next-fs-backend" seems to have no available TypeScript typings.
(22): The module "i18next-fs-backend" is not tested by community CITGM runs.
(23): The module "ioredis" is not tested by community CITGM runs.
(24): The module "node-rdkafka" seems to have no available TypeScript typings.
(25): The module "node-rdkafka" is not tested by community CITGM runs.
(26): The module "passport" is not tested by community CITGM runs.
(27): The module "pino" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(28): The module "rhea" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(29): The module "rhea" is not tested by community CITGM runs.
(30): The module "lru-cache" is not tested by community CITGM runs.
(31): The module "mocha" is not tested (skipped) by community CITGM runs.
(32): The module "mocha" has "72" dependencies (including sub-dependencies) which is more than the default "20".
(33): The "jest" seems that is lacking appropriate testing (https://www.github.com/facebook/jest)
(34): The module "jest" has "259" dependencies (including sub-dependencies) which is more than the default "20".
(35): The module "@ibm-cloud/cloudant" has "98" dependencies (including sub-dependencies) which is more than the default "20".
(36): The latest release of "nano" was 7 months ago
(37): The module "nano" is not tested by community CITGM runs.
(38): The module "nano" has "21" dependencies (including sub-dependencies) which is more than the default "20".
(39): The module "@elastic/elasticsearch" is not tested by community CITGM runs.
(40): The module "odbc" is not tested by community CITGM runs.
(41): The module "odbc" has "57" dependencies (including sub-dependencies) which is more than the default "20".
(42): The module "ibm_db" has "57" dependencies (including sub-dependencies) which is more than the default "20".
(43): The module "mongodb" is not tested by community CITGM runs.
(44): The module "mongodb" has "85" dependencies (including sub-dependencies) which is more than the default "20".
(45): The module "pg" is not tested by community CITGM runs.
(46): The module "kafkajs" is not tested by community CITGM runs.
(47): The "@openapitools/openapi-generator-cli" seems that is lacking appropriate testing (https://www.github.com/OpenAPITools/openapi-generator-cli)
(48): The module "@openapitools/openapi-generator-cli" seems to have no available TypeScript typings.
(49): The module "@openapitools/openapi-generator-cli" is not tested by community CITGM runs.
(50): The module "@openapitools/openapi-generator-cli" has "97" dependencies (including sub-dependencies) which is more than the default "20".
(51): The module "openapi-backend" is not tested by community CITGM runs.
(52): The module "openapi-backend" has "28" dependencies (including sub-dependencies) which is more than the default "20".
(53): The module "@stoplight/prism-cli" has no support for the LTS version(s) 14.20.1 of Node.js.
(54): The module "@stoplight/prism-cli" is not tested by community CITGM runs.
(55): The module "@stoplight/prism-cli" has "212" dependencies (including sub-dependencies) which is more than the default "20".
(56): The module "express-openapi-validator" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(57): The module "express-openapi-validator" seems to have no available TypeScript typings.
(58): The module "express-openapi-validator" is not tested by community CITGM runs.
(59): The module "express-openapi-validator" has "53" dependencies (including sub-dependencies) which is more than the default "20".
(60): The module "swagger-editor" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(61): The module "swagger-editor" seems to have no available TypeScript typings.
(62): The module "swagger-editor" is not tested by community CITGM runs.
(63): The module "swagger-editor" has "221" dependencies (including sub-dependencies) which is more than the default "20".
(64): The latest release of "openapi-editor" was almost 2 years ago
(65): The module "openapi-editor" is not tested by community CITGM runs.
(66): The module "openapi-editor" has "195" dependencies (including sub-dependencies) which is more than the default "20".
(67): The latest release of "nyc" was over 2 years ago
(68): The module "nyc" seems to have no available TypeScript typings.
(69): The module "nyc" is not tested by community CITGM runs.
(70): The module "nyc" has "143" dependencies (including sub-dependencies) which is more than the default "20".
(71): The module "dotenv" is not tested by community CITGM runs.
(72): The latest release of "node-vault" was over 1 year ago
(73): The module "node-vault" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(74): The module "node-vault" is not tested by community CITGM runs.
(75): The module "node-vault" has "55" dependencies (including sub-dependencies) which is more than the default "20".
(76): The module "@ibm-cloud/secrets-manager" seems to have no available TypeScript typings.
(77): The module "@ibm-cloud/secrets-manager" is not tested by community CITGM runs.
(78): The module "@ibm-cloud/secrets-manager" has "98" dependencies (including sub-dependencies) which is more than the default "20".
(79): The module "@opentelemetry/sdk-trace-base" is not tested by community CITGM runs.
(80): The module "@opentelemetry/sdk-trace-node" is not tested by community CITGM runs.
(81): The module "axios" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(82): The module "axios" is not tested by community CITGM runs.
(83): The module "node-fetch" is not tested by community CITGM runs.

problems: 83 (errors: 0 - warnings: 83)
```

New since last review (excluding ones were # deps was already over limit and changed):
```
> (36): The latest release of "nano" was 7 months ago
> (38): The module "nano" has "21" dependencies (including sub-dependencies) which is more than the default "20".
> (44): The module "mongodb" has "85" dependencies (including sub-dependencies) which is more than the default "20".
> (64): The latest release of "openapi-editor" was almost 2 years ago
> (67): The latest release of "nyc" was over 2 years ago
> (72): The latest release of "node-vault" was over 1 year ago
> (78): The module "@ibm-cloud/secrets-manager" has "98" dependencies (including sub-dependencies) which is more than the default "20".
> (79): The module "@opentelemetry/sdk-trace-base" is not tested by community CITGM runs.
> (81): The module "axios" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
> (82): The module "axios" is not tested by community CITGM runs.
> (83): The module "node-fetch" is not tested by community CITGM runs.
```
## Notes

* As of recent publish of node-rdkafka this issue is report `"note": "dev dependency toolkit-jsdoc appears to be UNLICENCED (reports as Undefined) and shoujld not be installed, not required for non-dev use",`. Not quite sure why it was not reported in earlier releases, but care should be taken and generally it would be good to only install node-rdkafka in production mode to avoid installing toolkit-jsdoc.
* The report for `CVE-2020-15168` against node-fetch seems odd in CVE says the issue is of low severity but report metadata returned through the API does conflicts with that. Since it is used in swagger-editor most likely to hit the APIs you are documenting/testing, it is likely low risk that the problem reported will be a concern.
* Additional flavors of BSD or BSD like licences are now reported, as always review/confirm these licences are acceptable to your organization.
* In terms of the specific new reports listed above, none of those are a concern such that we'd adjust/change their inclusion in the reference arcahtieture.
 

