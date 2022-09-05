# Variables, Simple Types and Declarations

A variable in Go can be declared using `var` keyword. The default datatypes supported in Go are:

* Boolean Types: They are boolean types and consists of the two predefined constants: 

      1. true
      2. false

> We can use the keyword `bool` to just declare a boolean, which will be initialized by the default value of `false`. As if we don't initialize any variable in Go it gets initialized by a `Zero value` which in the case of an integer are '0', for a float is '0.0', similarly, for boolean it is false.

* Numeric Types: They are again arithmetic types and they represent 

      1. Integers
      2. Floating point

* String types: A string type represents the set of string values. Its value is a sequence of runes. Strings are immutable types that are once created, it is not possible to change the contents of a string. The pre-declared string type is `string`.

* Derived types: They include 

      1. Pointer types
      2. Array types
      3. Structure types
      4. Union types
      5. Function types
      6. Slice types
      7. Interface types
      8. Map types
      9. Channel Types

Declaring a variable example:
```go
func main() {
      var message string
      message = "Hello, World!"
      fmt.Printf(message)
}
```

This gives the sense that Go is a statically typed language such as `Java` or `C` where we have to be explicit about the datatype of the variable we wish to use. But we can bypass this requirement by using `:=` operator. e.g:
```go
func main() {
      message := "Hello, World!"
      fmt.Printf(message)
}
```

Using `:=` you can declare and assign a value to a variable together giving you the feature and feel of a dynamically typed language. In the case of multiple variable declarations using `:=` Go will check if all the variables are declared or not if any one of the variables is not declared before then we can safely use the operator to declare the new variable and redefine existing ones.

> You can use the keyword `const` to declare a constant in Go.
> Quick word on constants from Effective Go:

```
Constants in Go are just that—constant.
They are created at compile time, even when defined as locals in functions, and can only be numbers, characters (runes), strings or booleans.
Because of the compile-time restriction, the expressions that define them must be constant expressions, evaluatable by the compiler.
For instance:
      1<<3 is a constant expression, while math.Sin(math.Pi/4) is not because the function call to math.Sin needs to happen at runtime.
      "foo" is a constant expression, while []string{"foo"} is not because slices and arrays are always evaluated during runtime.
```


Multiple declarations can be used by the usage of `()` with any declarative keyword such as `var` or `const`. e.g:
```go
var (
      message1 = "Hello,"
      message2 = " World!"
)
```

Another way of explicitly declaring the datatype and assigning the value can be as:
```go
func main() {
      message := string("Hello, World!")
      fmt.Printf(message)
}
```

> The keyword `iota` can be used as a variable with the initial value of 1. All the uninitialized variables after the first usage of the keyword get value assigned to it using the same expression in which `iota` was used. e.g:
```go
var (
      answer1 = iota
      answer2
) // answer2 will get the value of 2 as default.

var (
      answer1 = iota*2
      answer2
) // answer2 will get the value of 4 as default.
```

## Numeric

The whole list of numeric types that are available to us in Go is as following:

**Integer Types**

The pre-define architecture-independent integer types are:

1. uint8: Unsigned 8-bit integers (0 to 255)
2. uint16: Unsigned 16-bit integers (0 to 65535)
3. uint32: Unsigned 32-bit integers (0 to 4294967295)
4. uint64: Unsigned 64-bit integers (0 to 18446744073709551615)
5. int8: Signed 8-bit integers (-128 to 127)
6. int16: Signed 16-bit integers (-32768 to 32767)
7. int32: Signed 32-bit integers (-2147483648 to 2147483647)
8. int64: Signed 64-bit integers (-9223372036854775808 to 9223372036854775807)

**Floating Types**

The pre-define architecture-independent float types are:

1. float32: IEEE-754 32-bit floating-point numbers
2. float64: IEEE-754 64-bit floating-point numbers
3. complex64: Complex numbers with float32 real and imaginary parts
4. complex128: Complex numbers with float64 real and imaginary parts

> The value of an n-bit integer is n bits and is represented using two's complement arithmetic operations.

**Other Numeric Types**

There is also a set of numeric types with implementation-specific sizes:

1. byte: same as uint8
2. rune: same as int32
3. uint: 32 or 64 bits
4. int: same size as uint
5. uintptr: an unsigned integer to store the uninterpreted bits of a pointer value

We can use `%d` and `%f` to print integers and floating point values in a printf statement respectively. Similarly, all of the `C printf` flags will work.

## Strings

In Go, strings are treated as an internally defined array of runes due to which it enables a user to be able to perform slicing such as creating substrings by defining any two character positions just as in python. e.g:

```go
var message string
message = "the quick brown fox jumps over the lazy dog"

// This will print "the quick" excluding the 9th rune. Since array index starts from 0 and space is also a character.
fmt.Printf("%s", message[0:9])
// Same as above. Because if you don't provide the value on the left of the colon it defaults to 0.
fmt.Printf("%s", message[:9])
// This will print "fox jumps over the lazy dog" including the 16th rune. Because if you don't provide the value on the left of the colon it defaults to the length of the string.
fmt.Printf("%s", message[16:])
// This will print "fox jump" excluding the 24th rune 's'.
fmt.Printf("%s", message[16:24])
```

Apart from above, we can also use the `range` keyword to iterate over the string character by character. e.g:

```go
msg := "the quick brown fox jumps over the lazy dog"
for i, letter := range msg {
      fmt.Printf("%c is at %d", letter, i)
}
```

The `range` function returns two value
      
      1. index of the loop
      2. index respective value that is being iterated over

You can assign the values returned by the function to any variable using the assignment variable `:=` the values will be assigned to the variables from left to right respectively. We can discard any value returned by the function by assigning it to the gutter variable '**_**'. If discarding the value being iterated over, we can omit the second assignment part as that is optional, but the index is mandatory.

> In Go we can use backquotes( **``** ) around a string to consider the whole string as a literal, including escape characters and anything else.
