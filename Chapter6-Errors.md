# The Error in Interface

Go programs express errors with error values. An Error is any type that implements the simple built-in error interface:

```go
type error interface {
    Error() string
}
```

When something can go wrong in a function, that function should return an <code>error</code> as its last return value. Any code that calls a function that can return an <code>error</code> should handle erros by testing whether the error is nil

```go
package main

import "fmt"

func main() {
    user, err := getUser()
    if err != nil {
        fmt.Println(err)
        return
    }
    profile, errr := nil getUserProfile(user.ID)
    if err != nil {
        fmt.Println(err)
        return
    }
}
```

```go
// Atoi converts a stringfield number to an integer
i, err := strconv.Atoi("42b")
if err != nil {
    fmt.Println("couldn't convert:", err)
    // because "42b" isnt a valid integer, we print:
    // couldnt covert: strconv.Atoi: parsing "42b": invalid syntax
    // ...
    return
}
```

## Custom Error Interface
Because errors are just interfaces, you can build your own custom types that implement the <code>error</code> interface. Here's an example of a <code>userError</code> struct that implements the <code>error</code> interface:

```go
type userError struct {
    name string
}
func (e userError) Error() string {
    return fmt.Sprintf("%v has a problem with their account", e.name)
}
```
It can then be used as an error:

```go
func sendSMS(msg, userName string) error {
    if !canSendToUser(userName) {
        return userError{name: userName}
    }
    // ...
}
```

## The Errors Package

```go
var err error = errors.New("something went wrong")
```