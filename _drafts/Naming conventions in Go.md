link: https://talks.golang.org/2014/names.slide#3
name: Naming conventions in Go
topic: [[golang]] [[cs_learning]]
author: Andrew Gerrard
tags: #flashcards 

The greater the distance between a name's declaration and its uses,  
the longer the name should be.

Names in Go should use `MixedCase`.

(Don't use `names_with_underscores`.)

Acronyms should be all capitals, as in `ServeHTTP` and `IDProcessor`.

Keep local variables short
Fn parameters Where the types are descriptive, they should be short, otherwise names can provide documentation

Return values on exported functions should only be named for documentation purposes.

Receiver names should be consistent across a type's methods.

Exported names are qualified by their package names. That's why we have `bytes.Buffer` and `strings.Reader`,  
not `bytes.ByteBuffer` and `strings.StringReader`.

Interfaces that specify just one method are usually just that function name with 'er' appended to it.

When an interface includes multiple methods, choose a name that accurately describes its purpose

Error types should be of the form `FooError`, Error values should be of the form `ErrFoo`

Choose package names that lend meaning to the names they export. (no `util`, `common`)

The last component of a package path should be the same as the package name, avoid capital letters.

