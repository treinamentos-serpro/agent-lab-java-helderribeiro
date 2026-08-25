---
name: socops-workspace-instructions
description: "Instruções gerais para o workspace SocOps. Use para entender arquitetura, padrões de código, estrutura do projeto, convenções e workflow."
---

# SocOps Workspace Instructions

## 🎮 Project Overview

**SocOps** é um jogo interativo de Social Bingo para quebra-gelos em encontros presenciais. Jogadores encontram pessoas que correspondem às perguntas ("icebreaker prompts") e marcam em um tabuleiro 5x5, vencendo ao fazer 5 em linha.

### Tech Stack
- **Backend**: Java 21 + Spring Boot 3.4.2 + Tomcat
- **Build**: Apache Maven 3.9.9 (Maven Wrapper)
- **Frontend**: HTML5/CSS3/Vanilla JS (Thymeleaf templates)
- **Testing**: JUnit 5 + AssertJ
- **Deployment**: GitHub Pages (docs) + GitHub Actions

---

## 📂 Project Structure

```
socops/
├── pom.xml                          # Maven configuration
├── mvnw, mvnw.cmd                   # Maven Wrapper
└── src/
    ├── main/
    │   ├── java/com/socops/
    │   │   ├── SocOpsApplication.java          # Spring Boot entry point
    │   │   ├── data/
    │   │   │   └── IcebreakerPrompts.java      # Game prompts database
    │   │   ├── model/
    │   │   │   ├── BingoCell.java              # Single board cell
    │   │   │   ├── PlayPhase.java              # Game phases enum
    │   │   │   └── WinningStreak.java          # Win condition logic
    │   │   ├── service/
    │   │   │   └── BoardAssembler.java         # Game board assembly
    │   │   └── web/
    │   │       └── BingoRestController.java    # REST API endpoints
    │   └── resources/
    │       ├── application.properties          # Spring Boot config
    │       ├── static/css/
    │       │   └── app.css                     # Stylesheet
    │       └── templates/
    │           └── game.html                   # Game UI (Thymeleaf)
    └── test/
        └── java/com/socops/service/
            └── BoardAssemblerTests.java        # Unit tests

docs/                                 # Static documentation (HTML/CSS)
workshop/                             # Training guide (5 modules, 3 languages)
```

---

## 🛠️ Development Workflow

### Building & Running

```bash
# Start dev server (with hot reload on port 8080)
cd socops && ./mvnw spring-boot:run

# Build production package
cd socops && ./mvnw clean package

# Run tests
cd socops && ./mvnw test
```

### VS Code Tasks
- `mvn: run` — Start dev server (background)
- `mvn: build` — Build application
- `mvn: test` — Run tests

### Hot Reload
LiveReload is active on port 35729. Edit templates, CSS, or Java files and the browser reloads automatically.

---

## 🏗️ Architecture Guidelines

### Controllers (REST API)
- **File**: `web/BingoRestController.java`
- **Convention**: Use `@RestController` with `@RequestMapping`
- **Endpoints**: RESTful paths for game operations (new game, mark cell, check win)
- **Response**: Return DTOs with game state, never internal domain objects

### Services (Business Logic)
- **File**: `service/BoardAssembler.java`
- **Convention**: Stateless services with pure functions
- **Responsibility**: Assemble game boards, validate moves, determine winners
- **Testing**: 100% unit test coverage expected

### Models (Domain Objects)
- **Location**: `model/` package
- **Convention**: Immutable value objects where possible
- **Examples**:
  - `BingoCell` — Single board cell (marked/unmarked)
  - `PlayPhase` — Game state (SETUP, PLAYING, WON)
  - `WinningStreak` — Row/column/diagonal streak detection

### Data (Static Content)
- **File**: `data/IcebreakerPrompts.java`
- **Convention**: Static constants for game prompts
- **Customization**: Add new prompts here for different languages/themes

---

## 📝 Code Conventions

### Java Conventions
1. **Naming**:
   - Classes: PascalCase (`BingoRestController`)
   - Methods: camelCase (`assembleBoard()`)
   - Constants: UPPER_SNAKE_CASE (`MAX_BOARD_SIZE`)
   - Private fields: `private` with `final` where applicable

2. **Imports**: Organize by java.*, javax.*, spring.*, then project packages

3. **Documentation**:
   - Add Javadoc for public classes and methods
   - Explain "why" in complex logic, not just "what"
   - Example:
     ```java
     /**
      * Assembles a 5x5 bingo board from random prompts.
      * Ensures no duplicate prompts on the same board.
      */
     public Board assembleBoard() { ... }
     ```

4. **Error Handling**:
   - Use checked exceptions for recoverable errors
   - Use unchecked exceptions for programming errors
   - Include meaningful error messages

### Frontend Conventions (Thymeleaf/CSS/JS)
1. **HTML**: Use semantic HTML5 (`<section>`, `<article>`, `<button>`)
2. **CSS**: Follow `/github/instructions/css-utilities.instructions.md` for utility classes
3. **JavaScript**: Vanilla JS preferred; no jQuery dependencies
4. **Template Variables**: Use Thymeleaf syntax `[[${variable}]]` or `th:text="${variable}"`

---

## 🧪 Testing Strategy

### Unit Tests
- **Location**: `src/test/java/com/socops/service/`
- **Framework**: JUnit 5 + AssertJ
- **Convention**: `*Tests.java` filename pattern
- **Coverage Target**: ≥80% for services, ≥70% for controllers
- **Example**:
  ```java
  @Test
  void shouldAssembleBoardWithFiveRows() {
      Board board = assembler.assembleBoard();
      assertThat(board.getRows()).hasSize(5);
  }
  ```

### Running Tests
```bash
./mvnw test                    # All tests
./mvnw test -Dtest=BoardAssemblerTests  # Specific test class
./mvnw test -Dtest=*Tests     # Pattern matching
```

---

## 🎨 Frontend Design Guidelines

When designing UI/UX:
- Follow `/github/instructions/frontend-design.instructions.md` for design philosophy
- Avoid generic "AI slop" aesthetics
- Use distinctive typography, color schemes, and animations
- Match the playful, social nature of a bingo game
- Ensure accessibility (WCAG 2.1 AA minimum)
- Test on mobile devices (responsive design)

---

## 📚 Workshop Modules

This workspace includes a comprehensive training guide:

| Module | Topic | Time |
|--------|-------|------|
| [00-overview.md](workshop/pt_BR/00-overview.md) | Overview & Quick Start | — |
| [01-setup.md](workshop/pt_BR/01-setup.md) | Setup & Context Engineering | 15 min |
| [02-design.md](workshop/pt_BR/02-design.md) | Frontend Design-First | 15 min |
| [03-quiz-master.md](workshop/pt_BR/03-quiz-master.md) | Custom Quiz Master Agent | 10 min |
| [04-multi-agent.md](workshop/pt_BR/04-multi-agent.md) | Multi-Agent Development | 20 min |

**Access**: Read in browser at `/workspace/pt_BR/GUIDE.md` or in docs folder.

---

## 🔄 Git & GitHub Workflow

### Branch Naming
- Features: `feature/description` (e.g., `feature/dark-theme`)
- Fixes: `fix/description` (e.g., `fix/bingo-win-logic`)
- Docs: `docs/description`

### Commit Messages
```
feat: add dark theme toggle
fix: correct winning streak detection
docs: update API documentation
test: add test coverage for BoardAssembler
```

### Pull Requests
- Create draft PRs early for feedback
- Link related issues: `Closes #123`
- Request review from team before merging
- Enable GitHub Pages on main branch for docs deployment

---

## 🚀 Common Tasks

### Add a New Icebreaker Prompt
1. Edit `data/IcebreakerPrompts.java`
2. Add to appropriate language/theme constant
3. Run `./mvnw test` to ensure no side effects

### Change Game Board Size
1. Update `model/BingoCell.java` and board dimensions
2. Update `service/BoardAssembler.java` assembly logic
3. Update test expectations in `BoardAssemblerTests.java`

### Customize Frontend Styling
1. Edit `resources/static/css/app.css`
2. Reference utility classes from `css-utilities.instructions.md`
3. Test hot reload in browser (LiveReload on port 35729)

### Add a New REST Endpoint
1. Add method to `BingoRestController.java`
2. Document with Javadoc and `@ApiOperation` (if using Springdoc)
3. Write test in controller test class (if exists) or service test

---

## 📋 Checklist for New Features

- [ ] Code follows Java conventions (naming, imports, documentation)
- [ ] New classes/methods have Javadoc comments
- [ ] Unit tests written and passing (`./mvnw test`)
- [ ] Frontend changes tested in browser (hot reload)
- [ ] No console errors or warnings
- [ ] Commit message follows convention
- [ ] PR description explains "what" and "why"
- [ ] Reviewed by at least one team member before merge

---

## 🔗 Useful Links

- **Live Demo**: https://copilot-dev-days.github.io/agent-lab-java/
- **Repository**: https://github.com/copilot-dev-days/agent-lab-java/
- **Spring Boot Docs**: https://spring.io/projects/spring-boot
- **Thymeleaf Guide**: https://www.thymeleaf.org/doc/tutorials/3.1/usingthymeleaf.html
- **Maven Docs**: https://maven.apache.org/guides/

---

## 💡 Tips for Working with Copilot

1. **Provide Context**: Mention the class/module you're working on
2. **Be Specific**: "Add a test for..." instead of "Add a test"
3. **Request Reviews**: Ask Copilot to review code for bugs, performance, style
4. **Iterative Design**: Build incrementally; ask for refinements
5. **Reference Conventions**: Point to this file or related instructions when stuck

**Example prompt**: "I'm adding a new method to BoardAssembler. Following the style in this file and the workshop guide, can you generate a method that..."

---

**Last Updated**: 2026-08-25  
**Maintained by**: SocOps Development Team
