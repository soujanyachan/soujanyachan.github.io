link: https://www.youtube.com/watch?v=oL6JBUk6tj0
name: GopherCon 2018 - Kat Zien - How Do You Structure Your Go Apps
topic: [[golang]] [[cs_learning]]
author: Gopher Academy / Kat Zien
tags: 
github: https://github.com/katzien/go-structure-examples

# GopherCon 2018: Kat Zien - How Do You Structure Your Go Apps
- flat file structure -> removes chance of circular deps, but global state
- group by function / MVC - but what about shared data where, won't compile -> circular dependency, what does app do ?
	- presentation
	- business logic
	- infra
- group by module
	- beers/beer -> stutter
- group by context
	- domain driven development
	- define your bounded contexts, models winthin each context and the ubiquitous language
	- bounded contexts -> user in different POVs would have diff fields
	- building blocks
		- entity
		- value object
		- domain event
		- aggregate
		- service
		- repository
		- factory
	- ![[Screenshot 2021-07-15 at 23.18.00.png]]
	- sample data? 
	- cli instead of rest api
- hexagonal arch
	- core domain
	- db, mail clients etc
	- for modularity
	- dependencies only point inwards
	- interfaces, inversion of control
	- cmd, pkg -> separate binaries from go code, separate sample data also, another way to start app using cli
	- service / domain packages
	- i/o implementations
	- gives us a good idea of what the app actually does
	- extensible
	- https://github.com/thockin/go-build-template
	- keep test next to the main files
