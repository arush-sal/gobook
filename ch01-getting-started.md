# Getting started with Golang - a fast track overview.

## Installing Golang
---

Visit Golang's official installation instructions [at here](https://golang.org/doc/install)

## Hello World!
---

```go
package main // Everything in Golang revolves around packages
import (
    "fmt"
 ) // Import the fmt or formatting package

fucn main() { //Define main function "func" is the keyword of notice here.
    fmt.Printf("Hello, World!") // The letters aren't bytes or chars, infact in Golang these are called "runes". This adds unicode support, enabling the language to print any printable character.
}
```

> Notice the 'P' in Printf. To export any function outside of the package or to be able to use any fucntion from a package the first letter of the function needs to be a capital letter. Same goes with other things such as variables.

## Golang directory structre:
---

The Golang compiler is built to operate on a particular directory structre. Therefore having the structre correct is very import for working with Golang. The typical suggested directory structre should be like:

```
$GOPATH
      |__src
            |_<your project name>
                                |_*.go
```
If you use the defined dir structre, you can use the Golang "install" function which will store your compiled binary in a folder called bin like shown below.

```
$GOPATH
      |__src
      |     |_<your project name>
      |                         |_*.go
      |_bin/<your project name executable>
```

## Golang style:
---

`go fmt` is an inbuilt function that enforces the Golang formatting in the source code. Golang is very particular about the code formatting and things like braces after function declaration can't be overwritten.

## Getting help in Golang
---

The best place to get all the documentation is `Golang.org`. But we can also have a local help program, sort of Golang's own man pages. That program is called `godoc`. It alows you to have infomation about any package, including the one you have written.

e.g:

`godoc fmt Printf`