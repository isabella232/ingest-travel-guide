# Logging

Based on:
https://www.youtube.com/watch?v=MmL8H0oGGe8&feature=youtu.be&t=29m30s

See: [Structured Logging](https://www.thoughtworks.com/radar/techniques/structured-logging)

Loggin is an append-only, read-only, user interface

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
