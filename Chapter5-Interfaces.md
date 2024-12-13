# Intefaces in GO

Interfaces are collections of method signatures. A type "implements" an interface if it has all of the methods of the given interface defined on it.

In the following example, a "shape" must be able to return its area and perimeter. Both <code>rect</code> and <code>circle</code>

```go
type shape interface {
    area() float64
    perimeter()float64
}

type rect struct {
    width, height float64
}

func (r rect) area() float64 {
    return r.width * r.height
}

func (r rect) perimeter()foat {
    return 2 * r.width + 2 * r.height
}

type circle struct {
    radius float64
}

func (c circle) area() float64 {
    return math.Pi * c.radius * c.radius
}

func (c circle) perimeter() float64 {
    return 2 * math.Pi * c.radius
}
```

## Type switch

A type switch makes it easy to do several type assertions in a series

A type switch is similar to a regular switch statement, but the cases specify types instead of values

```go
func printNumericValue(num interface{}) {
    switch v := num.(type) {
    case int:
        fmt.Printf("%T\n", v)
    case string:
        fmt.Printf("%T\n", v)
    default:
        fmt.Printf("%T\n", v)
    }
}

func maiin () {
    printNumericValue(1)

    printNumericValue("1")

    printNumericValue(struct{}{})
}
```

## Clean interfaces

### 1. Keep Interface Small
Keep interfaces small! Interfaces are meant to define the minimal behavior necessary to accurately represent an idea or concept

Here is an example from the standard HTTP package of a large interface that's a good example of defining minimal behavior

```go
type File interface {
    io.Closer
    io.Reader
    io.Seeker
    Readdir(count int) ([]os.FileInfo, error)
    Stat() (os.FileInfo, error)
}
```

### 2. Interfaces should have no knowledge of satisfying types

### 3. Interfaces are not classes
