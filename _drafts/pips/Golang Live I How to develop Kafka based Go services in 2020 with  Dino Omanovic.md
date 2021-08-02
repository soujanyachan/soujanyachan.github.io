link: https://www.youtube.com/watch?v=tcaPzIXwj8A
name: Golang Live I How to develop Kafka based Go services in 2020 with  Dino Omanovic
topic: [[golang]]
author:
tags:
github:
creation date: 2021-08-02 16:41

lib, testing, best pracs

go + kafka is good because
- functionalish programming i.e. can use functions as handlers?
- easy to deploy
- fast
- no object oriented overhead
- control over pointers

libs
- confluent-kafka-go
	- c lib, cgo is required
	- official support
	- language agnostic
	- apache license
	- need to assign unique groupids to each consumer to opt-out of consumer groups
	- regex for topic name
	- manual close
	- no context support (not so idiomatic)
	- async only (sync produce has to be manually handled in code by waiting for p.Events())
	- p.ProduceChannel()
	- performance is not so much worse due to cgo 
- sarama
	- most popular and oldest
	- passes around massive amount of pointers
	- only godoc docs
	- context support
	- loop over consumer to recreate session in case of rebalance
	- consumer for partitions 
		- does not have context
		- needs list of partitions
	- sarama producers
		- context gone again
- goka
	- stream is api on top of sarama
	- irregular commit activity
	- persists calculation state in kafka topic / table
	- table is persisted in local storage too
	- similar to ksqldb
- segmentio kafka-go
	- youngest
	- idiomatics
	- same api for partitions and groups
	- supports context and autorecovery
	- writer supports sync and async with the same api
	- async => wont see error, will skip writing the msg

![[Screenshot 2021-08-02 at 20.36.57.png]]

testing pyramid
- smaller service mean logic shifts away from code to infra
- line bw E2E and component tests becomes a little blurry
- CI needs to cover more than one service to merge or deploy

testing rocket

- graceful shutdown
- test offset loss
- chaos test
- rebalance test

patterns and best pracs
- no domain logic, only boilerplate for kafka
- go mods **enforce semantic versioning**
- avoid breaking the API -> https://dave.cheney.net/2014/10/17/functional-options-for-friendly-apis

trust kafka

outbox pattern -> don't overuse
drop unnecessary dbs
use dbs due to features

should be able to handle duplicate messages, 
