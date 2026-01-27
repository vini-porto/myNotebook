# What is a Scope

Scope is the region or area of your code where a [[variable]], [[function]], or other identifier can be accessed and used.

---
# Types of Scope

## Local Scope 

(Block/Function Scope) Variables declared inside a [[function]] or block `{}` can only be used within that function or block.

## Global Scope 

Variables declared outside all functions can be accessed from anywhere in your program.

## Function/Method Scope

In some languages, variables exist for the entire function, not just within blocks. 

### Languages with Function Scope

In [[JavaScript]], `var` is **function-scoped**, not block-scoped:

``` javascript
function test() {
  if (true) {
    var x = 10;
  }
  console.log(x); // 10 (still accessible)
}

```

- `let` and `const` are block-scoped
- `var` is function-scoped

---

[[Python]] has function scope, not block scope:

``` python
def test():
    if True:
        x = 10
    print(x)  # works

```

---

In [[PHP]] Variables are function-scoped, not block-scoped:

``` php
function test() {
    if (true) {
        $x = 10;
    }
    echo $x; // works
}

```

### Languages with Block Scope 

>[!NOTE]
> These create new scope inside `{}` blocks:

- [[C]] / [[C++]]
- [[Java]]
- [[C#]]
- [[Go]]
- [[Rust]]
- [[Swift]]
- [[JavaScript]] (`let`, `const`)
## Class Scope

Variables that belong to a [[class]] or object (also called instance variables or fields)


