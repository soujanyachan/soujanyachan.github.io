name: Design Microservice Architectures the Right Way
topic:
author:
tags:
link: https://www.youtube.com/watch?v=j6ow-UemzBc

great architecture
- scale dev team
- quality
- high perf low cost
- supports future features naturally

not so great
- near term velocity vs future paralysis

misconception
- best programming lang for the services -> very expensive, team size and investment are critical inputs
- code gen is evil -> just a technique, defined schema is 100% trusted
- event log is source of truth -> 
- developers can maintain no more than 3 services each -> automation will shine here

- no internal apis -> same for internal devs and customers
- API definition has to be language neutral
- CI on the API definition
- linter for api definition -> 
- breaking changes in APIs - verify potentially breaking

- code is simple and consistent

- db arch
	- each microservice owns its db
	- no other service allowed to connect to db
	- other services use only the service interface (API + events) -> works if we have a great APi and publish the right events
- CLI as a single interface for infra and common dev tasks
- defining storage requirements in config
- only update db if the hash code is different than current
- proper indexes from start -> only define a fn if index is available, if fn not there, you need to add index

continuous delivery is essential to managing microservice

- deploy is triggered by git tag
- tag is created auto by a change on master (eg merge pr)
- 100% automated
- standard health check
- instance fails to become healthy and not put into prod

- principles of event interface
	- first class schema for all events
	- producer guarantee at least once delivery
	- consumers implement idempotency
	- based on postgres scaled to ~1b events/day/service
		- producers
		- create journal of all operations on table
		- record operation (insert update delete)
		- on creation, queue the journal record to be published
		- real time async 1 event per journal record
		- enable replay by simply requeueing journal record
		- consumers
		- store new event in local db partitioned for fast removal
		- on event arrival queue record to be consumed
		- process incoming events in micro batches 
		- record failures locally -> monitoring

- events schema is also made before time, linter
- stream owned by 1 microservice
- journal
	- doc retention period in config
	- code gen journal
	- use partitions to manage storage
- producer -> 
	- reflection used to generate stream name
	- content type in stream name
	- testing
- dependencies
	- auto update to all dependencies

API builder -> open source tool for this