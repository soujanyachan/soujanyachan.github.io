link: https://www.youtube.com/watch?v=1B71SL6Y0kA
name: go lift - john cinnamond
topic:
author:
tags:
github:
creation date: 2021-09-06 12:52

John explains how Category Theory can help you write better code, but without using the words "Category" or "Theory" (or monad or functor or any of the scary terminology). The idea behind "Errors are Values" from the Go blog can be applied to different kinds of programming problems, and we can make our code easier to compose by moving units of control flow into types.

error handling in go is very repetitive, getting in the way of the code, readability

- errors are values article

conn.Write(command)
conn is a value containing data about the connection

create a new type -> safe conn
```go
type SafeConn struct {
	conn Connection
	err error
}```
do we do this for all such objects in go ?
- cost of the new abstraction,
- need to dig into the implementation of the safe conn to understand what happens to the error

is this abstraction appropriate in the situation?

technique, and apply to other
