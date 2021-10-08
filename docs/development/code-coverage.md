# Code Coverage

Code coverage is a software testing metric that determines the number of lines of code that is successfully validated under a test procedure, which in turn, helps in analyzing how comprehensively a software is verified.

To measure the lines of code that are actually exercised by test runs, various criteria are taken into consideration. Outlined below are a few important coverage criteria are used.

Function Coverage – The functions in the source code that are called and executed at least once.

Statement Coverage – The number of statements that have been successfully validated in the source code.

Path Coverage – The flows containing a sequence of controls and conditions that have worked well at least once.

Branch or Decision Coverage – The decision control structures (loops, for example) that have executed fine.

Condition Coverage – The Boolean expressions that are validated and that executes both TRUE and FALSE as per the test runs.


## Recommended Components

- [nyc][]: the most popular code-coverage tool; the successor CLI for Istanbul
- [jest][]: Code coverage using the `--coverage` flag

# Guidance

* Key User Stories
  * Focus on higher coverage here

* Older Projects
  * 30% is a good threshold

* Greenfield Projects
  * 70% is a good threshold

* Output to a format like lcov

* Outside Contributors
  * For opensource projects it is good to post the coverage some where
  * Showing during PR's for opensource projects

  * not necesarrily used to block PR's, more for informational
  * Code coverage should never block a production deployment
