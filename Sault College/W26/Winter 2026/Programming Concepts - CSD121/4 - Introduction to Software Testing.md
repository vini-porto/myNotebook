# Introduction to Software Testing

Software testing is the practice of running your code in specific ways to **verify it works as expected**. Think of it as double-checking your work before submitting it — except automated and repeatable.

## Why Test?

Three main reasons:

- **Ensure software quality** — confidence that your code does what it's supposed to
- **Identify bugs** — catch mistakes early before they reach users
- **Detect regressions** — make sure new changes don't accidentally break things that already worked

## Kinds of Tests

There are many types of tests, organized by different criteria:

**By Scope** — how much of the system is tested at once:

|Type|What it tests|Examples|
|---|---|---|
|Unit|Individual functions/classes|JUnit, pytest|
|Integration|How components interact|API endpoint tests|
|End-to-end / System|The entire application|UI flows|
|Acceptance|Whether client requirements are met|UAT|

**By Execution Pattern** — how the tests are run:

|Type|Description|
|---|---|
|Manual|A human performs the test|
|Automatic|Scripts/code run the tests|
|Continuous|Automated tests in a CI/CD pipeline (e.g. GitHub Actions)|

**By Context:**

- **Static** — inspect code _without_ running it (code reviews, linters)
- **Dynamic** — tests that run during execution (most tests fall here)

**By Testing Purpose:**

|Type|Purpose|
|---|---|
|Functional|Tests desired behaviours (login, file upload)|
|Non-functional|Tests qualities like performance or security|
|Regression|Ensures new changes don't break old features|
|Smoke/Sanity|Quick check — does it even start?|
|Alpha/Beta|Early user testing before full release|

**By Special Focus:**

- **Performance** — speed and scalability (load, stress tests)
- **Security** — vulnerabilities (penetration testing, fuzzing)
- **Compatibility** — works across browsers/OS/devices
- **Usability** — ease of use and UX
- **Recovery/Failover** — resilience under failure (simulated crashes)

## When Should You Test?

> **Early and often!**

Two popular philosophies:

- **TDD (Test-Driven Development)** — write tests _before_ writing the code. This sounds backwards but leads to cleaner, more modular code.
- **BDD (Bug-Driven Development)** — write a test whenever you find a bug, to prevent it from coming back.

## Testing Frameworks

Most languages have a framework to make testing easier:

|Platform|Framework(s)|
|---|---|
|Java|JUnit, TestNG|
|Python|pytest|
|JavaScript|Jest, Mocha|
|C#/.NET|xUnit, NUnit|
|PHP|PHPUnit|
|Go|go test (built-in)|

See also: [[Software Engineering]]

## Why Automated Tests?

Manual testing is slow, error-prone, and easy to forget. Automated tests let you:

- Re-run _all_ tests instantly after any change
- Catch regressions immediately
- Have clear pass/fail feedback

## Unit Testing with JUnit

JUnit is the most widely used unit testing framework for Java. To add it to a Maven project, put this in your `pom.xml`:

```xml
<dependencies>
  <dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>6.0.2</version>
    <scope>test</scope>  <!-- only included during test runs -->
  </dependency>
</dependencies>
```

### Writing a JUnit Test

Suppose you have this method:

```java
public static boolean isPrime(int n) {
    // ... implementation
}
```

Here's how you'd test it:

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class TestIntUtils {

    @Test
    public void testThatPrimesArePrime() {
        assertTrue(IntUtils.isPrime(2));    // boundary: smallest prime
        assertTrue(IntUtils.isPrime(3));
        assertTrue(IntUtils.isPrime(251));
        assertTrue(IntUtils.isPrime(2147483647)); // large prime
    }

    @Test
    public void testThatNonPrimesAreNotPrime() {
        assertFalse(IntUtils.isPrime(0));   // edge case
        assertFalse(IntUtils.isPrime(1));   // edge case
        assertFalse(IntUtils.isPrime(-1));  // negative numbers
        assertFalse(IntUtils.isPrime(-2));
        assertFalse(IntUtils.isPrime(4));   // typical non-prime
        assertFalse(IntUtils.isPrime(15));
        assertFalse(IntUtils.isPrime(2019));
    }
}
```

Key points:

- The test class is typically named `TestX` or `XTest` where X is the class being tested
- Each test method gets the `@Test` annotation
- Method names should clearly describe what's being tested
- One test can (and should) have **multiple assertions**
- One class should have **multiple test methods** covering different scenarios

When you run tests in IntelliJ IDEA, you'll see green checkmarks for passing tests and red X marks for failures — including the expected vs. actual value and the exact failing line.

## Testing Classes (Instance Methods)

For testing objects, create an instance and configure it, then assert expected behaviour:

```java
class HeroTest {

    @Test
    public void testConstructor() {
        var hero = new Hero();
        assertEquals(100, hero.getHealth()); // verify initial state
    }

    @Test
    public void testTakeDamage() {
        var hero = new Hero();
        hero.takeDamage(10);
        assertEquals(90, hero.getHealth());
    }

    @Test
    public void testTakeDamage2() {
        var hero = new Hero();
        hero.takeDamage(110); // more than health
        assertEquals(0, hero.getHealth(), "Health should never be negative");
    }
}
```

Test constructors too — make sure instance variables are initialized correctly.

## Choosing What to Test

You can't always test every possible input (imagine testing every possible String!), so be strategic:

**1. Input Validation**

- Test that valid inputs produce correct results
- Test that _invalid_ inputs are handled appropriately too
- You don't need to test inputs outside precondition limits

**2. Boundary Conditions**

- Test values at the upper and lower bounds of acceptable ranges
- Test `null`, empty strings, empty lists

**3. Special Cases**

- Test inputs that trigger specific branches in your code (conditionals, loops)
- Think about zero values, empty collections, etc.

**4. Exception Handling**

- If certain inputs should throw an exception, write a test to confirm they do

**Example — testing `titleCase(String s)`:**

```java
@Test
void testValidInputs() {
    assertEquals("Hello", titleCase("hello"));
    assertEquals("Hello", titleCase("hElLo"));
    assertEquals("Hello, World!", titleCase("hEllO, wOrLd!"));
}

@Test
void nullRemainsNull() {
    assertNull(titleCase(null));
}

@Test
void emptyStringRemainsEmpty() {
    assertEquals("", titleCase(""));
}

@Test
void singleLetterIsCapitalized() {
    assertEquals("A", titleCase("a"));
    assertEquals("Z", titleCase("z"));
}
```

### Code Coverage

**Code coverage** = the percentage of your code that actually gets _executed_ by your tests. 100% is ideal but rarely practical in large projects. Instead, prioritize testing:

- The most critical components
- Frequently used functionality
- Code that many other parts depend on

> 💡 General rule: write tests that verify valid inputs work _and_ think about how your code could break — then write tests for those cases too.

---

**Further reading:** [GeeksforGeeks – Software Testing](https://www.geeksforgeeks.org/software-testing-basics/) | [JUnit 5 Docs](https://junit.org/junit5/docs/current/user-guide/)

Related: [[Software Engineering]] | [[Algorithms]] | [[Programming Languages]]

---
## Tags

#computer_science #software_testing #unit_testing #junit #java #tdd #software_engineering #study_notes #automation #testing_frameworks