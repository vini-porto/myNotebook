# What are classes?

A class is a blueprint or template for creating objects. It defines what data [[objects]] will hold and what actions the object can perform.

## Analogy

- **The Blueprint** (class): A detailed plan showing rooms, dimensions, features, and how everything works
- **Actual Houses** (objects): Individual houses built from that blueprint

> From one blueprint, you can build many houses. Each house has the same design (number of rooms, layout) but different details (different paint colors, furniture, residents).

# Core components of a Class

## Fields

Fields store the state/data of an object. Each object created from the class has its own copy of these fields.

``` java
public class Person {
    // Fields - the data each Person object will have
    private String name;
    private int age;
    private String email;
    private boolean isEmployed;
    
    // Each Person object will have their OWN name, age, email, employed status
}
```

## Constructors

Constructors are special methods that initialize new objects. They run automatically when you create an object using `new`.

``` java
public class Person {
    private String name;
    private int age;
    private String email;
    
    // Constructor - called when creating new Person objects
    public Person(String name, int age, String email) {
        this.name = name;      // 'this' refers to the current object
        this.age = age;
        this.email = email;
    }
    
    // You can have multiple constructors (constructor overloading)
    public Person(String name) {
        this.name = name;
        this.age = 0;          // Default values
        this.email = "";
    }
    
    // Default constructor (no parameters)
    public Person() {
        this.name = "Unknown";
        this.age = 0;
        this.email = "";
    }
}

// Using constructors
Person person1 = new Person("Alice", 25, "alice@email.com");
Person person2 = new Person("Bob");
Person person3 = new Person();
```

## Methods

Methods define what objects can do—their behaviors and actions.

``` java
public class Person {
    private String name;
    private int age;
    private String email;
    
    public Person(String name, int age, String email) {
        this.name = name;
        this.age = age;
        this.email = email;
    }
    
    // Method - an action this object can perform
    public void introduce() {
        System.out.println("Hi, I'm " + name + " and I'm " + age + " years old.");
    }
    
    // Method that modifies object state
    public void celebrateBirthday() {
        age++;
        System.out.println("Happy birthday! Now " + age + " years old.");
    }
    
    // Method that returns a value
    public boolean isAdult() {
        return age >= 18;
    }
    
    // Method with parameters
    public void sendEmail(String message) {
        System.out.println("Sending email to " + email + ": " + message);
    }
}

// Using methods
Person alice = new Person("Alice", 25, "alice@email.com");
alice.introduce();              // "Hi, I'm Alice and I'm 25 years old."
alice.celebrateBirthday();      // "Happy birthday! Now 26 years old."
boolean adult = alice.isAdult(); // true
alice.sendEmail("Hello!");       // "Sending email to alice@email.com: Hello!"
```

## Getters and Setters

These special methods control access to private fields, following the principle of encapsulation.

``` java
public class BankAccount {
    private double balance;  // Private - cannot be accessed directly
    private String accountNumber;
    
    public BankAccount(String accountNumber, double initialBalance) {
        this.accountNumber = accountNumber;
        this.balance = initialBalance;
    }
    
    // Getter - allows reading the value
    public double getBalance() {
        return balance;
    }
    
    // Getter for account number
    public String getAccountNumber() {
        return accountNumber;
    }
    
    // Setter - allows changing the value with validation
    public void setBalance(double newBalance) {
        if (newBalance >= 0) {  // Validation!
            balance = newBalance;
        } else {
            System.out.println("Balance cannot be negative!");
        }
    }
    
    // Better approach: specific methods instead of direct setters
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
        }
    }
    
    public boolean withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            return true;
        }
        return false;
    }
}

// Using getters and setters
BankAccount account = new BankAccount("ACC123", 1000);
double currentBalance = account.getBalance();  // Read balance
// account.balance = 5000;  // ERROR! Cannot access private field directly
account.deposit(500);       // Controlled way to modify balance
```

# Access Modifiers

Access modifiers control who can see and use different parts of your class.

``` java
public class Example {
    // PUBLIC - accessible from anywhere
    public String publicField = "Everyone can see me";
    
    // PRIVATE - only accessible within this class
    private String privateField = "Only Example class can see me";
    
    // PROTECTED - accessible within same package and subclasses
    protected String protectedField = "Subclasses can see me";
    
    // DEFAULT (no modifier) - accessible within same package
    String defaultField = "Same package can see me";
    
    public void publicMethod() {
        // Anyone can call this
    }
    
    private void privateMethod() {
        // Only methods within this class can call this
    }
}
```

# `this` Keyword

`this` refers to the current object—the object whose method is being called.

``` java
public class Student {
    private String name;
    private int grade;
    
    public Student(String name, int grade) {
        this.name = name;    // 'this.name' is the field, 'name' is the parameter
        this.grade = grade;
    }
    
    public void printInfo() {
        // 'this' refers to the current Student object
        System.out.println("Name: " + this.name);
        System.out.println("Grade: " + this.grade);
    }
    
    public Student getCopy() {
        // Return a new Student with the same data as this one
        return new Student(this.name, this.grade);
    }
    
    public boolean isOlderThan(Student other) {
        return this.grade > other.grade;
    }
}
```

# Static vs Instance Members

- **Instance variable** - each object has its own copy
- **Static variable** - shared by ALL objects

``` java
public class Counter {
    // Instance variable - each object has its own copy
    private int instanceCount = 0;
    
    // Static variable - shared by ALL objects
    private static int totalCount = 0;
    
    public void increment() {
        instanceCount++;     // This object's counter
        totalCount++;        // Global counter for all objects
    }
    
    public void showCounts() {
        System.out.println("This object's count: " + instanceCount);
        System.out.println("Total count (all objects): " + totalCount);
    }
    
    // Static method - called on the class, not an object
    public static int getTotalCount() {
        return totalCount;
        // return instanceCount;  // ERROR! Cannot access instance variable
    }
}

// Using static vs instance
Counter c1 = new Counter();
Counter c2 = new Counter();

c1.increment();  // c1: instance=1, total=1
c1.increment();  // c1: instance=2, total=2
c2.increment();  // c2: instance=1, total=3

c1.showCounts();  // This object's count: 2, Total: 3
c2.showCounts();  // This object's count: 1, Total: 3

// Static method called on class
int total = Counter.getTotalCount();  // 3
```

# Key Principles

## Encapsulation

Hide Internal details and provide controlled access.

``` java
public class TemperatureSensor {
    private double temperature;
    
    // Don't let users set temperature directly
    // private means it's hidden
    
    public double getTemperature() {
        return temperature;
    }
    
    // Only the sensor itself should update temperature
    private void updateReading() {
        // Read from actual sensor hardware
        temperature = readFromSensor();
    }
}
```

## Single Responsibility

Each class should have one clear purpose.

``` java
// GOOD - each class has one job
class User {
    // Manages user data
}

class UserRepository {
    // Handles database operations
}

class EmailService {
    // Sends emails
}

// BAD - class doing too many things
class User {
    // User data + database operations + email sending
    // Too much responsibility!
}
```

## DRY (Don't Repeat Yourself)

Use methods to avoid code duplication.

``` java
public class Circle {
    private double radius;
    
    // Instead of calculating area everywhere, make it a method
    public double getArea() {
        return Math.PI * radius * radius;
    }
    
    public double getCircumference() {
        return 2 * Math.PI * radius;
    }
}
```


#java #programming #OOP #classes #objects #encapsulation #constructors #methods #fundamentals #design-patterns