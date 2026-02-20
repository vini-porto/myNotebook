Here is the full Obsidian note in **plain Markdown**, easy to **copy and paste** into a `.md` file.  
No emojis, simple English, structured, and following your prompt exactly.

---

````markdown
# Test Preparation – Maven Configuration, Test Design, and Type Definitions

These notes explain the three possible written questions in the test:
1. Maven configuration  
2. Selecting a thorough set of tests for a method  
3. Writing a type definition (class / enum / record)

Related topics: [[Software Engineering]], [[Programming Languages]], [[Algorithms]]

---

## 1. Maven Configuration Question

> [!note]
> This question checks if you understand how to configure a Java project using Maven and the `pom.xml` file.

Maven is a build and dependency management tool used in Java projects.  
It helps with:
- Downloading libraries (dependencies)
- Compiling code
- Running tests
- Packaging the program (JAR file)

---

### What is `pom.xml`?

> [!note]
> `pom.xml` (Project Object Model) is the main configuration file of a Maven project.

It contains:
- Project information
- Dependencies
- Java version
- Plugins

Basic structure:

```xml
<project>
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.example</groupId>
  <artifactId>my-app</artifactId>
  <version>1.0-SNAPSHOT</version>

  <dependencies>
  </dependencies>
</project>
````

---

### Common things they may ask

> [!important]  
> Most Maven questions are about adding or modifying small parts of `pom.xml`.

They may ask you to:

- Add a dependency (for example, JUnit)
    
- Set Java version
    
- Configure a plugin
    
- Fix an incorrect configuration

### Example: Adding JUnit dependency

> [!example]  
> JUnit is used for testing Java programs.

```xml
<dependency>
  <groupId>org.junit.jupiter</groupId>
  <artifactId>junit-jupiter</artifactId>
  <version>5.10.0</version>
  <scope>test</scope>
</dependency>
```

Explanation:

- groupId: organization name
    
- artifactId: library name
    
- version: library version
    
- scope = test: used only for tests
    

---

### Example: Setting Java version

```xml
<properties>
  <maven.compiler.source>17</maven.compiler.source>
  <maven.compiler.target>17</maven.compiler.target>
</properties>
```

This means:

- Code is compiled using Java 17
    

---

> [!tip]  
> In the exam, write only the part of `pom.xml` they ask for. Do not rewrite the whole file unless required.

> [!warning]  
> Common mistakes:
> 
> - Missing closing XML tags
>     
> - Wrong dependency name
>     
> - Forgetting `<scope>test</scope>` for testing libraries
>     

External reference:  
[https://www.geeksforgeeks.org/maven-tutorial/](https://www.geeksforgeeks.org/maven-tutorial/)  
[https://cs50.harvard.edu](https://cs50.harvard.edu/)

---

## 2. Selecting a Thorough Set of Tests for a Method

> [!note]  
> This question checks if you can think like a tester and choose good test cases for a method.

You will be given a method, for example:

```java
int divide(int a, int b)
```

And asked:  
“Which tests would you write?”

You are not required to write full JUnit code.  
You must describe which test cases are important.

---

### Types of test cases you must think about

> [!important]  
> A thorough test set must include more than one simple example.

You should consider:

- Normal cases (valid input)
    
- Edge cases (boundary values)
    
- Invalid input
    
- Exception cases
    
- Special values (0, null, negative numbers)


### Example: Method `divide(int a, int b)`

> [!example]

1. Normal case
    
    - divide(10, 2) = 5
        
2. Zero case
    
    - divide(0, 5) = 0
        
3. Negative numbers
    
    - divide(-10, 2) = -5
        
    - divide(10, -2) = -5
        
4. Exception case
    
    - divide(10, 0) → should throw an exception
        

### Example: Method `isEven(int n)`

> [!example]

- isEven(2) → true
    
- isEven(3) → false
    
- isEven(0) → true
    
- isEven(-2) → true


### How to answer in the exam

> [!important]  
> Organize your answer clearly.

Example format:

- Test 1: valid input
    
- Test 2: edge case
    
- Test 3: invalid input
    
- Test 4: exception
    

This shows:

- Logical thinking
    
- Software testing knowledge
    
- Understanding of method behavior
    

> [!tip]  
> Always ask:
> 
> - What happens with 0?
>     
> - What happens with negative values?
>     
> - What happens with invalid input?
>     
> - Should an exception be thrown?
>     

Related note: [[Software Engineering]]

External reference:  
[https://www.geeksforgeeks.org/software-testing-basics/](https://www.geeksforgeeks.org/software-testing-basics/)

## 3. Writing a Type Definition (class / enum / record)

> [!note]  
> This question checks if you can design a data type correctly in Java.

They will describe something like:  
“Define a type representing a Student with name and grade.”

You must decide whether to use:

- class
    
- record
    
- enum

### When to use each type

|Type|Use when|
|---|---|
|class|Object with fields and methods|
|record|Simple data container (immutable)|
|enum|Fixed set of values|

---

### Example: Class

> [!example]

```java
public class Student {
    private String name;
    private int grade;

    public Student(String name, int grade) {
        this.name = name;
        this.grade = grade;
    }

    public String getName() {
        return name;
    }

    public int getGrade() {
        return grade;
    }
}
```

Explanation:

- Fields are private
    
- Constructor initializes values
    
- Getters allow access
    

---

### Example: Record (Java 16+)

> [!example]

```java
public record Student(String name, int grade) {}
```

This is used when:

- The object only stores data
    
- No complex behavior is needed
    

---

### Example: Enum

> [!example]

```java
public enum OrderStatus {
    PENDING,
    SHIPPED,
    DELIVERED
}
```

Enums are used for:

- Fixed choices
    
- States
    
- Categories
    

---

> [!important]  
> The description in the question tells you which type to use.

If the question says:

- “represents a state” → use enum
    
- “represents data” → use record or class
    
- “needs behavior” → use class
    

---

> [!warning]  
> Common mistakes:
> 
> - Forgetting constructor in class
>     
> - Using enum for objects with fields
>     
> - Missing access modifiers (public)
>     

Related note: [[Programming Languages]]

External reference:  
[https://www.w3schools.com/java/java_classes.asp](https://www.w3schools.com/java/java_classes.asp)  
[https://developer.mozilla.org](https://developer.mozilla.org/)

---

## Study Strategy Summary

> [!tip]  
> To prepare for the test:
> 
> - Practice writing small pom.xml sections
>     
> - Practice listing test cases for simple methods
>     
> - Practice defining class, record, and enum from descriptions
>     

Focus on:

- Clear structure
    
- Simple explanations
    
- Correct Java syntax
    
- Logical thinking
    

---

## Tags

#computer_science #software_engineering #programming #testing #maven #java #study_notes