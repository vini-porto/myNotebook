# What Is a Type Definition?

A type definition is a declaration that creates a new data type or describes the structure and behavior of data in your program. 

It tells the [[compiler]] what kind of data a [[variable]] can hold, what operations can be performed on it, and how much memory to allocate for it. 

## Analogy

Imagine you're designing forms for different purposes:

- **Driver's License Form**: Has specific fields like name, date of birth, license number, photo, expiration date
- **Passport Form** : Has different fields like passport number, nationality, issue date, photo
- **Library Card Form**: Has fields like member ID, name, address, borrowed books

>In programming, a type definition works the same way: you define what data belongs to a type, then create instances ([[objects]] or [[variables]]) of that type.

# Why Type Definitions Matter

1. **Data Organization:** Groups related data together logically 
2. **Type Safety:** Prevents errors by ensuring you use data correctly 
3. **Code Clarity:** Makes it clear what kind of data you're working with 
4. **Reusability:** Define once, use many times 
5. **Documentation:** The type definition itself documents what data structure looks like

# General Concepts Across Languages

1. **Primitive Types** (built-in): `int`, `float`, `boolean`, `char` 
2. **Composite Types:** Arrays, structures, records 
3. **User-Defined Types:** [[Classes]], [[Structs]], [[Enums]], [[Interfaces]]
4. **Type Aliases:** Alternative names for existing types

# Type Definition in [[Java]]

[[Java]] is a **statically-typed** language, meaning you must declare types explicitly and they're checked at compile time. 

## 1. Class Definitions
![[Classes#Core components of a Class]]

## 2. [[Interfaces]] Definition

>[!NOTE]
> Interfaces define a contract, what methods a type must implement:

![[Interfaces#Basic Interface Syntax]]

## 3. [[Enums]] Definitions

>[!NOTE]
>Enums define a type with a fixed set of constants:

![[Enums#Why Enums Matter]]

## 4. Abstract Class Definitions

>[!NOTE]
>Anstract [[classes]] define partial type definitions that must be completed by [[subclasses]]:

``` java
// Defining an abstract type
public abstract class Animal {
    protected String name;
    
    public Animal(String name) {
        this.name = name;
    }
    
    // Concrete method (implemented)
    public void sleep() {
        System.out.println(name + " is sleeping");
    }
    
    // Abstract method (must be implemented by subclasses)
    public abstract void makeSound();
}

// Extending the abstract class
public class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }
    
    @Override
    public void makeSound() {
        System.out.println(name + " says: Woof!");
    }
}

public class Cat extends Animal {
    public Cat(String name) {
        super(name);
    }
    
    @Override
    public void makeSound() {
        System.out.println(name + " says: Meow!");
    }
}

// Using the types
public class Main {
    public static void main(String[] args) {
        Animal dog = new Dog("Buddy");
        Animal cat = new Cat("Whiskers");
        
        dog.makeSound();  // "Buddy says: Woof!"
        cat.makeSound();  // "Whiskers says: Meow!"
    }
}
```

## Generic Type Definitions

Generics allow you to define types that work with different data types:

``` java
// Defining a generic type
public class Box<T> {
    private T content;
    
    public void set(T content) {
        this.content = content;
    }
    
    public T get() {
        return content;
    }
}

// Using the generic type
public class Main {
    public static void main(String[] args) {
        // Box of Strings
        Box<String> stringBox = new Box<>();
        stringBox.set("Hello");
        String message = stringBox.get();
        
        // Box of Integers
        Box<Integer> intBox = new Box<>();
        intBox.set(42);
        int number = intBox.get();
        
        // Box of custom types
        Box<Book> bookBox = new Box<>();
        bookBox.set(new Book("Java Guide", "Author", 300, 29.99));
    }
}
```

# How Type Definitions Work in Java

1. **Definition** You define a new type using `class`, `interface`, `enum`, or `abstract class`.

2. **Compilation** The Java [[compiler]] reads your type definition and creates [[bytecode]] that describes the structure.

3. **Instantiation** You create instances (objects) of your type using the `new` keyword.

4. **Type Checking** The compiler ensures you only use variables and methods that exist for that type.

``` java
Book myBook = new Book("Title", "Author", 200, 19.99);
myBook.displayInfo();  // ✓ Allowed - method exists
myBook.fly();          // ✗ Compile error - Book doesn't have fly() method
```

# Primitive vs Reference Types in Java

## Primitive Type

>built-in, not objects

```java
int number = 42;
double price = 19.99;
boolean isActive = true;
char letter = 'A';
```

## Reference Type

>[[Objects]], defined by [[Classes]]

```java
String name = new String("Alice");
Book book = new Book("Title", "Author", 300, 29.99);
ArrayList<Integer> numbers = new ArrayList<>();
```

# Type Definition vs Type Declaration
## Type Definition

>Creating a new type

```java
public class Student {  // Defining what a Student is
    String name;
    int grade;
}
```

## Type Declaration

>Declaring [[variables]] of a type

```java
Student alice;  // Declaring alice is of type Student
alice = new Student();  // Creating an instance
```

# Best Practices

- **Use meaningful names**: `Customer` not `C` or `Data`
- **Single Responsibility**: Each type should have one clear purpose
- **Encapsulation**: Use `private` fields with `public` getters/setters
- **Follow conventions**: Class names in PascalCase (`BookStore`)
- **Keep it simple**: Don't create overly complex type hierarchies
- **Document your types**: Use comments to explain what the type represents


#java #programming #types #data-types #OOP #classes #interfaces #type-system #fundamentals #compiler