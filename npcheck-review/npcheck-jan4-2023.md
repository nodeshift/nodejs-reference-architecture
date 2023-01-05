# npcheck review - October 20 - 2022

No major concerns were noted in this review.

## Diff in npcheck.json since last review 

```shell
diff --git a/npcheck.json b/npcheck.json
index 914e682..106fed5 100644
--- a/npcheck.json
+++ b/npcheck.json
@@ -173,6 +173,7 @@
     "allow": [
       "MIT", 
       "Apache-2.0", 
+      "Apache 2.0", 
       "ISC", 
       "BSD-2-Clause", 
       "BSD-3-Clause", 
@@ -185,7 +186,9 @@
         "allow": ["Apache"]
       },
       "ibmcloud-appid": {
-        "allow": ["BSD"]
+        "note": "dependency spdx-exceptions,spdx-license-ids uses CC0-1.0 indicates no copyright",
+        "note": "dependency spdx-exceptions uses CC-BY-3.0 allows broad use with attribution",
+        "allow": ["BSD", "CC0-1.0", "CC-BY-3.0" ]
       },
       "i18next-icu":{
         "allow": ["0BSD"]
@@ -246,13 +249,49 @@
       "mongodb": {
         "note": "dependency tslib@2.3.1 reports 0BSD which is less restrictive than BSD",
         "allow": ["0BSD"]
+      },
+      "@ibm-cloud/secrets-manager": {
+        "note": "dependency npm uses Artistic-2.0 which allows any use but no modifications",
+        "note": "dependency spdx-exceptions,spdx-license-ids uses CC0-1.0 indicates no copyright",
+        "note": "dependency spdx-exceptions uses CC-BY-3.0 allows broad use with attribution",
+        "allow": ["Artistic-2.0", "CC0-1.0", "CC-BY-3.0" ]
       }
     }
   },
   "citgm": {
     "note-1" : "ibmcloud-appid, @ibm-cloud/cloudant, opossum, ibm_db are Red Hat/IBM modules that would need broader usage before being considered for CITGM",
     "note-2" : "cldr-localenames-full does not have tests as it is a data delivery module and therefore does not beong in CITGM",
-    "skip": ["ibmcloud-appid", "@ibm-cloud/cloudant", "opossum", "ibm_db", "cldr-localenames-full"]
+    "note-3" : "eslint and mocha look to be permanently skipped in CIGTM due to needing headless chrome to run tests",
+    "note-4" : "node-rdkafka, rhea, odbc, @openapitools/openapi-generator-cli, openapi-backend, @stoplight/prism-http, express-openapi-validator, swagger-editor, openapi-editor have low download numbers and will be skipped in CITGM",
+    "note-5" : "kafkajs, @elastic/elasticsearch, helmet, passport propose additions to CITGM in the future",
+    "note-6" : "nano, express-prom-bundle, i18next-icu, i18next-http-middleware, i18next-fs-backend review in the future to see if they make sense to add to CITGM",
+    "skip": [
+      "ibmcloud-appid",
+      "@ibm-cloud/cloudant",
+      "opossum",
+      "ibm_db",
+      "cldr-localenames-full",
+      "eslint",
+      "mocha",
+      "node-rdkafka",
+      "rhea",
+      "odbc",
+      "@openapitools/openapi-generator-cli",
+      "openapi-backend",
+      "@stoplight/prism-http",
+      "express-openapi-validator",
+      "swagger-editor",
+      "openapi-editor",
+      "kafkajs",
+      "@elastic/elasticsearch",
+      "helmet",
+      "passport",
+      "nano",
+      "express-prom-bundle",
+      "i18next-icu",
+      "i18next-http-middleware",
+      "i18next-fs-backend"
+    ]
   },
   "audit": {
     "allow": {
@@ -264,7 +303,7 @@
       }],
       "CVE-2021-44906": [{
         "note": ["opencollective uses an old version of minimist. opencollective is used to ask for funding and the reported vulnerability is not a concern in that module"],
-	"note": ["mocha uses an old version of mkdirp. mocha is used for testing and the proptotype pollution vuln is not a concern in that module"],
+        "note": ["mocha uses an old version of mkdirp. mocha is used for testing and the proptotype pollution vuln is not a concern in that module"],
         "name": "minimist",
         "effects": ["opencollective", "mkdirp"]
       }],
@@ -274,9 +313,16 @@
         "effects": ["opencollective"]
       }],
       "CVE-2020-15168": [{
-        "note": ["swagger-editor isomorphic-fetch which uses node-fetch. The github and CVE list the severity as low/medium, while what is returned by the query to the github db says hight in one place and low in the other. This is unlikely to be an issue in use in swagger-editor and it seems like the rating should be low so just allow"],
+        "note": ["swagger-editor uses an old version of minimist. opencollective is used to ask for funding and the reported vulnerability is not a concern in that module"],
+        "note": ["swagger-editor isomorphic-fetch which uses node-fetch. The github and CVE list the severity as low/medium, while what is returned by the query to the github db says high in one place and low in the other. This is unlikely to be an issue in use in swagger-editor and it seems like the rating should be low so just allow"],
+        "note": ["swagger-client uses cross-fetch which uses node-fetch. The github and CVE list the severity as low/medium, while what is returned by the query to the github db says high in one place and low in the other. This is unlikely to be an issue in use in swagger-editor and it seems like the rating should be low so just allow"],
         "name": "node-fetch",
-        "effects": ["isomorphic-fetch"]
+        "effects": ["isomorphic-fetch", "cross-fetch", "opencollective"]
+      }],
+      "CVE-2022-3517": [{
+        "note": ["node-rdkafka uses a version of mocha that uses an old version of minimatch, as mocha is a test package used in dev, the ReDoS impact/risk is likely low"],
+        "name": "minimatch",
+        "effects": ["mocha"]
       }]
     }
   }
```

## Results

```shell
https://github.com/nodeshift/nodejs-reference-architecture/actions/runs/3842654743/jobs/6544158794

(1): The "cldr-localenames-full" seems that is lacking appropriate testing (https://www.github.com/unicode-cldr/cldr-json)
(2): The module "cldr-localenames-full" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(3): The module "cldr-localenames-full" seems to have no available TypeScript typings.
(4): The module "eslint" has "95" dependencies (including sub-dependencies) which is more than the default "20".
(5): The module "express" has "55" dependencies (including sub-dependencies) which is more than the default "20".
(6): The module "ibmcloud-appid" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(7): The module "ibmcloud-appid" has "218" dependencies (including sub-dependencies) which is more than the default "20".
(8): The module "i18next" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(9): The module "i18next" is not tested by community CITGM runs.
(10): The module "i18next-icu" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(11): The latest release of "i18next-http-middleware" was 7 months ago
(12): The module "i18next-http-middleware" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(13): The module "i18next-fs-backend" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(14): The module "ioredis" is not tested by community CITGM runs.
(15): The module "node-rdkafka" seems to have no available TypeScript typings.
(16): The latest release of "passport" was 8 months ago
(17): The module "pino" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(18): The module "rhea" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(19): The module "lru-cache" is not tested by community CITGM runs.
(20): The module "mocha" has "72" dependencies (including sub-dependencies) which is more than the default "20".
(21): The "jest" seems that is lacking appropriate testing (https://www.github.com/facebook/jest)
(22): The module "jest" has "259" dependencies (including sub-dependencies) which is more than the default "20".
(23): The module "@ibm-cloud/cloudant" has "98" dependencies (including sub-dependencies) which is more than the default "20".
(24): The module "nano" has "30" dependencies (including sub-dependencies) which is more than the default "20".
(25): The module "odbc" has "57" dependencies (including sub-dependencies) which is more than the default "20".
(26): The module "ibm_db" has "57" dependencies (including sub-dependencies) which is more than the default "20".
(27): The module "mongodb" is not tested by community CITGM runs.
(28): The module "mongodb" has "88" dependencies (including sub-dependencies) which is more than the default "20".
(29): The module "pg" is not tested by community CITGM runs.
(30): The "@openapitools/openapi-generator-cli" seems that is lacking appropriate testing (https://www.github.com/OpenAPITools/openapi-generator-cli)
(31): The module "@openapitools/openapi-generator-cli" seems to have no available TypeScript typings.
(32): The module "@openapitools/openapi-generator-cli" has "97" dependencies (including sub-dependencies) which is more than the default "20".
(33): The module "openapi-backend" has "28" dependencies (including sub-dependencies) which is more than the default "20".
(34): The module "@stoplight/prism-cli" has no support for the LTS version(s) 14.21.2 of Node.js.
(35): The module "@stoplight/prism-cli" is not tested by community CITGM runs.
(36): The module "@stoplight/prism-cli" has "212" dependencies (including sub-dependencies) which is more than the default "20".
(37): The module "express-openapi-validator" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(38): The module "express-openapi-validator" seems to have no available TypeScript typings.
(39): The module "express-openapi-validator" has "55" dependencies (including sub-dependencies) which is more than the default "20".
(40): The module "swagger-editor" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(41): The module "swagger-editor" seems to have no available TypeScript typings.
(42): The module "swagger-editor" has "258" dependencies (including sub-dependencies) which is more than the default "20".
(43): The latest release of "openapi-editor" was about 2 years ago
(44): The module "openapi-editor" has "197" dependencies (including sub-dependencies) which is more than the default "20".
(45): The latest release of "nyc" was over 2 years ago
(46): The module "nyc" seems to have no available TypeScript typings.
(47): The module "nyc" is not tested by community CITGM runs.
(48): The module "nyc" has "145" dependencies (including sub-dependencies) which is more than the default "20".
(49): The module "dotenv" is not tested by community CITGM runs.
(50): The latest release of "node-vault" was over 1 year ago
(51): The module "node-vault" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(52): The module "node-vault" is not tested by community CITGM runs.
(53): The module "node-vault" has "55" dependencies (including sub-dependencies) which is more than the default "20".
(54): The module "@ibm-cloud/secrets-manager" seems to have no available TypeScript typings.
(55): The module "@ibm-cloud/secrets-manager" is not tested by community CITGM runs.
(56): The module "@ibm-cloud/secrets-manager" has "337" dependencies (including sub-dependencies) which is more than the default "20".
(57): The module "@opentelemetry/sdk-trace-base" is not tested by community CITGM runs.
(58): The module "@opentelemetry/sdk-trace-node" is not tested by community CITGM runs.
(59): The module "axios" does not specify the engines field or package-support.json, so we cannot determine if it supports the LTS versions of Node.js.
(60): The module "axios" is not tested by community CITGM runs.
(61): The module "node-fetch" is not tested by community CITGM runs.

problems: 61 (errors: 0 - warnings: 61)
```

New (materially) since last review (excluding ones were # deps was already over limit and changed):
```
(7): The module "ibmcloud-appid" has "218" dependencies (including sub-dependencies) which is more than the default "20".
(11): The latest release of "i18next-http-middleware" was 7 months ago
(16): The latest release of "passport" was 8 months ago
(43): The latest release of "openapi-editor" was about 2 years ago
(56): The module "@ibm-cloud/secrets-manager" has "337" dependencies (including sub-dependencies) which is more than the default "20".
```
## Notes

* Many warnings about not being tested in CITGM were removed as we allowed them in npmcheck.json as we don't believe they
  would ever be added to CITGM testing
* With respect to 7) and 56) the number of dependencies increased significantly but that will not affect their inclusion in the reference architecture
* In respect to 11), 16), 43) we are not concerned with respect to the Length of time since last release
* Some warnings about not being test in CITGM went away since we've worked to get them added and are continuing to do that for those we believe can make it into CITGM

