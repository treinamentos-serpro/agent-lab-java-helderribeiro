---
description: "Java/Spring Boot patterns and conventions for SocOps backend development. Use when writing Java code, creating REST endpoints, services, or domain models."
applyTo: "**/*.java"
---

# Java & Spring Boot Patterns

This guide helps AI agents maintain consistency when generating Java code for the SocOps backend.

## Architecture Layers

### 1. Controllers (`web/` package)
**Purpose**: HTTP request routing and response handling.

**Pattern**:
```java
@Controller
public class BingoRestController {
    
    @GetMapping("/api/bingo/fresh-board")
    @ResponseBody
    public List<BingoCell> dispenseFreshBoard() {
        return BoardAssembler.assembleNewBoard();
    }
}
```

**Conventions**:
- Use `@Controller` (not `@RestController` for views + REST endpoints)
- Delegate all logic to services — controllers are thin
- Return domain models directly (no intermediate DTOs for simple cases)
- Use `@ResponseBody` for REST endpoints
- Name methods as verbs: `serveLobbyPage()`, `dispenseFreshBoard()`

### 2. Services (`service/` package)
**Purpose**: Stateless business logic and domain operations.

**Pattern**:
```java
public final class BoardAssembler {
    private static final int GRID_SIDE = 5;
    private static final int CENTER_SLOT = 12;

    private BoardAssembler() { /* static helper — never instantiated */ }

    /** Produce a fresh 25-cell board with shuffled prompts. */
    public static List<BingoCell> assembleNewBoard() {
        // Pure function: no side effects, no state
        var shuffledPrompts = new ArrayList<>(IcebreakerPrompts.ALL_PROMPTS);
        Collections.shuffle(shuffledPrompts);
        // ...
        return freshBoard;
    }
}
```

**Conventions**:
- Make services `final` (no subclassing)
- Use `static` methods for pure functions (no instance state needed)
- Private constructor for utility classes
- Document each method with Javadoc explaining the "why"
- Constants in `UPPER_SNAKE_CASE`
- No side effects — pure functions only

### 3. Models (`model/` package)
**Purpose**: Immutable domain value objects.

**Pattern**:
```java
/**
 * One tile on the 5×5 bingo grid.
 *
 * @param id        zero-based position (0-24)
 * @param prompt    display text shown on the tile
 * @param selected  whether the player has tapped this tile
 * @param freeCell  true only for the centre "FREE SPACE" tile
 */
public record BingoCell(int id, String prompt, boolean selected, boolean freeCell) {

    /** Build a regular, untapped prompt tile. */
    public static BingoCell ofPrompt(int id, String prompt) {
        return new BingoCell(id, prompt, false, false);
    }

    /** Build the centre free-space tile (always pre-tapped). */
    public static BingoCell ofFreeCell(int id) {
        return new BingoCell(id, IcebreakerPrompts.FREE_CELL_LABEL, true, true);
    }
}
```

**Conventions**:
- Use Java `record` (Java 16+) for immutable value objects
- Add Javadoc to the record explaining each field
- Include factory methods: `ofPrompt()`, `ofFreeCell()` for semantic construction
- Avoid setters — immutability first
- Keep records focused: one concept per record

### 4. Data (`data/` package)
**Purpose**: Centralized constants and static data.

**Pattern**:
```java
public final class IcebreakerPrompts {
    public static final String FREE_CELL_LABEL = "FREE SPACE";
    
    public static final List<String> ALL_PROMPTS = List.of(
        "has lived in another country",
        "speaks more than 2 languages",
        // ... more prompts
    );
}
```

**Conventions**:
- `public final class` for data holders
- `public static final` for constants
- Use `List.of()` for immutable lists
- Document the purpose and contents

---

## Java Language Conventions

### Naming
| Element | Convention | Example |
|---------|-----------|---------|
| Classes | PascalCase | `BingoRestController` |
| Methods | camelCase | `assembleNewBoard()` |
| Constants | UPPER_SNAKE_CASE | `GRID_SIDE`, `CENTER_SLOT` |
| Parameters | camelCase | `promptId`, `selectedCells` |
| Private fields | camelCase with `final` | `private final int gridSize` |

### Imports Organization
```java
// Standard library
import java.util.*;

// Spring Framework
import org.springframework.stereotype.Controller;

// Project-specific
import com.socops.model.*;
import com.socops.service.*;
```

### Documentation

**Every public class and method needs Javadoc:**
```java
/**
 * Assembles a 5x5 bingo board from random prompts.
 * Ensures no duplicate prompts on the same board.
 * The center cell (index 12) is always "FREE SPACE".
 *
 * @return a shuffled 25-cell board with center pre-marked
 */
public static List<BingoCell> assembleNewBoard() { ... }
```

**Explain "why" in complex logic:**
```java
// ❌ BAD: Describes what, not why
for (int i = 0; i < 25; i++) { ... }

// ✅ GOOD: Explains intent
// Skip center slot (12) — it's always the free space
for (int slot = 0; slot < GRID_SIDE * GRID_SIDE; slot++) {
    if (slot == CENTER_SLOT) { ... }
}
```

---

## Testing Patterns

See: [Backend Testing Guide](../skills/backend-testing/SKILL.md)

### Quick Reference

**Test Class Naming**: `*Tests.java` (not `*Test.java`)

**Test Method Structure** (AAA Pattern):
```java
@Test
@DisplayName("Centre slot (index 12) is always the free cell and pre-selected")
void centerSlotIsAlwaysFreeCell() {
    // Arrange: Set up test data
    List<BingoCell> generatedBoard = BoardAssembler.assembleNewBoard();
    BingoCell centreTile = generatedBoard.get(12);

    // Act: Execute the behavior
    // (implicit here: board assembly already happened)

    // Assert: Verify expectations
    assertTrue(centreTile.freeCell(), "Centre tile must be flagged as free");
    assertTrue(centreTile.selected(), "Free cell must start already tapped");
}
```

**Use AssertJ for readability:**
```java
// ✅ Clearer assertions
assertThat(generatedBoard).hasSize(25);
assertThat(centreTile)
    .extracting(BingoCell::selected)
    .isEqualTo(true);
```

**@DisplayName for English descriptions:**
```java
@DisplayName("Centre slot is always the free cell and pre-selected")
```

---

## Common Pitfalls to Avoid

| ❌ Avoid | ✅ Do |
|---------|------|
| Mutable state in services | Use static methods with pure functions |
| Mixing concerns (controller logic in service) | Keep controllers thin, services focused |
| DTOs everywhere | Return domain models directly when possible |
| Setter methods on models | Use records and factory methods |
| Generic `Exception` | Use specific exceptions or unchecked for programming errors |
| No Javadoc | Document public API + complex logic |
| Hardcoded values | Extract to named constants (`GRID_SIDE`, `CENTER_SLOT`) |
| Test methods without names | Use `@DisplayName` for clarity |

---

## File Structure Checklist

When adding a new feature:

- [ ] Model in `model/*.java` (record or immutable class)
- [ ] Service logic in `service/*.java` (static, pure functions)
- [ ] REST endpoint in `web/BingoRestController.java`
- [ ] Tests in `test/java/com/socops/service/*Tests.java`
- [ ] Constants in `data/IcebreakerPrompts.java` (if needed)
- [ ] Update Javadoc for all public APIs
- [ ] Run `./mvnw test` to verify

---

## Links

- [Spring Boot Documentation](https://spring.io/projects/spring-boot)
- [Java Records (JEP 395)](https://openjdk.org/jeps/395)
- [JUnit 5 User Guide](https://junit.org/junit5/docs/current/user-guide/)
- [AssertJ Documentation](https://assertj.github.io/assertj-core-features-highlight.html)

