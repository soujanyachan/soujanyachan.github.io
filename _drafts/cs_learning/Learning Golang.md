link: https://www.youtube.com/watch?v=xLf9oUfvvwo&list=PL7yAAGMOat_F7bOImcjx4ZnCtfyNEqzCy&index=2
name: Learning Golang
topic: [[golang]] [[cs_learning]]
author: Mario Carrion

# learning go interface types
types - a way to rep state/behaviour
- composite - ptr, map fn, slice, array channel, interface
- simple - str numeric bool

you assign an int8 value to an int8 types, but you cannot assign a previously instantiated int8 into an int8 types

function vs method

interface type - is a set of method signatures, it can hold any value that implements those methods (methods imply a type)

interfaces -> polymorphism in go 

```go
package main

import "fmt"

type Priority int8

func (p Priority) String() string {
	switch int8(p) {
	case 0:
		return "low"
	case 1:
		return "high"
	}

	return "unknown"
}

func main() {
	var p Priority = 1

	// Uncomment the following two lines to see the error when
	// trying to assign two different types
    // var i int8 = 2
	// p = i

	fmt.Println(p.String())         // "high"
	fmt.Println(Priority.String(p)) // "high"
	fmt.Println(p)                  // "high"
}
```

# Learning Golang: Dependencies, Modules and How to manage Packages
module -> collection of go packages stored in a file tree with go.mod file at its root
go.mod file handles
- module path
- dependency reqt (module path, sem ver)

```go
module <name>
go <version>
require <module-path> <version>
replace <module-path> <version>
exclude <module-path> <version>
```

indirect dependencies also there
go.sum
```go
module path version checksum
```

versioning a module, version needs to be in module path
- module path
- branch

```bash
go mod init example.com/this/package
go mod tidy (pulls the most recent version that applies)
go get pkg
go list -m -u all // updated all deps
go list -m -u pkg_name // to check for updates to a given pkg
```
can also specify a commit hash using the `@` symbol.
so a pseudo version is created

# Learning Golang: Context package: Cancellations, Deadlines and Request-scoped values
- context package
- deadlines
	- withDeadline (parent context.Context, d time.Time) => context.Context, context.CancelFunc
	- withTimeout (parent context.Context, timeout time.Duration) => context.Context, context.CancelFunc

```go
package main

import (
	"context"
	"fmt"
	"time"
)

const shortDuration = 1 * time.Millisecond
func main() {
	// Pass a context with a timeout to tell a blocking function that it
	// should abandon its work after the timeout elapses.
	ctx, cancel := context.WithTimeout(context.Background(), shortDuration)
	defer cancel()

	select {
		case <-time.After(1 * time.Second):
		fmt.Println("overslept")
		case <-ctx.Done():
		fmt.Println(ctx.Err()) // prints "context deadline exceeded"
	}
}
```
The `select` statement lets a goroutine wait on multiple communication operations.

A `select` blocks until one of its cases can run, then it executes that case. It chooses one at random if multiple are ready.

cancellation signal
- withCancel (parent context.Context) => ctx contaxt.Context, cancel context.CancelFunc

```go
package main

import (
	"context"
	"fmt"
	"time"
)

func main() {
	ch := make(chan struct{})

	run := func(ctx context.Context) {
		// listens and prints out a value
		n := 1
		for {
			select {
			case <-ctx.Done(): // 2. "ctx" is cancelled, we close "ch"
				fmt.Println("exiting")
				close(ch)
				return // returning not to leak the goroutine
			default:
				time.Sleep(time.Millisecond * 300)
				fmt.Println(n)
				n++
			}
		}
	}

	ctx, cancel := context.WithCancel(context.Background())
	go func() {
		time.Sleep(time.Second * 2)
		fmt.Println("goodbye")
		cancel() // 1. cancels "ctx"
	}()

	go run(ctx)

	fmt.Println("waiting to cancel...")

	<-ch // 3. "ch" is closed, we exit

	fmt.Println("bye")
}
```

request scoped values
- withValue = (parent context.Context, key, val interface {}) => context.Context
trying to pass single value into different areas of the code
```go
package main

import (
	"context"
	"fmt"
	"log"
)

type jwt string

const auth jwt = "JWT"

func main() {
	ctx := context.WithValue(context.Background(), auth, "Bearer hi")

	//-

	bearer := ctx.Value(auth)
	str, ok := bearer.(string)
	if !ok {
		log.Fatalln("not a string")
	}

	fmt.Println("value:", str)
}
```

best pracs
- define context as the first arg if you need for API
- ensure context.CancelFunc is called
- dont overuse WithValue