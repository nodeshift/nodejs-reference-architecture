# npcheck review - July 21 2023

No major concerns were noted in this review.

## Diff in npcheck.json since last review 

```shell
diff --git a/npcheck.json b/npcheck.json
index 517047f..4a9bb4b 100644
--- a/npcheck.json
+++ b/npcheck.json
@@ -428,6 +428,16 @@
       "section": [
         "Consuming Services"
       ]
+    },
+    {
+      "name": "cors",
+      "npmlink": "https://www.npmjs.com/package/cors",
+      "reviewlevel": "Yearly Watch",
+      "activitycurrent": "None",
+      "activitytarget": "None",
+      "section": [
+        "CORS"
+      ]
     }
   ],
   "licenses": {
@@ -517,6 +527,14 @@
         "note": "dependency spdx-exceptions uses CC-BY-3.0 allows broad use with attribution",
         "note": "dependency argparse@2.0.1 uses Python-2.0",
         "allow": ["Artistic-2.0", "CC0-1.0", "CC-BY-3.0", "Python-2.0" ]
+      },
+      "@opentelemetry/sdk-trace-base": {
+        "note": "dependency tslib@2.6.0 uses which is less restrictive than BSD",
+         "allow": ["0BSD" ]
+      },
+      "@opentelemetry/sdk-trace-node": {
+        "note": "dependency tslib@2.6.0 uses which is less restrictive than BSD",
+         "allow": ["0BSD" ]
       }
     }
   },
```

## Results

```shell
https://github.com/nodeshift/nodejs-reference-architecture/actions/runs/5625511727/job/15244434732

NPCheck Report
(1): The "cldr-localenames-full" seems that is lacking appropriate testing (https://www.github.com/unicode-cldr/cldr-json)
(2): The module "cldr-localenames-full" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(3): The module "cldr-localenames-full" seems to have no available TypeScript typings.
(4): The module "eslint" seems to have no available TypeScript typings.
(5): The module "eslint" has "95" dependencies (including sub-dependencies) which is more than the default "20".
(6): The latest release of "express" was 10 months ago
(7): The module "express" seems to have no available TypeScript typings.
(8): The module "express" has "56" dependencies (including sub-dependencies) which is more than the default "20".
(9): The latest release of "express-prom-bundle" was 7 months ago
(10): The module "ibmcloud-appid" has "213" dependencies (including sub-dependencies) which is more than the default "20".
(11): The module "i18next" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(12): The module "i18next" is not tested by community CITGM runs.
(13): The module "i18next-icu" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(14): The module "i18next-http-middleware" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(15): The module "i18next-fs-backend" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(16): The module "ioredis" is not tested by community CITGM runs.
(17): The module "node-rdkafka" seems to have no available TypeScript typings.
(18): The module "opossum" seems to have no available TypeScript typings.
(19): The latest release of "passport" was about 1 year ago
(20): The module "passport" seems to have no available TypeScript typings.
(21): The module "pino" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(22): The module "pino" has "22" dependencies (including sub-dependencies) which is more than the default "20".
(23): The module "rhea" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(24): The latest release of "mocha" was 7 months ago
(25): The module "mocha" seems to have no available TypeScript typings.
(26): The module "mocha" has "72" dependencies (including sub-dependencies) which is more than the default "20".
(27): The "jest" seems that is lacking appropriate testing (https://www.github.com/facebook/jest)
(28): The module "jest" has "260" dependencies (including sub-dependencies) which is more than the default "20".
(29): The module "@ibm-cloud/cloudant" has "87" dependencies (including sub-dependencies) which is more than the default "20".
(30): The module "odbc" has "57" dependencies (including sub-dependencies) which is more than the default "20".
(31): The module "ibm_db" seems to have no available TypeScript typings.
(32): The module "ibm_db" has "38" dependencies (including sub-dependencies) which is more than the default "20".
(33): The module "mongodb" is not tested by community CITGM runs.
(34): The module "pg" seems to have no available TypeScript typings.
(35): The module "pg" is not tested by community CITGM runs.
(36): The "@openapitools/openapi-generator-cli" seems that is lacking appropriate testing (https://www.github.com/OpenAPITools/openapi-generator-cli)
(37): The module "@openapitools/openapi-generator-cli" seems to have no available TypeScript typings.
(38): The module "@openapitools/openapi-generator-cli" has "106" dependencies (including sub-dependencies) which is more than the default "20".
(39): The module "openapi-backend" has "32" dependencies (including sub-dependencies) which is more than the default "20".
(40): The module "@stoplight/prism-cli" is not tested by community CITGM runs.
(41): The module "@stoplight/prism-cli" has "176" dependencies (including sub-dependencies) which is more than the default "20".
(42): The module "express-openapi-validator" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(43): The module "express-openapi-validator" seems to have no available TypeScript typings.
(44): The module "express-openapi-validator" has "56" dependencies (including sub-dependencies) which is more than the default "20".
(45): The module "swagger-editor" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(46): The module "swagger-editor" seems to have no available TypeScript typings.
(47): The module "swagger-editor" has "319" dependencies (including sub-dependencies) which is more than the default "20".
(48): The latest release of "openapi-editor" was over 2 years ago
(49): The module "openapi-editor" has "199" dependencies (including sub-dependencies) which is more than the default "20".
(50): The latest release of "nyc" was about 3 years ago
(51): The module "nyc" seems to have no available TypeScript typings.
(52): The module "nyc" is not tested by community CITGM runs.
(53): The module "nyc" has "145" dependencies (including sub-dependencies) which is more than the default "20".
(54): The module "dotenv" is not tested by community CITGM runs.
(55): The module "node-vault" seems to have no available TypeScript typings.
(56): The module "node-vault" is not tested by community CITGM runs.
(57): The module "node-vault" has "59" dependencies (including sub-dependencies) which is more than the default "20".
(58): The module "@ibm-cloud/secrets-manager" seems to have no available TypeScript typings.
(59): The module "@ibm-cloud/secrets-manager" is not tested by community CITGM runs.
(60): The module "@ibm-cloud/secrets-manager" has "87" dependencies (including sub-dependencies) which is more than the default "20".
(61): The module "@opentelemetry/sdk-trace-base" is not tested by community CITGM runs.
(62): The module "@opentelemetry/sdk-trace-node" is not tested by community CITGM runs.
(63): The module "axios" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(64): The module "axios" is not tested by community CITGM runs.
(65): The module "node-fetch" is not tested by community CITGM runs.
(66): The latest release of "cors" was over 4 years ago
(67): The module "cors" seems to have no available TypeScript typings.
(68): The module "cors" is not tested by community CITGM runs.

problems: 68 (errors: 0 - warnings: 68)


```

New (materially) since last review (excluding ones were # deps was already over limit and changed):
```
3): The module "cldr-localenames-full" seems to have no available TypeScript typings.
(4): The module "eslint" seems to have no available TypeScript typings.
(7): The module "express" seems to have no available TypeScript typings.
(9): The latest release of "express-prom-bundle" was 7 months ago
(18): The module "opossum" seems to have no available TypeScript typings.
(20): The module "passport" seems to have no available TypeScript typings.
(22): The module "pino" has "22" dependencies (including sub-dependencies) which is more than the default "20".
(24): The latest release of "mocha" was 7 months ago
(25): The module "mocha" seems to have no available TypeScript typings.
(31): The module "ibm_db" seems to have no available TypeScript typings.
(34): The module "pg" seems to have no available TypeScript typings.
(46): The module "swagger-editor" seems to have no available TypeScript typings.
(51): The module "nyc" seems to have no available TypeScript typings.
(55): The module "node-vault" seems to have no available TypeScript typings.
(66): The latest release of "cors" was over 4 years ago
(67): The module "cors" seems to have no available TypeScript typings.
(68): The module "cors" is not tested by community CITGM runs.
```
## Notes
The increased warnings about no avilable TypeScript typings is because the api we used to use
to find typings was deprecated and we have not managed to find an alternative yet. This
results in modules that have typings now being reported as not having them.


