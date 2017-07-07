# Fucntions

We have already used functions in form of the `main` funcion using the `func` keyword.

Format:

```go
func awesomeFunction() { // Notice the same line curly brace, its a mandatory formatting rule to have it like that.
      <cool stuffs>
}
```

We can specify the fucntion arguments like:

```go
func awesomeFunction(arg1 string, arg2 int, arg3 float32) { 
      <cool stuffs>
}
```

Declaring multiple same datatype arguments:

```go
func awesomeFunction(arg1, arg2 string) { 
      <cool stuffs>
}
```

or:

```go
func awesomeFunction(arg1 ...string) { // 
      <cool stuffs>
}
```

Using function `return` values:

```go
func awesomeFunction() error {
      // Notice that it is not mandator-y to specify the return value name but we can still specify one if we wish, in which case it would be
      // returned implicitly.
      <cool stuffs>

      return err
}
```

In Golang are not bound to return just a single value but instead we can even return multiple values from a fucntion

```go
func awesomeFunction() (someNumber int, e error) {
      <cool stuffs>

      return // someNumber and e will be returned implicitly.
}
```

**Defer**

The keyword `defer` can be used to perform aany certain operation that we wish to perform before the function exit. This is specicially useful for doing things like closing opened resources such as a file or open connections such as to a socket file.

We can have multiple `defer` in a single function, they works by `FILO(First In Last Out)` so the first defer you define in the function will always will be executed as the last operation of the funcion.

Example:

```go
func awesomeFunction() {
      defer fmt.Printf("Final Goodbye.") // this will be executed last.
      defer fmt.Printf("Just Kidding..\n")
      defer fmt.Printf("Goodbye.\n") // this will run as the first defer.
}
```

The output of above will be as:

```
Goodbye.
Just Kidding
Final Goodbye.
```

> Must Read [Don’t defer Close() on writable files](https://joeshaw.org/dont-defer-close-on-writable-files/)