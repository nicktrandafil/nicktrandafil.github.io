---
layout: default
title: "Additional output in Catch2"
excerpt: "`REQUIRE` uses `Catch::StringMaker<T>`, while `INFO` uses `ostream& operator<<(ostream&, T)`."
---

# Additional output in Catch2

In Catch2 there is this feature where you can print some output only if a `REQUIRE` fails. It is useful to put there some state related information. It is done by using `INFO` macro.

For example, in a [UnibitTrie](https://github.com/nicktrandafil/unibit-trie/blob/9fe917be972b514c30bf16e23a3fd53e5af436de/test_unibit_trie.cpp#L233) data structure I have:

```
std::optional<Prefix> expected;
INFO(trie.ascii_string());
INFO("expected = " << sub);
INFO("it = " << it);
auto const it = trie.match_longest(sub);
REQUIRE((it != trie.end() == expected.has_value()));
if (expected)
    REQUIRE(it->prefix == expected);
```

This is very helpful when debugging - if the test fails I immediately see the iterator value and the trie, and I can figure out what I did wrong.

There is one surprising distinction between `REQUIRE` and `INFO` in how the arguments are turned to strings. The former uses `Catch::StringMaker<T>`, while the latter - `ostream& operator<<(ostream&, T)`.
