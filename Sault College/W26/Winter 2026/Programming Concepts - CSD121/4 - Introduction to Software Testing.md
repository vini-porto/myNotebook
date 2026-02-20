# Introduction to Software Testing

## What is Software Testing?

**Software testing** means running your code — or parts of it — in controlled ways to verify it behaves as expected. Think of it like a quality check on a production line: before a product ships, you make sure it actually works.

---

## Why Test?

There are three core reasons to test software:

- **Ensure software quality** — confirm the program does what it's supposed to do
- **Identify bugs** — catch errors before users encounter them
- **Detect [[Regression Testing|regressions]]** — make sure that new changes don't accidentally break things that were already working

---

## Types of Tests

Tests can be categorized in several ways. Here's a quick overview:

### By Scope

|Type|What it tests|
|---|---|
|**[[Unit Testing]]**|Individual functions or classes|
|**[[Integration Testing]]**|How components interact with each other|
|**[[End-to-End Testing]]**|The entire system as a whole|
|**[[Acceptance Testing]]**|Whether the system meets client requirements|

Think of it like building a car: unit tests check individual parts (the engine, the brakes), integration tests check that those parts work together, and end-to-end tests check that the whole car actually drives.

### By Execution Pattern

- **Manual** — a human runs the test (e.g., exploratory testing)
- **Automatic** — code runs the tests for you (e.g., [[JUnit]], Selenium)
- **[[Continuous Integration]] (CI)** — automated tests that run every time you push new code (e.g., GitHub Actions)

### By Context

- **Static testing** — examining code _without_ running it (e.g., code reviews, linters)
- **Dynamic testing** — testing that happens _during_ execution (most tests fall here)

### By Purpose

- **[[Functional Testing]]** — does the system do what it should? (e.g., login works)
- **[[Non-functional Testing]]** — does it do it _well_? (e.g., load times, security)
- **[[Regression Testing]]** — does the new code break old features?
- **Smoke/Sanity** — does the app even start? Can a user log in?
- **Alpha/Beta** — early user testing before broad release

### By Special Focus

- **[[Performance Testing]]** — speed and scalability under load
- **[[Security Testing]]** — vulnerability checks, penetration testing
- **Compatibility** — does it work across browsers/devices/OS?
- **Usability** — is it easy to use?
- **Recovery/Failover** — does it survive crashes gracefully?

---

## When Should You Test?

**Early and often.** Two common philosophies:

- **[[Test-Driven Development]] (TDD)** — write the tests _before_ writing the code. This forces you to think about what the code should do before you write it, often leading to cleaner, more modular designs.
- **Bug-Driven Development (BDD)** — write a test each time a bug is discovered, so that bug can never silently return.

---

## Testing Frameworks

Most platforms have frameworks that make writing and running tests much easier:

|Platform|Framework(s)|
|---|---|
|Java|[[JUnit]], TestNG|
|Python|[[pytest]]|
|JavaScript|Jest, Mocha|
|C# / .NET|xUnit, NUnit|
|PHP|PHPUnit|

---

## Unit Testing with JUnit

[[JUnit]] is the most popular testing framework for Java. To use it in a [[Maven]] project, add it as a dependency in `pom.xml`:

```xml
<dependencies>
  <dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>6.0.2</version>
    <scope>test</scope>
  </dependency>
</dependencies>
```

The `<scope>test</scope>` means this library is only included when running tests — not in your final application.

### Anatomy of a JUnit Test

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class TestIntUtils {

    @Test
    public void testThatPrimesArePrime() {
        assertTrue(IntUtils.isPrime(2));   // boundary: lowest prime
        assertTrue(IntUtils.isPrime(3));   // typical prime
        assertTrue(IntUtils.isPrime(251)); // another typical prime
        assertTrue(IntUtils.isPrime(2147483647)); // large prime
    }
}
```

Key elements:

- The **test class** is named after the class being tested (e.g., `TestIntUtils`)
- Each **test method** is annotated with `@Test`
- Methods use **[[Assertions]]** like `assertTrue()`, `assertFalse()`, `assertEquals()`, `assertNull()` to check expected outcomes
- A single test method can (and should) contain **multiple assertions** that relate to the same theme

---

## Choosing What to Test

You can't test every possible input, so focus on:

- **Valid inputs** — do correct inputs produce correct outputs?
- **[[Boundary Conditions]]** — test values at the very edge of acceptable ranges (e.g., the smallest/largest valid value)
- **Special cases** — values that trigger unique code paths (e.g., `null`, empty string `""`, zero, negative numbers)
- **Invalid inputs** — what happens when bad data is passed? Does the code handle it gracefully?
- **[[Exception Handling]]** — if certain inputs should throw an error, verify that they actually do

### Code Coverage

**[[Code Coverage]]** measures what percentage of your code is actually executed during tests. Ideally 100%, but in large projects that's rarely feasible. Prioritize testing:

- Critical components that affect program correctness
- Frequently used parts of the system
- Components that many other components depend on

### Practical Mindset

> Write tests for valid inputs — but also think about _how your code could break_, and write tests that try to trigger those scenarios.

---

## Testing Classes (Not Just Functions)

When testing a class, you should:

- **Test constructors** — verify instance variables are initialized correctly
- **Test each method** — create an object, configure its state, then call the method and assert the result

```java
@Test
public void testTakeDamage2() {
    var hero = new Hero();
    hero.takeDamage(110);
    assertEquals(0, hero.getHealth(), "Health should never be negative");
}
```

This test checks a **special case**: what if damage exceeds current health? The hero's health should floor at 0, not go negative.

---

## Summary

- [[Software Testing]] verifies that code works as expected, catches bugs, and prevents regressions
- Tests can be categorized by scope, execution pattern, context, purpose, and special focus
- [[Unit Testing]] focuses on individual functions and classes
- [[JUnit]] makes it easy to write and run unit tests in Java
- Good tests cover valid inputs, boundary conditions, special cases, and error handling
- Write tests early and think about how your code could fail

# Tags

#software-testing #unit-testing #JUnit #Java #test-driven-development #code-quality #programming-fundamentals