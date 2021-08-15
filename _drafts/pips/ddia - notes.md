# Chapter 1 - reliable, scalable and maintainable solutions
**glossary**
data-intensive - quanity complexity or the speed at which data is changing
compute-intensive - CPU cycles are the bottleneck
reliability - system should work correctly 
scalability - system should be able to grow / deal with growth reasonably
maintainability - people working on the system should be able to do so productively
fault - one component of the system deviating from its spec
fault-tolerant - 
failure - the system as a whole stops providing the required service to the user
MTTF - mean time to failure
redundancy - having backups
rolling upgrade - upgrade with no downtime by patching one node at a time
telemetry - performance metrics, error rates
load parameters - 
fan-out - number of requests to other services we need to make to service one incoming request
throughput - number of records we can process per second / time it takes to run a job on a dataset of a certain size.
response time - time between client sending a request and receiving a response.
latency - 
tail latencies - 
SLO -
SLA -
head of line blockers - 
tail latency amplification - 
horizontal scaling - 
vertical scaling - 
shared nothing arch - 
elastic systems - 
operability - 
simplicity - 
evolvability - 
accidental complexity - 
abstraction - 

What are the standard buidling blocks of a data-intensive application ? 
- databases
- caches
- search indexes
- stream processing
- batch processing

