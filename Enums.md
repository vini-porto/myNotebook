# What Are Enums?

An enum (short for "enumeration") is a special data type that represents a fixed set of named constants. It allows you to define a [[variable]] that can only hold one value from a predefined list of options. 

Enums make your code more readable, type-safe, and less error-prone by replacing "magic numbers" or arbitrary strings with meaningful names.

## Analogy

Think of enums like an multiple-choice question you can only select one answer from a specific list:

**Question: What's your shirt size?**

- Small
- Medium
- Large
- Extra Large

you can't answer "Purple" or "7.5" because those aren't valid shirt sizes. The list is fixed and predefined.

>An enum defines all the valid options:

``` java
enum ShirtSize {
    SMALL,
    MEDIUM,
    LARGE,
    EXTRA_LARGE
}
```

Now [[variables]] of type `ShirtSize` can **only** be one of these four values—nothing else is allowed.

# Why Enums Matter

## Without Enums

``` java
// Using magic numbers - BAD!
int status = 2;  // What does 2 mean?

if (status == 1) {
    // pending?
} else if (status == 2) {
    // shipped?
} else if (status == 3) {
    // delivered?
}

// Or using strings - BETTER but still problematic
String status = "Shipped";

if (status.equals("shipped")) {  // Oops! Case mismatch
    // Won't work
}

if (status.equals("Shippd")) {  // Typo! Won't be caught until runtime
    // Won't work
}
```

## With Enums

``` java
// Using enums - GOOD!
enum OrderStatus {
    PENDING,
    SHIPPED,
    DELIVERED
}

OrderStatus status = OrderStatus.SHIPPED;

if (status == OrderStatus.SHIPPED) {  // Clear and type-safe
    System.out.println("Order is on its way!");
}

// OrderStatus status = OrderStatus.SHIPPD;  // Compile error! Typo caught immediately
// OrderStatus status = 2;  // Compile error! Can't use numbers
```

# Enum Methods in Java

- values()
- valueOf()
- name()
- ordinal()
- compareTo()

``` java
public enum Color {
    RED, GREEN, BLUE
}

// Get all enum constants as an array
Color[] allColors = Color.values();
for (Color c : allColors) {
    System.out.println(c);
}

// Convert string to enum
Color color = Color.valueOf("RED");  // Returns Color.RED
// Color invalid = Color.valueOf("PURPLE");  // Throws IllegalArgumentException

// Get the name as a string
String name = Color.RED.name();  // "RED"

// Get the ordinal position (0-indexed)
int position = Color.BLUE.ordinal();  // 2

// Compare enum values
Color c1 = Color.RED;
Color c2 = Color.RED;
System.out.println(c1 == c2);  // true (can use == for enums)
System.out.println(c1.equals(c2));  // also true

// Enums implement Comparable
System.out.println(Color.RED.compareTo(Color.BLUE));  // negative (RED comes before BLUE)
```

# Enums in Switch Statements

``` java
public enum HttpStatus {
    OK, NOT_FOUND, INTERNAL_SERVER_ERROR, UNAUTHORIZED, FORBIDDEN
}

public void handleResponse(HttpStatus status) {
    switch (status) {
        case OK:
            System.out.println("Success!");
            break;
        case NOT_FOUND:
            System.out.println("Resource not found");
            break;
        case UNAUTHORIZED:
            System.out.println("Please log in");
            break;
        case FORBIDDEN:
            System.out.println("Access denied");
            break;
        case INTERNAL_SERVER_ERROR:
            System.out.println("Server error");
            break;
        // Compiler warns if you miss a case!
    }
}
```

# Enums in Other Languages

## [[C]]/[[C++]]

In C/C++, enums are simpler—just integer [[constants]]:

``` java
// C enum
enum Color {
    RED,      // 0
    GREEN,    // 1
    BLUE      // 2
};

// You can specify values
enum Status {
    PENDING = 1,
    ACTIVE = 2,
    CLOSED = 5
};

// Usage
enum Color myColor = RED;

if (myColor == RED) {
    printf("Red color\n");
}
```

## [[Python]]

[[Python]] has an `enum` module:

``` python
from enum import Enum

class Color(Enum):
    RED = 1
    GREEN = 2
    BLUE = 3

# Usage
my_color = Color.RED

if my_color == Color.RED:
    print("It's red!")

print(my_color.name)   # "RED"
print(my_color.value)  # 1

# Iterate through enum
for color in Color:
    print(color)
```

## TypeScript

``` typescript
enum Direction {
    North,
    South,
    East,
    West
}

let heading: Direction = Direction.North;

// Enum with values
enum HttpStatus {
    OK = 200,
    NotFound = 404,
    ServerError = 500
}

let status: HttpStatus = HttpStatus.OK;
console.log(status);  // 200
```

# [[EnumSet]] and [[EnumMap]]

Java provides special, highly-efficient collections for enums:

``` java
import java.util.EnumSet;
import java.util.EnumMap;

public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

// EnumSet - efficient set implementation for enums
EnumSet<Day> weekend = EnumSet.of(Day.SATURDAY, Day.SUNDAY);
EnumSet<Day> weekdays = EnumSet.range(Day.MONDAY, Day.FRIDAY);
EnumSet<Day> allDays = EnumSet.allOf(Day.class);

if (weekend.contains(Day.SATURDAY)) {
    System.out.println("Saturday is a weekend day");
}

// EnumMap - efficient map with enum keys
EnumMap<Day, String> schedule = new EnumMap<>(Day.class);
schedule.put(Day.MONDAY, "Team meeting");
schedule.put(Day.WEDNESDAY, "Project review");
schedule.put(Day.FRIDAY, "Weekly standup");

System.out.println("Monday: " + schedule.get(Day.MONDAY));
```

# Best Practices

## 1. Use Enums Instead of Constants

``` java
// BAD - magic numbers
public static final int STATUS_PENDING = 1;
public static final int STATUS_ACTIVE = 2;
public static final int STATUS_CLOSED = 3;

// GOOD - enum
public enum Status {
    PENDING, ACTIVE, CLOSED
}
```
## 1. Add Methods fo Behavior

``` java
public enum Operation {
    PLUS {
        public double apply(double x, double y) {
            return x + y;
        }
    },
    MINUS {
        public double apply(double x, double y) {
            return x - y;
        }
    },
    TIMES {
        public double apply(double x, double y) {
            return x * y;
        }
    },
    DIVIDE {
        public double apply(double x, double y) {
            return x / y;
        }
    };
    
    public abstract double apply(double x, double y);
}

// Usage
double result = Operation.PLUS.apply(5, 3);  // 8.0
```

## Use Descriptive Names

``` java
// GOOD
enum OrderStatus { PENDING, PROCESSING, SHIPPED, DELIVERED }

// BAD
enum Status { S1, S2, S3, S4 }
```

## Consider Adding [[toString()]]

``` java
public enum Priority {
    LOW("Low Priority"),
    MEDIUM("Medium Priority"),
    HIGH("High Priority"),
    URGENT("Urgent!");
    
    private final String displayName;
    
    Priority(String displayName) {
        this.displayName = displayName;
    }
    
    @Override
    public String toString() {
        return displayName;
    }
}

System.out.println(Priority.HIGH);  // "High Priority" instead of "HIGH"
```


#java #programming #enums #constants #type-safety #fundamentals #best-practices #design-patterns #state-machines