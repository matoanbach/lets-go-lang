# Mutexes in Go

Mutexes allow us to lock access to data. This ensures that we can control which gorountines can access data at which time.

Go's standard library provides a built-in implementation of a mutex with the <code>sync.Mutex</code> type and its two methods:

- <code>Lock()</code>
- <code>Unlock()</code>

We can protect a block of code by surronding it with a call to <code>Lock</code> and <code>Unlock</code> as shown on the <code>protected()</code> method below.

It's good practice to structure the protected code within a function so that <code>defer</code> can be used to ensure that we never forget to unlock the mutex.

```go
func protected() {
    mux.Lock()
    defer mux.Unlock()
    // the rest of the function is protected
    // any other calls to `mux.Lock()` will block
}
```

# RW Mutex

The standard library also exposes a <code>sync.RWMutex</code>

In addition to these methods:

- <code>Lock()</code>
- <code>Unlock()</code>

The <code>sync.RWMutex</code> also have these methods:

- <code>RLock()</code>
- <code>RULock()</code>

The <code>sync.RWMutex</code> can help with performance if we have a read-intensive process. Many goroutines can safely read from the map at the same time (mutiple <code>RLock()</code> calls can happen simultaneously). However, only one goroutine can hold a <code>Lock()</code> and all <code>RLock()</code>'s will also be excluded.
