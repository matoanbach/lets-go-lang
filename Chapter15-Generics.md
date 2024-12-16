# Generics in Go

As we've mentioned, Go does not support classes. For a long time, that meant that Go code couldn't easily be reused in many circumstances. For example, imagine some code that splits a slice into 2 equal parts. The code that splits the slice doesn't really care about the values stored in the slice. Unfortunately in Go we would need to write it multiple times for each time, which is a very un-dry thing to do.

```go
func slitIntSlice(s []int) ([]int, []int) {
    mid := len(s)/2
    return s[:mid], s[mid:]
}
```

```go
func splitStringSlice(s []string) ([]string, []string) {
    mid := len(s)/2
    return s[:mid], s[mid:]
}
```

# Type parameters

Put simply, generics allow us to use variables to refer to specific types. This is an amazing feature because it allows us to write abstract functions that drastically reduce code duplicatin.

```go
func splitAnySlice[T any] (s []T) ([]T, []T) {
    mid := len(s) / 2
    return s[:mid], s[mid:]
}
```

In the example above, <code>T</code> is the name of the type parameter for the <code>splitAnySplice</code> function, and we've said that it must match any <code>any</code> constraint, which means it can be anything. This makes sense because the body of the function doesn't care about the types of things stored in the slice.

```go
firstInts, secondsInts := splitAnySlice([]int{0,1,2,3,})
fmt.Println(firstInts, secondsInts)
```

Example:

```go
func getLasT[T any](s []T) T {
    if len(s) == 0 {
        var zero T
        return zeroVal
    }
    return s[len(s) - 1]
}
```

# Constraints

```go
type stringer interface {
    String() string
}

func concat[T stringer](vals []T) string {
    results := ""
    for _, val := range vals {
        // This is where the .String() method
        // is used. That's why we need a more specific
        // contraint instead of the any constraint
        result += val.String()
    }

    return result
}
```
