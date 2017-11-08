# Ingest Design
## Design Philosophy
In the early 1970’s [Alan Kay](https://en.wikipedia.org/wiki/Alan_Kay), a computer scientist working Xerox PARC proposed a new perspective of thinking about large-scale software systems. His background in Molecular Biology inspired him to consider software as a biological system as a means of enabling scaling and evolution. 

He argued that if you build an passenger aircraft and a year later require an aircraft with twice the capacity you cannot just make it bigger by adding bits on. You have to redesign it and start again and this was the same problem he was seeing with software systems. On the other hand biological systems can grow and evolve without issue.

He proposed treating software as a collection of self-contained “cells” that communicate through messages. This became the basis of Object Oriented Software design and the programming language SmallTalk, the predecessor to many modern programming languages such as Java and Swift.

With the move to cloud-based software Alan Kay’s work has come to the fore again and the idea of building highly scalable distributed systems by creating self-contained pieces and using messages between them for orchestration is a preferred approach to building cloud-based software and one I propose using on HCA DCP Ingest.

By building a system based a self contained cells that perform a single task that communicate by messaging we can build a system with minimal dependencies. 

## References
* [The Quest to Make Code Work Like Biology Just Took A Big Step](https://www.wired.com/2016/06/chef-just-took-big-step-quest-make-code-work-like-biology/)
* [The Deep Insights of Alan Kay](http://mythz.servicestack.net/blog/2013/02/27/the-deep-insights-of-alan-kay/)
* [Seven Concurrency Models in 7 Weeks](https://www.safaribooksonline.com/library/view/seven-concurrency-models/9781941222737/0)
