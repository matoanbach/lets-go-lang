# Loops in Go

```go
for INITIAL; CONDITION; AFTER {
    // Do something
}
```

```go
for i := 0; i < 10; i++ {
    fmt.Println(i)
}
```

## There is no while loop in GO

```go
go CONDITION {
    // Do some stuff while CONDITION is true
}
```

```go
planHeight := 1
for planHeight < 5 {
    fmt.Println("still growing! current height:", planHeight)
    planHeight++
}

fmt.Println("plant has grown to ", planHeight, " inches")
```
