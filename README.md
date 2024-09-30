# The Perfect Programming Language

## TODO:
- enums
- more details on structs
- throwing functions
- type aliases
- generics
- module system
- standard library


## Goals
- Approachable
- Powerful
- Fast
- Safe

## Features
- static typing
- type inference
- named returns
- typed throws
- no semicolons
- no parens for if/while/for/etc.
- implicit returns
- variables are snake_case
- types are PascalCase
- named arguments

## Examples

### Variable definition
```
// variable definition
let x = 4 // creates a mutable variable called x (type Int is inferred)
let y: Int = 4 // creates a mutable variable called y explicitly typed as Int

// constant definition
val z = 4 // creates an immutable variable called z (type Int is inferred)
val w: Int = 4 // creates an immutable variable called w explicitly typed as Int
```

### Basic types
```
// note: types are explicitly shown in examples for clarity, but are inferred in practice

// numbers
val x: Int = 4
val y: Float = 4.0

// strings
val str: String = "hello"

// booleans
val b: Bool = true

// lists
val names: List of String  = ["Alice", "Bob", "Charlie"]
val numbers: List of Int = [1, 2, 3, 4, 5]

// tuples
val tuple: (Int, String) = (4, "hello")
// alternatively:
val tuple: Tuple of Int, String = (4, "hello")

// ranges
val range: Range = 1 to 4 // 1, 2, 3, 4
val stepped_range: Range = 1 to 4 step 2 // 1, 3
val reversed_range: Range = 4 to 1 // 4, 3, 2, 1
val reversed_stepped_range: Range = 4 to 1 step 2 // 4, 2
```

### Control flow
```
// if
val x = 4
if x > 3
    print "x is greater than 3"
--

// if/else
val x = 4
if x > 3
    print "x is greater than 3"
else
    print "x is less than or equal to 3"
--

// while
let x = 4
while x > 0
    print x
    x = x - 1
--
// prints 4, 3, 2, 1

// for
for i in 1 to 4 print i
// prints 1, 2, 3, 4

for i in 8 to 1 step 2 print i
// prints 8, 6, 4, 2

for i in [1, 2, 3, 4] print i
// prints 1, 2, 3, 4

// for with index
for i, index in [1, 2, 3, 4] print i, index
// prints 1, 0\n2, 1\n3, 2\n4, 3

// match
val x = 4
match x
    1 then print "one"
    2 then print "two"
    3 then print "three"
    other then print "something else"
--

// match with multiple cases
val x = 4
match x
    1, 2, 3 then print "one, two, or three"
    other then print "something else"
--

// match with codeblocks
val x = 4
match x
    1, 2, 3 then
        print "one"
        print "another line"
    --
    other then print "something else"
--

// value capturing
val x = 4
match x
    3 then print "you got magic number!"
    other num then print "you got {num}"
--
```

### Function definition
```
// unnamed arguments
fn add Int, Int -> Int
    _0 + _1
--

// named arguments
fn add_named_arguments x: Int, y: Int -> Int
    x + y
--

// one-liner
fn add_named_arguments x: Int, y: Int -> Int x + y

// no return type
fn print_hello
    print "hello"
--

// no return type with arguments
fn print_name name: String
    print name
--

one unnamed argument
fn print_name_2 String
    print it // it is the default name for the first argument (like in Kotlin)
--

// named returns
fn add_named_return x: Int, y: Int -> result: Int
    x + y
--
```

### Function calls
```
// unnamed arguments
val three = add 1, 2

// named arguments
val three = add_named_arguments x: 1, y: 2

// no arguments
print_hello
```

### Closures
```
// named arguments
let my_closure = x: Int, y: Int -> Int x + y
val three = my_closure x: 1, y: 2

// unnamed arguments
let my_closure = Int, Int -> _0 + _1
val three = my_closure 1, 2
```

### Structs
```
// basic definition
struct Point
    x: Int
    y: Int
--

// instantiation
val p = Point x: 4, y: 5
```

### Enums
```
// TODO
```
