link: https://blog.learngoprogramming.com/special-packages-and-directories-in-go-1d6295690a6b
name: Special Packages and Directories in Go
topic: [[golang]] [[cs_learning]]
author: Inanc Gumus
tags:

- > **Every runnable program should contain a package named main and a function named main.**
- > Naming your package as internal, hides your package’s internals even more, **brings more encapsulation** When you name a package as internal, it can only be imported from its parent directory’s packages. If you put into deeper sub-folders, one-step up, its parent packages can access it.
- Library pkg is a pkg that does not have an entrypoint, not runnable
- vendor dir, external pkg dependencies
- testdata dirs get skipped by gotools