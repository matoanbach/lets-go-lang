# Functions

```go
func sub(x int, y int) int {
    return x - y
}
```

Here, <code>func sub(x int, y int) int</code> is known as the "function signature".

## Multiple parameters

When multiple arguments are of the same type, the type only needs to be declared after the last one, assuming they are in order

```go
func add (x, y int) int {
    return x + y
}
```

## Go-style syntax

```go
x int
p *int
a [3]int
```

It's nice for more complex signatures, it makes them easier to read

```go
f func(func(int, int), int, int) int
```

### Passing variables by value
Variables in Go are passed by value (except for a few data types we haven't covered yet). "Pass by value" means that when a variable is passed into a function, that function receives a copy of the variable. The function is unable to mutate the caller's data.

```go
func main() {
    x := 5
    increment(x)
    fmt.Println(x)
    // still prints 5,
    // because the increment function
    // received a copy of x
}

func increment(x int){
    x++
}
```