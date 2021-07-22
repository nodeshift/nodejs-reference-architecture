

# npcheck review - July 22 - 2021

## Results

```shell
(1): The "cldr-localenames-full" seems that is lacking appropriate testing (https://www.github.com/unicode-cldr/cldr-json)

(2): The module "cldr-localenames-full" appears to have no support for the LTS version(s) 12.22.3, 14.17.3 of Node.js.

(3): The latest release of "express" was over 1 year ago

(4): The latest release of "ibmcloud-appid" was 12 months ago

(5): The module "ibmcloud-appid" appears to have no support for the LTS version(s) 12.22.3, 14.17.3 of Node.js.

(6): The module "i18next" appears to have no support for the LTS version(s) 12.22.3, 14.17.3 of Node.js.

(7): The module "i18next-icu" appears to have no support for the LTS version(s) 12.22.3, 14.17.3 of Node.js.

(8): The module "i18next-http-middleware" appears to have no support for the LTS version(s) 12.22.3, 14.17.3 of Node.js.

(9): The module "i18next-fs-backend" appears to have no support for the LTS version(s) 12.22.3, 14.17.3 of Node.js.

(10): The latest release of "node-rdkafka" was 6 months ago

(11): The latest release of "passport" was over 1 year ago

(12): The module "pino" appears to have no support for the LTS version(s) 12.22.3, 14.17.3 of Node.js.

(13): The module "rhea" appears to have no support for the LTS version(s) 12.22.3, 14.17.3 of Node.js.

(14): The latest release of "lru-cache" was about 1 year ago

problems: 14 (errors: 0 - warnings: 14)
```

## Notes

* With respect to (10) Issues in terms of node-rdkafka have already been noted in the section on messings.
* With respect to (4), (11), (14) we don't see a concern with those not having done a recent release.
* With respect to (3) we are looking at web frameworks but the concensus is still the current recommendations
* With respect to (1), after review it seems that being a data delivery package no testing is needed
* With respect to the comments about "no support", those indicate that the package does not include
  an engines field or package-support.json file. We plan to update the message to indicate that we
  cannot tell autimatically if they support LTS versions. We have no reason to believe any of those
  flagged don't support the current LTS Node.js versions.
