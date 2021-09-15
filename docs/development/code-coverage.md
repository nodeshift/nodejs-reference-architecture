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


RH Node.js team has been using nyc, posting to coveralls

Jim, not used to often, more important to focus on integration stories, versus code coverage

Dominic, sometime use the built in coverage with Jest, don’t typically publish it.

Weather company, generate reports using built in Jest support, don’t publish anywhere

Is there a module/application distinction

Unit versus end-to-end tests make a difference

Coverage is good if you want outside coverage/contributions

Dominic, big customer project, fed into sonar cube which collects a bunch of stuff on code quality. Uses lcov file (both Jest can istanbul) can generate that, pipeline blocked if falls below 85%, probably common

Dominic, fairly common position, don’t need to target 100% coverage, upin 80-90s is good enough.

System testing through, micro outages, was much more valuable than coverage.
koasmonkey

Running with Test

output to a service?



