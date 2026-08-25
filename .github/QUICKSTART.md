# 🚀 SocOps AI Agent Quick Start

This guide shows common workflows using AI agents to accelerate development.

## Setup (One-time)

1. ✅ Open VS Code Chat (`Ctrl/Cmd + Shift + I`)
2. ✅ Ensure GitHub Copilot extension is installed
3. ✅ You're ready! Agents load automatically from `.github/agents/`

---

## 📋 Common Workflows

### Workflow 1: Add a New REST Endpoint with TDD

**Goal**: Add an endpoint to toggle bingo cell markers

**Steps**:

1. **Start TDD Supervisor**
   - Open Chat → Select "TDD Supervisor" agent
   - Or type: `@TDD Supervisor`

2. **Describe the feature**:
   ```
   Add a POST endpoint /api/bingo/toggle/{cellId} that:
   - Takes a cell ID
   - Marks/unmarks it in the current board
   - Returns updated board state
   - Include comprehensive tests
   ```

3. **Watch the flow**:
   - ✅ TDD Red: Writes failing tests
   - ✅ TDD Green: Implements minimal code
   - ✅ TDD Refactor: Polishes the implementation
   - ✅ Summary: Shows all changes

4. **Review output** → Commit to branch → Create PR

---

### Workflow 2: Design New UI Component

**Goal**: Create a scoreboard component showing top players

**Steps**:

1. **Open Pixel Jam**
   - Select "Pixel Jam" agent in chat

2. **Describe the design**:
   ```
   Create a scoreboard component that:
   - Shows top 5 players with ranks (#1, #2, etc)
   - Displays score, wins, streak
   - Animated rank changes
   - Dark theme with green accents
   - Mobile-responsive
   ```

3. **Iterate**:
   - Agent generates HTML/CSS/JS
   - "Make the animations more playful"
   - "Add sound effects on rank changes"
   - "Optimize for small screens"

4. **Use UI Review**
   - When happy: Select "UI Review" agent
   - "Check this component for accessibility and mobile"
   - Review suggestions → Refine

---

### Workflow 3: Generate Custom Bingo Prompts

**Goal**: Create prompts for a tech company offsite

**Steps**:

1. **Open Quiz Master**
   - Select "Quiz Master" agent

2. **Provide theme**:
   ```
   Generate icebreaker prompts for a tech company offsite.
   Make them:
   - Funny and slightly chaotic
   - Related to tech culture
   - Inclusive and non-controversial
   - 25 unique prompts
   ```

3. **Refine**:
   - "Make #7 and #12 more challenging"
   - "Add more questions about remote work"
   - "Remove the one about programming languages"

4. **Use the prompts**:
   - Copy to `src/main/java/com/socops/data/IcebreakerPrompts.java`
   - Run tests → Deploy

---

### Workflow 4: Write Tests for Game Logic

**Goal**: Add test coverage for winning streak detection

**Steps**:

1. **Open Chat** → Select "Backend Testing" skill
   - Or type: `/backend-testing`

2. **Request tests**:
   ```
   Write comprehensive tests for WinningStreak.java:
   - Test horizontal wins (all 5 rows)
   - Test vertical wins (all 5 columns)
   - Test diagonal wins (both directions)
   - Test no-win cases (3 in a row, corners)
   - Test edge cases
   ```

3. **Follow AAA pattern**:
   - **Arrange**: Set up test data
   - **Act**: Call the method
   - **Assert**: Verify results

4. **Copy to** `src/test/java/com/socops/service/WinningStreakTests.java`

---

### Workflow 5: Refactor Existing Code

**Goal**: Improve BoardAssembler readability

**Steps**:

1. **Select default agent** (or any agent)

2. **Request refactoring**:
   ```
   Refactor src/main/java/com/socops/service/BoardAssembler.java:
   - Extract magic numbers to named constants
   - Break large methods into smaller functions
   - Add inline documentation for complex logic
   - Keep all tests passing
   ```

3. **If using TDD workflow**:
   - Select "TDD Refactor" agent
   - Paste current code
   - Review changes → Run tests → Commit

---

## 💡 Pro Tips

### Tip 1: Chain Commands
```
Describe feature → TDD Red creates tests → 
Copy tests to file → TDD Green implements → 
Run ./mvnw test locally → TDD Refactor polishes
```

### Tip 2: Provide File Context
```
❌ "Add validation"
✅ "Add email validation to BingoRestController.java, 
   following the pattern in BoardAssembler.java"
```

### Tip 3: Reference Existing Patterns
```
"Following the style in BoardAssemblerTests.java, 
write comprehensive tests for WinningStreak.java"
```

### Tip 4: Use Instructions Files
When agents write Java, they **automatically** load:
- `instructions/java-spring-patterns.instructions.md`
- `instructions/css-utilities.instructions.md`
- No need to manually reference them!

### Tip 5: Ask for Specific Frameworks
```
❌ "Add a form"
✅ "Add a form using Thymeleaf with validation 
   and custom CSS utility classes"
```

---

## 🔥 Advanced: Multi-Agent Orchestration

**Goal**: Complete feature request: "Dark mode toggle"

**Sequence**:

1. **Plan** (Chat → @TDD Supervisor)
   ```
   High-level requirement: Add dark mode toggle to game UI
   Should support persistence and smooth transitions
   ```

2. **Backend Tests** (@TDD Red)
   ```
   Write tests for theme preference storage in service layer
   ```

3. **Backend Implementation** (@TDD Green + @TDD Refactor)
   ```
   Implement theme service, persistence, API endpoint
   ```

4. **Frontend Design** (@Pixel Jam)
   ```
   Design toggle button, smooth transitions, theme switching
   ```

5. **Frontend Tests** (Default agent)
   ```
   Test localStorage, DOM updates, CSS transitions
   ```

6. **QA Review** (@UI Review)
   ```
   Check accessibility, mobile responsiveness, cross-browser
   ```

7. **Ship** (Create PR → Review → Merge)

---

## 🎓 Next Steps

- 📚 Read [AGENTS.md](./AGENTS.md) for detailed agent documentation
- 🎯 See [copilot-instructions.md](./copilot-instructions.md) for architecture
- 📖 Complete [workshop/pt_BR/GUIDE.md](../workshop/pt_BR/GUIDE.md) for hands-on practice
- 🧪 Use `/backend-testing` skill for testing workflows

---

## ❓ Troubleshooting

**"Agent isn't responding"**
- Restart Chat (`Ctrl+Shift+P` → "Clear Chat History")
- Check agent file exists in `.github/agents/`
- Reload VS Code window

**"Code doesn't match project style"**
- Mention `copilot-instructions.md` patterns in your prompt
- Reference similar files in the codebase
- Ask agent to "follow the style in [existing file]"

**"Tests are failing"**
- Run locally: `cd socops && ./mvnw test`
- Check agent used correct Java/Maven versions
- Verify fixture data matches your domain model

---

**Happy coding! 🎮**
