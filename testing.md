# Testing

## Recommended Packages

## Mocha - https://mochajs.org

[Mocha][] is the most _depended-upon_ package on the npm registry. It is a mature (created in 2011) and stable project. While Node.js is the main area of focus and support, Mocha can also be used in a browser context.  Mocha values flexibility, and as such, is considered an _unopinionated_ framework.  Mocha has a large ecosystem of plugins and extensions.

Mocha is an [OpenJS Foundation][] project with open governance.  An IBMer (@boneskull) is a lead maintainer of the project.

## Jest - https://jestjs.io

[Jest][] is a popular testing framework from Facebook.  It excels at testing React and other component-based web applications, and can be used in other contexts.  It is considered an _opinionated_ framework, as it provides its own set of assertions, spies/stubs/mocks, and other features (such as snapshot testing and code coverage) out-of-the-box.

Jest is owned by Facebook.

## Guidance

While in some cases the choice between the two frameworks is a matter of personal or team preference, Jest has a clear advantage when unit testing React- or component-based applications.  Jest's opinions, environment proxies and dependency upon [Babel][] may be unfavorable for your use-case.  Mocha provides the same environment as the context in which it runs (Node.js or browser), which makes it suitable for testing directly within a real browser.  When using a compile-to-JavaScript language (like TypeScript), Jest has better support out-of-the-box.

Both Mocha and Jest provide test parallelization, but this is disabled by default in Mocha, as many use-cases see a negative performance impact when running tests in parallel.

Mocha supports ESM natively in Node.js v12 and newer.

Both testing frameworks are used widely within IBM, though Mocha is supported directly.

### Recommended Packages to Use Alongside Mocha

Because Mocha is unopinionated, it does not ship with "batteries included."  While Mocha is usable without any other third-party library, many users find the following libraries and tools helpful.

_See the [Mocha documentation][] and [examples repository][] for more information on integrating with other tools_.

#### Assertion Library

Most Mocha users will want to consume a third-party _assertion library_.  Besides the Node.js built-in [`assert` module][], Mocha recommends one of the following:

- [Chai][]: the most popular general-purpose assertion library, with traditional and "natural language" APIs available 
- [Unexpected][]: a string-based natural language API, Mocha uses Unexpected in its own tests

Both of the above have their own plugin ecosystems.

#### Stubs, Spies and Mocks

Many users will want a library providing _stubs, spies and mocks_ to aid isolation when writing unit tests.

- [Sinon][]: the most popular stub, spy and mock library; mature
- [Testdouble][]: a full-featured library with the ability to mock at the module level

Both of the above have their own plugin ecosystems.

#### Code Coverage

Mocha does not automatically compute code coverage. If you need it, use:

- [nyc][]: the most popular code-coverage tool; the successor CLI for Istanbul

#### Running Tests in the Browser

Mocha runs natively in a browser, but it does not provide means of automation. For integration into your CI suite, use:

- [webdriverio][]: for end-to-end tests of any browser-based application
- [Protractor][]: for end-to-end tests of Angular/AngularJS applications
- [Karma][]: a general-purpose _test runner_ for browser automation with a large ecosystem of plugins; can be used for a variety of testing strategies and across different browsers

### Recommended Packages to use Alongside Jest

TBD

[`assert` module]: https://nodejs.org/api/assert.html#assert_assert
[Babel]: https://babeljs.io
[Chai]: https://www.npmjs.com/package/chai
[examples repository]: https://github.com/mochajs/mocha-examples
[Jest]: https://www.npmjs.com/package/jest
[Karma]: https://www.npmjs.com/package/karma
[Mocha documentation]: https://mochajs.org
[Mocha]: https://www.npmjs.com/package/mocha
[nyc]: https://www.npmjs.com/package/nyc
[OpenJS Foundation]: https://openjsf.org
[Protractor]: https://www.npmjs.com/package/protractor
[Sinon]: https://www.npmjs.com/package/sinon
[Testdouble]: https://www.npmjs.com/package/testdouble
[Unexpected]: https://www.npmjs.com/package/unexpected
[webdriverio]: https://www.npmjs.org/package/webdriverio
