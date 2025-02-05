---
title: Test-Driven Development By Example - Kent Beck
markmap:
  colorFreezeLevel: 2
---
# Test-Driven Development: By Example - Kent Beck

## Core Principles
- **Red, Green, Refactor Cycle**
  - Write a failing test (Red)
    - Start by imagining the perfect API for the operation
    - Example:
      ```java
      public void testMultiplication() {
          Money five = Money.dollar(5);
          assertEquals(Money.dollar(10), five.times(2));
      }      ```
  - Make the test pass (Green)
    - Write the minimal code required to make the test pass
    - Use quick solutions (e.g., hardcoded values initially)
    - Example:
      ```java
      public Money times(int multiplier) {
          return new Money(amount * multiplier);
      }      ```
  - Refactor to improve code quality
    - Eliminate duplication
    - Improve design by simplifying methods, introducing abstractions, or consolidating code

## TDD Strategies
- **Fake It**: Return hardcoded results to make the test pass
  - Example:
    ```java
    public int add() {
        return 42;  // Fake result
    }    ```
- **Obvious Implementation**: Implement the solution directly
  - Example:
    ```java
    public int add(int a, int b) {
        return a + b;  // Direct implementation
    }    ```
- **Triangulation**: Use multiple test cases to drive generalization

## Part I: The Money Example
- **Scenario**: Multi-currency arithmetic
  - Support operations like addition and multiplication for different currencies
  - Handle exchange rates between currencies
- **Tests**
  - Multiplication
    ```java
    public void testMultiplication() {
        Money five = Money.dollar(5);
        assertEquals(Money.dollar(10), five.times(2));
        assertEquals(Money.dollar(15), five.times(3));
    }    ```
  - Equality
    ```java
    public void testEquality() {
        assertTrue(Money.dollar(5).equals(Money.dollar(5)));
        assertFalse(Money.dollar(5).equals(Money.dollar(6)));
    }    ```
  - Currency Conversion (To be implemented later)

- **Refactoring Steps**
  - Introduce a common superclass (`Money`) to remove duplication
  - Use factory methods (`Money.dollar()`, `Money.franc()`) to encapsulate object creation
  - Improve test readability by using object equality comparisons

## Part II: The xUnit Example
- **Building a Test Framework**
  - Implement core components of a testing framework
  - **Test Case Execution**
    ```java
    public class TestCase {
        public void run() {
            setUp();
            testMethod();
            tearDown();
        }

        public void setUp() {}
        public void tearDown() {}
    }    ```
  - **Handling Failures**
    - Assert methods to verify test outcomes
    - Example:
      ```java
      public void assertTrue(boolean condition) {
          if (!condition) {
              throw new AssertionError("Test failed");
          }
      }      ```
  - **Reflection and Test Suites**
    - Dynamically discover and run multiple test methods

## Part III: Patterns for Test-Driven Development
- **Red Bar Patterns**
  - Write minimal tests to ensure a failure occurs (red bar)
- **Green Bar Patterns**
  - Implement minimal code to pass the test (green bar)
- **Testing Patterns**
  - **Assertion Patterns**: Verify expected outcomes
  - **Setup and Teardown Patterns**: Initialize and clean up test state
- **Design Patterns**
  - Use **Dependency Injection** to reduce coupling
  - Apply **Factory Methods** to control object creation
- **Refactoring Techniques**
  - Consolidate duplicated code
  - Simplify method signatures
  - Extract helper methods or classes

## Key Takeaways
- TDD provides a structured approach to software development
- Testing guides design decisions and ensures functionality
- Frequent feedback cycles help manage complexity and improve code quality
