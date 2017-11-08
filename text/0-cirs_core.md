- Feature Name: cirs_core
- Start Date: 2017-11-7
- RFC PR: (leave this empty)
- Cirs Issue: (leave this empty)

# Summary

Provide an implementation of Rust `libcore` that suits to Cirs Project
needs.

# Motivation

Currently there is one implementation of `libcore`, which is Rust language's
default. However it is filled with unnecessary items that we currently don't
need, and perhaps never will have a use for.

# Guide-level explanation

We have a new `cirs_core` crate that provides our implementation of `libcore`.
`cirs_core` is a dependency of `cirs`. Any extra libraries that are used by
the Cirs Project also use `cirs_core` as a dependency.

# Reference-level explanation

## New Libraries
A new crate `cirs_core` is introduced. As discussed above, this crate is meant
to be a minimalistic implementation of `libcore`. Only functionality required
by the various libraries in the Cirs Project are implemented.

`cirs_core` is to be licensed under `MIT/Apache-2.0` license, same as
`libcore`.

Every Cirs Project library that depends on `cirs_core` has it as a feature
`cirs_core`, which is part of the `default` feature. Builds and tests are run
once with `cirs_core` implementation and once with 'libcore'.

## Language Items

There are 3 language items that compose of this RFC:

### `sized`
`panic_fmt` and `copy` lang items depend on lang item `sized`. This involves of
trait `::marker::Sized`:

```rust
// Module ::marker

#[lang = "sized"]
#[rustc_on_unimplemented = "`{Self}` does not have a constant size known at \
compile-time"]
#[fundamental]
pub trait Sized {}
```

### `copy`

`panic_fmt` lang item depends on lang item `copy`. This involves of traits
`::clone::Clone` and `::marker::Copy`:

```rust
// Module ::clone

pub trait Clone: ::marker::Sized {
  fn clone(&self) -> Self;

  #[inline]
  fn clone_from(&mut self, source: &Self) {
      *self = source.clone()
  }
}

// Module ::marker

#[lang = "copy"]
pub trait Copy : Clone {}
```

### `panic_fmt`

As any `no_std` requires lang item `panic_fmt`, a barebones `panic_fmt`
function is introduced to allow `cirs_core` to compile:

```rust
#[lang = "panic_fmt"]
extern fn panic_fmt() -> !;
```

It is expected that the signature and location of the function will change,
which is not part of the scope of this RFC.

## Requirements

We have two main requirements for `cirs_core`:

1. The public API of `cirs_core` has the same layout as `libcore` for
   compatibility.
2. `cirs_core` is implemented in such a way that it can easily be replaced with
   `libcore` and still work as expected. This depends on requirement 1.

# Drawbacks

There will a maintainance burden, with us having to make sure we are correct
when implementing `libcore` functionality.

# Rationale and alternatives

- Just use the Rust provided `libcore`. It already provides a solid base for
  cirs. This does allow us to focus on other parts of the project. We can
  perhaps provide `cirs_core` later.

# Unresolved questions

- How likely is it that we will have specific requirements in `cirs_core`?
- Is `cirs_core` really needed?
- Should there be any other requirements?
