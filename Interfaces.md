# What is an Interface

An interface is a contract that defines **what** [[Classes]] must do, without specifying **how** it should do it. 

>It's a blueprint of [[methods]] that implementing [[Classes]] must provide. Interfaces define capabilities or behaviors that classes can adopt, promoting loose coupling and enabling [[polymorphism]].

Think of an interface as a promise: "Any class that implements me **must** provide these specific methods."

#  Basic Interface Syntax

``` java
// Define an interface
public interface Drawable {
    // Abstract methods (no implementation)
    void draw();
    void resize(int width, int height);
    String getDescription();
}

// Class implementing the interface
public class Circle implements Drawable {
    private int x, y, radius;
    
    public Circle(int x, int y, int radius) {
        this.x = x;
        this.y = y;
        this.radius = radius;
    }
    
    // MUST implement ALL interface methods
    @Override
    public void draw() {
        System.out.println("Drawing circle at (" + x + "," + y + 
                         ") with radius " + radius);
    }
    
    @Override
    public void resize(int width, int height) {
        // For a circle, use average as new radius
        radius = (width + height) / 4;
    }
    
    @Override
    public String getDescription() {
        return "Circle with radius " + radius;
    }
    
    // Can have additional methods not in the interface
    public double getArea() {
        return Math.PI * radius * radius;
    }
}

// Another class implementing the same interface
public class Rectangle implements Drawable {
    private int x, y, width, height;
    
    public Rectangle(int x, int y, int width, int height) {
        this.x = x;
        this.y = y;
        this.width = width;
        this.height = height;
    }
    
    @Override
    public void draw() {
        System.out.println("Drawing rectangle at (" + x + "," + y + 
                         ") size " + width + "x" + height);
    }
    
    @Override
    public void resize(int width, int height) {
        this.width = width;
        this.height = height;
    }
    
    @Override
    public String getDescription() {
        return "Rectangle " + width + "x" + height;
    }
}

// Using the interface
public class Main {
    public static void main(String[] args) {
        // Polymorphism - interface reference, different implementations
        Drawable shape1 = new Circle(10, 20, 5);
        Drawable shape2 = new Rectangle(0, 0, 100, 50);
        
        // Same method calls work for both!
        shape1.draw();
        shape2.draw();
        
        // Treating different objects uniformly
        Drawable[] shapes = {shape1, shape2};
        for (Drawable shape : shapes) {
            System.out.println(shape.getDescription());
            shape.resize(20, 20);
            shape.draw();
        }
    }
}
```

# Why Interfaces Matter

## 1. [[Polymorphism]]

Different [[Classes]] can be treated the same way through their common interface:

``` java
public interface PaymentMethod {
    boolean processPayment(double amount);
    String getPaymentType();
}

public class CreditCard implements PaymentMethod {
    private String cardNumber;
    
    @Override
    public boolean processPayment(double amount) {
        System.out.println("Processing $" + amount + " via Credit Card");
        // Credit card processing logic
        return true;
    }
    
    @Override
    public String getPaymentType() {
        return "Credit Card";
    }
}

public class PayPal implements PaymentMethod {
    private String email;
    
    @Override
    public boolean processPayment(double amount) {
        System.out.println("Processing $" + amount + " via PayPal");
        // PayPal processing logic
        return true;
    }
    
    @Override
    public String getPaymentType() {
        return "PayPal";
    }
}

public class Cryptocurrency implements PaymentMethod {
    private String walletAddress;
    
    @Override
    public boolean processPayment(double amount) {
        System.out.println("Processing $" + amount + " via Crypto");
        // Cryptocurrency processing logic
        return true;
    }
    
    @Override
    public String getPaymentType() {
        return "Cryptocurrency";
    }
}

// The power of interfaces - one method works with ALL payment types!
public class ShoppingCart {
    public void checkout(PaymentMethod payment, double amount) {
        System.out.println("Processing payment with: " + payment.getPaymentType());
        
        if (payment.processPayment(amount)) {
            System.out.println("Payment successful!");
        } else {
            System.out.println("Payment failed!");
        }
    }
}

// Usage
ShoppingCart cart = new ShoppingCart();
cart.checkout(new CreditCard("1234-5678"), 99.99);
cart.checkout(new PayPal("user@example.com"), 49.99);
cart.checkout(new Cryptocurrency("0xABC123"), 199.99);
```

## 2. Loose Coupling

Code depends on interfaces, not concrete implementations:

``` java
// BAD - tightly coupled to specific class
public class EmailService {
    private MySQLDatabase database;  // Depends on specific implementation
    
    public void sendEmail(String email) {
        database.saveEmail(email);
    }
}

// GOOD - loosely coupled to interface
public interface Database {
    void save(String data);
    String retrieve(String id);
}

public class EmailService {
    private Database database;  // Depends on interface, not implementation
    
    public EmailService(Database database) {
        this.database = database;
    }
    
    public void sendEmail(String email) {
        database.save(email);
    }
}

// Can easily swap implementations
Database mysql = new MySQLDatabase();
Database mongo = new MongoDatabase();
Database postgres = new PostgresDatabase();

EmailService service1 = new EmailService(mysql);
EmailService service2 = new EmailService(mongo);
EmailService service3 = new EmailService(postgres);
```

## 3. Multiple Inheritance of Behaviour

A class can implement multiple interfaces (but can only extend one class):

``` java
public interface Flyable {
    void fly();
    void land();
}

public interface Swimmable {
    void swim();
}

public interface Eatable {
    int getCalories();
    String getTaste();
}

// A duck can fly AND swim
public class Duck implements Flyable, Swimmable {
    @Override
    public void fly() {
        System.out.println("Duck is flying");
    }
    
    @Override
    public void land() {
        System.out.println("Duck is landing");
    }
    
    @Override
    public void swim() {
        System.out.println("Duck is swimming");
    }
}

// A fish can only swim
public class Fish implements Swimmable {
    @Override
    public void swim() {
        System.out.println("Fish is swimming");
    }
}

// A chicken can be eaten but can't really fly
public class Chicken implements Eatable {
    @Override
    public int getCalories() {
        return 239;
    }
    
    @Override
    public String getTaste() {
        return "Delicious!";
    }
}

// Usage
Duck duck = new Duck();
duck.fly();    // Has flying capability
duck.swim();   // Also has swimming capability

Fish fish = new Fish();
fish.swim();   // Only has swimming capability
// fish.fly(); // ERROR! Fish doesn't implement Flyable
```

# Interface Features In Java

## Constants

All fields in interfaces are automatically `public static final` (constants):

``` java
public interface MathConstants {
    double PI = 3.14159265359;           // public static final (automatic)
    double E = 2.71828182846;
    int MAX_ITERATIONS = 1000;
}

// Usage
System.out.println(MathConstants.PI);
System.out.println(MathConstants.E);
```

## Default Methods

Interfaces can have default implementations that implementing classes can use or override:

``` java
public interface Vehicle {
    // Abstract methods (must be implemented)
    void start();
    void stop();
    
    // Default method (can be overridden, but doesn't have to be)
    default void honk() {
        System.out.println("Beep beep!");
    }
    
    default void displayInfo() {
        System.out.println("This is a vehicle");
    }
}

public class Car implements Vehicle {
    @Override
    public void start() {
        System.out.println("Car engine starting...");
    }
    
    @Override
    public void stop() {
        System.out.println("Car engine stopping...");
    }
    
    // Using default honk() - no need to override
    // But we CAN override if we want different behavior
    @Override
    public void honk() {
        System.out.println("Car horn: HONK HONK!");
    }
}

public class Bicycle implements Vehicle {
    @Override
    public void start() {
        System.out.println("Pedaling...");
    }
    
    @Override
    public void stop() {
        System.out.println("Braking...");
    }
    
    // Using default honk() without overriding
}

// Usage
Car car = new Car();
car.honk();  // "Car horn: HONK HONK!" (overridden)

Bicycle bike = new Bicycle();
bike.honk(); // "Beep beep!" (default implementation)
```

## Static Methods

Interfaces can have static Ultility methods:

``` java
public interface StringUtils {
    // Abstract method
    String transform(String input);
    
    // Static method
    static boolean isEmpty(String str) {
        return str == null || str.trim().isEmpty();
    }
    
    static String reverse(String str) {
        if (isEmpty(str)) return "";
        return new StringBuilder(str).reverse().toString();
    }
    
    static int countWords(String str) {
        if (isEmpty(str)) return 0;
        return str.trim().split("\\s+").length;
    }
}

// Usage - call static methods on the interface
boolean empty = StringUtils.isEmpty("   ");
String reversed = StringUtils.reverse("Hello");
int words = StringUtils.countWords("Hello World Java");

System.out.println(empty);     // true
System.out.println(reversed);  // "olleH"
System.out.println(words);     // 3
```

## Private Methods

Interfaces can have private helper methods:

``` java
public interface Logger {
    default void logInfo(String message) {
        log("INFO", message);
    }
    
    default void logError(String message) {
        log("ERROR", message);
    }
    
    default void logWarning(String message) {
        log("WARNING", message);
    }
    
    // Private helper method - reduces code duplication
    private void log(String level, String message) {
        System.out.println("[" + level + "] " + 
                         java.time.LocalDateTime.now() + 
                         ": " + message);
    }
}
```

# Interface Inheritance

Interfaces can extend other interfaces:

``` java
public interface Animal {
    void eat();
    void sleep();
}

public interface Mammal extends Animal {
    void giveBirth();
    void produceMilk();
}

public interface Flyer {
    void fly();
}

// Can extend multiple interfaces
public interface Bat extends Mammal, Flyer {
    void useEcholocation();
}

// Class implementing the extended interface must implement ALL methods
public class FruitBat implements Bat {
    @Override
    public void eat() {
        System.out.println("Eating fruits");
    }
    
    @Override
    public void sleep() {
        System.out.println("Sleeping upside down");
    }
    
    @Override
    public void giveBirth() {
        System.out.println("Giving birth to live young");
    }
    
    @Override
    public void produceMilk() {
        System.out.println("Producing milk");
    }
    
    @Override
    public void fly() {
        System.out.println("Flying with wings");
    }
    
    @Override
    public void useEcholocation() {
        System.out.println("Using echolocation to navigate");
    }
}
```

# Functional Interfaces

Interfaces with exactly one abstract method, used with lambda expressions:

``` java
@FunctionalInterface
public interface Calculator {
    int calculate(int a, int b);
}

// Usage with lambda expressions
Calculator add = (a, b) -> a + b;
Calculator multiply = (a, b) -> a * b;
Calculator subtract = (a, b) -> a - b;

System.out.println(add.calculate(5, 3));       // 8
System.out.println(multiply.calculate(5, 3));  // 15
System.out.println(subtract.calculate(5, 3));  // 2

// Built-in functional interfaces
// Predicate<T> - tests a condition
Predicate<String> isEmpty = s -> s.isEmpty();
System.out.println(isEmpty.test(""));      // true
System.out.println(isEmpty.test("hello")); // false

// Function<T, R> - transforms input to output
Function<String, Integer> length = s -> s.length();
System.out.println(length.apply("Hello")); // 5

// Consumer<T> - performs action on input
Consumer<String> printer = s -> System.out.println(s);
printer.accept("Hello World");

// Supplier<T> - provides a value
Supplier<Double> randomValue = () -> Math.random();
System.out.println(randomValue.get());
```


# Interface vs Abstract Class

| Feature                  | Interface                     | Abstract Class              |
| ------------------------ | ----------------------------- | --------------------------- |
| **Multiple inheritance** | Yes (can implement many)      | No (can extend only one)    |
| **Fields**               | Only constants (static final) | Can have instance variables |
| **Methods**              | Abstract + default + static   | Abstract + concrete         |
| **Constructor**          | No                            | Yes                         |
| **Access modifiers**     | Methods public by default     | Any access modifier         |
| **Purpose**              | Define contract/capability    | Share common code           |
| **When to use**          | "Can do" relationship         | "Is a" relationship         |

# Best Practices

## 1. Keep Interfaces Focused

``` java
// GOOD - focused interface
interface Readable {
    String read();
}

// GOOD - focused interface
interface Writable {
    void write(String data);
}

// BAD - too many responsibilities
interface FileOperations {
    String read();
    void write(String data);
    void delete();
    void copy(String destination);
    void move(String destination);
    void compress();
    void encrypt();
}
```

## 2. Use interface Segregation Principle

``` java
// BAD - clients forced to implement methods they don't need
interface Worker {
    void work();
    void eat();
    void sleep();
}

// GOOD - segregated interfaces
interface Workable {
    void work();
}

interface Eater {
    void eat();
}

interface Sleeper {
    void sleep();
}

// Now classes can implement only what they need
class Robot implements Workable {
    @Override
    public void work() {
        System.out.println("Robot working");
    }
    // Doesn't need eat() or sleep()
}

class Human implements Workable, Eater, Sleeper {
    @Override
    public void work() {
        System.out.println("Human working");
    }
    
    @Override
    public void eat() {
        System.out.println("Human eating");
    }
    
    @Override
    public void sleep() {
        System.out.println("Human sleeping");
    }
}
```

## Program to Interfaces, Not Implementations

``` java
// BAD - depends on concrete class
ArrayList<String> names = new ArrayList<>();

// GOOD - depends on interface
List<String> names = new ArrayList<>();
// Can easily change to: LinkedList, Vector, etc.
```

## Use Meaningful Names

``` java
// GOOD
interface Serializable { }
interface Comparable<T> { }
interface Runnable { }
interface Closeable { }

// Convention: -able suffix for capabilities
interface Drawable { }
interface Printable { }
interface Sortable { }
```

# Common [[Java]] Interfaces

**Collections Framework:**

- `List`, `Set`, `Map`
- `Collection`, `Iterator`

**I/O:**

- `Closeable`, `Serializable`

**Concurrency:**

- `Runnable`, `Callable`, `Future`

**Comparison:**

- `Comparable<T>`, `Comparator<T>`

**Functional:**

- `Predicate<T>`, `Function<T,R>`, `Consumer<T>`, `Supplier<T>`


#java #programming #interfaces #OOP #polymorphism #abstraction #design-patterns #SOLID #loose-coupling #contracts #fundamentals