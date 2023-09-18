---
sidebar_position: 5
---

# Testing

## Recommended Packages

The best package to use for testing often depends on the type and scope of a project
versus one size fits all. For that reason we'll mention two of the test frameworks
that the team has had success with.

## Jest - <https://jestjs.io>

[jest][] is a popular testing framework from Facebook. It excels at testing React and other
component-based web applications, and can be used in other contexts. It is considered an
_opinionated_ framework, as it provides its own set of assertions, spies/stubs/mocks, and
other features (such as snapshot testing and code coverage) out-of-the-box.

Jest is now an [OpenJS Foundation project](https://openjsf.org/blog/2022/05/11/openjs-foundation-welcomes-jest/)

## Mocha - <https://mochajs.org>

[mocha][] is a widely used, mature (created in 2011) and stable project. While Node.js
is the main area of focus and support, Mocha can also be used in a browser context.
Mocha is an _unopinionated_ framework with a large ecosystem of plugins and extensions.

Mocha is an [OpenJS Foundation][] project with open governance.

## Guidance

Both Mocha and Jest provide test parallelization. By default this is disabled in Mocha,
as many use-cases see a negative performance impact when running tests in parallel. If you
experience longer test times than expected you should check if enabling or disabling
parallelism will improve test run times.

### When Jest might be the better choice

When testing React or component-based applications.

When using a compile-to-JavaScript language (like TypeScript).

When snapshots are useful. [Snapshots][] provide an easy to use way of testing output
of a function and saving the result as a snapshot artifact, which can then be used to
compare against as a test. As an example:

```shell
test('unknown service', () => {
    expect(() => {
      bindings.getBinding('DOEST_NOT_EXIST');
    }).toThrowErrorMatchingSnapshot('unknown service');
  });
```

The first time the test is run it will create/store a snapshot of the expected exception.
On subsequent runs if the exception does not match the snapshot, it will report
a test failure. This makes generating/capturing the result from an operation being tested
fast and easy.

### When Mocha might be the better choice

When you want a smaller dependency tree (91 packages versus 522).

When Jest's opinions, environment proxies and dependency upon [babel][] are unfavorable for your use-case.

As an example of potential problems with Jest's environment proxies, Jest replaces globals in the environment in a
way that can cause failures with native addons. As an example, this simple test fails:

```JavaScript
const addon = require('bindings')('hello');

describe('test suite 1', () => {
  test('exception', () => {
    expect(addon.exception()).toThrow(TypeError);
  });
});
```

even thought the addon is throwing the expected exception:

```C++
static napi_value ExceptionMethod(napi_env env, napi_callback_info info) {
   napi_throw_type_error(env, "code1", "type exception");
   return NULL;
}
```

and the failure reports the exception as `TypeError: type exception`

```shell
 FAIL  __tests__/test.js
  ● test suite 1 › exception

    TypeError: type exception

      3 | describe('test suite 1', () => {
      4 |   test('exception', () => {
    > 5 |     expect(addon.exception()).toThrow(TypeError);
        |                  ^
      6 |   });
      7 | });
      8 |

      at Object.<anonymous> (__tests__/test.js:5:18)
```

An equivalent test runs successfully with Mocha. The full source for the test is here: https://github.com/nodeshift-blog-examples/jest-with-native-addon-issue

### Recommended Packages to Use Alongside Mocha

Because Mocha is unopinionated, it does not ship with "batteries included." While Mocha is usable
without any other third-party library, many users find the following libraries and tools helpful.

_See the [mocha documentation][] and [examples repository][] for more information on integrating with other tools_.

#### Assertion Library

Most Mocha users will want to consume a third-party _assertion library_. Besides the Node.js
built-in [`assert` module][], Mocha recommends one of the following:

- [chai][]: the most popular general-purpose assertion library, with traditional and "natural language" APIs available
- [unexpected][]: a string-based natural language API, Mocha uses Unexpected in its own tests

Both of the above have their own plugin ecosystems.

#### Stubs, Spies and Mocks

Many users will want a library providing _stubs, spies and mocks_ to aid isolation when writing unit tests.

- [sinon][]: the most popular stub, spy and mock library; mature
- [testdouble][]: a full-featured library with the ability to mock at the module level

Both of the above have their own plugin ecosystems.

#### Code Coverage

Mocha does not automatically compute code coverage. If you need it, use:

- [nyc][]: the most popular code-coverage tool; the successor CLI for Istanbul

For more on Code Coverage, see the [Code Coverage](./code-coverage) section

[`assert` module]: https://nodejs.org/api/assert.html#assert_assert
[babel]: https://babeljs.io
[chai]: https://www.npmjs.com/package/chai
[examples repository]: https://github.com/mochajs/mocha-examples
[jest]: https://www.npmjs.com/package/jest
[karma]: https://www.npmjs.com/package/karma
[mocha documentation]: https://mochajs.org
[mocha]: https://www.npmjs.com/package/mocha
[nyc]: https://www.npmjs.com/package/nyc
[openjs foundation]: https://openjsf.org
[protractor]: https://www.npmjs.com/package/protractor
[sinon]: https://www.npmjs.com/package/sinon
[testdouble]: https://www.npmjs.com/package/testdouble
[unexpected]: https://www.npmjs.com/package/unexpected
[webdriverio]: https://www.npmjs.org/package/webdriverio
[snapshots]: https://jestjs.io/docs/snapshot-testing

## Further Reading

* [Introduction to the Node.js reference architecture: Testing](https://developers.redhat.com/articles/2023/07/27/introduction-nodejs-reference-architecture-testing)
