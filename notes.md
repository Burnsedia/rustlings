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
