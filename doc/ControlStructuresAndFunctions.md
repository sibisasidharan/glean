Control Structures
==================

If Control
----------

- ``val result = if(true) "hai" else "not returned"``
- ``val result = if(false) "not returned"``

  Returns `Unit`

While and do while
------------------
- similar to other languages
- usage is discourage
- opt for recursive implementation

For expressions
----------------

- Iterating through collections
 ```
 val l = List(1, 2, 3)

 for(element <- l)
    println(element)
 ```
- Iterating through integers can be achieved through Range
  ```
  for(element <- 1 to 3)
    println(element)
  ```  
- Filtering can be done in for by
  ```
  for(element <- 1 to 10; if(element % 2 == 0))
    println(element)  
  ```
  This prints only even number b/w 1 and 10

  ```
  for(
    element <- 1 to 10;
    if(element % 2 == 0);
    if(element != 4)
  ) println(element)
  ```
  This does the same as above, but omits 4.

  ```
  for{
    element <- 1 to 10
    if(element % 2 == 0)
    if(element != 4)
  } println(element)
  ```
  This is syntactically different but is the same as the above. Is enclosed in curly brackets and semicolons are avoided.

- Nested iterations can be done by
  ```
  for{
    element  <- 1 to 10
    if(element % 2 == 0)
    element2 <- 10 to 20
    if(element2 != 12)
  } println(element)
  ```
- Mid-stream assignment can used to assign values to `val`

  ```
  for{
    element  <- 1 to 10
    if(element % 2 == 0)
    endRange  = 20
    element2 <- 10 to endRange
    if(element2 != 12)
  } println(element)
  ```
- Unlike `while` or `do while`, `For` can return a collection it is processing
  ```
  for{
    element <- 1 to 10
    if(element % 2 == 0)
    if(element != 4)
  } yield element  
  ```
  This is equivalent to
  ```
  1 to 10 filter (e => (e%2 ==0 && e != 4) )
  ```

  ```
  for{
    element  <- 1 to 10
    if(element % 2 == 0)
    endRange  = 12
    element2 <- 10 to endRange
    if(element2 != 12)
  } yield element
  ```
  This is equivalent to
  ```
  (1 to 10).filter(x => x%2 == 0).flatMap(
  x => {
      val endRange = 12
      (10 to endRange).filter(y => y != 12).map(y => x)
    }
  )
  ```

Try-catch-finally
-----------------
- try similar to Java
- catch is done through pattern matching
  ```
  try{
    ...   
  }
  catch {
    case ex: IOException => println("Oops!")
    case ex: NullPointerException => println("Oops!!")
  }
  ```
- finally similar Java
- `try-catch-finally` clause can yield value. It can assign values to val or var
- If `return` is explicitly specified in the `finally` it will overrule any previous returns
  ```
  def e: Int = try { 1/0}
    catch{case ae: ArithmeticException => 1}
    finally { return 3}
  ```
  returns 3
  ```
  def e: Int = try { 1/0}
    catch{case ae: ArithmeticException => 1}
  ```
  returns 1
  ```
  def e: Int = try { 1}

    finally {3}
  ```
  returns 1

Place holder syntax
-------------------
- `_` can be used as place holders for parameters as long as the parameter is used only once inside the declaration.
- If the compiler is not able to infer the datatypes of the variables it can be explicitly specified
  ```
  val f = (_: Int) + (_: Int)
  ```
- For defining partially applied functions
  `def sum(a: Int, b: Int, c: Int) = a + b + c`
  `val a = sum _`
  The partially applied function can be used
  `a(1, 2, 3)`

  - Scala compiler generates another class which takes in 3 arguments and assigns it to `a`. The above call is equivalent to `a.apply(1, 2, 3)` which internally calls `sum(1, 2, 3)`
  `val a = sum(1, _: Int, 3)`
  Will result in Scala creating class with 1 argument. Hence, the partial function can be called as `a(2)`

Closure
-------

- In Scala, values of variable used inside a function can change with variable change.
  `val add = (x: Int) => x + more`  

  `var more = 1`

  `add(1) res: 2`
- Function can change values of variables defined outside the scope of the Function

  ```
  var sum = 1
  var function = (x: Int) => sum += x

  function(2)
  ```
  `res: sum = 3`

Repeated parameters
------------------
- `def sumOf(values: Int*) = values.sum`
  This can accept variable number of Integer arguments.
- can be called by `sumOf(1,2,3)` or pass in `List`, `Seq` or `Array` as `sumOf(Array(1,2,3): _*)`

Tail Recursion
---------------
- Recursive function that calls itself, by not doing any addition operation when the function is called recursively.
  ```
  def function(value: Int) = {
    if(value >= 5)
      0
    else
      function(value -1)
  }
  ```
  This is a recursive function
  ```
  def function(value: Int) = {
    if(value >= 5)
      0
    else
      function(value -1) -2
  }
  ```
  This not a recursive function

- Scala does optimization on recursive functions so that they as efficient as a while loop doing the same functionality.
