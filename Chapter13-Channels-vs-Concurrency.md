# Go routine

```go
go doSomething()
```

# Channels

Channels are a typed, thread-safe queue. Channels allow different gorountines to communicate with each other.

## Create a channel

Like maps and slices, channels must be created before use. They also use the same <code>make</code> keyword.

```go
ch := make(chan int)
```

## Send data to a channel

```go
ch <- 69
```

## Receive data from a channel

```go
v := <- ch
```

## Token

Empty structs are often used as <code>tokens</code> in Go programs. In this context, a token is unary value. In other words, we don't care what is passed through the channel. We care when and if it is passed.

We can block and wait until something is sent on a channel using the following syntax

```go
<-ch
```

# Buffered Channels

## Creating a channel with a buffer

You can provide a buffer length as the second argument to <code>make()</code> to create a buffered channel:

```go
ch := make(chan int, 100)
```

Sending on a buffered channel only blocks when the buffer is full.

Receiving blocks only when the buffer is empty.

# Closing channels in Go

Channels can be explicitly closed by a sender:

```go
ch := make(chan int)

// do some stuff with the channel

close(ch)
```

## Checking if a channel is closed

Similar to the <code>ok</code> value when accessing data in a <code>map</code>, receivers can check the <code>ok</code>value when receiving from a channel to test if a channel was closed.

```go
v, ok := <-ch
```

# Select

Sometimes we have a single goroutine listening to multiple channels and want to process data in the order it comes through each channel.

A <code>select</code> statement is used to listen to mutiple channels at the same time. It is similar to a <code>switch</code> statement but for channels.

```go
select {
    case i, ok := <- chInts:
        fmt.Println(i)
    case s, ok := <- chStrings:
        fmt.Println(s)
}
```

# Tickers

- <code>time.Tick()</code> is a standard library function that returns a channel that sends a value on a given interval
- <code>time.After()</code> sends a value once after the duration has passed.
- <code>time.Sleep()</code> blocks the current goroutine for the specified amount of time.

# Read-only channels

A channel can be marked as read-only by casting it from a <code>chan</code> to a <code><-chan</code>. For example:

```go
func main() {
    ch := make(chan int)
    readCh(ch)
}

func readCh(ch <-chan int) {
    // ch can only be read from
    // in this function
}
```

# Write-only channels

The same goes for write-only channels, but the arrow's position moves.

```go
func writeCh(ch chan<- int) {
    // ch can only be written to
    // in this function
}
```
