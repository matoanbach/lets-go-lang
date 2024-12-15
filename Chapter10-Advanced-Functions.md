# Advanced Functions

```go
func add(x, y, int) int {
    return x + y
}

func mul(x, y int) int {
    return x * y
}

// aggregate applies the given math function to the first 3 inputs
func aggregate(a, b, c int, arithmetic func(int, int) int) int {
    return arithmetic(arithmetic(a, b), c)
}

func main() {
    fmt.Println(aggregate(2,3,4, add))
    fmt.Println(aggregate(2,3,4, mul))
}
```

# Currying

```go
func main() {
    squareFunc := selfMath(multiply)
    doubleFunc := selfMath(add)

    fmt.Println(squareFunc(5))
    fmt.Println(doubleFunc(5))
}

func multiply(x, y, int) int {
    return x * y
}

func add(x, y int) int {
    return x + y
}

func selfMath(mathFunc func(int, int) int) func (int) int {
    return func(x int) int {
        return mathFunc(x, x)
    }
}
```

# Defer

The <code>defer</code> keyword is a fairly unique feature of Go. It allows a function to be executed automatically just before its enclosing function returns.

The Deferred call's arguments are evaluated immediately, but the function call is not executed until the surrounding function returns.

Deferred functions are typically used to close database connections, file handlers and the like.

For example:

```go
// CopyFile copies a file form srcName to dstName on the local file
func CopyFile(dstName, srcName string) (written int64, err error) {

    // Open the source file
    src, err := os.Open(srcName)
    if err != nil {
        return
    }

    // close the source file when the Copyfile function returns
    defer src.Close()

    // Create the destination file
    dst, err := os.Create(dstName)
    if err != nil {
        return
    }

    // Close the destination file when the CopyFile function return
    defer dst.Close()

    return io.Copy(dst, src)
}
```

# Closures

A closure is a function that references variables from outside its own function body. The function may access and assign to the referenced variables.

In this example, the <code>concatter()</code> function returns a function that has reference to an enclosed <code>doc</code> value. Each successive call to <code>harryPotterAggregator</code> mutates that same <code>doc</code> variable.

```go
func concatter() func(string) string {
    doc := ""
    return func(word string) string {
        doc += word + " "
        return doc
    }
}

func main() {
    harryPotterAggregator := concatter()
    harryPotterAggregator("Mr.")
    harryPotterAggregator("and")
    harryPotterAggregator("Mrs.")
    harryPotterAggregator("Dursley")
    harryPotterAggregator("of")
    harryPotterAggregator("number")
    harryPotterAggregator("four")
    harryPotterAggregator("Privet")

    fmt.Println(harryPotterAggregator("Drive"))
}
```

# Anonymous Functions

Anonymous functions are true to form in that they have no name. We've been using them throughout this chapter, but we haven't really talked about them yet.

Anonymous functions are useful when defining a function that will only be used once or to create a quick closure.

```go
// doMath accepts a function that converts on int into another
// and a slice of ints. It returns a slice of ints that have been
// converted by the passed in function
func doMath(f func(int) int, nums[] int) []int {
    var results []int
    for _, n := range nums {
        results = append(results, f(n))
    }

    return results
}

func main() {
    nums := []int{1,2,3,4,5}

    // Here we define an anonymous function that doubles an int
    // here pass it to doMath
    allNumsDoubled := doMath(func(x int) int {
        return x + x
    }, nums)

    // prints:
    // [2,4,6,8,10]
    fmt.Pring(allNumsDoubled)
}
```
