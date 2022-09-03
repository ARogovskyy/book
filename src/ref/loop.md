Infinite Loop
=============

Infinite loops follow Rust syntax.

`continue` can be used to skip to the next iteration, by-passing all following statements;
`break` can be used to break out of the loop unconditionally.

```rust
let x = 10;

loop {
    x -= 1;

    if x > 5 { continue; }  // skip to the next iteration

    print(x);

    if x == 0 { break; }    // break out of loop
}
```

~~~admonish danger.small "Remember the `break` statement"

A `loop` statement without a `break` statement inside its loop block is infinite.
There is no way for the loop to stop iterating.
~~~