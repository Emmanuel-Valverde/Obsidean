---
title: "Test Patterns: Refactoring Test Code"
markmap:
  colorFreezeLevel: 2
---

# xUnit Test Patterns: Refactoring Test Code - Gerard Meszaros

## Core Concepts
- **Purpose of Test Automation**
  - Reduce risk and detect defects early.
  - Improve confidence in code changes.
  - Support continuous integration and deployment.

## Test Organization Patterns
- **Fixture Setup**
  - **Testcase Class per Fixture**: Group related tests in a class.
  - **Testcase per Class**: One test case per class or component under test.
- **Setup Methods**
  - Use `setUp()` for shared initialization across tests.
  - Avoid excessive setup to keep tests independent.

## Test Verification Patterns
- **Result Verification**
  - **State Verification**: Assert final object states.
  - **Behavior Verification**: Assert interactions with dependencies.
- **Assertions**
  - **Assert Equals**: Compare expected vs actual values.
  - **Multiple Assertions**: Ensure each test checks one behavior.

## Test Double Patterns
- **Types of Test Doubles**
  - **Dummy Object**: Passed but not used (e.g., placeholder).
  - **Stub**: Provides canned responses to specific calls.
  - **Mock**: Verifies interactions and expectations.
  - **Fake**: Simplified implementation (e.g., in-memory database).
  - **Test Spy**: Records method calls for later verification.
  
- **Example: Mocking a Payment Gateway**
  ```java
  @Test
  public void testPaymentProcessing() {
      MockPaymentGateway gateway = new MockPaymentGateway();
      PaymentService service = new PaymentService(gateway);

      service.processPayment(100);

      gateway.verifyPayment(100);
  }
  ```

## Test Smells
- **Common Smells**
  - **Assertion Roulette**: Multiple asserts without descriptive failure messages.
  - **Mystery Guest**: Hidden dependencies or external systems.
  - **Test Logic in Production Code**: Conditional logic specific to tests.
  - **Excessive Setup**: Overly complex test initialization.
  
- **Strategies to Fix Smells**
  - Use descriptive assertions.
  - Replace external dependencies with test doubles.
  - Simplify setup and teardown logic.

## Fixture Setup Strategies
- **Inline Setup**
  - Define test data directly in the test case.
- **Shared Setup**
  - Common initialization logic in setup methods (`setUp()`).
- **Parameterized Tests**
  - Reuse test logic with different input sets.

## Test Lifecycle Management
- **Test Phases**
  - Setup -> Exercise -> Verify -> Teardown.
- **Teardown**
  - Clean up resources to prevent side effects on other tests.
  - Use `tearDown()` methods in xUnit frameworks.

## Advanced Patterns
- **Test Isolation**
  - Ensure tests do not depend on shared state.
  - Use mocks and stubs to control dependencies.
  
- **Test Data Builders**
  - Simplify test data creation.
  ```java
  PaymentBuilder builder = new PaymentBuilder().withAmount(100).withCurrency("USD");
  Payment payment = builder.build();
  ```

## Summary
- **Key Takeaways**
  - Tests must be reliable, independent, and maintainable.
  - Test doubles and patterns help simplify test automation.
  - Continuous refactoring of test code is essential to prevent test smells.