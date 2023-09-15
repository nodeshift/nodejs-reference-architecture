---
sidebar_position: 7
---

# Code Coverage

Code coverage is a software testing metric that determines the number of lines of code that is successfully validated under a test procedure, which in turn, helps in analyzing how comprehensively a software is verified.

To measure the lines of code that are actually exercised by test runs, various criteria are taken into consideration. Outlined below are a few important coverage criteria are used.

Function Coverage – The functions in the source code that are called and executed at least once.

Statement Coverage – The number of statements that have been successfully validated in the source code.

Path Coverage – The flows containing a sequence of controls and conditions that have worked well at least once.

Branch or Decision Coverage – The decision control structures (loops, for example) that have executed fine.

Condition Coverage – The Boolean expressions that are validated and that executes both TRUE and FALSE as per the test runs.


## Recommended Modules

- [nyc][]: the most popular code-coverage tool; the successor CLI for Istanbul
- [jest][]: Code coverage using the `--coverage` flag

# Guidance

##  Where to focus on higher coverage

For applications, the coverage should be driven by the key user stories/key paths that the application can take.  For modules, it is important to cover all public APIs.



## Coverage percentage thresholds

For those projects that are new, and just starting out, a good percentage threshold is about 70%.  This is because with new projects, it is easier to add tests while creating the application.


If adding coverage to a project that is older that might not have any coverage yet, it might be a little harder since adding tests to an older project with technical debt can be a challenge, especially for someone new coming into the project.  In this case a good percentage threshold is about 30%.  It is also our experience that when adding coverage to a older code base, focusing on the key user stories will give you the best return on investment.  Focusing on the Path and/or Branch/Decision coverage will also maximize the investment on getting to 30%.


## OpenSource Projects

For OpenSource projects, it might be helpful to post the results of the coverage to an external service, such as coveralls and creating an issue related to increasing the code coverage could be a way to attract contributors to the project.

It is also common to report the coverage increase or decrease percentage during a PR CI run.  In our experience, it is best to use this information in a code review rather than blocking a merge.

Code coverage should never block a production deployment


## Output Formats

A common output format is the lcov format, which the recommended modules can produce.

[jest]: https://www.npmjs.com/package/jest
[nyc]: https://www.npmjs.com/package/nyc


## Further Reading

[Introduction to the Node.js reference architecture: Choosing Web Frameworks](https://developers.redhat.com/articles/2022/03/02/introduction-nodejs-reference-architecture-part-7-code-coverage)
