---
layout: default
title: "Transparent function objects"
excerpt: "Transparent function objects enable operations on heterogeneous types..."
---

# Transparent function objects

In Rust I tried to binary search a string slice in a string collection, and was surpriced that I had to resort from `binary_search` to either `binary_search_by` or `binary_search_by_key`:

```rust
fn main() {
    let vec: Vec<String> = Vec::new();
    // vec.binary_search("foo"); // doesn't compile, because a `String` is required
    vec.binary_search_by(|x| x.as_str().cmp("foo"));
    vec.binary_search_by_key(&"foo", |s| s.as_str());
}
```

In C++ the same scenario works just as I expect it to work - without any need to use a custom comparator:

```cpp
#include <algorithm>
#include <vector>
#include <string>
using namespace std;
int main() {
    vector<string> const els{"a", "b", "c"};
    lower_bound(els.begin(), els.end(), "b"sv);
}
```

Then I decided to remember and summarize what I know about searching string slices in C++ string sets and compare it to Rust.

The example below presents three ways to declare a set of strings, the first of which have a hidden allocation in `find`. The second and third declarations are the ways
to overcome the pitfall.

```cpp
#include <map>
#include <string_view>
#include <string>
#include <set>
#include <functional>

using namespace std;
using namespace string_view_literals;

struct MyString {
    std::string inner;
};

struct MyLess {
    using is_transparent = void;
    
    template <class T>
    bool operator()(MyString const& x, T const& y) const {
        return x.inner < y;
    }

    template <class T>
    bool operator()(T const& x, MyString const& y) const {
        return x < y.inner;
    }

    bool operator()(MyString const& x, MyString const& y) const {
        return x.inner < y.inner;
    }
};

int main() {
    // (1)
    set<string> s1;
    s1.find("foo");      // implicitly creates `string`
    // s1.find("foo"sv); // compilation error

    // (1)
    set<string, less<>> s2;
    s2.find("foo");   // doesn't create `string`
    s2.find("foo"sv); // doesn't create `string`, and compiles OK
    
    // (1) (for custom types)
    // `MyString` doesn't have conversion constructors, therefore any attempt to create `MyString` in the function calls below
    // would lead to compilation errors.
    set<MyString, MyLess> s3;
    s3.find("foo");   // doesn't create `MyString`
    s3.find("foo"sv); // doesn't create `MyString`
    s3.find("foo"s);  // doesn't create `MyString`
}
```

The `find` functin method's prototype is `foo(std::string const&)`, which requires a string argument. Because C-strings are implicitly convertible to `std::string`,
this function method is successfully selected in the call `.find("foo")` with me implicitly paying for a conversion hidden at the call point. Even though [Small String Optimization]({% post_url 2024-8-20-launder %}) alleviates this problem, sometimes the problem is unaffordable.

A _transparent function object_ can be used to enable a templated `find(T)` memeber function, which solves the problem. There are `void` specializations of many function objects in the standard library, for example `std::less<>`, that essentially are _transparent function objects_. They provide the functionality on heterogeneous objects. It is possible to create custom _transparent objects_ by providing `using is_transparent = /*unspecified*/;` type in the _function object's_ class scope or base class scopes.

In Rust this case works just as I expect it to work - without any need to use a custom comparator to avoid a hidden allocation.

```rust
use std::collections::HashMap;

fn main() {
    let foo: HashMap<String, u32> = HashMap::new();
    let key1 = "foo";
    let key2: String = "foo".into();

    // no implicit stirng slice to Strings, because `get` is a generic
    foo.get(key1);

    // the constraints on the generic parameter
    // require a pointer or a slice (which is a fat pointer)
    foo.get(&key2);
}
```
