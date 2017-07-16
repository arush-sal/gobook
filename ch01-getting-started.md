# Getting started with Go - a fast track overview.

## Installing Go
---

Visit Go's official installation instructions [at here](https://golang.org/doc/install)

## Hello World!
---

```go
package main // Everything in Go revolves around packages
import (
    "fmt"
 ) // Import the fmt or formatting package

func main() { //Define main function "func" is the keyword to notice here.
    fmt.Printf("Hello, World!") // The letters aren't bytes or chars, in fact in Go these are called "runes". This adds unicode support, enabling the language to interpret and work in any printable character.
    // Also, we can use "Println" instead of "Printf" to print with a newline at end of string. Just as in Java.
}
```

> Notice the 'P' in Printf. To export any function outside of a package or to be able to use any function from a package the first letter of the function needs to be a capital letter. Same goes with other things such as variables.

## Go directory structure:
---

The Go compiler is built to operate on a particular directory structure. Therefore having the structure correct is very important for working with Go. The typical suggested directory structure should be like:

```
$GOPATH
      |__src
            |_<your project name>
                                |_*.go
```
If you use the defined dir structure, you can use the `go install` function which will store your compiled binary in a folder called bin like shown below.

```
$GOPATH
      |__src
      |     |_<your project name>
      |                         |_*.go
      |_bin/<your project name executable>
```

## Go style:
---

`go fmt` is an inbuilt function that enforces the Go formatting in the source code. Go is very particular about the code formatting and things like braces after function declaration can't be overwritten.

## Getting help in Go
---

The best place to get all the documentation is `golang.org`. But we can also have a local help program, sort of Go's own man pages. That program is called `godoc`. It allows you to have information about any package, including the one you have written.

e.g:

`godoc fmt Printf`