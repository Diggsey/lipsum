# Lorem Ipsum

[![](https://img.shields.io/crates/v/lipsum.svg)][crates-io]
[![](https://docs.rs/lipsum/badge.svg)][api-docs]
[![](https://img.shields.io/badge/rustc-1.31.0-blue.svg)][rust-2018]
[![](https://travis-ci.org/mgeisler/lipsum.svg?branch=master)][travis-ci]
[![](https://ci.appveyor.com/api/projects/status/github/mgeisler/lipsum?branch=master&svg=true)][appveyor]
[![](https://codecov.io/gh/mgeisler/lipsum/branch/master/graph/badge.svg)][codecov]

Lipsum is a small Rust library for generating pseudo-Latin [lorem
ipsum filler text][lorem ipsum]. This is a standard placeholder text
used in publishing. It starts with:

> Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
> eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim
> ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut
> aliquip ex ea commodo consequat…

The text is generated using a [Markov chain] that has been trained on
the first book in Cicero's work *De finibus bonorum et malorum* (*On
the ends of good and evil*), of which the lorem ipsum text is a
scrambled subset.

## Usage

Add this to your `Cargo.toml`:
```toml
[dependencies]
lipsum = "0.6"
```

## Documentation

Please see the **[API documentation][api-docs]**.


## Getting Started

Use the `lipsum` function to generate lorem ipsum text:
```rust
use lipsum::lipsum;

fn main() {
    // Print 25 random words of lorem ipsum text.
    println!("{}", lipsum(25));
}
```

This generates the lorem ipsum text show above:

> Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do
> eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim
> ad minim veniam, quis nostrud exercitation ullamco…

The text becomes random after 18 words, so you might not see exactly
the same text.

Use `lipsum_title` instead if you just need a short text suitable for
a document title or a section heading. The text generated by that
function looks like this:

> Refugiendi et Omnino Rerum

Small words are kept uncapitalized and punctuation is stripped from
all words.


## Release History

This is a changelog with the most important changes in each release.

### Unreleased

We now require the [Rust 2018 edition][rust-2018]. Over the years,
we’ve repeatedly seen build failures in our CI, even when nothing
changed in `lipsum`. The failures happened because we tested against a
fixed version of Rust, but our dependencies kept releasing new patch
it has versions that would push up the minimum required Rust version.

The build failures makes it infeasible to keep `lipsum` compatible
with any particular version of Rust. We will therefore track the
latest stable version of Rust from now on.

### Version 0.6.0 — December 9th, 2018

The new `lipsum_words` function can be used to generate random lorem
ipsum text that doesn't always start with "Lorem ipsum".

Dependencies were updated and the oldest supported version of Rust is
now 1.22.

### Version 0.5.0 — April 22nd, 2018

The new `lipsum_title` function can be used to generate a short string
suitable for a document title or a section heading.

Dependencies were updated and the oldest supported version of Rust is
now 1.17.

### Version 0.4.0 — September 24th, 2017

The `generate` and `generate_from` now always generate proper
sentences, meaning that they generate sentences that start with a
capital letter and end with `.` or some other punctuation character.
Use `iter` and `iter_from` directly if you need more control.

### Version 0.3.0 — July 28th, 2017

Performance is improved by about 50% when generating text, but
training the Markov chain now takes about twice as long as before.

The `MarkovChain` struct has many new methods:

* `new_with_rng` makes it possible to specify the random number
  generator used by the Markov chain. Use this to get deterministic
  and thus reproducible output for tests. `MarkovChain` now owns the
  RNG it uses and as a consequence, it has an extra type parameter.
  This is a breaking change if you used struct directly in your code.

* `iter` and `into_from` return iterators over words in the Markov
  chain. The `generate` and `generate_from` methods are now
  straight-forward convenience wrappers for the iterators.

* `len` tells you the number of stats in the Markov chain and
  `is_empty` tells you if the Markov chain is empty, meaning that it
  hasn't been trained on anything yet.

### Version 0.2.0 — July 10th, 2017

Rust version 1.6.0 is now supported. This is checked with TravisCI.

### Version 0.1.0 — July 2nd, 2017

First public release.


## License

Lipsum can be distributed according to the [MIT license][mit].
Contributions will be accepted under the same license.


[crates-io]: https://crates.io/crates/lipsum
[api-docs]: https://docs.rs/lipsum/
[codecov]: https://codecov.io/gh/mgeisler/lipsum
[lorem ipsum]: https://en.wikipedia.org/wiki/Lorem_ipsum
[Markov chain]: https://en.wikipedia.org/wiki/Markov_chain
[travis-ci]: https://travis-ci.org/mgeisler/lipsum
[appveyor]: https://ci.appveyor.com/project/mgeisler/lipsum
[rust-2018]: https://doc.rust-lang.org/edition-guide/rust-2018/
[mit]: LICENSE
