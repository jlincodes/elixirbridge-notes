# Elixirbridge Notes

## Types
- Numbers (Integers) & Floats
  - Integer
  ```Elixir
  1                 # 1
  is_integer(42)    # true
  is_integer(3.14)  # false
  ```
  - Floats
  ```Elixir
  1.0
  2000.8
  1.0e-10
  is_float(3.14)  # true
  ```

  ```Elixir
  1 + 1             # 2
  div(10,2)         # 5
  rem(10,3)         # 1
  ## Works without parenthesis too
  rem 10,3          # 1
  10/2              # 5.0
  ```
  - Hex, Octal, Binary
    - Elixir support notation for entering binary, hex, octal, & hexidecimal numbers
- Booleans
```Elixir
true                  # true
false                 # false
is_boolean(true)      # true
is_boolean(false)     # true
```
- Strings
  - Strings in Elixir are values between *double quotes* and are UTF-8 encoded.

    ```Elixir
    ## Output values to the console using `IO.puts/1` command
    IO.puts("Hello world!")
    hello world!
    :ok

    String.length("hello world")    # 11
    String.upcase("hello world")    # HELLO WORLD

    ## String Interpolation
    receiver = "World"
    "Hello #{receiver}"

    ## Concatenate Operator <>
    "Hello" <> "World"          # "HelloWorld"
    ```
- Atoms (like Symbols in Ruby or Enumerations in C/C++)
```Elixir
:hello
:world
:true
:this_has_underscores
```

## Data Structures
- Lists
  - Collection of objects in Linked List O(n)

    ```Elixir
    [1,2,3]
    ["a", "b", "c"]

    ## A List can hold on to multiple different data types
    [1, :b, "c", "c"]

    ## Lists can contain both literal values and variables
    foo = "bar"
    [1, foo, 3] # [1, "bar", 3]
    ```
  - Head/Tail
  ```Elixir
  [h | tail] = [1,2,3]
  h # 1
  tail # [2,3]
  ```
  - Concatenation and Subtracting Lists
  ```Elixir
  [1] ++ [2] # [1,2]
  [1, 2, 3] -- [2] # [1,3]
  ```
- Tuples
  - Datatype similar to lists but used to store a fixed number of elements.
  ```Elixir
  {:ok, "hello"}
  ## fetching the first el in a tuple with `tuple_size/1`
  elem({:ok, "hello"}, 0) # :ok
  ## get tuple size
  tuple_size({:ok, "hello"}) # 2
  ## replace elements in a tuple with `put_elem/3`
  put_elem({:ok, "hello"}, 1, "world") # {:ok, "world"}
  ```
- Tuples vs Lists
  - Lists are slow to mod & read, but fast creation
  - Tuples are expensive to mod but good for pattern matching and additional information
- Keyword Lists
  - A list of tuples where the first element in each tuple is an atom.
  - We often want to set up a 2-item tuple as a representation of a `key-value` data structure.

    ```Elixir
    [greeting: "hello", receiver: "world"]
    [{greeting: "hello"}, {receiver: "world"}]

    ## concatnate a list using the key-value syntax with `++`
    list = [a: 1, b: 2]
    list[:a] # 1
    list[:c] # nil
    new_list = list ++ [c: 3]
    new_list[:c] = 3
    list[:c] # nil
    ```
  - Keys are:
    - Atoms
    - Ordered
    - Not unique
- Maps
  - key-value stores created by using `%{}` & similar to keyword lists except they are unordered
  - key cans be any data type

    ```Elixir
    map = %{:msg => "Hello", "receiver" => :world}
    map[:msg] # "Hello"
    map["msg"] # nil
    map[:"msg"] # "Hello"

    ## dot `.` syntax can be used to access map keys
    map.msg # "Hello"

    ## variables can also be used as keys
    name = "Foo"
    map = %{name => "world"}
    map[name] # "world"
    map["Foo"] # "world"
    ```
- Nested Data Structures
  - Elixir provides a way for us to hold variables inside of maps. We’ll use this a lot in the Phoenix framework, where we’ll have variables that represent data structures in our database.

    ```Elixir
    users = [
      john: %{name: "John", age: 27, languages: ["Erlang", "Ruby", "Elixir"]},
      mary: %{name: "Mary", age: 29, languages: ["Elixir", "F#", "Clojure"]}
    ]

    ## get variables using  `[]` (dynamic access) and `.` (strict access)
    users[:john].age # 27
    ```
  - Manipulate variables using `put_in/2` function to create a new value
  ```Elixir
  users = put_in users[:john].age, 31
  users
  # [john: %{age: 31, languages: ["Erlang", "Ruby", "Elixir"], name: "John"},
  # mary: %{age: 29, languages: ["Elixir", "F#", "Clojure"], name: "Mary"}]
  ```
<!--
```Elixir
```
-->


## Operators & Variables
- Comparison
  ```Elixir
  1 + 1 == 2    # true
  1 > 2         # false
  2 <= 4        # true
  1 != 2        # true

  ## Strict Comparison
  2 == 2.0      # true
  2 === 2.0     # false
  ```
- Variables
  - Value assignment to variables in Elixir work differently than it does in imperative languages (like Ruby or JavaScript)
  - In Elixir, there is no "assignment operator". Instead, the "=" is a "match operator" meaning that the "=" matches the term on the right to the "pattern" on the left.
  ```Elixir
  a = 1 # 1
  list = [1,2,3]
  tuple = {:ok, "Hello"}
  ```
  - Erlang and Elixir create immutable data. No variable is manipulated after it's create. Instead, a new one is created.
- Operators
  - Addition (`+`), division (`/`)
  - List manipulation (`++` and `--`)
  ```Elixir
  [1,2,3] ++ [4,5,6]  # [1,2,3,4,5,6]
  [1,2,3] -- [2]      # [1,3]
  ```
- Operators
  - Boolean operators `and`, `or`, and `not`
  ```Elixir
  false or true # true
  true or IO.puts("this won't print") # true
  ```
  - Logical operators `||`, `&&`, and `!`; accepts arguments of all types
  ```Elixir
  1 || true # 1
  nil && 13 # nil
  !1 # false
  ```
  - Equality
    - `==`, `!=`, `===`, `!==`, `<=`, `>=`, `<`, and `>`
  - Pipe Operator
    - `|>` passes the result of one function to the next function.
    ```Elixir
    ## the equivalent version of f(d(b(:atom))) using pipes is:
    b(:atom) |> d() |> f()
    ```
    - helps code stay clean and readable; used for cases where we want to transform a request type, or build up a data structure with different functions

## Enumerables
  - `Enum.map/2`
  ```Elixir
  Enum.map([1, 2, 3], fn(x) -> x * 2 end)   # [2, 4, 6]
  ```
  - `Enum.reduce/2`
  ```Elixir
  Enum.reduce([1, 2, 3, 4], fn(x, acc) -> x * acc end)    # 24
  Enum.reduce(["I", "Like", "Cheese"], "The truth is:", fn(x, sentence) -> sentence <> " " <> x end)    # "The truth is: I Like Cheese"
  ```
  - `Enum.all?`
  - `Enum.any?`
  - `Enum.chunk/2`
  ```Elixir
  Enum.chunk([1, 2, 3, 4], 2)   # [[1, 2], [3, 4]]
  ```
  - `Enum.max`
  - `Enum.sort`
  - `Enum.uniq/1`
  ```Elixir
  Enum.uniq([1, 1, 1, 2, 3])    # [1, 2, 3]
  ```

<!--
  ```Elixir
  ```
-->
