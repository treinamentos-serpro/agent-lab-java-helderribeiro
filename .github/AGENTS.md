# SocOps Custom Agents

This file documents the specialized agents available in this workspace. Use them for specific development workflows and tasks.

## 🎮 Agents Directory

### Core Development

#### **TDD Supervisor** 
**Purpose**: Orchestrate the complete Test-Driven Development cycle  
**Use when**: Starting a new feature or bug fix with a high-level specification  
**Workflow**: TDD Red → TDD Green → TDD Test Runner → TDD Refactor → Summary

```
User: "Add a Scavenger Hunt mode with checkboxes and progress meter"
Agent: Runs TDD Red (tests), TDD Green (impl), TDD Refactor, outputs summary
```

**File**: `.github/agents/tdd.agent.md`

---

#### **TDD Red**
**Purpose**: Write failing unit tests that specify the desired behavior  
**Use when**: Starting TDD phase 1 — before implementing code  
**Workflow**: Reads user story → writes comprehensive failing tests → shows test file

```
User: "Write tests for a board shuffle function"
Agent: Generates JUnit 5 tests with AssertJ assertions, all initially failing
```

**File**: `.github/agents/tdd-red.agent.md`

---

#### **TDD Green**
**Purpose**: Write minimal implementation to pass failing tests  
**Use when**: TDD phase 2 — make tests pass with simplest code  
**Workflow**: Reads failing tests → writes lean implementation → shows code  

```
User: "Implement the board shuffle function"
Agent: Writes only what's needed to pass TDD Red tests
```

**File**: `.github/agents/tdd-green.agent.md`

---

#### **TDD Refactor**
**Purpose**: Improve code quality while keeping tests green  
**Use when**: TDD phase 3 — after tests pass, time to polish  
**Workflow**: Reviews implementation → refactors for clarity/perf → verifies tests still pass

```
User: "Refactor the shuffle logic for readability"
Agent: Improves code style, extracts constants, maintains green tests
```

**File**: `.github/agents/tdd-refactor.agent.md`

---

### Frontend & Design

#### **Pixel Jam**
**Purpose**: Design and build web components iteratively with creative, polished aesthetics  
**Use when**: Creating or redesigning UI components, pages, or full applications  
**Workflow**: Interactive iteration — you request, agent designs, you refine

```
User: "Design a beautiful game lobby screen"
Agent: Creates HTML/CSS with distinctive typography, animations, and colors
```

**File**: `.github/agents/pixel-jam.agent.md`

---

#### **UI Review**
**Purpose**: Review frontend components for design quality, accessibility, responsiveness  
**Use when**: Before shipping UI — needs final polish and validation  
**Workflow**: Analyze component → suggest improvements → maintain code style

```
User: "Review the game board grid for mobile responsiveness"
Agent: Checks CSS, accessibility, mobile breakpoints, suggests fixes
```

**File**: `.github/agents/ui-review.agent.md`

---

### Content & Quiz Generation

#### **Quiz Master**
**Purpose**: Generate custom icebreaker prompts and quiz themes  
**Use when**: Adapting the game for new events, languages, or team cultures  
**Workflow**: Takes theme description → generates creative, context-specific questions

```
User: "Generate tech industry icebreaker questions"
Agent: Creates 24 fun, relevant prompts for a tech team bingo game
```

**File**: `.github/agents/quiz-master.agent.md`  
**Related Docs**: `workshop/pt_BR/03-quiz-master.md`

---

## 🔧 Instructions & Skills

### Backend Patterns  
**File**: `.github/instructions/java-spring-patterns.instructions.md`  
**Applies to**: All Java files (`**/*.java`)  
**Content**: Controllers, Services, Models, Data layer patterns + naming conventions  
**Loaded automatically** when you ask agents to write Java code

---

### Frontend Design Philosophy  
**File**: `.github/instructions/frontend-design.instructions.md`  
**Applies to**: HTML/CSS/JS files  
**Content**: Avoid "AI slop" — distinctive typography, colors, animations  
**Loaded automatically** when designing UIs

---

### CSS Utilities  
**File**: `.github/instructions/css-utilities.instructions.md`  
**Content**: Custom utility classes for responsive layouts, spacing, colors  
**Reference when**: Styling components — no Tailwind, custom utilities instead

---

### Backend Testing Skill
**File**: `.github/skills/backend-testing/SKILL.md`  
**Use when**: `/init backend-testing` or when TDD agents ask for test guidance  
**Content**: JUnit 5 + AssertJ patterns, AAA (Arrange-Act-Assert), best practices

---

## 🚀 Quick Start by Task

| Task | Recommended Agent |
|------|-------------------|
| Build a new REST endpoint with tests | **TDD Supervisor** (Red → Green → Refactor) |
| Redesign the game UI | **Pixel Jam** → **UI Review** |
| Add custom bingo questions for an event | **Quiz Master** |
| Write tests only | **TDD Red** |
| Implement code to pass tests | **TDD Green** |
| Improve code quality | **TDD Refactor** |
| Check UI for accessibility/mobile | **UI Review** |

---

## 📚 Workshop Integration

For hands-on practice using these agents:

- **Part 3**: Using Quiz Master → `workshop/pt_BR/03-quiz-master.md`
- **Part 4**: Multi-agent workflows (TDD + Pixel Jam) → `workshop/pt_BR/04-multi-agent.md`
- **Part 5**: Complete example → `workshop/pt_BR/05-complete.md`

---

## 💡 Tips for Best Results

1. **Be specific**: Instead of "add a feature", say "add dark mode toggle with smooth transitions"
2. **Provide context**: Mention which component/file you're working on
3. **Ask for iteration**: "Make it more playful" or "Refactor for performance"
4. **Chain agents**: Use TDD Red → Green → Refactor in sequence
5. **Review output**: Always review generated code before committing

---

## 🔗 Useful Links

- [Main Instructions](./copilot-instructions.md) — Project overview & architecture
- [Workshop Guide](../workshop/pt_BR/GUIDE.md) — 5-part training course
- [Contributing](../CONTRIBUTING.md) — CLA and code of conduct
- [Spring Boot Docs](https://spring.io/projects/spring-boot)
- [JUnit 5 Guide](https://junit.org/junit5/docs/current/user-guide/)

