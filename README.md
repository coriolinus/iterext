# `iterext`: A few more extension methods on iterators.

This crate is not likely to ever be published on <https://crates.io> because it's
far more appropriate to attepmt to get these extensions added to
[`itertools`](https://crates.io/crates/itertools). However, I haven't yet made the time
to attempt to contribute them there.

A few quick examples from the tests should show what it's about:

```rust
use iterext::prelude::*;

#[test]
fn test_separate() {
    for (msg, expect) in &[
        ("abc", "abc"),
        ("zyx", "zyx"),
        (
            "abcdefghijklmnopqrstuvwxyz",
            "abcde fghij klmno pqrst uvwxy z",
        ),
        (
            "thequickbrownfoxjumpedoverthelazydog",
            "thequ ickbr ownfo xjump edove rthel azydo g",
        ),
        (
            "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz",
            "abcde fghij klmno pqrst uvwxy zabcd efghi jklmn opqrs tuvwx yz",
        ),
    ] {
        let got: String = msg.chars().separate(' ', 5);
        assert_eq!(&got, expect,);
    }
}

#[test]
fn test_padding_chars() {
    let have = "foo".chars().pad('X', 5).collect::<String>();
    assert_eq!(have, "fooXX");
}
```

## Provenance

Originally wrote these extensions as part of the [`textbyte`](https://github.com/coriolinus/solitaire/blob/master/src/textbyte.rs)
module for my [`solitaire`](https://github.com/coriolinus/solitaire/) implementation.
