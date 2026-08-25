---
name: backend-testing
description: Write robust JUnit 5 + AssertJ tests for Java services following AAA (Arrange, Act, Assert) pattern. Use when: creating new service tests, adding test coverage, testing business logic, validating domain models.
---

# Backend Testing (Java/JUnit 5 + AssertJ)

Write high-quality unit tests for Java services using JUnit 5 and AssertJ.

## When to Use This Skill

- ✅ Writing tests for new service methods
- ✅ Adding test coverage for business logic
- ✅ Testing domain models and records
- ✅ Validating edge cases and error handling

## AAA Pattern

Every test follows **Arrange → Act → Assert**:

```java
@Test
@DisplayName("Fresh board has exactly 25 cells")
void freshBoardHasTwentyFiveCells() {
    // Arrange: Set up test data and mocks
    // (No setup needed here — BoardAssembler is stateless)
    
    // Act: Call the method under test
    List<BingoCell> board = BoardAssembler.assembleNewBoard();
    
    // Assert: Verify results
    assertThat(board).hasSize(25);
}
```

## Test Structure

### 1. Test Class Setup

```java
package com.socops.service;

import com.socops.model.*;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import static org.assertj.core.api.Assertions.*;

/**
 * Tests for {@link BoardAssembler}.
 * Validates board assembly, cell flipping, and victory detection.
 */
class BoardAssemblerTests {
    // Test methods here
}
```

**Conventions**:
- Class name: `{ServiceName}Tests.java` (not `*Test.java`)
- Package: Same as the class under test
- Javadoc: Briefly describe what this test class validates

### 2. Test Method Anatomy

```java
@Test
@DisplayName("Empty prompt causes IllegalArgumentException")
void emptyPromptThrowsException() {
    // Arrange
    String emptyPrompt = "";
    
    // Act & Assert
    assertThatThrownBy(() -> BoardAssembler.validatePrompt(emptyPrompt))
        .isInstanceOf(IllegalArgumentException.class)
        .hasMessage("Prompt cannot be empty");
}
```

**Naming**:
- Method name: Describe the scenario + expected outcome
- `@DisplayName`: Human-readable description for test reports

### 3. Assertion Patterns

#### Simple Values

```java
// ✅ AssertJ (preferred)
assertThat(board).hasSize(25);
assertThat(freeCell.selected()).isTrue();
assertThat(gamePhase).isEqualTo(PlayPhase.PLAYING);

// ❌ JUnit (harder to read)
assertEquals(25, board.size());
assertTrue(freeCell.selected());
```

#### Collections

```java
assertThat(board)
    .hasSize(25)
    .doesNotContainNull()
    .filteredOn(cell -> cell.freeCell())
    .hasSize(1);

assertThat(prompts)
    .contains("has lived in another country", "speaks multiple languages")
    .doesNotContainDuplicates();
```

#### Objects & Records

```java
BingoCell cell = BingoCell.ofPrompt(0, "test prompt");

assertThat(cell)
    .hasFieldOrPropertyWithValue("id", 0)
    .hasFieldOrPropertyWithValue("selected", false)
    .hasFieldOrPropertyWithValue("freeCell", false);

// Or extract specific fields
assertThat(cell)
    .extracting(BingoCell::prompt, BingoCell::selected)
    .containsExactly("test prompt", false);
```

#### Exceptions

```java
// Single exception check
assertThatThrownBy(() -> method())
    .isInstanceOf(IllegalArgumentException.class)
    .hasMessage("Board size must be 25");

// Multiple exception types
assertThatAnyOf(
    () -> assertThatThrownBy(() -> method()).isInstanceOf(NullPointerException.class),
    () -> assertThatThrownBy(() -> method()).isInstanceOf(IllegalArgumentException.class)
).anyMatch(t -> true);
```

## Test Organization

### Grouping with Nested Classes

```java
class BoardAssemblerTests {
    
    @Nested
    @DisplayName("Board creation")
    class BoardCreation {
        
        @Test
        void freshBoardHasTwentyFiveCells() { ... }
        
        @Test
        void centerCellIsAlwaysFree() { ... }
    }
    
    @Nested
    @DisplayName("Cell flipping")
    class CellFlipping {
        
        @Test
        void flippedCellBecomesSelected() { ... }
    }
}
```

### Test Fixtures (Setup/Teardown)

```java
@BeforeEach
void setUp() {
    // Runs before each test
    // Use for common Arrange steps
}

@AfterEach
void tearDown() {
    // Runs after each test
    // Use for cleanup
}

@BeforeAll
static void setUpOnce() {
    // Runs once before all tests in class
}
```

## Common Test Scenarios

### Testing Immutable Records

```java
@Test
@DisplayName("BingoCell records are immutable")
void cellRecordIsImmutable() {
    BingoCell cell = BingoCell.ofPrompt(0, "test");
    
    // Records automatically have equals() and hashCode()
    assertThat(cell).isEqualTo(BingoCell.ofPrompt(0, "test"));
    assertThat(cell).isNotEqualTo(BingoCell.ofPrompt(1, "test"));
}
```

### Testing Factory Methods

```java
@Test
@DisplayName("ofFreeCell creates pre-selected free space")
void freeCellFactoryMethodWorks() {
    BingoCell freeCell = BingoCell.ofFreeCell(12);
    
    assertThat(freeCell)
        .hasFieldOrPropertyWithValue("selected", true)
        .hasFieldOrPropertyWithValue("freeCell", true)
        .hasFieldOrPropertyWithValue("prompt", "FREE SPACE");
}
```

### Testing Edge Cases

```java
@Test
@DisplayName("Empty board returns 0 winning streaks")
void emptyBoardHasNoWins() {
    List<BingoCell> emptyBoard = emptyList();
    
    assertThat(BoardAssembler.detectWin(emptyBoard))
        .isEmpty();
}

@Test
@DisplayName("Single cell cannot win")
void singleCellCannotWin() {
    List<BingoCell> singleCell = List.of(BingoCell.ofPrompt(0, "test"));
    
    assertThatThrownBy(() -> BoardAssembler.detectWin(singleCell))
        .isInstanceOf(IllegalArgumentException.class);
}
```

## Running Tests

```bash
# All tests
./mvnw test

# Specific class
./mvnw test -Dtest=BoardAssemblerTests

# Specific method
./mvnw test -Dtest=BoardAssemblerTests#freshBoardHasTwentyFiveCells

# Matching pattern
./mvnw test -Dtest=*Tests
```

## Best Practices

| ✅ Do | ❌ Avoid |
|------|---------|
| One assertion per test (or related assertions) | Multiple unrelated assertions in one test |
| Meaningful test names with @DisplayName | Generic names like "testIt()" |
| Test one behavior per method | Testing multiple scenarios in one method |
| Use test fixtures for shared setup | Duplicating Arrange code |
| Assert on specific fields | Asserting on toString() |
| Document complex assertions | Leaving confusing assertions unexplained |
| Test edge cases (null, empty, boundary) | Only testing happy path |

## Quick Reference

```java
// Common AssertJ assertions
assertThat(value).isEqualTo(expected);
assertThat(value).isNotEqualTo(expected);
assertThat(value).isNull();
assertThat(value).isNotNull();
assertThat(bool).isTrue().isFalse();
assertThat(collection).hasSize(5).isEmpty().contains(item);
assertThat(string).startsWith("prefix").endsWith("suffix").contains("substring");
assertThat(number).isPositive().isGreaterThan(0).isLessThan(10);
```

## Resources

- [JUnit 5 User Guide](https://junit.org/junit5/docs/current/user-guide/)
- [AssertJ Fluent Assertions](https://assertj.github.io/assertj-core-features-highlight.html)
- [Testing Best Practices](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.testing)

