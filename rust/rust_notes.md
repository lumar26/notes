
# Rust Data Types

### Char

Rust stores characters as 4 Byte variable, which means that Unicode chars can be used

### Array

Declaring an array with uninitialized integers : `let integers: [i32, 10]` -> array of 10 ints

Initializing array with dummy values: `let integers: [12, 10]` -> all twelves

For indexing arrays in rust we use **usize** data type which is determined in compile time

### Tuple

It is also indexed as array starting with zero.

Accessing elements is done as follows: `tuple.0` for getting first element
Declaring tuple with given types: `let tuple: (u8, f32, char)`
Another common operation is destructuring tuples like following: `let (item1, item2, item3) = old_tuple_with_three_items`

### Functions

When we leave last line of the function as expression (without semicolon) that expression evaluates as return value

If function does not return anything explicitly, by default it return _unit_ type which can be interpreted as empty tuple `()` 

Return value of function is declared with `->` operator

### If

If statement allows only booleans as condition, there are no falsy or truthy values

Conditional assignment: `let x = if is_odd {1} else {2}`

### loop

We use `loop` for infinite loops which are manually stopped

Also, loop can return a value that we specify after **break** keyword: 

```rust
     let result = loop {
          ...
          if condition_is_true 
               break result;
     }

```
In basic while, break cannot return a value

### for _x_ in _collection_

For loop in Rust is used primarily for iterating through collections, and thus it uses Iterator pattern

**Watch out**
     In older vesions of rust it was necessary to call iterator explicitly: `for x in collection.iter()`

`for (index, x) in collection.iter().enumerate()` is convenient when we want for loop to return tuple that contains both index and value

Iterating a range of int values: `for i in 0..10` : iterating 0 through 9 (last excluded)

### Shadowing

This is process of redeclarting a variable with a same name. if we try to access that variable in a scope where shadowing was done then we can only access newly declared variable (which can be if deifferent data type than initial one).

Shadowing lasts onl within scope where new variable was declared / initialized:
```rust
let variable = "Some string";
{
     let variable  = 13;
     println!("var is {}", variable)
}
println!("var is {}", variable)
```
-> 13
-> Some string

**Watch out**
     If mutable variable is shadowed immutably (i.e. 
```rust
let mut s = String::from("asdf); 
{
     let s = s; // this new s in this scope is not mutable. Mutability is not "inherited"
}
```
) then new variable is not mutable by default as it was previous.


## Stack and Heap

Data stored on stack must have size know in compile time
**Pointer**: Data type that stores memory address

Strings are stored on heap (not string literal but String   _type_)
`let str = String::from("str");"`
String package in Rust: std::string::String

# Ownership

In all programming languages memory management is important problem, and can be solved in 3 ways. First is way of C and C++ and that is that programmer is responsible for allocation and deallocation of memory on heap. In Java, Python, Ruby, GoLang there is Garbage collector that takes care of all allocation and deallocation of memory chunks on heap so that programmer does not have to pay attention on memory menagement.

Rust uses third aproach and that is called **ownership**. Every value on heap is owned by one and only one variable at a time. When that variable goes out of scope, that value is dropped from heap.

The point is that Rust compiler can determine in compile time which value can be deallocated and when.

After one variable goes out of scope (at closed curly brace or some other way of dropping out of scope) Rust internaly calls `.drop()` function on that clears variable on heap

Key concepts:

     **Moving ownership**
```rust
let var1 = "Var";
let var2: String;
var2 = var1;
print!("var1 is {}", var1); // ----> compile error
```
In example above we see moving ownership. Since value (in this case _Var_) can have only one owner, after it is assigned to var2 var1 loses ownership and therefore is considered gone out of scope. We cannot access that variable after its ownership had been moved.

Moving is variant of _shallow copy_ where previous owner of 'reference' to a value gets out of scope afterwards.

**Rust will never make deep copy of value unless we explicitly demand it**

**Cloning**

If we wanted to explicitly make a new copy of value _Var_ then we should use `.clone()` method when assigning to new variable. By doing so we will have new string on heap with same value

**Copying**
Bitwise copying of value. For data types annotated with `Copy`. All primitive values such as integers, booleans and **tuples containing only copiable types**

We use method `.clear()` on data types held on heap when we want to clear the value and free that space on heap

**Watch out**
     All of forementioned does not apply to data types of known size because they are held on stack. On stack there is no cloning or moving, instead it is all copying values  and there is no ownership.

**Watch out**
     When passing "heap variables" as parameter to a function there is also moving of ownership, so if we try to access variable that we passed as parameter to a functiona after a function is invoked, we will get compilation error because that variable is now out of scope.
There are two *simple* ways of solving this:
1. pass cloned value as parameter -> `fn(var.clone())`
2. shadow variable passed as parameter by returning value from a function

Since it is too compilcated Rust intorduces another way of solving this:

## References and borrowing

When we want to pass value of some variable to a function without changing its owner we use **references** that can be thaught of as pointers to memory location of that value.

We make a refference with **&** operator. Variable that holds reference to value on heap is specific because after it goes out of scope value it was pointing to *is not dropped*.

If we want reference variable to be mutable i.e. value can be changed, then we define that reference variable as mutable `let &mut mut_ref: String`. Only precondition is that owner variable must also be mutable

**Watch out**
      you cannot have a mutable reference to a value while there are other references to the same value.

It is possible to have only one _mutable_ reference to one variable at a time. Multiple mutable referencing is not allowed, or, more accurately, not possible because previous reference vanishes after new on is made (i.e. previous reference goes out of scope - is not used anymore).


### Slices

Slices are special reference types that have pointer to specific part of collection (any value stored as indexed collection, such as array, string...)
`let substring = &string[10..]` creates slice called substring form 10th haracter to the end of the string
Length of slices is calculated in bytes, not in characters. Keep this in mind since most of commonly used characters are 1B long in UTF8 encoding

Slice variable has pointer to beginning of "slice" and length of a slice

Slice points directly to the heap, to specific part of value. This is allowed since *slice variable is never going to have ownership over variable on heap*

We can use string slice (&str) in place of string reference (&String) but not vice versa.

**&str is an immutable reference.**

# Structs

Like advanced tuples. Like Object in oop but just with the fields.
They have named fields.

Structs allow shorthand init like in javascript. If field name is same as variable to be assigned to field, then we can omit field name: 
```rust
let email = "luka@gmail.com";
let username = String:from("lukica");
User {
        email,
        username,
        active: true,
        sign_in_count: 1,
    }
```

Another convinience is when we want to create a new struct that has common fields with existing one. We use `..` notation:
```rust
  let user2 = User {
        email: String::from("another@example.com"),
        ..user1 // this means that other fields except email will be the same as in user1
    };
```

Note that the struct update syntax uses `=` like an assignment; this is because it **moves** the data. That means that  al the fields we used from existing struct are no longer owned by that struct. That applies to whole struct, not just borrowed fields. In esence, `..struct` means that `struct` is no longer valid, and it is moved.
     ^
     |
__not entirely true__, this is only the when we use update syntax for filling in heap values, but if all heap values are manually defined and we update only stack variables (e.g. primitives) then there is no moving and first structure is still valid.


For using references in structs we need knowledge of lifetimes.

______

If we want to print structs that do not implement Display trait, we can use in `println!()` macro a specifier: `{:#?}` that prints struct in readable manner
______

`dbg!` macro is useful when we want to print to stdout something, in debug mode. `dbg!` prints passed value in pretty format and returns ownership of value of passed expression.

     `#[derive(Debug)]` specifies that struct (or sth) other implements Debug trait which enables dbg printing

### Methods 

Mathods are functions defined in context of some struct/enum/trait. First parameter of method is always `&self` which indicates that object (trait/enum/struct).

Methods can take ownership of self (`self`), borrow self immutably as we’ve done here (`&self`), or borrow self mutably (`&mut self`), just as they can any other parameter.

____________________________________________________________________________________________________________________________________________

__-> operator__
In C and C++, two different operators are used for calling methods: you use `.` if you’re calling a method on the object directly and `->` if you’re calling the method on a pointer to the object and need to dereference the pointer first. In other words, if object is a pointer, `object->something()` is similar to `(*object).something()`.

Rust doesn’t have an equivalent to the `->` operator; instead, Rust has a feature called automatic referencing and dereferencing.  
Here’s how it works: when you call a method with `object.something()`, Rust automatically adds in `&`, `&mut`, or `*` so object matches the signature of the method. In other words, the following are the same:

```rust
p1.distance(&p2);
(&p1).distance(&p2);
```
____________________________________________________________________________________________________________________________________________

In Rust we have __associated functions__ that are not methods and are defined on some type, e.g. `String::from()`. Those functions do not have `&self` as parameter and are invoked with `::` notation.

# Enums

Enum is another convinient mechanism in Rust. In following example we see one definition of RUst enum. Enum si a type that declares set of possible manifestations or shapes in which value of that enum type can be defined. Comparing to enums in other languages that rarely contain value for each variant, Rust enums can contain value of any type as well as different types across variants.

```
enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}
```

We can also define methods on enums as with the structs, using `impl` block

Option<> is built in enum that handles problem of a null value. It makes programmer to make sure some value is not null.

_you have to convert an Option<T> to a T before you can perform T operations with it. Generally, this helps catch one of the most common issues with null: assuming that something isn’t null when it actually is._

_In order to have a value that can possibly be null, you must explicitly opt in by making the type of that value Option<T>. Then, when you use that value, you are required to explicitly handle the case when the value is null._

## Matching pattern

Matching pattern control flow enables us to determine the value or variant (enums) of value passed to this construct and conduct an action according to matched pattern. 

```rust
     match k {
            Kin::Parent(Parent::Father(name)) => println!("This is my parent: {:?}", name), // its possible to match patterns different specificity
            Kin::Parent(parent_type) => println!("This is my parent: {:?}", parent_type),
            Kin::Cousin { name, distance } => println!("This is my cousin: {:?} and is away {}", name, distance),
            _ => println!("Default")
        }
```
It is important that __scrutinee__ expression is of same type as pattern. First pattern that meets condition of equality is evaluated.
Match can return a value if expression after pattern returns a value.

Another standard usage of pattern match is when we want to extract `T` value from `Option<T>`. Idea is that if value is `None` then we do nothing or return None, but when value is Some(T) then we can extract that `T` and further use it.

```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
        match x {
            None => None,
            Some(i) => Some(i + 1),
        }
    }

```

For default case, or case that we did not cover, we have two options for handling that case:  
1. We can collect value with `other` pattern and do with it what we neet to do: 
```rust
match dice_roll {
        3 => add_fancy_hat(),
        7 => remove_fancy_hat(),
        other => move_player(other),
    }
```
2. Or if we do not need that value we can use `_` pattern that matches all other cases as well, but the value is not kept in any variable. Additionally, if we want _nothing_ to happent after `_` pattern is matched then we can simply evaluate __unit value__ (empty tuple `()`).

### if let

`if let` construct is a shorthand for `match` if we only want to check one pattern. Body of `if let` will execute if pattern matches expression.

```
let config_max = Some(15);
if let Some(max) = config_max {
        println!("The maximum is configured to be {}", max);
    } 
```

```
if let pattern = expression {
     // execute sth
    }
```

# Packages and Crates

Crate is atomic unit of code that compiler is aware of in some point in time.  
There are two types of crates:
1. Binary crate that contains executable rust program. Binary crate consists of code that has entry point i.e. `fn main() {...}`
2. Library crate is library of code that is not compiled to executable but is intended to be used by other crates.

__Package__ encaptulates multiple crates that represent some set of similar functionalities

All starts with package. Package is created, for example, when we create new Cargo project - result is package with Cargo.toml and src/ inside it. Seems like package is synonym for a project...

_A package can contain as many binary crates as you like, but at most only one library crate._ This is curious...?

#### Modules

Modules are contained inside crates. We need modules to:

- define visibility of some part of code
- encapsulate certain parts of code
- to organize code in file system style

Everything inside crate, including modules, is ***private by default***. This means that child module is not accessible outside parent module. On the other hand child module can access everything from parent module. 

Every crate by default has so called `crate` module in it. This module is not declared anyhow but it exists. Imagine that content of crate (declared modules, functions, structs) is wrapped around by this `crate` module.

Even though struct is declared *public*, fields of that struct are by default *private*. On the contrary Enum options are public by default.

`use` keyword is used to import some module or other type from other module. By convention if we import functions then we import parent module of that function and then reference it manually, like this: `other_module::function()` instead of importing whole path and then

Submodules are referred to with `::` from parent module. 

