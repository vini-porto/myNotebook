# Designing Types

This lecture is about how to represent data in programs by creating **types**. Rather than using simple variables or generic data structures, you'll learn how to design your own custom types that accurately model real-world concepts and give you compiler support to catch errors.

# Why We Need Types: The Problem with Generic Data Structures

### Modelling Complex Data

Programs must represent data from their domain. For example:

- **E-commerce**: customers, products, orders, employees
- **Personal finances**: accounts, transactions, loans, assets
- **Video games**: players, NPCs, items
- **Web browsers**: pages, links, paragraphs, URLs
- **IDEs**: code files, undo/redo history, commands

Without proper structure, managing this data becomes messy and error-prone.

### From Variables to Collections

You might start with individual variables:

```
hackathon_title = "Hackathon"
hackathon_start = "2023-10-01T10:00:00"
```

Then move to lists (tuples):

```
events = [("Hackathon", "2023-10-01", ...), ...]
```

But you lose track of which index means what. Then you try maps:

```
events = [{"title": "Hackathon", "start": "2023-10-01", ...}]
```

### The Problem with Maps

**Maps don't work well for complex data because:**

- Typos in key names cause **runtime errors** (not caught when you write the code)
- When your data structure changes (new keys, renamed keys), **all code using those keys must be updated manually**
- The compiler can't help you—it has no idea what keys should exist

**Solution**: Define your own types that correspond to your data!

---

## Scalar vs. Composite Values

Understanding how to structure data starts with knowing two categories:

|Type|Definition|Examples|
|---|---|---|
|**Scalar**|Single, indivisible value|Integer, Boolean, Character|
|**Composite**|Multiple parts combined|String, List, Map, Object|

### Flat vs. Nested Structures

- **Flat**: One level of organization (e.g., a list of integers, or a Point with x, y, z)
- **Nested**: Multiple levels (e.g., a list of lists, or a list of Points)

---

## Defining Types in Java

### Types vs. Objects: The Blueprint Analogy

- **[[Type]]**: The blueprint (the code definition)
- **[[Object]]**: An actual instance created from the blueprint (exists in memory at runtime)

Think of a house blueprint vs. actual houses built from it:

- The blueprint says "all houses have a door and a fire"
- Each house **object** might have the door open or closed differently
- But all houses follow the same rules (same behavior, potentially different state)

### The `class` Structure

The main way to define a custom type in Java:

```java
class Event {
    // Instance variables (data)
    String title;
    LocalDateTime startTime;
    LocalDateTime endTime;
    
    // Constructor (how to create instances)
    Event(String title, LocalDateTime startTime, LocalDateTime endTime) {
        this.title = title;
        this.startTime = startTime;
        this.endTime = endTime;
    }
    
    // Instance method (behavior)
    Duration getDuration() {
        return Duration.between(startTime, endTime);
    }
}
```

#### The `this` Keyword

Inside a type definition, **`this`** refers to "the current instance being used":

```java
var e1 = new Event(..);
e1.getDuration();  // Inside getDuration(), 'this' refers to e1

var e2 = new Event(..);
e2.getDuration();  // Inside getDuration(), 'this' now refers to e2
```

---

## Constructors

### What Are Constructors?

A **[[Constructor]]** is a special method that runs when you create a new object. It initializes the instance variables.

**Rules:**

- Must have the same name as the type
- No explicit return type (returns the type implicitly)
- Can be overloaded (multiple constructors with different parameters)

### Default Constructor

If you don't define any constructor, Java automatically creates a **no-parameter constructor**:

```java
class Counter {
    int count;
    // Java automatically creates: Counter() { }
}
var c = new Counter();  // Works fine
```

**BUT** if you define even one constructor, Java **does not** create the default:

```java
class Counter {
    int count;
    Counter(int initialCount) {  // You defined a constructor
        count = initialCount;
    }
}
var c = new Counter();  // ERROR: no default constructor!
```

### Overloading Constructors

You can create multiple constructors with different parameters:

```java
Event(String title, LocalDateTime startTime, LocalDateTime endTime) {
    this.title = title;
    this.startTime = startTime;
    this.endTime = endTime;
}

// Different way to construct (using duration instead of end time)
Event(String title, LocalDateTime start, Duration duration) {
    this.title = title;
    this.startTime = start;
    this.endTime = start.plus(duration);
}
```

### Calling Constructors from Constructors

You can call one constructor from another using `this`:

```java
class Point {
    int x, y;
    
    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    Point() {
        this(12, 34);  // Call the other constructor with default values
    }
}
```

### Common Error: Forgetting to Initialize

If you don't initialize an instance variable, it stays `null`:

```java
class Foo {
    List<Integer> list;  // Null by default!
    void add(int x) {
        list.add(x);  // NullPointerException at runtime!
    }
}
```

**Fix:**

```java
class Foo {
    List<Integer> list = new ArrayList<>();  // Initialize it!
    void add(int x) {
        list.add(x);  // Works
    }
}
```

---

## Access Modifiers: Controlling What's Visible

### The Three Levels of Access

|Modifier|Accessible From|
|---|---|
|`private`|Only within the same type definition|
|package-private (no modifier)|Any file in the same package|
|`public`|Any file, anywhere|

```java
class Foo {
    int a;           // package-private by default
    private int b;   // Only Foo can see this
    public int c;    // Everyone can see this
}
```

### Access on Type Definitions

- **Top-level types**: Can be `public` or package-private (not `private`)
- **Nested types**: Can be `public`, package-private, or `private`

```java
class TypeA { }              // Package-private
public class TypeB { }       // Public
class TypeC {
    private class Nested { } // Private nested type
}
```

### Access on Constructors

Usually constructors are `public`, but you might make them `private` if:

- You want a **namespace class** (like `Math`) that shouldn't be instantiated
- You want users to use **class methods** instead (like `LocalDateTime.of()` or `LocalDateTime.now()`)

---

## Abstraction and Encapsulation

These are two powerful design principles:

### [[Abstraction]]

Focus on **essential details** and ignore irrelevant complexity. Show users the simple "interface" they need to work with.

### [[Encapsulation]]

Hide the **internal complexity** so users see only what they need to see. The designer keeps complex details private.

**The Pattern: Private Variables, Public Methods**

```java
public class Counter {
    private int count;  // Hidden (encapsulated)
    
    public void increment() {
        count++;
    }
    
    public int getCount() {
        return count;
    }
}

var c1 = new Counter();
c1.increment();
c1.getCount();  // 2 - User never needs to know how count is stored!
```

**Why is this better than public variables?**

Imagine thousands of projects use your `Counter`. If you later want to change how it works internally (like tracking timestamps instead of just an int), you can do it without breaking any existing code:

```java
// New implementation, same public interface
public class Counter {
    private List<Long> timestamps = new ArrayList<>();
    
    public void increment() {
        timestamps.add(System.currentTimeMillis());
    }
    
    public int getCount() {
        return timestamps.size();
    }
}
// Users' code never changes!
```

### Accessor, Mutator, Getter, Setter

- **[[Accessor]]**: A method that reads values (never changes anything)
- **[[Mutator]]**: A method that changes values
- **[[Getter]]**: An accessor that gets an instance variable (named `get` + variable name)
- **[[Setter]]**: A mutator that sets an instance variable (named `set` + variable name)

### Type Design Tip: Minimize Public Interface

Every public member is a **promise**. Users will rely on it existing forever. The less you expose, the more freedom you have to change the implementation later without breaking user code.

---

## Useful Methods for Any Type

### `toString` Method

Converts an object to a string representation. Automatically called when you print:

```java
class Event {
    public String toString() {
        return "Event %s starts at %s".formatted(title, start);
    }
}

var e = new Event(..);
IO.println(e);  // Automatically calls toString()
```

### `equals` Method

Determines if two objects should be considered **equal** (value equality, not reference equality):

```java
public boolean equals(Object other) {
    if (other == null || this.getClass() != other.getClass()) {
        return false;
    }
    Event otherEvent = (Event) other;
    return title.equals(otherEvent.title) 
        && start.equals(otherEvent.start) 
        && end.equals(otherEvent.end);
}
```

### `hashCode` Method

Returns a unique integer representing the object. Used by hash-based collections like `HashMap`.

**Important rule:** Objects that are equal according to `.equals()` **must** return the same `hashCode`:

```java
public int hashCode() {
    return Objects.hash(title, start, end);
}
```

Whenever you implement `.equals()`, **also implement `.hashCode()`**!

### Copy Constructor

Creates a new instance as a copy of an existing one:

```java
public Event(Event other) {
    this.title = other.title;
    this.start = other.start;
    this.end = other.end;
}
```

**Question**: Is this a deep or shallow copy?

**Answer**: Shallow, but it doesn't matter! `String` and `LocalDateTime` are **immutable**, so there's no way to change the copy (and thus no way to accidentally affect the original).

### IDE Code Generation

Most IDEs have tools that automatically generate boilerplate code like getters, setters, `equals`, `hashCode`, and copy constructors. Use them!

---

## Enumerations

Sometimes you need a type with a **limited set of fixed values**:

- Answer: Yes / No / Maybe
- Status: Ordered / Shipped / Complete
- Direction: North / South / East / West
- Service: Wifi / Catering / Security

### The Problem with Strings

Using strings is error-prone:

```java
var direction = "nrth";  // Typo! No compiler error, crashes at runtime
```

You'd need to manually validate every value.

### The Solution: `enum`

[[Enum|Enumerations]] are a special type where you define exactly which values are allowed:

```java
enum Answer { YES, NO, MAYBE }
enum Direction { NORTH, SOUTH, EAST, WEST }
enum Service { WIFI, CATERING, SECURITY }

var a = Answer.YES;
var d = Direction.NORTH;
```

**Benefits:**

- Compiler catches typos: `Direction.NRHT` is a compile-time error
- Compiler catches type errors: `Direction d = "NORTH"` is a compile-time error
- Compiler ensures all cases are handled in switches:

```java
public static Direction opposite(Direction d) {
    return switch (d) {
        case NORTH -> SOUTH;
        case SOUTH -> NORTH;
        case EAST -> WEST;
        case WEST -> EAST;
        // If you forget any case, compile error!
    };
}
```

---

## Records

[[Record|Records]] are a concise way to define types that are primarily about storing a multi-part value.

### What Are Records?

```java
public record Person(String name, int age) {}

var person = new Person("Alice", 30);
IO.println(person.name());  // Alice
IO.println(person.age());   // 30
```

### What Do Records Automatically Provide?

- **Constructor**: With parameters matching the fields
- **Getters**: Named the same as the fields (not `getName`, just `name()`)
- **Immutability**: No setters; you can't change the values after creation
- **`equals` method**: Compares all fields
- **`toString` method**: Nice string representation
- **`hashCode` method**: Automatically implemented

### When to Use Records

Use a **record** instead of a **class** whenever you just need to store multiple values that don't change. Example use cases:

- Person with name and age
- Rectangle with x, y, width, height
- Coordinate with latitude and longitude

**Rule of thumb**: In Java, if you just need a way to store a multi-part value that's not a collection (list, map), use a record instead of a class!

### Adding Methods to Records and Enums

Both `enum` and `record` can have custom methods added:

```java
enum Direction {
    NORTH, SOUTH, EAST, WEST;
    
    public Direction opposite() {
        return switch(this) {
            case NORTH -> SOUTH;
            case SOUTH -> NORTH;
            case EAST -> WEST;
            case WEST -> EAST;
        };
    }
}

Direction d = Direction.NORTH;
Direction opposite = d.opposite();  // SOUTH
```

---

## Summary: Four Ways to Define Types in Java

|Structure|Use When|Example|
|---|---|---|
|**`class`**|You need full control over behavior and state|Event, Counter|
|**`record`**|You just need to store multiple immutable values|Person, Rectangle|
|**`enum`**|You have a fixed set of named constant values|Direction, Status, Answer|
|**`interface`**|You want to define a contract that multiple types follow|(covered later)|

---

## Key Concepts to Review

- [[Type|Types]] and [[Object|Objects]]
- [[Scalar]] vs. [[Composite]] values
- [[Flat]] vs. [[Nested]] data structures
- [[Constructor]]
- [[Access Modifiers]] (private, public, package-private)
- [[Abstraction]]
- [[Encapsulation]]
- [[Accessor]] and [[Mutator]] methods
- [[Getter]] and [[Setter]] methods
- [[toString]] method
- [[equals]] method
- [[hashCode]] method
- [[Copy Constructor]]
- [[Enumeration|Enumerations]] (`enum`)
- [[Record|Records]]
- Method [[Overloading]]
- The `this` keyword
- Default constructor behavior