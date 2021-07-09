[[golang]]
[[cs_learning]]
Maybe this helps:

-   A Module is a set of packages versioned together. If two packages evolve in lockstep they should be part of the same Module. Not every "dependency" should be its own Module, only dependencies with their own, independent lifecycle.
    
-   What is written in go.mod is the rule. If you add a replace directive then this dependency is replaced. No magic there.
    
-   Modules are never imported. Packages are imported and packages are how Go code is reused, evolves and is used. Modules are just a group of packages with the same version number (you know that by now, but this seems to be a major obstacle for lots of people to understand modules).
    
-   There is no need for a "source folder". Go code lives in packages and each package is one file system folder. You can use whatever filesystem layout you find okay. Most people prefer packages organized pretty flat (i.e. <module>/some/functionality and not <module>/src/main/really/sources/some/functionality) with the executable pretty simple in an almost empty main.go or, especially if multiple executables are built in <module>/cmd/...
    
-   Go is not some other language. The concept of a Go package is not a class and not a simple source code file. It is the fundamental building block you have to get used to think in packages. And a module is nothing but a set of related packages.