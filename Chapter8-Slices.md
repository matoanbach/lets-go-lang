## Arrays in GO

Arrays are fixed-size groups of variables of the same type

The type <code>[n]T</code> is an array of n values of type <code>T</code>

To declare an array of 10 integers:

```go
var myInts [10]int
```

```go
primes := [6]int{2, 3, 5, 7, 11, 13}
```

# Slices in GO

Slice is mostly used instead of array when working with ordered lists

Arrays are fixed in size. Once you make an array like <code>[10]int</code> you can't add an 11th element

A slice is a dynamically-sized, flexible view of the elements of an array

Slices always have an underlying array, though it isn't always specified explicitly. To explicitly create a slice on top of an array we can do:

```go
primes := [6]int{2, 3, 5, 7, 11, 13}
// mySlice = {3, 5, 7}
mySlice := primes[1:4]
```

The syntax is:

```go
arrayname[lowIndex:hightIndex]
arrayname[lowIndex:]
arrayname[:highIndex]
arrayname[:]
```

# Make

Most of the time we don't need to think about the underlying array of a slice. We can create a new slice using the <code>make</code> function:

```go
// func make([]T, len, cap) []T
mySlice :=  make([]int, 5, 10)

// the capacity argument is usually omitted and defaults to the
mySlice := make([]int, 5)
```

Slices created with <code>make</code> will be filled with the zero value of the type.

If we want to create a slice with a specified set of values, we can use a slice literal:

```go
mySlice := []string{"I", "love", "go"}
```

# Length

The length of a slice is sipmply the number of elements it contains. It is accessed using the built-in <code>len()</code> function:

```go
mySlice := []string{"I", "love", "go"}
fmt.Println(len(mySlice)) // 3
```

# Capacity

The capacity of a slice is the number of elements in the underlying array, counting from the first element in the slice. It is accessed using the built-in <code>cap()</code>

```go
mySlice := []string{"I", "love", "go"}
fmt.Println(cap(mySlice)) // 3
```

# Variadic

Many functions, especially those in the standard library, can take an arbitrary number of final arguments. This is accomplished by using the "..." syntax in the function signature

A variadic function receives the variadic arguments as a slice

```go
func sum(nums ...int) {
    // nums is just a slice
    for i := 0; i < len(nums); i++ {
        num := nums[i]
    }
}

func main() {
    total := sum(1, 2, 3)
    // prints "6"
    fmt.Println(total)
}
```

# Spread operator

The spread operator allows us to pass a slice into a variadic function. The spread operator consists of three dots following the slice in the function call.

```go
func printStrings(strings ...string) {
    for i := 0; i < len(strings); i++ {
        fmt.Println(strings[i])
    }
}

func main() {
    names := []string{"bob", "sue", "alice"}
    printStrings(names...)
}
```

# Append
The built-in append funtion is used to dynamically add elements to a slice:

```go
func append(slice []Type, elems ...Type) []Type
```
If the underlying array is not large enough, <code>append()</code> will create a new underlying array and point the slice to it

Notice that <code>append()</code> is variadic, the following are all valid:

```go
slice = append(slice, oneThing)
slice = append(slice, firstThing, secondThing)
slice = append(slice, anotherSlice...)
```

# Slice of Slices
Slices can hold other slices, effectively creating a matrix, or 2D slice

```go
rows := [][]int{}
```

```go
func createMatrix(rows, cols int) [][]int {
    matrix := make([][]int, 0)
    for i := 0; i < rows; i++ {
        row := make([]int, 0)
        for j := 0; j < cols; j++ {
            row = append(row, i * j)
        }
        matrix = append(matrix, row)
    }
}
```