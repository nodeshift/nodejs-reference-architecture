
RH Node.js team has been using nyc, posting to coveralls
Jim, not used to often, more important to focus on integration stories, versus code coverage
Dominic, sometime use the built in coverage with Jest, don’t typically publish it.
Weather company, generate reports using built in Jest support, don’t publish anywhere
Is there a module/application distinction
Unit versus end-to-end tests make a difference
Coverage is good if you want outside coverage
Dominic, big customer project, fed into sonar cube which collects a bunch of stuff on code quality. Uses lcov file (both Jest can istanbul) can generate that, pipeline blocked if falls below 85%, probably common
Dominic, fairly common position, don’t need to target 100% coverage, upin 80-90s is good enough.

System testing through, micro outages, was much more valuable than coverage.
koasmonkey


# Code Coverage



## Recommended Components

- [nyc][]: the most popular code-coverage tool; the successor CLI for Istanbul

# Guidance

Running with Test

output to a service?



