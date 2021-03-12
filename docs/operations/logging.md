# Logging

## Recommended Components

- Pino - http://getpino.io/#/

Pino provides an easily consumed API, structured logging and good performance
which makes it well suited to cloud native deployments were more complicated
APIs/features are not required as log output is simply written to standard out
It has a respective level of weekly npm downloads (495k as of Nov 2019)
and is growing. It was inspired by Bunyan which no longer seems to be maintained
and is a good migration option.

# Guidance

Pino http://getpino.io/#/ is the recommended log framework for Node.js due
to its easily consumed API, structured json logging by default
and good performance.

When deploying Pino we have the following additional recommendations:

- Send logs to standard out and use log aggregation tools to collect
  logs across processes, containers and applications. All log processing
  should be done in a separate process.
- Plan for a final resting place for log data. After 7 days migrate
  log data to a lower cost storage (manual retrieval is likely ok).
- Add code to your application in order to allow logger.level
  to be set through an Environment variable so that can be easily
  changed in container environments.
- Use the [redaction](https://github.com/pinojs/pino/blob/HEAD/docs/redaction.md)
  option to ensure sensitive data is not logged. Do note that this implementation 
  does not allow one to dynamically add fields to be redacted <sup>[1](#footnote1)</sup>.
- Limit the use of warn, error, and fatal levels to information
  which must always be logged.
- Limit the use of info level to important information which can
  always be logged without introducing significant overhead.
- Don't throw and catch multiple errors, throw once and catch/log at the
  highest level,
- When catching errors at a high level, log the error.stack unless the thrown error 
  type is known and expected.
- Every source file should utilize Pino's child method off of the common logger
  instance, passing in { file: module } to make the source file path is part of
  the log.

### Footnotes:
<a name="footnote1">1</a>: If you require ability to dynamically append what is 
  redacted (like values read from a secret-storage like Vault), one can implement 
  redacting logic inside a Pino
  [logMethod](https://getpino.io/#/docs/api?id=logmethod) to filter the message 
  string and objects.

