# SocOps Custom Agents

Pre-configured specialized agents for accelerated development workflows.

## ✅ Mandatory Development Checklist

Before committing code:
- [ ] **Lint**: `./mvnw spotless:apply` (format code)
- [ ] **Build**: `./mvnw clean package` (compile & package)
- [ ] **Test**: `./mvnw test` (run all tests)
- [ ] **Review**: Check agent-generated code matches patterns in `.github/instructions/`

---

## 🎮 Core Development Agents

| Agent | Purpose | Use When | File |
|-------|---------|----------|------|
| **TDD Supervisor** | Orchestrate Red → Green → Refactor cycle | Starting a feature with high-level spec | `tdd.agent.md` |
| **TDD Red** | Write failing tests first | Need comprehensive test coverage | `tdd-red.agent.md` |
| **TDD Green** | Minimal implementation to pass tests | Make tests pass with simplest code | `tdd-green.agent.md` |
| **TDD Refactor** | Improve code quality (tests stay green) | Polish code after tests pass | `tdd-refactor.agent.md` |

**Example workflow:**
```
1. @TDD Supervisor "Add toggle endpoint for bingo cells"
2. Agent runs: Red (tests) → Green (impl) → Refactor → Summary
3. Run checklist above → Commit
```

---

## 🎨 Frontend Agents

| Agent | Purpose | Use When |
|-------|---------|----------|
| **Pixel Jam** | Design iterative UI with creative aesthetics | Creating/redesigning UI components |
| **UI Review** | Polish UI for accessibility & responsiveness | Before shipping (final validation) |

---

## 📝 Content Agents

| Agent | Purpose | Use When |
|-------|---------|----------|
| **Quiz Master** | Generate custom icebreaker prompts | Adapting game for events/themes |

---

## 📚 Automatic Instructions (Loaded by File Type)

| File Type | Instructions | Content |
|-----------|--------------|---------|
| `**/*.java` | `java-spring-patterns.instructions.md` | Controllers, Services, Models, naming conventions |
| `**/*.css` | `css-utilities.instructions.md` | Custom utility classes (no Tailwind) |
| UI/HTML | `frontend-design.instructions.md` | Anti-"AI slop" design guidelines |

---

## 🔧 Backend Testing Skill

**Use when**: Writing service tests  
**Invoke**: `/backend-testing` or when TDD agents ask for guidance  
**Pattern**: JUnit 5 + AssertJ with AAA (Arrange-Act-Assert)

```java
@Test
@DisplayName("Fresh board has 25 cells")
void freshBoardHasTwentyFiveCells() {
    // Arrange: Setup
    // Act: Call method
    // Assert: Verify results
}
```

---

## 🚀 Quick Start by Task

| Task | Agent |
|------|-------|
| New REST endpoint + tests | TDD Supervisor |
| Redesign game UI | Pixel Jam → UI Review |
| Add bingo prompts | Quiz Master |
| Write tests | TDD Red |
| Implement code | TDD Green |
| Refactor | TDD Refactor |

---

## 💡 Best Practices

1. **Be specific**: "Add dark mode toggle with smooth transitions" (not just "add feature")
2. **Provide context**: Mention relevant files/components
3. **Ask for iteration**: "More playful" or "Better performance"
4. **Chain agents**: Red → Green → Refactor in sequence
5. **Review output**: Always verify before committing
6. **Run checklist**: Lint → Build → Test (mandatory)

---

## 🔗 Related Resources

- [Main Instructions](./copilot-instructions.md) — Architecture & conventions
- [Quick Start](./QUICKSTART.md) — 5 practical workflows
- [Workshop](../workshop/pt_BR/GUIDE.md) — Hands-on training
- [Spring Boot Docs](https://spring.io/projects/spring-boot)
- [JUnit 5](https://junit.org/junit5/docs/current/user-guide/)
