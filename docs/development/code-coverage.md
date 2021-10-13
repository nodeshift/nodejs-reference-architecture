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

##  Key User Stories

If your application/module has some key user stories, it is important to focus on higher coverage there.


## Coverage percentage thresholds

If adding coverage to a project that is older that might not have any coverage yet, a good percentage threshold is about 30%.

For those projects that are new, and just starting out, a good percentage threshold is about 70%.

## OpenSource Projects

For OpenSource projects, it might be helpful to post the results of the coverage to an external service, such as coveralls and creating an issue related to increasing the code coverage could be a way to attract contributors to the project.

It is also common to report the coverage increase or decrease percentage during a PR.  This is more for informational purposes and not necessarily to block a merge.

Code coverage should never block a production deployment

## Output Formats

A common output format is the lcov format, which the recommeneded modules can produce.

[jest]: https://www.npmjs.com/package/jest
[nyc]: https://www.npmjs.com/package/nyc
