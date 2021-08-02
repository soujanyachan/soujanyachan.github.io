link: https://www.youtube.com/watch?v=chIW4GGGIfs
name: Building an event driven microservice using Kafka and MongoDB in Golang - Salman Bilal Shah
topic: [[golang]]
author:
tags:
github:
creation date: 2021-08-02 15:40
used in myntra

understanding event driven systems
- event gen
- event channel
- event processor 
- downstream activity 

nodejs to go shift why ?
- performance - greater through equivalent along db interactions
- concurrency - goroutines vs single threaded
- error handling - explicit error checks vs try catch

kafka
- high throughput
- scalability
- batch handling

using sync.Once for config
using sarama

prefer async producer to reduce latencies

testify