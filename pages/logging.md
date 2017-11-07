# Logging

Based on:
https://www.youtube.com/watch?v=MmL8H0oGGe8&feature=youtu.be&t=29m30s

## Log Meesages Content
* Unique correlation ID "edge-to-edge" 
  * see AWS XRay/Dapper/Zipkin
  * trackable back to source action
* Timestamps:
  * Human Readable
  * Machine Readable (for grep and sort)
* The cause, the whole cause and nothing but the cause
  * No noise
* Answer three questions:
  * What went wrong?
  * Who is impacted?
  * How do I fix it?
