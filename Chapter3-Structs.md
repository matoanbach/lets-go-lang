# Struct in Go

We use structs in Go to represent structured data. It's often convenient to group different types of variables together. For example, if we want to represent a car we could do the following:

```go
type car struct {
    Make string
    Model string
    Height int
    Width int
}
```

## Nested structs in go

Structs can be nested to represent more complex entities

```go
type car struct {
    Make string
    Model string
    Height int
    Width int
    FrontWheel Wheel
    BackWheel Wheel
}

type Wheel struct {
    Radius int
    Material string
}
```

## Anonymous structs in go

An anonymous struct is just like a normal struct, but it is defined without a name and therefore cannot be referenced elsewhere in the code

```go
myCar := struct {
    Make string
    Model string
} {
    Make: "tesla",
    Model: "model 3"
}
```

You can even nest anonymous structs as fields within other structs

```go
type car struct {
    Make string
    Model string
    Height int
    Width int
    Wheel struct {
        Radius int
        Material string
    }
}
```

## Embedded struct

Go is not an object oriented language. However, embedded structs provide a kind of data-only inheritance that can be useful at times. Keep in mind, Go doesn't support classes or inheritance in the complete sense, embedded structs are just a way to elevate and share fields between struct definitions.

```go
type car struct {
    make string
    model string
}

type truck struct {
    // "car" is embedded, so the definition of a
    // "truck" now also additionally contains all
    // of the fields of the car struct
    car
    bedSize int
}
```

## Embedded vs Nested
- An embedded struct's fields are accessed at the top-level, unlike nested structs.
- Promoted fields can be access like normal fields except that can't be used in composite literals

```go
lanesTruck := truct {
    bedSize := 10,
    car: car {
        make: "toyota",
        model: "camry"
    },
}

fmt.Println(lanesTruck.bedSize)

// embedded fields promoted to the top-level
// instead of lanesTruck.car.make
fmt.Println(lanesTruck.make)
fmt.Println(lanesTruck.model)
```

## Struct methods in Go

While Go is not object oriented, it does support methods which can be defined on structs. Methods are just functions that have a receiver. A receiver is a speicial parameter that syntatically goes before the name of the function

```go
type rect struct {
    width int
    height int
}

// area has a receiver of (r rect)
func (r rect) area() int {
    return r.widht * r.height
}

r := rect{
    width: 5, e
    height: 10,
}
```