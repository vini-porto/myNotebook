# What Are Structs

A struct ("structure") is a user-defined data type that groups together related variables of different types under a single name. 

>Structs are primarily designed to hold data with minimal or no behavior. 

## Analogy

Think of a struct like a form or index card:

- Name: ========
- Phone: ========
- Email: ========
- Address: ========

The card itself (the struct) defines what information goes where. Each actual card you fill out is an instance of that structure. The card doesn't "do" anything—it just holds information in an organized way.

Compare this to [[Classes]], which would be more like a smartphone contact that can:

- Store the same information (name, phone, email)
- **Plus** perform actions (call this person, send email, show on map)

>[!NOTE]
>Structs are simpler—just the data, minimal behavior.

# Core Characteristics of Structs

## 1. Value Types

>Structs are typically **value types**, meaning they're copied when assigned or passed to functions.

## 2. Lightweight

>Structs are designed to be simple and efficient, usually allocated on the stack rather than the heap.

## 3. Data-Focused

>Structs primarily hold data, though they can have simple methods in some languages.

## 4. No Inheritance

>Structs typically don't support inheritance hierarchies like [[Classes]] do.

# Structs in C

C is where structs originated. They're purely data containers with no methods.

``` C
#include <stdio.h>
#include <string.h>

// Defining a struct
struct Point {
    double x;
    double y;
};

// Struct with different data types
struct Person {
    char name[50];
    int age;
    double height;
};

// Struct containing another struct
struct Rectangle {
    struct Point topLeft;
    struct Point bottomRight;
};

int main() {
    // Creating struct instances
    struct Point p1;
    p1.x = 10.5;
    p1.y = 20.3;
    
    // Creating and initializing in one line
    struct Point p2 = {15.0, 25.0};
    
    // Creating a person
    struct Person john;
    strcpy(john.name, "John Doe");
    john.age = 30;
    john.height = 5.9;
    
    // Accessing struct members
    printf("Point 1: (%.2f, %.2f)\n", p1.x, p1.y);
    printf("Person: %s, Age: %d, Height: %.2f\n", 
           john.name, john.age, john.height);
    
    // Structs are copied (value semantics)
    struct Point p3 = p1;  // p3 is a COPY of p1
    p3.x = 100.0;          // Changing p3 doesn't affect p1
    
    printf("p1.x = %.2f\n", p1.x);  // Still 10.5
    printf("p3.x = %.2f\n", p3.x);  // Now 100.0
    
    // Nested struct
    struct Rectangle rect;
    rect.topLeft.x = 0.0;
    rect.topLeft.y = 10.0;
    rect.bottomRight.x = 20.0;
    rect.bottomRight.y = 0.0;
    
    return 0;
}
```

## Using typedef

`typedef` creates an alias so you don't have to write `struct` every time:

``` C
// Define struct with typedef
typedef struct {
    int red;
    int green;
    int blue;
} Color;

// Now you can use it without the 'struct' keyword
Color background = {255, 255, 255};  // White
Color text = {0, 0, 0};               // Black

printf("Background: RGB(%d, %d, %d)\n", 
       background.red, background.green, background.blue);
```

# Scructs in C++

C++ structs can have [[methods]], [[constructors]], and are very similar to [[classes]]. The main difference is that struct members are public by default, while class members are private by default.

``` cpp
#include <iostream>
#include <cmath>
using namespace std;

// Simple struct
struct Point {
    double x;
    double y;
    
    // Constructor
    Point(double xVal, double yVal) : x(xVal), y(yVal) {}
    
    // Method to calculate distance from origin
    double distanceFromOrigin() {
        return sqrt(x * x + y * y);
    }
    
    // Method to calculate distance to another point
    double distanceTo(Point other) {
        double dx = x - other.x;
        double dy = y - other.y;
        return sqrt(dx * dx + dy * dy);
    }
    
    // Method to display point
    void display() {
        cout << "(" << x << ", " << y << ")" << endl;
    }
};

// Struct for storing RGB color
struct Color {
    unsigned char r, g, b;
    
    // Default constructor
    Color() : r(0), g(0), b(0) {}
    
    // Parameterized constructor
    Color(unsigned char red, unsigned char green, unsigned char blue) 
        : r(red), g(green), b(blue) {}
    
    void print() {
        cout << "RGB(" << (int)r << ", " << (int)g << ", " << (int)b << ")" << endl;
    }
};

// Struct for a student record
struct Student {
    string name;
    int id;
    double gpa;
    
    // Check if student is on honor roll
    bool isHonorRoll() {
        return gpa >= 3.5;
    }
};

int main() {
    // Using Point struct
    Point p1(3.0, 4.0);
    Point p2(6.0, 8.0);
    
    p1.display();
    cout << "Distance from origin: " << p1.distanceFromOrigin() << endl;
    cout << "Distance to p2: " << p1.distanceTo(p2) << endl;
    
    // Using Color struct
    Color red(255, 0, 0);
    Color blue(0, 0, 255);
    
    red.print();
    blue.print();
    
    // Using Student struct
    Student alice = {"Alice Johnson", 12345, 3.8};
    
    cout << "Student: " << alice.name << endl;
    cout << "ID: " << alice.id << endl;
    cout << "GPA: " << alice.gpa << endl;
    cout << "Honor Roll: " << (alice.isHonorRoll() ? "Yes" : "No") << endl;
    
    // Value semantics - copying
    Student bob = alice;  // bob is a COPY
    bob.name = "Bob Smith";
    bob.id = 67890;
    
    // alice is unchanged
    cout << "Alice: " << alice.name << endl;  // Still "Alice Johnson"
    cout << "Bob: " << bob.name << endl;      // "Bob Smith"
    
    return 0;
}
```

# Structs in C-Sharp

C# structs are value types that live on the stack. They're perfect for small, frequently-used data structures.

``` csharp
using System;

// Simple struct for 2D coordinates
public struct Point {
    public double X;
    public double Y;
    
    // Constructor
    public Point(double x, double y) {
        X = x;
        Y = y;
    }
    
    // Method
    public double DistanceFromOrigin() {
        return Math.Sqrt(X * X + Y * Y);
    }
    
    // Override ToString for nice output
    public override string ToString() {
        return $"({X}, {Y})";
    }
}

// Struct for RGB color with validation
public struct Color {
    private byte r, g, b;
    
    public byte R {
        get { return r; }
        set { r = value; }
    }
    
    public byte G {
        get { return g; }
        set { g = value; }
    }
    
    public byte B {
        get { return b; }
        set { b = value; }
    }
    
    public Color(byte red, byte green, byte blue) {
        r = red;
        g = green;
        b = blue;
    }
    
    public override string ToString() {
        return $"RGB({r}, {g}, {b})";
    }
}

// Struct for date and time (simplified)
public struct DateTime {
    public int Year;
    public int Month;
    public int Day;
    public int Hour;
    public int Minute;
    
    public DateTime(int year, int month, int day, int hour, int minute) {
        Year = year;
        Month = month;
        Day = day;
        Hour = hour;
        Minute = minute;
    }
    
    public bool IsWeekend() {
        // Simplified - would need actual day of week calculation
        return false;
    }
    
    public override string ToString() {
        return $"{Year}-{Month:D2}-{Day:D2} {Hour:D2}:{Minute:D2}";
    }
}

class Program {
    static void Main() {
        // Creating struct instances
        Point p1 = new Point(3.0, 4.0);
        Point p2 = new Point(0.0, 0.0);
        
        Console.WriteLine($"Point 1: {p1}");
        Console.WriteLine($"Distance: {p1.DistanceFromOrigin()}");
        
        // Value semantics - structs are COPIED
        Point p3 = p1;  // p3 is a copy of p1
        p3.X = 100;     // Changing p3 doesn't affect p1
        
        Console.WriteLine($"p1.X = {p1.X}");  // Still 3.0
        Console.WriteLine($"p3.X = {p3.X}");  // Now 100.0
        
        // Color struct
        Color red = new Color(255, 0, 0);
        Color blue = new Color(0, 0, 255);
        
        Console.WriteLine($"Red: {red}");
        Console.WriteLine($"Blue: {blue}");
        
        // DateTime struct
        DateTime meeting = new DateTime(2024, 12, 25, 14, 30);
        Console.WriteLine($"Meeting: {meeting}");
    }
}
```

# Structs in Go

Go structs are the primary way to create composite data types. Go doesn't have classes—it uses structs with methods.

``` go
package main

import (
    "fmt"
    "math"
)

// Define a struct
type Point struct {
    X float64
    Y float64
}

// Method on a struct (value receiver)
func (p Point) DistanceFromOrigin() float64 {
    return math.Sqrt(p.X*p.X + p.Y*p.Y)
}

// Method with pointer receiver (can modify the struct)
func (p *Point) Move(dx, dy float64) {
    p.X += dx
    p.Y += dy
}

// Struct with different field types
type Person struct {
    Name    string
    Age     int
    Email   string
    IsAdmin bool
}

// Method on Person
func (p Person) Greet() string {
    return fmt.Sprintf("Hello, I'm %s and I'm %d years old", p.Name, p.Age)
}

// Nested struct
type Address struct {
    Street  string
    City    string
    Country string
}

type Employee struct {
    Name    string
    ID      int
    Address Address  // Embedded struct
}

func main() {
    // Creating struct instances
    p1 := Point{X: 3.0, Y: 4.0}
    p2 := Point{5.0, 12.0}  // Can omit field names if in order
    
    fmt.Printf("Point 1: (%.2f, %.2f)\n", p1.X, p1.Y)
    fmt.Printf("Distance: %.2f\n", p1.DistanceFromOrigin())
    
    // Using pointer receiver method
    p1.Move(1.0, 1.0)
    fmt.Printf("After move: (%.2f, %.2f)\n", p1.X, p1.Y)
    
    // Person struct
    person := Person{
        Name:    "Alice",
        Age:     30,
        Email:   "alice@example.com",
        IsAdmin: false,
    }
    
    fmt.Println(person.Greet())
    
    // Nested struct
    emp := Employee{
        Name: "Bob",
        ID:   12345,
        Address: Address{
            Street:  "123 Main St",
            City:    "New York",
            Country: "USA",
        },
    }
    
    fmt.Printf("%s lives in %s, %s\n", 
        emp.Name, emp.Address.City, emp.Address.Country)
    
    // Struct comparison (if all fields are comparable)
    p3 := Point{3.0, 4.0}
    p4 := Point{3.0, 4.0}
    fmt.Printf("p3 == p4: %v\n", p3 == p4)  // true
}
```

# Value Semantics vs Reference Semantics

## Value Semantics

Structs in C, C#, GO

``` csharp
// C# example
struct Point {
    public int X;
    public int Y;
}

Point p1 = new Point { X = 10, Y = 20 };
Point p2 = p1;  // p2 is a COPY of p1

p2.X = 100;     // Change p2

Console.WriteLine(p1.X);  // 10 (unchanged!)
Console.WriteLine(p2.X);  // 100

// When you pass structs to functions, they're copied
void ModifyPoint(Point p) {
    p.X = 999;  // Modifies the COPY, not the original
}

ModifyPoint(p1);
Console.WriteLine(p1.X);  // Still 10!
```

## Reference Semantics

Classes in most languages

``` csharp
// C# class for comparison
class PointClass {
    public int X;
    public int Y;
}

PointClass p1 = new PointClass { X = 10, Y = 20 };
PointClass p2 = p1;  // p2 REFERENCES the same object as p1

p2.X = 100;     // Change through p2

Console.WriteLine(p1.X);  // 100 (changed!)
Console.WriteLine(p2.X);  // 100 (same object)
```

# Java [[Records]]

Since [[Java]] doesn't have structs, it introduced **[[Records]]** as a concise way to create simple data carriers

``` java
// Java Record - similar concept to struct
public record Point(double x, double y) {
    // Automatically generates:
    // - Constructor: Point(double x, double y)
    // - Getters: x() and y()
    // - equals(), hashCode(), toString()
    
    // You can add custom methods
    public double distanceFromOrigin() {
        return Math.sqrt(x * x + y * y);
    }
}

// Using the record
Point p1 = new Point(3.0, 4.0);
Point p2 = new Point(3.0, 4.0);

System.out.println(p1.x());  // Getter method
System.out.println(p1.y());
System.out.println(p1.distanceFromOrigin());

// Records are immutable
// p1.x = 10;  // ERROR! Cannot modify

// Records have automatic equals
System.out.println(p1.equals(p2));  // true

// More complex record
public record Person(String name, int age, String email) {
    // Compact constructor for validation
    public Person {
        if (age < 0) {
            throw new IllegalArgumentException("Age cannot be negative");
        }
    }
    
    public boolean isAdult() {
        return age >= 18;
    }
}

Person alice = new Person("Alice", 25, "alice@example.com");
System.out.println(alice.name());     // "Alice"
System.out.println(alice.isAdult());  // true
```

# Java Simple Classes

Before records, Java used simple "data classes":

``` java
// Traditional Java approach - simple data class
public class Point {
    private final double x;  // immutable
    private final double y;
    
    public Point(double x, double y) {
        this.x = x;
        this.y = y;
    }
    
    public double getX() {
        return x;
    }
    
    public double getY() {
        return y;
    }
    
    public double distanceFromOrigin() {
        return Math.sqrt(x * x + y * y);
    }
    
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Point other = (Point) obj;
        return Double.compare(x, other.x) == 0 && 
               Double.compare(y, other.y) == 0;
    }
    
    @Override
    public int hashCode() {
        return Objects.hash(x, y);
    }
    
    @Override
    public String toString() {
        return "Point(" + x + ", " + y + ")";
    }
}
```


# Struct vs [[Classes]] 

|Feature|Struct|Class|
|---|---|---|
|**Primary Purpose**|Data container|Data + behavior|
|**Semantics**|Usually value (copied)|Usually reference|
|**Memory**|Stack (often)|Heap|
|**Inheritance**|Limited or none|Full support|
|**Size**|Small, lightweight|Can be large|
|**Mutability**|Often immutable|Often mutable|
|**Use Case**|Simple data (Point, Color)|Complex entities (Person, BankAccount)|


#programming #structs #data-structures #value-types #C #Cpp #Csharp #Go #java-records #fundamentals #memory-management #OOP