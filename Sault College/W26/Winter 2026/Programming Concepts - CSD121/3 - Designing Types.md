# Introduction to Data Modeling

When you write a program, you need to **represent the real-world data** your program works with. This is called [[Data Modeling]].

Think about different types of programs:

- **E-commerce**: needs to represent customers, products, orders, employees
- **Personal finance app**: needs accounts, transactions, loans, assets
- **Video game**: needs players, NPCs, items, inventory
- **Web browser**: needs pages, links, bookmarks, URLs
- **IDE**: needs code files, commands, plugins, undo history

All of these examples involve **complex data** that has multiple properties and relationships. The question is: how do we model this data effectively in code?

---

# Scalar vs Composite Values

## [[Scalar Values]]

A **scalar value** is a single, indivisible piece of data.

**Examples:**

- Integer: `42`
- Boolean: `true`
- Character: `'A'`

### [[Composite Values]]

A **composite value** consists of multiple parts combined together.

**Examples:**

- String: `"Hello"` (composed of multiple characters)
- Lists: `[1, 2, 3, 4]`
- Maps: `{"name": "Alice", "age": 30}`
- Objects with multiple properties

---

## Flat vs Nested Data Structures

### [[Flat Data Structures]]

**One level** of sub-components.

**Examples:**

- List of integers: `[1, 2, 3]`
- Point in 3D space: `Point(x, y, z)`

### [[Nested Data Structures]]

**Multiple levels** of sub-components (structures within structures).

**Examples:**

- List of lists: `[[1, 2], [3, 4], [5, 6]]`
- List of Points: `[Point(1, 2, 3), Point(4, 5, 6)]`

---

## The Problem: How to Model Complex Data?

Let's use a real example: modeling **events at a conference center**.

Each event has:

- A title
- Start and end dates/times
- A list of requested services (WiFi, catering, security, etc.)

### Approach 1: Just Variables

```java
String hackathon_title = "Hackathon";
String hackathon_start = "2023-10-01T10:00:00";
String hackathon_end = "2023-10-01T18:00:00";
List<String> hackathon_services = List.of("wifi");
```

**Problem:** This doesn't scale. What if you need to manage multiple events? You'd need dozens of separate variables.

### Approach 2: Lists of Tuples

```java
List<Object> events = List.of(
    List.of("Hackathon", "2023-10-01T10:00:00", "2023-10-01T18:00:00", List.of("wifi")),
    List.of("Conference", "2023-10-02T09:00:00", "2023-10-02T17:00:00", List.of("catering"))
);
```

**Problem:** You need to remember that index 0 is the title, index 1 is start time, etc. This is error-prone and hard to read.

### Approach 3: Maps (Dictionaries)

```java
List<Map<String, Object>> events = List.of(
    Map.of("title", "Hackathon", "start", "2023-10-01T10:00:00", "end", "2023-10-01T18:00:00"),
    Map.of("title", "Conference", "start", "2023-10-02T09:00:00", "end", "2023-10-02T17:00:00")
);
```

**Better**, because you can access data by meaningful names like `event.get("title")`.

**But still problems:**

- **Typos in key names** cause runtime errors (not caught by compiler)
- If you rename a key, you must find and update **every** place it's used
- No help from your IDE or compiler

---

## The Solution: Custom Types

Instead of using generic data structures like maps, **define your own types** that match your data!

```java
var event = new Event(
    "Hackathon",
    LocalDateTime.of(2023, 10, 1, 10, 0),
    LocalDateTime.of(2023, 10, 1, 18, 0),
    List.of(Event.Service.WIFI)
);
```

**Why this is better:**

- The **compiler verifies correctness**
- **Refactoring is safer** (IDE can find all uses of a method)
- **Type checking** prevents many bugs

---

## Four Ways to Define Types in Java

Java provides four structures for defining custom types:

1. **[[Class]]** - for general-purpose types with behavior
2. **[[Record]]** - for simple data containers (immutable)
3. **[[Enum]]** - for types with a fixed set of values
4. **[[Interface]]** - for defining contracts (covered later)

---

## Defining Types with Classes

The **class** structure is the most flexible way to define types.

### Basic Class Structure

```java
class <TypeName> {
    // Instance variables (the data)
    // Constructors (how to create instances)
    // Instance methods (the behavior)
}
```

### Example: Event Class

```java
class Event {
    // Instance variables
    String title;
    LocalDateTime startTime;
    LocalDateTime endTime;
    
    // Constructor
    Event(String title, LocalDateTime startTime, LocalDateTime endTime) {
        this.title = title;
        this.startTime = startTime;
        this.endTime = endTime;
    }
    
    // Instance method
    Duration getDuration() {
        return Duration.between(startTime, endTime);
    }
}
```

### The `this` Keyword

The **[[this Keyword]]** refers to "the current instance being accessed."

```java
var e1 = new Event(...);
e1.getDuration(); // Inside getDuration, 'this' refers to e1

var e2 = new Event(...);
e2.getDuration(); // Inside getDuration, 'this' refers to e2
```

**Important:** `this` only works in instance methods, not in [[Static Methods]] (class methods).

---

## Types vs Objects: Understanding the Distinction

### [[Type]]

The **blueprint** or **template**. The code that defines what all instances will look like and how they'll behave.

### [[Object]]

An actual **instance** created from that blueprint. A real thing in memory at runtime.

**Analogy:** A house blueprint (type) vs. actual houses built from that blueprint (objects).

### Example

```java
class House {
    boolean isDoorOpen = false;
    boolean isFireLit = false;
    
    void openDoor() {
        isDoorOpen = true;
    }
    
    void lightFire() {
        isFireLit = true;
    }
}

House house1 = new House();
House house2 = new House();
house2.openDoor();
house2.lightFire();
```

**Key insight:**

- All `House` objects have the **same behavior** (methods `openDoor()` and `lightFire()`)
- But they can have **different state** (house1's door is closed, house2's door is open)

---

## Constructors

A **[[Constructor]]** is a special method that creates and initializes a new object.

### Constructor Rules

1. **Same name as the type**
2. **No explicit return type** (implicitly returns the type)
3. Can have **parameters** to initialize the object

```java
class Event {
    String title;
    LocalDateTime startTime;
    LocalDateTime endTime;
    
    Event(String title, LocalDateTime startTime, LocalDateTime endTime) {
        this.title = title;
        this.startTime = startTime;
        this.endTime = endTime;
    }
}
```

### Default Constructor Behavior

- If you define **no constructors**, Java automatically provides a **no-parameter constructor**
- If you define **any constructor**, Java does NOT provide the default one

```java
class Counter {
    int count;
    
    Counter(int initialCount) {
        count = initialCount;
    }
}

var c1 = new Counter();      // ERROR! No default constructor
var c2 = new Counter(10);    // OK
```

---

## Method Overloading

**[[Method Overloading]]** means defining multiple methods with the **same name** but **different parameters** (different [[Method Signature]]).

### Example: Overloaded Constructors

```java
class Event {
    String title;
    LocalDateTime startTime;
    LocalDateTime endTime;
    
    // First constructor
    Event(String title, LocalDateTime startTime, LocalDateTime endTime) {
        this.title = title;
        this.startTime = startTime;
        this.endTime = endTime;
    }
    
    // Second constructor (overloaded)
    Event(String title, LocalDateTime start, Duration duration) {
        this.title = title;
        this.startTime = start;
        this.endTime = start.plus(duration);
    }
}
```

### Calling One Constructor from Another

Use `this(...)` to call another constructor:

```java
class Point {
    int x, y;
    
    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
    
    Point() {
        this(12, 34);  // Call the other constructor with defaults
    }
}
```

---

## Common Errors: Uninitialized Instance Variables

### The Problem

```java
class Foo {
    List<Integer> list;
    
    void add(int x) {
        list.add(x);  // CRASH! NullPointerException
    }
}

var f = new Foo();
f.add(10);  // Error here
```

**Why?** The `list` variable was never initialized—it's still `null`!

### The Solution

```java
class Foo {
    List<Integer> list = List.of();  // Initialize when declared
    
    void add(int x) {
        list.add(x);  // Now it works
    }
}
```

---

## Access Modifiers

**[[Access Modifiers]]** control who can see and use different parts of your code.

### Three Levels of Access

|Modifier|Who Can Access|
|---|---|
|`private`|Only within the same class|
|(package-private, default)|Any code in the same package|
|`public`|Any code anywhere|

### Example

```java
class Foo {
    int a;              // Package-private (default)
    private int b;      // Private
    public int c;       // Public
}
```

### Access Modifiers on Type Definitions

- Top-level classes can be **package-private** or **public**
- Nested classes can also be **private**

```java
class TypeA { }              // Package-private
public class TypeB { }       // Public

class TypeC {
    private class Nested { } // Private nested class
}
```

### Access Modifiers on Constructors

Constructors are usually `public`, but can be `private` to:

- Prevent direct instantiation (e.g., `Math` class)
- Force use of factory methods (e.g., `LocalDateTime.of()`)

---

## Why Access Modifiers? Abstraction and Encapsulation

### [[Abstraction]]

**Focus on essential details; ignore irrelevant complexity.**

Like using a car: you don't need to know how the engine works internally—you just use the steering wheel, pedals, and gear shift.

### [[Encapsulation]]

**Hide complexity to expose a simpler interface.**

- **Exposed abstraction:** what users interact with (public methods)
- **Hidden complexity:** internal implementation details (private variables)

### The Common Pattern: Private Variables, Public Methods

```java
public class Counter {
    private int count;  // Hidden implementation
    
    public void increment() {  // Public interface
        count++;
    }
    
    public int getCount() {  // Public interface
        return count;
    }
}
```

**Why this matters:**

If the instance variable was public, users would access it directly. Then if you want to change the internal implementation later, **everyone's code breaks**.

With private variables and public methods, you can change the implementation without affecting users:

```java
// Version 1
class Counter {
    private int count;
    public int getCount() { return count; }
}

// Version 2 - different implementation, same public interface
class Counter {
    private List<Long> timestamps = new ArrayList<>();
    public int getCount() { return timestamps.size(); }
}
```

**Users' code doesn't need to change!**

---

## Getters, Setters, Accessors, and Mutators

### [[Accessor Method]]

A method that **reads** values without changing anything.

### [[Mutator Method]]

A method that **changes** one or more values.

### [[Getter Method]]

An accessor that returns the value of an instance variable. Named `get` + variable name.

```java
public int getCount() {
    return count;
}
```

### [[Setter Method]]

A mutator that sets the value of an instance variable. Named `set` + variable name.

```java
public void setCount(int newCount) {
    count = newCount;
}
```

---

## Type Design Principle: Minimize the Public Interface

**A public member is a promise:** "This will be available forever."

- The **less you expose**, the more freedom you have to change implementation later
- The **more you expose**, the harder it is to evolve your code

**Rule of thumb:** Make everything `private` by default. Only make things `public` when necessary.

---

## Useful Methods for Any Type

### The `toString` Method

Converts an object to a **string representation**. Automatically called when printing.

```java
class Event {
    public String toString() {
        return "Event %s starts at %s and ends at %s"
            .formatted(title, start, end);
    }
}

var e = new Event(...);
IO.println(e);  // Calls toString automatically
```

### The `equals` Method

Determines **value equality** between objects (not reference equality).

```java
public boolean equals(Object other) {
    if (other == null || this.getClass() != other.getClass()) {
        return false;
    }
    
    Event otherEvent = (Event)other;
    return title.equals(otherEvent.title) 
        && start.equals(otherEvent.start) 
        && end.equals(otherEvent.end);
}
```

### The `hashCode` Method

Returns an integer "hash" for use in hash-based collections like `HashMap`.

**Critical rule:** Objects that are equal according to `equals()` **must** return the same `hashCode()`.

```java
public int hashCode() {
    return Objects.hash(title, start, end);
}
```

**Always implement both `equals` and `hashCode` together!**

### [[Copy Constructor]]

Creates a new object as a copy of an existing one.

```java
public Event(Event other) {
    this.title = other.title;
    this.start = other.start;
    this.end = other.end;
}
```

**Question:** Is this a deep or shallow copy?

**Answer:** It's a **shallow copy**, but that's okay! Both `String` and `LocalDateTime` are [[Immutable Types]], so there's no way to accidentally modify the original through the copy.

---

## Enumerations (Enums)

Sometimes you need a type with a **fixed, limited set of possible values**.

**Examples:**

- Answer: Yes, No, Maybe
- Status: Ordered, Shipped, Complete
- Direction: North, South, East, West

### The Problem with Strings

```java
var answer = "Yes";  // or "No" or "Maybe"
var direction = "North";

// Typos cause runtime errors
var answer = "Yse";      // Oops!
var direction = "Nrth";  // Oops!
```

### The Solution: Enums

**[[Enumeration]]** types define a specific set of named values.

```java
enum Answer { YES, NO, MAYBE }
enum Direction { NORTH, SOUTH, EAST, WEST }
enum Service { WIFI, CATERING, SECURITY }

var a = Answer.YES;
var s = Service.WIFI;
```

### Benefits of Enums

**Type safety:**

```java
opposite("NORTH")           // Type Error!
opposite(Direction.NRTH)    // Compile Error! (typo caught)
opposite(Direction.NORTH)   // Works correctly
```

**Exhaustiveness checking:**

```java
public static Direction opposite(Direction d) {
    return switch (d) {
        case NORTH -> Direction.SOUTH;
        case SOUTH -> Direction.NORTH;
        case EAST -> Direction.WEST;
        case WEST -> Direction.EAST;
        // Compiler ensures all cases are covered!
    };
}
```

---

## Records

A **[[Record]]** is a concise way to define a type that's primarily about storing data (not behavior).

### Example: Person Record

```java
public record Person(String name, int age) {}

var person = new Person("Alice", 30);
IO.println(person.name());  // Alice
IO.println(person.age());   // 30
```

### What Records Provide Automatically

1. **Constructor** matching the properties
2. **Getters** with the same name as properties (not `getName()`, just `name()`)
3. **Immutability** (no setters)
4. Automatic `toString()`, `equals()`, and `hashCode()` methods

### Another Example

```java
public record Rectangle(int x, int y, int width, int height) {}

var r = new Rectangle(10, 10, 100, 200);
System.out.printf("x=%d, y=%d, width=%d, height=%d%n",
    r.x(), r.y(), r.width(), r.height());
```

### When to Use Records

**Use a record when:**

- You need a simple data container
- The type is primarily about the values it holds
- You don't need mutability (changing values after creation)

**Use a class when:**

- You need complex behavior
- You need mutable state
- You need inheritance

---

## Adding Methods to Enums and Records

Even though enums and records have concise syntax, you can still add custom methods to them:

```java
enum Direction {
    NORTH, SOUTH, EAST, WEST;
    
    public Direction opposite() {
        return switch (this) {
            case NORTH -> SOUTH;
            case SOUTH -> NORTH;
            case EAST -> WEST;
            case WEST -> EAST;
        };
    }
}

public record Rectangle(int x, int y, int width, int height) {
    public int area() {
        return width * height;
    }
}
```

# Tags

#java #oop #types #classes #encapsulation #abstraction #data-modeling #software-design