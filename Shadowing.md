# What Is Shadowing?

Shadowing occurs when a [[variable]] declared in an inner [[Scope]] has the same name as a variable in an outer scope. 

The inner variable hides the outer one, making the outer variable temporarily inaccessible within that inner scope. 

>It's like the inner variable casts a shadow over the outer one.

---

# How Shadowing Works

When you reference a variable name, the program looks for it in this order:

1. Current (innermost) scope
2. Next outer scope
3. Next outer scope
4. ... and so on until global scope

>[!NOTE]
>The first match wins, which means inner variables shadow outer ones


# Pratical Examples

``` java
public class ShadowExample {
    private int value = 100;  // Instance variable
    
    public void demonstrate() {
        int value = 200;  // Local variable shadows instance variable
        System.out.println(value);       // Prints: 200 (local)
        System.out.println(this.value);  // Prints: 100 (instance, using 'this')
        
        for (int i = 0; i < 3; i++) {
            int value = 300;  // Shadows the method's local variable
            System.out.println(value);   // Prints: 300 (block scope)
        }
        
        System.out.println(value);       // Prints: 200 (method scope)
    }
}
```


# Accessing Shadowed Variables

## JavaScript/Java

Use `this` for instance variables:

``` javascript
class Person {
    constructor(name) {
        this.name = name;
    }
    
    greet(name) {  // Parameter shadows instance variable
        console.log(name);        // Parameter
        console.log(this.name);   // Instance variable
    }
}
```

## Python

Use `global` or `nonlocal` keywords

``` python
count = 0

def increment():
    global count  # Access global variable instead of creating local
    count += 1
```

## C++

Use `::` for global variables

``` cpp
int x = 5;

void test() {
    int x = 10;
    cout << x;    // Local: 10
    cout << ::x;  // Global: 5
}
```

# Variables Shadowing vs Variables Reassignment

>[!NOTE] Attention
>Don't confuse shadowing with reassignment

``` python
# Reassignment (same variable, new value)
x = 10
x = 20  # Same x, just changed value

# Shadowing (different variable, same name)
x = 10
def demo():
    x = 20  # Different x, shadows outer x
```


#programming #variables #scope #shadowing #functions #fundamentals #debugging #best-practices