link: https://www.youtube.com/watch?v=oL6JBUk6tj0
name: GopherCon 2018 - Kat Zien - How Do You Structure Your Go Apps
topic: [[golang]] [[cs_learning]]
author: Gopher Academy / Kat Zien
tags: 
github:

# GopherCon 2018: Kat Zien - How Do You Structure Your Go Apps
- flat file structure -> removes chance of circular deps, but global state
- group by function / MVC - but what about shared data where, won't compile -> circular dependency, what does app do ?
	- presentation
	- business logic
	- infra
- group by module
	- beers/beer -> stutter