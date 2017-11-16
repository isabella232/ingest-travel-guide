# Logging
These are proposals for Ingest logging. For logging for the wider DCP please see the [Logging RFC](https://docs.google.com/document/d/15RUEodhwS8wtgkIpoJ_6uI9eCErzAw2YXzY6MwwUcG4/edit#heading=h.idqe72fdu9u0)

Based on:
https://www.youtube.com/watch?v=MmL8H0oGGe8&feature=youtu.be&t=29m30s

See: [Structured Logging](https://www.thoughtworks.com/radar/techniques/structured-logging)
Consider: [GELF Format](http://docs.graylog.org/en/2.2/pages/gelf.html)

Logging is an append-only, read-only, user interface

## Log Meesages Content
* Unique correlation ID "edge-to-edge" 
  * See AWS XRay/Dapper/Zipkin
  * Trackable back to source action
* Timestamps:
  * Human Readable
  * Machine Readable (for grep and sort)
* The cause, the whole cause and nothing but the cause
  * No noise
* Answer three questions:
  * What went wrong?
  * Who is impacted?
  * How do I fix it?
