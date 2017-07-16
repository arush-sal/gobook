# Controlling Conditional follow 

Conditional flow in Go is achieved using `if-else-if` and `switch-case`.

## If-Else-If

Format:

```go
if <assignment or initialization>; <condition> {
      <things to do>
} else {

}
```
Just like in above example we can do multiple assignments in a single line and can base our condition on that.

Example:

```go
if totalBytes, error := fmt.Printf("Hello, World!"); error != nil {
      os.Exit(1)
} else {
      fmt.Printf("%d", totalBytes)
}
```

Note that the `<assignment or initialization>` part is totally optional and _is available if required_. Also, if using `<assignment or initialization>` make sure to end it with a semi-colon( **;** ).

Similarly, we can use multiple `if` statements in conjunction with `else` to form multiple condition sequence. e.g:

```go
if totalBytes, error := fmt.Printf("Hello, World!"); error != nil {
      os.Exit(1)
} else if totalBytes == 0 {
      fmt.Printf("Empty string")
} else {
      fmt.Printf("%d", totalBytes)
}
```

## Switch-Case

`switch-case` works a bit different in Go as compared to other languages such as `C`, for example, it doesn't fallthrough i.e, not all of the `case` defined will be evaluated as it is done in `C`. We can use the keyword `fallthrough` to explicitly enforce this behavior.

Format:

```go
switch <variable> {
      case <condition>:
            <things to do>
      default:
            <things to do>
}
```

> Note: The `<variable>` part with `switch` is totally optional.

Example:

```go
message := "the quick brown fox jumps over the lazy dog"

vowel := 0
consonants := 0

for _, letter := range message{
      switch letter {
            case 'a', 'e', 'i', 'o', 'u':
                  vowel += 1
            default:
                  consonants += 1
      }
}

fmt.Printf("Vowels = %d, Consonants = %d", vowel, consonants)
```
Example, `fallthrough`:

```go
message := "the quick brown fox jumps over the lazy dog"

vowel := 0
consonants := 0
aes := 0
zeds := 0

for _, letter := range message{
      switch letter {
            case 'a', 'e', 'i', 'o', 'u':
                  vowel += 1
                  fallthrough // Next case will also be evaluated.
            case 'a':
                  aes += 1
            case 'z':
                  zeds += 1
                  fallthrough // Next case will also be evaluated.
            default:
                  consonants += 1
      }
}

fmt.Printf("Vowels = %d, Consonants = %d, Aes = %d, Zeds = %d", vowel, consonants, aes, zeds)
```

Similarly, we could also do the following:

```go
totalBytes, err := fmt.Printf("Hello, World!")

switch {
      case err != nil:
            os.Exit(1)
      case totalBytes == 0:
            fmt.Printf("Empty string")
      default:
            fmt.Printf("This is strange.")
}
```

#### Loops

Go has only one keyword to be used for loops i.e `for` but it supports all different kind of formats. Therefore we can use `for` to achieve the functionality of `while` and traditional `C` `for`.

`while` Format:

```go
var counter bool
for !counter {
      <do-something>
      if <condition> {
            counter = true
      }
}
```

`for` Format:

```go
for i := 0; i < 10; i++ { // we can also do double initialization and assignment i.e 'i, j := 1; i < 10; i, j = i++, j*2'
      <do-something>
}
```