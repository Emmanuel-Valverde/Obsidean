---
title: Growing Object-Oriented Software, Guided by Tests - Steve Freeman & Nat Pryce
markmap:
  colorFreezeLevel: 2
---


# Growing Object-Oriented Software, Guided by Tests - Steve Freeman & Nat Pryce

## Historical Context
- **TDD Origins**
  - Kent Beck's *Test-Driven Development: By Example* (2002)
  - Focus: Red-Green-Refactor cycle
- **Challenges with Early TDD**
  - Difficulty testing complex systems with external dependencies
  - Tests were brittle, slow, and dependent on infrastructure
- **Mock Objects Development**
  - Developed by Tim Mackinnon, Steve Freeman, and Philip Craig (2008)
  - Invented within the Extreme Programming (XP) community in the 2000s
  - Purpose: Simplify unit testing by isolating external dependencies

## Core Concepts
- **Growing Software**
  - Software is not built, it's grown incrementally.
  - Always maintain a working, deployable version.
- **Starting Point: Walking Skeleton**
  - Create a minimal, vertical slice through the entire system early on.
  - Ensures end-to-end connectivity and defines high-level architecture.

## Testing Strategy
- **Acceptance Tests**
  - Define the overall behavior the system should exhibit.
  - Drive the implementation of key features.
- **Unit Tests**
  - Focus on individual object behavior in isolation.
  - Utilize mock objects for dependencies that are:
    - Expensive to use (e.g., databases)
    - Slow or unreliable (e.g., external APIs)
    - Not yet implemented
- **Integration Tests**
  - Validate that multiple components interact correctly.
  - Limited use to reduce test brittleness.

## Dependency Management
- **When to Substitute Dependencies**
  - Mock objects for complex or external dependencies.
  - Stubs for read-only data.
  - Real objects for internal logic where behavior is critical.
- **Types of Dependencies**
  - **Internal**: Within the same module or domain context.
  - **External**: Cross-system dependencies (e.g., services, databases).
- **Example: Auction Sniper**
  ```java
  public void testAuctionFailure() {
      MockAuctionServer server = new MockAuctionServer();
      server.simulateFailure();

      auctionSniper.connectTo(server);
      assertFalse(auctionSniper.isWinning());
      server.verify();
  }
  ```

## Design Principles
- **Growing Objects through Tests**
  - Iterative cycles of adding tests, implementing, and refactoring.
- **Object Collaboration**
  - Emphasize message-passing and interaction between objects.
  - Avoid tight coupling by focusing on contracts and interfaces.
- **Tell, Don’t Ask**
  - Objects encapsulate behavior and act on messages without exposing state.
  
## Patterns and Practices
- **Dependency Injection**
  - Pass dependencies into objects to allow for easy substitution in tests.
- **Ports & Adapters (Hexagonal Architecture)**
  - Separate core business logic from infrastructure.
  - Use adapters to handle external interfaces.
- **Smart Handlers**
  - Delegate complex behavior to specialized objects.
  
## Project Example: Auction Sniper
- **Scenario**
  - Bidding in online auctions.
  - System requirements:
    - Connect to an auction server.
    - Display real-time updates.
    - Handle multiple auction events.
- **Development Process**
  - Acceptance tests define behavior (e.g., successful bid, auction close).
  - Mock auction server used to simulate server responses.
  - Iterative development, continuously integrating new features and tests.

## Test Writing Guidelines
- **Start with the Highest Value Tests**
  - Begin with an acceptance test to define system behavior.
  - Write unit tests for core logic.
  - Use mocks to test object interactions and collaborations.
- **Fail Fast**
  - Ensure tests provide immediate feedback on failures.
  - Clearly communicate what went wrong with detailed assertions.

## Advanced Topics
- **Test Resilience**
  - Avoid tests that are overly dependent on implementation details.
  - Ensure tests remain valid after code refactoring.
- **Diagnostics and Debugging**
  - Design tests to provide informative error messages.
  - Failures should pinpoint the issue without extensive debugging.
  
## Summary
- **TDD as a Design Tool**
  - Tests guide the evolution of software architecture.
  - Mock objects support isolation and improve design.
  - Iterative cycles foster sustainable, maintainable software growth.
