Scala Basics
============

 - It runs on the standard Java platform and interoperates seamlessly with all Java libraries.
 - Scala is a fusion of object-oriented and functional programming
 - Immutable data structures are one of the cornerstones of functional programming
 - Methods should not have any side effects. They should communicate with their environment only by taking arguments and returning results.

Why use scala
-------------

 - Scala code is compatible with existing Java classes
 - Scala programs tend to be short.

Scala is statically typed
-------------------------

 - Verbosity is avoided through type inference and flexibility is gained through pattern matching and several new ways to write and compose types.
 - The most important of these benefits are verifiable properties of program abstractions, safe refactorings, and better documentation.
 - Scala has a very sophisticated type inference system that lets you omit almost all type  information  that’s usually considered as annoying

  `val x = new HashMap[Int, String]()`  
  `val x: Map[Int, String] = new HashMap()`

Scala variables
---------------
- var - Mutable
- val - Immutable

Functions
---------

- Created by `def` keyword
- Return type of the function can be ommitted, this will be inferred by scala's type inference.
- If the function is recursive Scala compiler will explicitly need the return type.
- Function that doesnot take in any parameters can be defined by, `def functionName() = ...` or `def functionName = ...`

  `functionName()` should be used if the function performs certain operation.
  `functionName` should be used if the function returns a conceptual property i.e. if it acts as a getter function


Scala script
------------

- In unix, one can write scala scripts by prepending this to the top of the file

  ```
  #!/bin/sh
  exec scala "$0" "$@"
  !#
  ```
  provided scala is configured on that machine and scala bin is added in the `PATH`

Moving from imperative to functional
------------------------------------

- In functional no `vars` to be used

Scala List
----------

- Are immutable
- `:::`, used for prepending the passed list
- `::`, pronounced cons, prepends a element to the beginning of a list, `1 :: List(2, 3)`
- List of numbers 1,2 and 3  can be created by

   `List(1, 2, 3)`   
   `1 :: 2 :: 3 :: Nil`

    Just specifying `1 :: 2 :: 3` will yield error because the operation `::` is not defined for `Int`

Scala Set and Map
-----------------

- Scala Set can be defined as
  - `Set(1 , 2, 4)`, immutable. Is a factory method which inturn a Set of type `scala.collection.immutable.HashSet[Int]`
  - `new scala.collection.mutable.HashSet[Int]`, Mutable

  `+=` function can be used to append to Set
- Similar to Set Scala Map has mutable and immutable implementations of `HashMap`. It also has a factory method `Map("key" -> "value")`, which creates a immutable HashMap

Scala Objects
-------------
- are singleton in nature
- Scala objects can be:
  - `Companion object` a corresponding class is defined with the same name. This enables the object to access the private members defined inside the class
  - `Standalone object` no coresponding class is defined

Scala Traits
------------
- Can extend 0 or more Traits
- Can contain non abstract Functions
- if a function is overridden in the extended class `override` modifier needs to be specified
- Scala can be mixed in at the time of class instantiation

 ```
 trait Friendly {
   def greet() = "hi"
 }

 class Dog extends Friendly {
   override def greet() = "Woof"
 }

 trait ExclamatoryGreet extends Friendly {
   override def greet() = super.greet() + "!"
 }

 ```

 `new Dog with ExclamatoryGreet`, by doing so Scala creates an `Synthetic class` which overrides the function `greet()` with the implementation in `ExclamatoryGreet`

Scala String
------------

- Support special syntax for multi line strings, string enclosed in `""" ... """` can be used to define strings that span many lines. `|` can used in start to of each new line to strip of spaces or margin from the beginning of that line

Scala Operators
---------------------

- In scala all operators `+, -, /, *` are Functions
- To implement `1 + 2`, Scala transforms this into method `1.+(2)`
-To implement `-2`, scala transforms this into `2.unary_-`
- `===` can be used to compare if to objects are equal in value
- `eq` can be used to to compare reference equality
- if the method ends with `:`, it is evaluated right to left. i.e  `1 :: Nil` is evaluated as `Nil.::(1)`

Scala constructors
------------------

- `primary constructor`, takes the class parameters and executes everthig defined in the body of the class
- `auxiliary constructor`, for multiple constructor support. defined as `def this(...) = this(...)`. This constructor should inturn call the primary constructor or another auxiliary constructor. The primary constructor is the single point of entry

Scala Identifier
----------------

- support alphanumeric identifier, starting with _ or character followed  by letter, digits or underscores
- `$` is also accepted at compile time as a identifier, but should not be used as it is used by scala internally and it would lead to name clashes with identifiers generated by scala interanally
- Scala supports creating identifier with the same name as any reserved keyword in Scala. This can be accomplished by enclosing the identifier in `` ` ` `` (backtick). A usecase is calling Java method `Thread.yield()` in Scala can be done as ``Thread.`yield()` `` as `yield` is a reserved keyword in scala

Scala Implicits
---------------
- Scala implicit conversions that enable to one to add functions to a class other than user defined classes
 
