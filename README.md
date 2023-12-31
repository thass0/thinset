<div align="center">
  <h1>thinset</h1>
  <p>
    <strong>A set implementation for sparse sets of unsigned integers.</strong>
  </p>
  <p>

[![crates.io][crates.io shield]][crates.io link]
[![Documentation][docs.rs badge]][docs.rs link]
![Rust CI][github ci badge]
[![rustc 1.0+]][Rust 1.0]
<br />
<br />
[![Dependency Status][deps.rs status]][deps.rs link]
[![Download Status][shields.io download count]][crates.io link]

  </p>
</div>

[crates.io shield]: https://img.shields.io/crates/v/thinset?label=latest
[crates.io link]: https://crates.io/crates/thinset
[docs.rs badge]: https://docs.rs/thinset/badge.svg?version=0.1.0
[docs.rs link]: https://docs.rs/thinset/0.1.0/thinset/
[github ci badge]: https://github.com/contain-rs/linked-hash-map/workflows/Rust/badge.svg?branch=master
[rustc 1.0+]: https://img.shields.io/badge/rustc-1.0%2B-blue.svg
[Rust 1.0]: https://blog.rust-lang.org/2015/05/15/Rust-1.0.html
[deps.rs status]: https://deps.rs/crate/thinset/0.1.0/status.svg
[deps.rs link]: https://deps.rs/crate/thinset/0.1.0
[shields.io download count]: https://img.shields.io/crates/d/thinset.svg

## Usage

Add this to your Cargo.toml:

```toml
[dependencies]
thinset = "0.1"
```

<!-- cargo-rdme start -->

An implementation of a set using a sparse and dense array as an underlying
representation for holding unsigned numbers.

This type of set is useful when you need to efficiently track set membership for items
from a large universe, but the number of items in the sets is comparatively smaller.

The sparse set supports constant-time insertion, removal, lookups.
Compared to the standard library's `HashSet`, clearing the set is constant-time instead of
linear time.
Compared to bitmap-based sets like the `bit-set` crate, iteration over the set is
proportional to the cardinality of the set (how many elements you have) instead of proportional
to the maximum size of the set.
The only downside is that the set requires more memory than other set implementations.

The implementation is based on the paper "An efficient representation for sparse sets" (1993)
by Briggs and Torczon.

### Examples

```rust
use thinset::SparseSet;

// Specify a maximum value for the set
let mut s: SparseSet<usize> = SparseSet::new(100);
s.insert(0);
s.insert(3);
s.insert(7);

s.remove(7);

if !s.contains(7) {
    println!("There is no 7");
}

// Print 0, 1, 3 in some order
for x in s.iter() {
    println!("{}", x);
}
```

<!-- cargo-rdme end -->

## License

Dual-licensed for compatibility with the Rust project.

Licensed under the Apache License Version 2.0: http://www.apache.org/licenses/LICENSE-2.0,
or the MIT license: http://opensource.org/licenses/MIT, at your option.