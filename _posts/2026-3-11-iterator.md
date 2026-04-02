---
layout: default
title: "Iterators with non-reference value types"
excerpt: "`pair<Key const&, T&>` can be used instead of `pair<Key const, T>&` when the iterated collection doesn't store elements in pairs."
---

# Iterators with non-reference value types

How do you implement an iterator when its value type should be structurally different from the container's stored type? It is easer to understand the case by the following two examples.

Standard associative containers store values in `pair<K const, V>`, and their iterators dereference to `pair<K const, V>&`, therfore the iterators implementation is straightforward:

```cpp
pair<K const, V>& operator*() const {
    return *current;
}
pair<K const, V>* current;
```

This [Unibit Trie](https://github.com/nicktrandafil/unibit-trie/) data structure stores values in (See the [Node](https://github.com/nicktrandafil/unibit-trie/blob/9fe917be972b514c30bf16e23a3fd53e5af436de/unibit_trie.h#L32)):

```cpp
struct Node {
    K key;
    optional<V> value;
    ...
};
```

I don't want to expose this `Node` type, therefore the iterators can't dereference to `Node&`. The other issue is that what the user would do with the optional? The optional is an implemenattion detail, which helps to manage stub-nodes. The iterators should filter out nodes that have no value.

My solution is to use `pair<Key const&, T&>`. It has one inconvenience though - it lacks copy the copy assignment operator. To overcome this I define a custom pair-like type and provide a copy assignment.

There remains two details to take care of for this to work. The first - declare `using reference_type = value_type`, because the iterator will return values, not references. Forget I this detail and the client code would use danglings references. The second - implement identity `operator->()` on `value_type`, otherwise `it->first` will not work.

Conceptually what happens here is that I use a reference-like type instead of a reference. The type refers to sub-objects of the stored value.

The iterator looks like this:

```cpp
template <class K, class V>
struct Iterator {
    // std::iterator concept
    // @{

    using iterator_category = std::forward_iterator_tag;

    struct value_type {
        K const& first;
        V& second;

        // init with a kay and value, disable default construction
        value_type(K const& k, V& v)
                : first{k}
                , second{v} {
        }

        // enable copy
        value_type& operator=(value_type const& rhs) {
            this->~value_type();
            return *new (this) value_type{rhs};
        }

        // maybe enable comparison
        bool operator==(value_type const&) const = default;

        // identity
        value_type* operator->() {
            return this;
        }
    };

    using reference_type = value_type;

    value_type operator*() const {
        return value_type{current->first, current->second.value()};
    }

    value_type operator->() const {
        return value_type{current->first, current->second.value()};
    }

    Iterator& operator++() {
        // ...
    }

    bool operator==(Iterator const&) const = default;

    // @}

    Iterator() : current{nullptr} {
    }

private:
    template <class>
    friend class Trie;

    explicit Iterator(Node<K, V>* root)
            : current{root} {
        // ...
    }

    Node<K, V>* current;
}
```
