Strict Variables Mode
=====================

{{#include ../links.md}}

~~~admonish tip.side "`Scope` constants"

[Constants] in the external [`Scope`], when provided, count as definition.
~~~

By default, Rhai looks up access to [variables] from the enclosing block scope,
working its way outwards until it reaches the top (global) level, then it
searches the [`Scope`] (if any) that is passed into the `Engine::eval_with_scope` call.

Setting [`Engine::set_strict_variables`][options] to `true` turns on _Strict Variables Mode_,
which requires that:

* all [variables]/[constants] be defined within the same script before use,
  or they must be [variables]/[constants] within the provided [`Scope`] (if any),
* [modules] must be [imported][`import`], also within the same script, before use.

Within _Strict Variables_ mode, any attempt to access a [variable] or [module] before
definition/[import][`import`] results in a parse error.

This way, variable access errors (usually typos) are caught during compile time instead of runtime.

```rust
let x = 42;

let y = x * z;          // <- parse error under strict variables mode:
                        //    variable 'z' is not yet defined

let z = x + w;          // <- parse error under strict variables mode:
                        //    variable 'w' is undefined

foo::bar::baz();        // <- parse error under strict variables mode:
                        //    module 'foo' is not yet defined

import "my_module" as foo;

foo::bar::baz();        // ok!

print(foo::xyz);        // ok!

let x = abc::def;       // <- parse error under strict variables mode:
                        //    module 'abc' is undefined
```