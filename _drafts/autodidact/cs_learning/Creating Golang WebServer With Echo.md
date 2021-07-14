link: https://www.youtube.com/watch?v=_pww3NJuWnk&list=PLFmONUGpIk0YwlJMZOo21a9Q1juVrk4YY
name: Creating Golang WebServer With Echo
topic: [[golang]] [[cs_learning]]
author: Blue Bot

# Part 1: Project Setup and HelloWorld
```go
package main

import(
	"fmt"
	"net/http"
	"github.com/labstack/echo"
)

func yallo(c echo.Context) error {
	return c.String(http.StatusOK, "yallo from the web side!")
}

func main() {
	fmt.Println("Welcome to the server")
	e := echo.New()
	e.GET("/", yallo)
	e.Start(":8000")
}
```

# Url Params Query Params and Json Responses
```go
c.QueryParam
```