# Custom Datatypes

## Arrays and Slices

In Go to deal with linear ordered data sets or data structures we have two datatypes
1. `Arrays`
2. `Slices`

> `Arrays` are rarely used in Go and in general `slices` are always used and preferred for reasons of flexibility and speed. Read [this](https://stackoverflow.com/questions/30525184/array-vs-slice-accessing-speed).

#### Arrays

Format:
```go
array := [10] string{"a","b","c","d","e","f","g","h","i","j"} // Declared a fixed size array
array := [...] string{"a","b","c","d","e","f","g","h","i","j"} // Declared a arbitrary size array
```

> Note: Array is always passed around as "value" instead of reference i.e it will pass a copy of the array not the actual array, that had some significant memory performance implications. As every time it will create a new memory block.

#### Slices

`Slices` by nature are typically a data chunk out of an under lying `array` i.e a part of some existing `array`. Therefore it always will have a starting and an end point, if you don't provide any then it will take the beginning and ending point of the `array` as the default.

> Note: `Slices` are always passed around as "reference" instead of value i.e it will pass the actual `slice` not the copy of the `slice`. Because `slices` are passed by reference, therefore, they are mutable by nature i.e you can change the slice values by replacing it with another value.

Format:
```go
slice := [] string{"a","b","c","d","e","f","g","h","i","j"} // This is a static slice with the elements pre-declared.
slice := make([] string M, N) // This is a dynamic slice with no elements in it. 'M' and 'N' are an optional value that needs to a positive integer to initialize the 'slice' with the given number of empty or 'null' elements. 'M' will define it's current capacity and 'N' will define its maximum capacity.

// Assigning value to an element position of slice
slice[0] = "a"
slice[1] = "b"
```

**Common slice/array functions:**

* To find the length of a slice/array: `len(slice/array)`
* Slice of a Slice: `slice[0:6]`
    > The ending index is exclusive, therefore that element will not be including printing 5 elements.
* `Append` new element to slice: `append(slice, "The")`
    > If you try to append more elements to s slice than its capacity i.e `N` from above example then the capacity is doubled implicitly.
* To know capacity of a slice: `cap(slice)`
* To create a new copy of a slice: `copy(newSlice, slice)`
* Changing Datatypes: We can change the datatype of a slice using: `byte(slice)` or `foobar([]byte(slice))`
    > It does look like a `type casting` as in `C` or `Java` but it is a real change of datatype instead. So, use it carefully to interchange compatible datatypes only.
* Passing slice as an argument to a function: `foobar(slice []string)`

## Maps

Maps are heterogeneous data structures with no fixed numerical index part. These are best used to create `key`-`value` stores, lookup tables, implementing sets, etc. In other languages, it is called `Dictionary`, `Hash`, `Assertive Array`, etc.

Format:
```go
newMap := make(map[string]string) // In '[]' we provide the datatype for the key and outside it we provide the datatype of the 'value'. This will create a dynamic size map.
newMap["Name"] = "Arush"
newMap["TwitterHandle"] = "arush_sal"
newMap["Email"] = "me@aru.sh"

// Creating a static map.
newMap := make(map[string]string){
    "Name": "Arush",
    "TwitterHandle": "arush_sal",
    "Email": "me@aru.sh",
}

fmt.Printf(newMap["Name"]) // If you try to access a non-existing element in a map you will get a `zero-type` value for that datatype i.e `nil` for `string`, `0` for `int`, `0.0` for float and so on.
```

> A map returns two values, the `value` for the `key` mentioned and a boolean status. We test an element existence using the [comma-ok](./ch05-custom-datatypes.md#comma-ok-format) syntax.

#### Comma-Ok Syntax
```go
mailId, ok := newMap["Email"] = "me@aru.sh" // If the particular 'key-value' doesn't exist it will return 'false' and it will return 'true' if it exists, assigning the value to 'ok'.

if !ok {
    fmt.Printf("Key not found")
} else {
    fmt.Printf(mailId)
}
```

#### Common slice/array functions:

* Looping: We can iterate over a map just like any other data structure using the keyword `range` and it will return both the `keys` and the `values` **in no particular order**, but we can define the order by the use of sorting.
* Deleting an element of a map: `delete(newMap, "TwitterHandle")`
    > If you try to delete a non-existing element from a map then Go won't complain about it i.e it won't through an error.

## Errors

Errors are a first-class citizen of Go ecosystem i.e it is an internal default variable of interface datatype provided by the language. The language is built around handling errors returned by functions as compared to exceptions. Therefore there is no `error handling` provided by default in Go although there is an exception process called `panic` and `recover` which does seem like sort of `error handling` but it is not recommended to use that quite often. By convention, errors are returned by the functions and he calling function has to take care of it.

Format:
```go
fmt.Errorf("My error message")
```

Usage:
```go
func foobar(dividend, divisor int) (int, error) {
    if divisor == 0 {
        return fmt.Errorf("Can't divide by Zero")
    } else {
        result := dividend/divisor
        return result
    }
}

func main() {
    division, err := foobar(20,0)

    if err != nil {
        fmt.Printf("OMG! What have you DONE.")
    } else {
        fmt.Printf(division)
    }
}
```

#### Errors package

To define a custom `error type` or to retrieve the `error type` we use the `errors package`.

Format:
```go
import "errors"

mathematicalArmageddon = errors.New("Can't divide by Zero") // Define a new error type called "mathematicalArmageddon, which we can later on compare to certain error conditions and define our flow control based on that."
```

#### Other return types

> panic() - We can use this function as a self destruct on the program itself in case of an error. It will cause an immediate program termination with the `stacktrace` printed to the STDOUT.

> recover() - This can be used to recover from a `panic()` but should only be used a feature of _very rare_ usage.
