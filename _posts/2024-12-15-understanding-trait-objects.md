---
title: "Understanding Trait Objects (dyn Trait)"
date: 2024-12-15
categories: [programming, rust]
tags: [rust, traits, programming, tutorial]
excerpt: "Learn how to use trait objects in Rust for dynamic dispatch and polymorphism"
---

# Understanding Trait Objects (dyn Trait)

In Rust, trait objects allow you to work with different concrete types through a shared trait interface at runtime. This is useful when you want to abstract over multiple types that implement the same trait. Trait objects are created using the dyn Trait syntax, where Trait is the name of the trait.

For example, given a trait Logic:

```rust
pub trait Logic {
    fn process(&self, input: &str) -> String;
}
```

We can create trait objects by boxing a concrete type that implements Logic into a Box<dyn Logic>.

## Box<dyn Trait> for Dynamic Dispatch

In Rust, trait objects (dyn Trait) have a size that is not known at compile time because they could represent any type that implements the specified trait. 

To handle trait objects efficiently, Rust requires them to be behind a pointer like:

```rust
Box<dyn Trait> or &dyn Trait
``` 

This pointer abstracts away the actual size of the underlying type and enables dynamic dispatch.

When we define a field like general_logic: Box<dyn Logic> in a struct, we're saying that general_logic can hold any type that implements the Logic trait. The trait object is stored on the heap because its size isn't known at compile time.

## Using Box<dyn Logic> in method

```rust
impl Example {
    pub fn new(logic: impl Logic + 'static) -> Self {
        Example {
            general_logic: Box::new(logic),
        }
    }
}
```

impl Logic + 'static: This syntax specifies that the logic parameter must implement the Logic trait (impl Logic) and must have a 'static lifetime. 

The 'static lifetime indicates that the object (logic parameter) will live for the entire duration of the program. This is necessary because we're going to store logic in a trait object (Box<dyn Logic>), which requires a static lifetime.

Box::new(logic): Inside the new method, we use Box::new(logic) to create a heap-allocated box (Box) containing logic. This Box<dyn Logic> is a trait object that can hold any type implementing Logic.

Box::new(logic) takes ownership of logic and allocates memory on the heap to store logic as a trait object. This box (Box<dyn Logic>) is then stored in the general_logic field of the Example struct.

## Benefits of Using Trait Objects

Using trait objects (Box<dyn Trait>) allows us to write more flexible and generic code:

- We can write functions and structs that accept trait objects as parameters, enabling dynamic dispatch.
- We can store different types that implement the same trait in a single data structure (e.g., vector of trait objects).
- Trait objects facilitate polymorphism and abstraction, making it easier to work with different types through a common interface.

## Example Usage

Once an instance of API is created with a concrete type that implements Logic (e.g., MyLogic), we can use the trait object (general_logic) to invoke trait methods dynamically, like this:

```rust
impl Example {
    pub fn use_logic(&self, input: &str) -> String {
        self.general_logic.process(input)
    }
}
```

In this example, self.general_logic.process(input) dynamically dispatches the process method based on the actual type stored in general_logic at runtime. This enables polymorphic behavior without knowing the exact type of general_logic at compile time.

I hope this detailed explanation helps clarify how trait objects (dyn Trait) and Box<dyn Trait> work in Rust and why they are useful for building flexible and generic code. 