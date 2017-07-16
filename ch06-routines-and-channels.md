# Go Routines and Channels

## Routines
---

A Go `routine` is an individual part or thread of a program that is running `concurrently` with the main program itself.

Format:
```go
go foobar()
```

## Channels
---

A `channel` is a data stream(more like a data pipe) through which you can send or receive values to and from any `Go function or routine`.

Format:
```go
c := make(chan string)
```

> `<-` is called the `channel operator` and it is used to send or receive values over a channel. The operator works on right to left assignment, so if your `channel` is on right and the `function/routine` on left, then your `channel` is sending data. If your `channel` is on left and `function/routine` on right then it is receiving the data.

You can easily receive whatever is being sent on a `channel` by iterating over it using `range`. e.g:
```go
for data := range c {
    fmt.Printf(data)
}
```

In above example once the `channel` closes(stops sending data) the `range` receives a close or `Zero value` and it stops the iteration. If you explicitly try to receive on a closed channel(like shown below), then it will not issue an error, rather it will just assign the `Zero value` to the receiving variable. You can check if a `channel` is open or not by using the [comma-ok syntax](./ch05-custom-datatypes.md#comma-ok-format).
```go
var data int
data = <-c
```

#### Closing a channel:

The Go channels are blocking nature i.e it will block the code execution when ever the operation execution is passed to it. Therefore, whenever there is no more data value to be sent on a channel we should close the channel to specify that no more data will be sent on the channel. The keyword `close` can be used to close a channel like `close(c)`, but its not closing a channel is not exclusive to `close`, it can also be done by various other ways.

> **Always make sure to close all the `channels` else the compiler will complain about deadlock.

#### Working with multiple channels

We can use `Select-Case` in Go to work with multiple channels based on different conditions. Just as in `switch-case` we define different operations  as per `case`, similarly we can define different channels to each case in `Select-Case`. e.g:
```go
func fibonacci(c, quit chan bool) {
	x, y := 0, 1
	for {
		select {
		case c <- x:
			x, y = y, x+y
		case <-quit:
			fmt.Println("quit")
			return
		}
	}
}

func main() {
	c := make(chan int)
	quit := make(chan bool)
	go func() {
		for i := 0; i < 10; i++ {
			fmt.Printf(<-c)
		}
		quit <- 0
	}()
	fibonacci(c, quit)
}
```

#### Closing a channel by itself

A channel is bidirectional and therefore it can be used to close itself without the need of `close` explicitly when used with `select`. e.g:

```go
func fibonacci(c, quit chan bool) {
	x, y := 0, 1
	for {
		select {
		case c <- x:
			x, y = y, x+y
		case <-quit:
			fmt.Println("quit")
			quit <- true // This will close the waiting channel "<-quit" in main().
			return // This will close the channel in routines.
		}
	}
}

func main() {
	c := make(chan int)
	quit := make(chan bool)
	go func() {
		for i := 0; i < 10; i++ {
			fmt.Printf(<-c)
		}

		quit <- true // This will make the case <-quit to be executed.
		<-quit // This will still keep the channel open and waiting for values.
	}()
	fibonacci(c, quit)
}
```
_Original example from: https://tour.golang.org/concurrency/5_

#### Channel of Channels