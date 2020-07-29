# Internationalization

## Recommended Components

* Built in to JavaScript

Ecma-402/Ecma-262 support for `Intl` object and related functionality such as String.localeCompare [Node Intl.html](https://github.com/nodejs/node/blob/master/doc/api/intl.md) . Widely supported, growing feature set. Use the API when possible. (Also available on all major browsers.) These functions, in general, accept a Locale string (such as `en-CA` for English in Canada) to specify which language and cultural preference should be used.

- Collation: language-sensitive comparison and sorting
  - Always use `String.localeCompare()` to compare textual content from users.
- Date/Time and Number formatting: language-aware output of dates/times and numbers.

- Upper/Lower casing and normalization: converting strings to a normalized or cased form…  In many languages, there are multiple representations of the same character which will not compare as equal with `===` unless they are normalized. In Turkish, the uppercase of `i` is `İ` (with a dot), not `I` (without a dot).

* Language data use by the above functions is bundled into the Node.js runtime As of Node.js 13. For versions prior to Node.js 13
  this data must be installed separately and configured as outlined in [providing icu data at runtime](https://github.com/nodejs/node/blob/master/doc/api/intl.md#providing-icu-data-at-runtime).  We recommend using the [full-icu]( https://www.npmjs.com/package/full-icu) module to install this data when needed.

The built-in `Intl` does not currently support some of the functionality that may be required for an internationalized user experience. For example, a common requirement is to present a translated version of a message such as `You have ${count} messages.` Two components are required:

- Resource Loading: A way to load the translated version of this message. The application must be able to find a suitable fallback if the user’s specific language and region is not available, possibly falling back to a different language if the message has not been translated yet. Other types of resources, such as images, may need to be loaded as well.

- Message Format: Once a message is loaded, a library must be called to format this string, along with the parameter data, to produce the final string to display to the user.
  - English (Canada): `You have ${count} messages.` -> **You have 1,234 messages.**
  - Spanish (Spain): `Tienes ${count} mensajes.` -> **Tienes 1.234 mensajes.**
  - Note: that translation may require a re-ordering of the substituted components, and is also affected by specific plural rules in a particular language.

For Resource Loading and Message Format, we recommend [i18next](https://www.i18next.com/) --  With >500,000 downloads a month, i18next is one of the most popular internationalization framework for Node.js.
It provides the capabilities needed to manage strings within your application so that they can be
displayed in the locale appropriate for the end user. It is also supported on the browser.

  - We recommend using i18next with the [i18next-icu](https://www.npmjs.com/package/i18next-icu) module so that ICU MessageFormat syntax is used. There is industry wide work to standardize on the MessageFormat syntax. For more details you can read about current progress [https://github.com/unicode-org/message-format-wg](https://github.com/unicode-org/message-format-wg).

  - For loading localized content, we recommend using [i18next-node-fs-backend](https://www.npmjs.com/package/i18next-node-fs-backend) which is a backend that allows you to load translated resources as JSON files from the filesystem.

  - If you are using express or a web framework that supports express middleware, [i18next-express-middleware](https://github.com/i18next/i18next-express-middleware)
  provides support for language detection/management when using i18next.

Translated Language and Region Names: Applications which display a list of languages or countries/regions to users often must translate that list into many other languages according to their ISO code. Using the industry-standard vetted [CLDR](https://unicode.org/cldr) data will avoid the need to manually maintain and translate such a list. We recommend that you use this data via its [NPM module](https://npmjs.com/package/cldr-localenames-full). For example, to fetch the name of "French" in "Spanish". Note that this is a large package, containing data for over 500 locales.

```shell
$ npm i cldr-localenames-full
$ node -p "require('cldr-localenames-full/main/es/languages').main.es.localeDisplayNames.languages['fr']"
francés
```

Also Note that there is ongoing active work to move the above features into JavaScript. To see details or even to influence the priorities, see [github.com/tc39/ecma402](https://github.com/tc39/proposals/blob/master/ecma402/README.md#active-proposals).


## Guidance

### When to internationalize

Internationalizing your application will require some extra work. If your company supports their applications across geographies it's beneficial
to build in the internationalization components from the start. In addition, if it's a case of when the application will go into production
versus if, it is also beneficial to build internationalization in from the start.

On the other hand, for initial proof of concepts or limited releases where time to delivery is critical, the additional cost could prevent the project
from being successful and it's accepted that hard coding strings is ok. The same is also often true for one-off demos and other
similar short lived assets.

### Logging

It is not recommended to translate low-level error and status messages.
See [logging](./logging.md) for additional guidance.

