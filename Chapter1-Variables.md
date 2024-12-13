# Chapter 1 - Variables

## Basic types

```go
bool

int     int8    int16    int32   int64
uint    uint8   uint16   uint32  uint64 uintptr

byte // alias for uint8

rune    // alias for int32
        // represents a Unicode code point

float32     float64
complex64   complex128
```

## Declaring A Variable

```go
var number int

var pi float64 = 3.14159
```

## Short Variable Declaration

```go
var empty string
// is the same as
empty := ""

// more
numCars := 10 // inferred to be an integer
temperture := 0.0 // temperture is inferred to be a floating point number
var isFunny = true // isFunny is inferred to be a boolean
```

## String formating

### %v - Interpolate the default representation

The <code>%v</code> variant prints to Go syntax representation of a value. You can usually use this if you're unsure what else to use. That said, it's better to use the type-specific variant if you can.

```go
// I am 10 years old
fmt.Printf("I am %v years old", 10)

// I am way too many years old
fmt.Printf("I am %v years old", "way too many")
```

### %s - Interpolate a string

```go
// I am way too many years old
fmt.PrintF("I am %s years old", "way too many")
```

### %d - Interpolate an integer in decimal form

```go
fmt.Printf("I am %d years old", 10)
```

### %f - Interpolate a decimal

```go
// I am 10.532000 years old
fmt.Printf("I am %f years old", 10.523)

//The ".2" rounds the number to 2 decimal places
// I am 10.53 years old
fmt.Printf("I am %.2f years old", 10.523)
```

### conditionals

```go
if height > 6 {
    fmt.Println("You are super tall!")
} else if {
    fmt.Println("You are tall enough!")
} else {
    fmt.Println("You are not tall enough!")
}
```
