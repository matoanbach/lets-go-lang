# Pointers

As we have learned, a variable is a named location in memory that stores a value. We can manipulate the value of a variable by assigning a new value to it or by performing operations on it. When we assign a value to a variable, we are storing that value in a specific location in memory.

```go
// "x" is the name of a location in memory.
x := 42
```

## A pointer is a varialbe

A pointer is a variable that store the memory address of another variable. This means that a pointer "points to" the location of where the data is stored NOT the actual data itself.

The <code>*</code> syntax defines a pointer:

```go
var p *int
```

The <code>&</code> operator generates a pointer to its operand.

```go
myString := "hello"
myStringPtr = &myString // var myStringPtr *int = &myString
```

The <code>*</code> dereferences a pointer to gain access to the value
```go
fmt.Println(*myStringPtr)   // read myString through the pointer
*myStringPtr = "world"      // set myString through the pointer
```