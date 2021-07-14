link: https://www.youtube.com/watch?v=_pww3NJuWnk&list=PLFmONUGpIk0YwlJMZOo21a9Q1juVrk4YY
name: Creating Golang WebServer With Echo
topic: [[golang]] [[cs_learning]]
author: Blue Bot
tags: #flashcards
github: https://github.com/verybluebot/echo-server-tutorial
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
c.QueryParam() -> for query params
c.Param
```

# Parsing JSON From Request
```go
ioutil.ReadAll(c.Request().Body)
defer c.Request().Body.Close()

unmarshal - fastest
newdecoder
c.Bind() - slower than other two, 
```

# Part 4: Intro to Middlewares
echo group
can add middlewate as third params in the fn
or .Use()
middleware.Logger, middleware.LoggerWithConfig

# Part 5 Basic auth
```go
g.Use(middleware.BasicAuth(func(username, password string, c echo.Context) (error, bool) {

// check in the DB

if username == "jack" && password == "1234" {

return nil, true;

}

return nil, false;

}))
```

# Part 6 custom middleware
```go
func ServerHeader(next echo.HandlerFunc) echo.HandlerFunc {
	return func(c echo.Context) error {
		c.Response().Header().Set(echo.HeaderServer, "BlueBot/1.0")
		c.Response().Header().Set("notReallyHeader", "thisHaveNoMeaning")
		return next(c)
	}
}
 e.Use(ServerHeader)
```

# part 7 cookies
```go

cookie := &http.Cookie{}

// this is the same

//cookie := new(http.Cookie)

cookie.Name = "sessionID"

cookie.Value = "some_string"

cookie.Expires = time.Now().Add(48 * time.Hour)

c.SetCookie(cookie)

return c.String(http.StatusOK, "You were logged in!")


 cookie, err := c.Cookie("sessionID")
```

# part 8 JWT
```go
type JwtClaims struct {
	Name string `json:"name"`
	jwt.StandardClaims
}

func mainJwt(c echo.Context) error {
	user := c.Get("user")
	token := user.(*jwt.Token)
	claims := token.Claims.(jwt.MapClaims)
	log.Println("User Name: ", claims["name"], "User ID: ", claims["jti"])
	return c.String(http.StatusOK, "you are on the top secret jwt page!")
}

func createJwtToken() (string, error) {
	claims := JwtClaims{
			"jack",
			jwt.StandardClaims{
			Id: "main_user_id",
			ExpiresAt: time.Now().Add(24 * time.Hour).Unix(),
		},
	}
	rawToken := jwt.NewWithClaims(jwt.SigningMethodHS512, claims)
	token, err := rawToken.SignedString([]byte("mySecret"))
	if err != nil {
		return "", err
	}
	return token, nil
}

jwtGroup.Use(middleware.JWTWithConfig(middleware.JWTConfig{
	SigningMethod: "HS512",
	SigningKey: []byte("mySecret"),
}))
```

# part 8.1 jwt from cookie
can be done by changing some echo related config

# part 9 
```go
e.Use(middleware.Static("./static"))
```

# part 10 refactoring
- main will only initialise things
- split into router, middlewares, controller based on shared functions / resp