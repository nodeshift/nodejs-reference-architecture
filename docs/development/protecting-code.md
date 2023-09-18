# Protecting Code

Within some organizations (including IBM) there are requirements
to protect source code.

The motivations that have been mentioned include:

* protection of intellectual property by making it harder for the
  code to be copied.
* making it easier to pursue those who copy it by ensuring
  it takes more than casual/accidental access to the code to see it.
* reducing exposure to liability by limiting analysis of the
  code.
* making it harder for hackers to find/exploit vulnerabilities
  in the code. 

The preferred approach to protect source code is most often
by shipping binaries after the source code has been compiled.
This is not an option for JavaScript (without extreme effort
for front-end JavaScript and significant effort for server side JavaScript)
and `obfuscation` is typically used instead.

Only source code that is available to customers or end users needs
to be protected. Front-end JavaScript is almost always available
to end users and while less common, back-end JavaScript may be
available to customers when it is included in products that
are sold to and run by customers.

It is understood that obfuscation does not make it impossible
to recover the original source code, only that is is harder
and that steps have been taken to avoid obvious disclosure.

## Recommendation Components

N/A
## Guidance

Before employing obfuscation, validate that the value provided
by obfuscation warrants the effort and downsides. Including
license headers in the code may be an alternative in some cases.
If the product is based on an open source upstream, the code is already
available publicly and therefore many of the motivations listed above
will not apply. Typically obfuscation is not used within Red Hat
as products are based on freely available open source.

Minification is a related practice to obfuscation in that it
makes source code less readable with the motivation of reducing
the number of bytes that must be transferred to a clients browser.
It is widely used for front-end JavaScript.

In the team's experience the use of existing minification tools
are often enough to meet an organization's requirement for obfuscation.
These tools are broadly used, and therefore add little risk of
functional or performance issues being introduced. Our teams have
had success using [Terser](https://www.npmjs.com/package/terser) and
[esbuild](https://esbuild.github.io/).

If you are going to both minify and use a separate obfuscator,
minify first.

Expect a performance degradation if you use an obfuscator as
opposed to one of the minification tools. For example
[javascript-obfuscator](https://www.npmjs.com/package/javascript-obfuscator)
indicates you can expect your code to be 15-80% slower.

For those cases where minification tools are not sufficient one of
our teams has used [bytenode](https://github.com/bytenode/bytenode)
succesfully.

### Source maps

One of the downsides of using obfuscation is that it makes
debugging more difficult. minification tools typically support
the generation of
[source maps](https://en.wikipedia.org/wiki/Minification_(programming)#Source_mapping)
which can help map back to the original source code. Making
source maps available would at least partially invalidate
the benefits of obfuscation so when obfuscation is a requirement they
should not be made publicly available.

Source maps should still be generated and stored with the original
source code for each release. For front-end JavaScript teams should validate
the process of using offline source maps in their typical problem
investigation workflow. This
[article](https://dev.to/ivanstanevich/using-js-source-maps-in-production-1ecc)
has some suggestions for doing that.

For back end JavaScript it should be possible to use the source maps
to get a readable stack trace from a minified version provided by a
customer. There are packages to do this like [stacktracey](https://github.com/xpl/stacktracey),
however, the team does not have direct experience doing this yet to report on
how easy that is to do.


