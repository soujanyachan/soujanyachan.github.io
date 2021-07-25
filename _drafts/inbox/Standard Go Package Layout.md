link: https://www.gobeyond.dev/standard-package-layout/
name: Standard Package Layout
topic: [[golang]] [[cs_learning]]
author: Ben Johnson
tags:

The package strategy that I use for my projects involves 4 simple tenets:

1.  Root package is for domain types
2.  Group subpackages by dependency
3.  Use a shared __mock__ subpackage
4.  __Main__ package ties together dependencies

These rules help isolate our packages and define a clear domain language across the entire application. 

1. root
I place my domain types in my root package. This package only contains simple data types like a __User__ struct for holding user data or a __UserService__ interface for fetching or saving user data. Domain stuff that doesn’t depend on your underlying technology.

__The root package should not depend on any other package in your application!__

2. group packages by subdependency
subpackages exist as an adapter between your domain and your implementation.
isolates the dependency on the infra/implementation, pluggable
layering implementations
dependencies communicate solely through our common domain language.
not just 3rd party deps

3. shared mock subpackage
4. main package

