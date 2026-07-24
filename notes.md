> [!NOTE]
> I forgot the systax for rust vectors

> [!TIP]
> use chatgpt to learn systax

```ruut
warning: unused variable: `element`
 --> exercises/05_vecs/vecs2.rs:4:9
  |
4 |     for element in input {
  |         ^^^^^^^ help: if this is intentional, prefix it with an underscore: `_element`
  |
  = note: `#[warn(unused_variables)]` (part of `#[warn(unused)]`) on by default


running 3 tests
test tests::test_vec_loop ... FAILED
test tests::test_vec_map ... ok
test tests::test_vec_map_example ... ok

failures:

---- tests::test_vec_loop stdout ----

thread 'tests::test_vec_loop' (17030) panicked at exercises/05_vecs/vecs2.rs:49:9:
assertion `left == right` failed
  left: [2, 4, 6, 2, 4, 6, 2, 4, 6, 2, 4, 6, 2, 4, 6]
 right: [4, 8, 12, 16, 20]
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace


failures:
    tests::test_vec_loop

test result: FAILED. 2 passed; 1 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s

error: test failed, to rerun pass `--bin vecs2`

Output


Hint
In the first function, we create an empty vector and want to push new elements
to it.

In the second function, we map the values of the input and collect them into
a vector.

After you've completed both functions, decide for yourself which approach you
like better.

What do you think is the more commonly used pattern under Rust developers?

Progress: [#######################################>------------------------------------------------------------------------------------------------------------------]  24/94
Current exercise: exercises/05_vecs/vecs2.rs

l:list / c:check all / x:reset / q:quit ?

We hope you're enjoying learning Rust!
If you want to continue working on the exercises at a later point, you can simply run `rustlings` again in this directory.
[cypher@overlord rustlings]$

```

2026-01-05T22:22:43
> [!NOTE]
> I am not using the right syntax, I need to use camel case

> [!TIP]
> setup a good lsp, the AI is dumb

> [!NOTE]
> the AI gave bad example code, may not be as usual unless I understand the syntax

> [!NOTE]
> 15:02
> needs to be mutable  

# exercise/06/move_semantics3

```bash
error[E0596]: cannot borrow `vec` as mutable, as it is not declared as mutable
 --> exercises/06_move_semantics/move_semantics3.rs:3:5
  |
3 |     vec.push(88);
  |     ^^^ cannot borrow as mutable
  |
help: consider changing this to be mutable
  |
2 | fn fill_vec(mut vec: Vec<i32>) -> Vec<i32> {
  |             +++

For more information about this error, try `rustc --explain E0596`.
error: could not compile `exercises` (bin "move_semantics3") due to 1 previous error


Progress: [############################################>-------------------------------------------------------------------------------------------------------------]  27/94
Current exercise: exercises/06_move_semantics/move_semantics3.rs

h:hint / l:list / c:check all / x:reset / q:quit ?

```

> [!TIP]
> I nedd to make the vectotr mutable

> [!NOTE]
> Hint
The difference between this one and the previous ones is that the first line
of `fn fill_vec` that had `let mut vec = vec;` is no longer there. You can,
instead of adding that line back, add `mut` in one place that will change
an existing binding to be a mutable binding instead of an immutable one :)

> [!NOTE]
> I am getting this error

```bash
error[E0308]: mismatched types
  --> exercises/06_move_semantics/move_semantics5.rs:13:12
   |
12 | fn string_uppercase(mut data: &String) {
   |                               ------- expected due to this parameter type
13 |     data = data.to_uppercase();
   |            ^^^^^^^^^^^^^^^^^^^ expected `&String`, found `String`
   |
help: you might have meant to mutate the pointed at value being passed in, instead of changing the reference in the local binding
   |
12 ~ fn string_uppercase(data: &mut String) {
13 ~     *data = data.to_uppercase();
   |

error[E0382]: borrow of moved value: `data`
  --> exercises/06_move_semantics/move_semantics5.rs:23:22
   |
19 |     let data = "Rust is great!".to_string();
   |         ---- move occurs because `data` has type `String`, which does not implement the `Copy` trait
20 |
21 |     get_char(data);
   |              ---- value moved here
22 |
23 |     string_uppercase(&data);
   |                      ^^^^^ value borrowed here after move
   |
note: consider changing this parameter type in function `get_char` to borrow instead if owning the value isn't necessary
  --> exercises/06_move_semantics/move_semantics5.rs:7:19
   |
 7 | fn get_char(data: String) -> char {
   |    --------       ^^^^^^ this parameter takes ownership of the value
   |    |
   |    in this function
help: consider cloning the value if the performance cost is acceptable
   |
21 |     get_char(data.clone());
   |                  ++++++++

Some errors have detailed explanations: E0308, E0382.
For more information about an error, try `rustc --explain E0308`.
error: could not compile `exercises` (bin "move_semantics5") due to 2 previous errors
```

> I need do a stack trace

Expected type did not match the received type.

Erroneous code examples:

```
fn plus_one(x: i32) -> i32 {
    x + 1
}

plus_one("Not a number");
//       ^^^^^^^^^^^^^^ expected `i32`, found `&str`

if "Not a bool" {
// ^^^^^^^^^^^^ expected `bool`, found `&str`
}

let x: f32 = "Not a float";
//     ---   ^^^^^^^^^^^^^ expected `f32`, found `&str`
//     |
//     expected due to this
```

This error occurs when an expression was used in a place where the compiler
expected an expression of a different type. It can occur in several cases, the
most common being when calling a function and passing an argument which has a
different type than the matching type in the function declaration.

> [!NOTE]
>I am going to add the clone and string types

I am getting this error

```bash
error[E0614]: type `char` cannot be dereferenced
 --> exercises/06_move_semantics/move_semantics5.rs:8:5
  |
8 |     *data.chars().last().unwrap();
  |     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ can't be dereferenced

error[E0308]: mismatched types
 --> exercises/06_move_semantics/move_semantics5.rs:7:35
  |
7 | fn get_char(mut data: &String) -> char {
  |    --------                       ^^^^ expected `char`, found `()`
  |    |
  |    implicitly returns `()` as its body has no tail or `return` expression

error[E0308]: mismatched types
  --> exercises/06_move_semantics/move_semantics5.rs:13:12
   |
12 | fn string_uppercase(mut data: &String) {
   |                               ------- expected due to this parameter type
13 |     data = data.to_uppercase();
   |            ^^^^^^^^^^^^^^^^^^^ expected `&String`, found `String`
   |
help: you might have meant to mutate the pointed at value being passed in, instead of changing the reference in the local binding
   |
12 ~ fn string_uppercase(data: &mut String) {
13 ~     *data = data.to_uppercase();
   |

error[E0308]: mismatched types
  --> exercises/06_move_semantics/move_semantics5.rs:21:14
   |
21 |     get_char(data.clone());
   |     -------- ^^^^^^^^^^^^ expected `&String`, found `String`
   |     |
   |     arguments to this function are incorrect
   |
note: function defined here
  --> exercises/06_move_semantics/move_semantics5.rs:7:4
   |
 7 | fn get_char(mut data: &String) -> char {
   |    ^^^^^^^^ -----------------
help: consider borrowing here
   |
21 |     get_char(&data.clone());
   |              +

Some errors have detailed explanations: E0308, E0614.
For more information about an error, try `rustc --explain E0308`.
error: could not compile `exercises` (bin "move_semantics5") due to 4 previous errors


Progress: [###############################################>----------------------------------------------------------------------------------------------------------]  29/94
Current exercise: exercises/06_move_semantics/move_semantics5.rs

h:hint / l:list / c:check all / x:reset / q:quit ?

We hope you're enjoying learning Rust!
If you want to continue working on the exercises at a later point, you can simply run `rustlings` again in this directory.
[cypher@overlord rustlings]$

```

After I made these changes

```typescript
#![allow(clippy::ptr_arg)]

// TODO: Fix the compiler errors without changing anything except adding or
// removing references (the character `&`).

// Shouldn't take ownership
fn get_char(mut data: &String) -> char {
    *data.chars().last().unwrap();
}

// Should take ownership
fn string_uppercase(mut data: &String) {
    data = data.to_uppercase();

    println!("{data}");
}

fn main() {
    let data = "Rust is great!".to_string();

    get_char(data.clone());

    string_uppercase(&data);
} 
```

I added mut and '&' to the inputs of get_char function

> [!NOTE]
> I need to learn stucts impl stuff

```bash
error[E0600]: cannot apply unary operator `!` to type `()`
  --> exercises/07_structs/structs3.rs:62:9
   |
62 |         assert!(package.is_international());
   |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ cannot apply unary operator `!`

error[E0600]: cannot apply unary operator `!` to type `()`
  --> exercises/07_structs/structs3.rs:72:17G
   |
72 |         assert!(!package.is_international());
   |                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^ cannot apply unary operator `!`

error[E0308]: mismatched types
  --> exercises/07_structs/structs3.rs:84:54
   |
84 |         assert_eq!(package.get_fees(cents_per_gram), 4500);
   |                                                      ^^^^ expected `()`, found integer

error[E0308]: mismatched types
  --> exercises/07_structs/structs3.rs:85:58
   |
85 |         assert_eq!(package.get_fees(cents_per_gram * 2), 9000);
   |                                                          ^^^^ expected `()`, found integer

warning: unused variable: `cents_per_gram`
  --> exercises/07_structs/structs3.rs:33:24
   |
33 |     fn get_fees(&self, cents_per_gram: u32) {
   |                        ^^^^^^^^^^^^^^ help: if this is intentional, prefix it with an underscore: `_cents_per_gram`
   |
   = note: `#[warn(unused_variables)]` (part of `#[warn(unused)]`) on by default

Some errors have detailed explanations: E0308, E0600.
For more information about an error, try `rustc --explain E0308`.
error: could not compile `exercises` (bin "structs3" test) due to 4 previous errors; 1 warning emitted

Output


Progress: [####################################################>-----------------------------------------------------------------------------------------------------]  32/94
Current exercise: exercises/07_structs/structs3.rs

h:hint / l:list / c:check all / x:reset / q:quit ?

```

Expected type did not match the received type.

Erroneous code examples:

```
fn plus_one(x: i32) -> i32 {
    x + 1
}

plus_one("Not a number");
//       ^^^^^^^^^^^^^^ expected `i32`, found `&str`

if "Not a bool" {
// ^^^^^^^^^^^^ expected `bool`, found `&str`
}

let x: f32 = "Not a float";
//     ---   ^^^^^^^^^^^^^ expected `f32`, found `&str`
//     |
//     expected due to this
```

This error occurs when an expression was used in a place where the compiler
expected an expression of a different type. It can occur in several cases, the
most common being when calling a function and passing an argument which has a
different type than the matching type in the function declaration.

> [!NOTE]
> I am not passing the right parmito, I need to learn the impl system

```bash
error[E0600]: cannot apply unary operator `!` to type `()`
  --> exercises/07_structs/structs3.rs:62:9
   |
62 |         assert!(package.is_international());
   |         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^ cannot apply unary operator `!`

error[E0600]: cannot apply unary operator `!` to type `()`
  --> exercises/07_structs/structs3.rs:72:17
   |
72 |         assert!(!package.is_international());
   |                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^ cannot apply unary operator `!`

error[E0308]: mismatched types
  --> exercises/07_structs/structs3.rs:84:54
   |
84 |         assert_eq!(package.get_fees(cents_per_gram), 4500);
   |                                                      ^^^^ expected `()`, found integer

error[E0308]: mismatched types
  --> exercises/07_structs/structs3.rs:85:58
   |
85 |         assert_eq!(package.get_fees(cents_per_gram * 2), 9000);
   |                                                          ^^^^ expected `()`, found integer

warning: unused variable: `cents_per_gram`
  --> exercises/07_structs/structs3.rs:33:24
   |
33 |     fn get_fees(&self, cents_per_gram: u32) {
   |                        ^^^^^^^^^^^^^^ help: if this is intentional, prefix it with an underscore: `_cents_per_gram`
   |
   = note: `#[warn(unused_variables)]` (part of `#[warn(unused)]`) on by default

Some errors have detailed explanations: E0308, E0600.
For more information about an error, try `rustc --explain E0308`.
error: could not compile `exercises` (bin "structs3" test) due to 4 previous errors; 1 warning emitted

Output


Progress: [#################################################################>-------------------------------------------------------------------------------------------------------------------------------]  32/94
Current exercise: exercises/07_structs/structs3.rs

h:hint / l:list / c:check all / x:reset / q:quit ?

We hope you're enjoying learning Rust!
If you want to continue working on the exercises at a later point, you can simply run `rustlings` again in this directory.
[cypher@overlord rustlings]$
```

```bash
error[E0433]: failed to resolve: use of undeclared type `SystemTime`
 --> exercises/10_modules/modules3.rs:9:11
  |
9 |     match SystemTime::now().duration_since(UNIX_EPOCH) {
  |           ^^^^^^^^^^ use of undeclared type `SystemTime`
  |
help: consider importing this struct
  |
8 + use std::time::SystemTime;
  |

error[E0425]: cannot find value `UNIX_EPOCH` in this scope
 --> exercises/10_modules/modules3.rs:9:44
  |
9 |     match SystemTime::now().duration_since(UNIX_EPOCH) {
  |                                            ^^^^^^^^^^ not found in this scope
  |
help: consider importing this constant
  |
8 + use std::time::UNIX_EPOCH;
  |

error[E0282]: type annotations needed
  --> exercises/10_modules/modules3.rs:10:74
   |
10 |         Ok(n) => println!("1970-01-01 00:00:00 UTC was {} seconds ago!", n.as_secs()),
   |                                                                          ^ cannot infer type

Some errors have detailed explanations: E0282, E0425, E0433.
For more information about an error, try `rustc --explain E0282`.
error: could not compile `exercises` (bin "modules3") due to 3 previous errors

```

```bash
error[E0425]: cannot find value `basket` in this scope
  --> exercises/11_hashmaps/hashmaps1.rs:14:5
   |
14 |     basket.insert(String::from("banana"), 2);
   |     ^^^^^^ not found in this scope

error[E0425]: cannot find value `basket` in this scope
  --> exercises/11_hashmaps/hashmaps1.rs:18:5
   |
18 |     basket
   |     ^^^^^^ not found in this scope

For more information about this error, try `rustc --explain E0425`.
error: could not compile `exercises` (bin "hashmaps1") due to 2 previous errors


Progress: [########################################################################################>--------------------------------------------------------------------------------------------------------]  43/94
Current exercise: exercises/11_hashmaps/hashmaps1.rs

h:hint / l:list / c:check all / x:reset / q:quit ?

We hope you're enjoying learning Rust!
If you want to continue working on the exercises at a later point, you can simply run `rustlings` again in this directory.
[cypher@overlord rustlings]$
```

```bash
running 2 tests
test tests::at_least_five_fruits ... FAILED
test tests::at_least_three_types_of_fruits ... FAILED

failures:

---- tests::at_least_five_fruits stdout ----

thread 'tests::at_least_five_fruits' (64927) panicked at exercises/11_hashmaps/hashmaps1.rs:39:9:
assertion failed: basket.values().sum::<u32>() >= 5
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace

---- tests::at_least_three_types_of_fruits stdout ----

thread 'tests::at_least_three_types_of_fruits' (64928) panicked at exercises/11_hashmaps/hashmaps1.rs:33:9:
assertion failed: basket.len() >= 3


failures:
    tests::at_least_five_fruits
    tests::at_least_three_types_of_fruits

test result: FAILED. 0 passed; 2 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s

error: test failed, to rerun pass `--bin hashmaps1`

Output


Progress: [########################################################################################>--------------------------------------------------------------------------------------------------------]  43/94
Current exercise: exercises/11_hashmaps/hashmaps1.rs

h:hint / l:list / c:check all / x:reset / q:quit ?

```

to create a hashmap I instance its like this

```rust
let mut basket = HashMap::new();
```

to append to a hashmap I insert like this

```rust

basket.insert(String::from("apple"), 2);
```

> [!NOTE]
> in functions you can just have the contents of the {} block without the ; and it will return
