---
layout: default
title: "String formatting for debugging"
excerpt: "Some programming languages explicitly distinguish string formatting for debug purposes and string formatting for displaying to the user. Other languages, including C++, decide not to have such semantics in the standard library"
---

# String formatting for debugging

Some programming languages explicitly distinguish string formatting for debug purposes and string formatting for displaying to the user. In the case of Rust, it provides two separate traits - `Debug` and `Display` respectively. When there’s no obvious user-facing representation, Rust uses display adapters - the wrapper types like Escaped or Quoted that implement Display with a specific meaning.

Some languages, including C++, decide not to have such semantics in the standard library. I guess it depends on the design principles of the language. Rust prefers doing things in one way and imposes this principle to the programmer. C++ is the opposite. In a C++ program you have the option of choosing what approach to use to implement the formatting semantic. You can end up not choosing, but then your program will be mixing different approaches, because there are many available: `operator<<` overload, string conversion operator, `std::to_string` overload, `std::format`, and custom functions.

If you choose to go with `std::format`, then it is possible to use a formatting option to distinguish between the two semantics. For example, 'd' for debug and lack of 'd' for human readable string.

```cpp
#include <print>

using namespace std;

struct Something {
    string_view field1;
    size_t field2;
    string_view debug_field2;
};

namespace std {

template <>
struct formatter<Something> {
    bool debug = false;

    constexpr auto parse(format_parse_context& ctx) {
        auto it = ctx.begin();

        if (*it == '}') {
            debug = false;
        } else if (*it == 'd') {
            debug = true;
        } else {
            throw std::format_error("Supported format options are: 'd' - debug; none - human readable");
        }

        return ++it;
    }

    template <typename FormatContext>
    auto format(Something const& x, FormatContext& ctx) const {
        if (debug) {
            return format_to(ctx.out(), "Something({}, {}, {})", x.field1, x.field2, x.debug_field2);
        } else {
            return format_to(ctx.out(), "Something({}, {})", x.field1, x.field2);            
        }
    }
};

}

int main() {
    Something x{"a", 1, "b"};
    println("{}", x);
    println("{:d}", x);
}

// cd /tmp && g++ -std=c++23 foo.cpp && ./a.out
```

If you work with non-standard strings, then a CPO function object per formatting semantic might be a good solution.

Swift uses different terminology for string formatting — string interpolation. It has the `CustomStringConvertible` and `CustomDebugStringConvertible` protocols, which semantically correspond to Rust’s `Display` and `Debug` traits.

Kotlin, similar to C++, doesn’t distinguish between display and debug string representations. To make your class formattable, you need to implement the `toString` method.
