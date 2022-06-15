# Rust Arg Parsing Benchmarks

This repo tries to assess Rust arg parsing performance.

We currently compare:

Name                                                 | Style                 | Notes
-----------------------------------------------------|-----------------------|------
No-op                                                | N/A                   | N/A
[argh](https://github.com/google/argh)               | `derive`              |
[bpaf](https://github.com/pacak/bpaf)                | Combinator            |
[clap_lex](https://github.com/clap-rs/clap)          | Imperative            | No help generation
[clap](https://github.com/clap-rs/clap)              | Builder or `derive`   | Color, suggested fixes, completions
[gumdrop](https://github.com/murarth/gumdrop)        | `derive`              |
[lexopt](https://github.com/blyxxyz/lexopt)          | Imperative            | No help generation
[pico-args](https://github.com/razrfalcon/pico-args) | Imperative            | No help generation
[xflags](https://github.com/matklad/xflags)          | proc-macro            |

*Note: any non-performanve comparison is meant to provide context for what you
gain/lose with each crate's overhead.  For a full comparison, see each parser
docs*

# Results

Name | Overhead (release) | Build (debug) | Parse (release) | Invalid UTF-8 | Downloads | Version
-----|--------------------|---------------|-----------------|---------------|-----------|--------
null | 0 KiB | 670ms | 2ms | Y | - | -
argh | 41 KiB | 5s | 3ms | N | ![Download count](https://img.shields.io/crates/dr/argh) | v0.1.7
bpaf | 162 KiB | 1s | 3ms | Y | ![Download count](https://img.shields.io/crates/dr/bpaf) | v0.3.2
clap | 572 KiB | 6s | 2ms | Y | ![Download count](https://img.shields.io/crates/dr/clap) | v3.1.9
clap-minimal | 537 KiB | 5s | 3ms | Y | ![Download count](https://img.shields.io/crates/dr/clap) | v3.1.9
clap_derive | 577 KiB | 12s | 2ms | Y | ![Download count](https://img.shields.io/crates/dr/clap) | v3.1.9
clap_lex | 39 KiB | 1s | 2ms | Y | ![Download count](https://img.shields.io/crates/dr/clap_lex) | v0.1.1
gumdrop | 36 KiB | 5s | 2ms | N | ![Download count](https://img.shields.io/crates/dr/gumdrop) | v0.8.1
lexopt | 39 KiB | 898ms | 2ms | Y | ![Download count](https://img.shields.io/crates/dr/lexopt) | v0.2.0
pico-args | 23 KiB | 901ms | 2ms | Y | ![Download count](https://img.shields.io/crates/dr/pico-args) | v0.4.2
xflags | 22 KiB | 1s | 2ms | Y | ![Download count](https://img.shields.io/crates/dr/xflags) | v0.2.4

Notes:
- Overhead will be lower if your application shares dependencies with your argument parsing library.

# Running the Benchmarks

```bash
$ ./bench.py
$ ./format.py
```

To be included, the crate needs meet one of the following criteria:
- 10k+ recent downloads
- Unique API design

# Special Thanks

- RazrFalcon for creating the [initial benchmarks](https://github.com/RazrFalcon/pico-args)
- djc for inspiration with [template-benchmarks-rs](https://github.com/djc/template-benchmarks-rs)
- sharkdp for [hyperfine](https://github.com/sharkdp/hyperfine)
