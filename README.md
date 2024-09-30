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

## The language

### Variable definition
Mutable and immutable variables are defined using `let` and `val`, respectively.

#### Varibale definiteion
```
let x = 4 // creates a mutable variable called x (type Int is inferred)
let y: Int = 4 // creates a mutable variable called y explicitly typed as Int
```

#### Constant definition
```
val z = 4 // creates an immutable variable called z (type Int is inferred)
val w: Int = 4 // creates an immutable variable called w explicitly typed as Int
```

### Basic types
The basic types are `Int`, `Float`, `String`, and `Bool`.
In the following examples, the type of each variable is explicitly shown for clarity, but in practice, types are inferred.

#### Numbers
```
val x: Int = 4
val y: Float = 4.0
```
#### Strings
```
val str: String = "hello"

// string interpolation
val name = "Alice"
val greeting = "Hello, {name}!"
```

#### Booleans
```
val b: Bool = true
```

### More complex types
Perfect also has lists, tuples, and ranges.

#### Lists
```
val names: List of String  = ["Alice", "Bob", "Charlie"]
val numbers: List of Int = [1, 2, 3, 4, 5]
```

#### Tuples
```
val tuple: (Int, String) = (4, "hello")

// alternatively:
val tuple: Tuple of Int, String = (4, "hello")
```

#### Ranges
```
val range: Range = 1 to 4 // 1, 2, 3, 4
val stepped_range: Range = 1 to 4 step 2 // 1, 3
val reversed_range: Range = 4 to 1 // 4, 3, 2, 1
val reversed_stepped_range: Range = 4 to 1 step 2 // 4, 2
```

### Control flow
If/else, while, and for loops. If/else blocks are expressions.

#### If
```
val x = 4
if x > 3
  |print| "x is greater than 3"
--
```

#### If/else
```
val x = 4
if x > 3
  |print| "x is greater than 3"
else
  |print| "x is less than or equal to 3"
--
```

#### If/else as an expression
```
val x = 4

val message = if x > 3
  "x is greater than 3"
else
  "x is less than or equal to 3"
--

|print| message
```

#### While
```
let x = 4
while x > 0
  |print| x
  x = x - 1
--
// prints 4, 3, 2, 1
```

#### For
```
for i in 1 to 4 |print| i
// prints 1, 2, 3, 4

for i in 8 to 1 step 2 |print| i
// prints 8, 6, 4, 2

for i in [1, 2, 3, 4] |print| i
// prints 1, 2, 3, 4

// for with index
for i, index in [1, 2, 3, 4] |print| i, index
// prints 1, 0\n2, 1\n3, 2\n4, 3
```

### Match
Perfect has a `match` expression that can be used to match values against patterns. Similar to switch statements in many languages, or match expressions in Rust.

#### Basic usage
```
val x = 4
match x
  1 then |print| "one"
  2 then |print| "two"
  3 then |print| "three"
  other then |print| "something else"
--
```

#### With multiple cases
```
val x = 4
match x
  1, 2, 3 then |print| "one, two, or three"
  other then |print| "something else"
--
```

#### With code blocks
```
val x = 4
match x
  1, 2, 3 then
    |print| "one"
    |print| "another line"
  --
  other then |print| "something else"
--
```

#### Value capturing
```
val x = 4
match x
  3 then |print| "you got magic number!"
  other num then |print| "you got {num}"
--
```

#### Using match as an expression
```
val x = 4

val message = match x // message is inferred as String
  1 then "one"
  2 then "two"
  3 then "three"
  other then "something else"
--

|print| message
```

### Function definition
Functions are defined using the `fn` keyword. Functions can have unnamed arguments, named arguments, and named returns.

#### Unnamed arguments
```
fn add Int, Int -> Int
  _0 + _1
--
```

#### Named arguments
```
fn add_named_arguments x: Int, y: Int -> Int
  x + y
--
```

#### One-liner
```
fn add_named_arguments x: Int, y: Int -> Int x + y
```

#### No return type
```
fn print_hello
  |print| "hello"
--
```

#### No return type with arguments
```
fn print_name name: String
  |print| name
--
```

#### One unnamed argument
```
fn print_name_2 String
  |print| it // it is the default name for the first argument (like in Kotlin)
--
```

#### Named returns
```
fn add_named_return x: Int, y: Int -> result: Int
  x + y
--
```

### Function calls
To call a function, surround its name with pips (`|`), like so: `|function_name| <arguments>`.

#### Unnamed arguments
```
val three = |add| 1, 2
```

#### named arguments
```
val three = |add_named_arguments| x: 1, y: 2
// when the arguments are named, they can be called in any order
val four = |add_named_arguments| y: 2, x: 2
```

#### No arguments
```
|print_hello|
```

### Closures
Similar to other languages; closures are anonymous functions that can capture variables from their environment.

#### Named arguments
```
let my_closure = x: Int, y: Int -> Int x + y
val three = |my_closure| x: 1, y: 2
```

#### Unnamed arguments
```
let my_closure = Int, Int -> _0 + _1
val three = |my_closure| 1, 2
```

### Structs
TODO

#### basic definition
```
struct Point
  x: Int
  y: Int
--
```

#### Instantiation
```
val p = Point x: 4, y: 5
val x = p.x
```

#### Methods
```
struct Point
  x: Int
  y: Int

  fn distance_to Point -> Float
    let dx = self.x - it.x
    let dy = self.y - it.y
    (dx * dx + dy * dy) ^ 0.5
  --
--

val p = Point x: 4, y: 5
val q = Point x: 1, y: 1
val distance = p.|distance_to| q
```

#### Mutating methods
```
struct Point
  x: Int
  y: Int

  mut fn move_to x: Int, y: Int
    self.x = x
    self.y = y
  --
--

// incorrect
val p = Point x: 4, y: 5
p.|move_to| x: 1, y: 1 // ERROR: move_to is a mutating method and p is not mutable

// should be:
let p = Point x: 4, y: 5 // use let instead
p.|move_to| x: 1, y: 1
```

#### Default values
```
struct Point
  x: Int = 0
  y: Int = 0
--

val p = Point
p.x // 0
p.y // 0
```

#### Extensions
```
struct Point
  x: Int
  y: Int
--

extend Point with
  fn distance_to Point -> Float
    let dx = self.x - it.x
    let dy = self.y - it.y
    (dx * dx + dy * dy) ^ 0.5
  --
--
```

#### Inheritance
```
struct Shape
  x: Int
  y: Int
--

struct Circle extends Shape
  radius: Int
--

val c = Circle x: 4, y: 5, radius: 10

fn print_coordinates Shape
  |print| it.x, it.y
--

|print_coordinates| c // works
```

### Enums
```
// TODO
```
