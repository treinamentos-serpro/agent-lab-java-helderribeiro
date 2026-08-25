🌐 [Português (BR)](README.pt_BR.md) | [Español](README.es.md)

# 🎮 Soc Ops — Social Bingo for Mixers

> **Break the ice. Find connections. Win together.**
>
> An interactive Social Bingo game that transforms icebreakers into engaging, memorable experiences at in-person events. Find people who match the prompts, mark your card, and compete to get 5 in a row! 🏆

---

## ⭐ Quick Start (< 5 minutes)

```bash
# 1. Clone & navigate
git clone <repo> && cd agent-lab-java-helderribeiro/socops

# 2. Run the app
./mvnw spring-boot:run

# 3. Open browser
open http://localhost:8080
```

**That's it!** Game ready at http://localhost:8080

---

## ✨ What Makes SocOps Special

### 🎯 **For Event Organizers**
- ✅ Customizable icebreaker prompts in any language
- ✅ Real-time game state management
- ✅ Mobile-responsive design (works on phones!)
- ✅ Zero setup complexity — just deploy and play

### 👨‍💻 **For Developers**
- ✅ **AI-powered development** — 7 custom GitHub Copilot agents
- ✅ **100% Test-driven** — JUnit 5 + AssertJ patterns
- ✅ **Production-ready** — Spring Boot 3.4 + Java 21
- ✅ **Beautiful codebase** — Clean architecture + comprehensive docs

---

## 🚀 Features

| Feature | Details |
|---------|---------|
| 🎲 **Dynamic Boards** | 5x5 bingo grid with random prompts, no duplicates |
| 🎨 **Responsive UI** | Mobile-first design with custom CSS utilities |
| ⚡ **Real-time Updates** | Instant board state sync and win detection |
| 🌍 **Multi-language** | English, Português (BR), Español ready |
| 🤖 **AI-Ready** | Custom agents for TDD, design, testing workflows |
| 📊 **Battle-tested** | 100% test coverage on core logic |

---

## 🎓 Learn & Build

### Choose Your Path:

#### 🟢 **No AI Experience?** 
Start here → [**Lab Guide (50 min)**](workshop/00-overview.md)
- Part 1: Setup & context
- Part 2: Design-first frontend
- Part 3: Custom quiz themes
- Part 4: Multi-agent workflows
- Part 5: Complete example

#### 🟡 **Familiar with AI Agents?**
Jump to → [**AI Quick Start (5 min)**](.github/QUICKSTART.md)
- 5 ready-to-use workflows
- TDD supervisor orchestration
- UI design patterns
- Quiz generation

#### 🔴 **Building Production Features?**
Reference → [**Agent Registry**](.github/AGENTS.md)
- 7 specialized agents
- Best practices
- Checklist (lint → build → test)

---

## 🛠️ Tech Stack

```
Frontend           Backend             DevOps
├── HTML5          ├── Java 21         ├── GitHub Actions
├── CSS3           ├── Spring Boot 3.4 ├── GitHub Pages
├── Vanilla JS     ├── Tomcat 10       └── Maven 3.9
└── Thymeleaf      └── JUnit 5 + AssertJ
```

---

## 📊 Project Status

| Aspect | Status |
|--------|--------|
| **Build** | [![Build](https://img.shields.io/badge/build-passing-brightgreen)]() |
| **Tests** | [![Tests](https://img.shields.io/badge/tests-passing-brightgreen)]() (100% coverage) |
| **Code Quality** | [![Lint](https://img.shields.io/badge/lint-spotless-blue)]() |
| **Java** | [![Java](https://img.shields.io/badge/java-21-orange)]() |
| **Spring Boot** | [![Spring](https://img.shields.io/badge/spring--boot-3.4.2-green)]() |

---

## 🎯 Development with AI Agents

**This workspace is optimized for AI-driven development using GitHub Copilot.**

### Pre-configured Agents:

- 🧪 **TDD Supervisor** — Orchestrate full TDD cycles (Red → Green → Refactor)
- 🎨 **Pixel Jam** — Design beautiful UIs iteratively
- 📝 **Quiz Master** — Generate custom prompts for any theme
- ✅ **Backend Testing** — Write robust tests (JUnit 5 + AssertJ)
- 🔍 **UI Review** — Polish & validate components

### Get Started:

**1. Read the Quick Start:**
```
.github/QUICKSTART.md  ← 5 practical workflows
```

**2. Pick an Agent:**
```
Chat → Select "TDD Supervisor" → Describe your feature
```

**3. Follow the Checklist:**
```
✓ Lint:   ./mvnw spotless:apply
✓ Build:  ./mvnw clean package
✓ Test:   ./mvnw test
```

---

## 📚 Documentation

### Essential Reading
| Document | Purpose | Time |
|----------|---------|------|
| [QUICKSTART](.github/QUICKSTART.md) | 5 workflows to try now | 5 min |
| [AGENTS](.github/AGENTS.md) | All agents + patterns | 10 min |
| [Lab Guide](workshop/GUIDE.md) | Full training course | 50 min |
| [Architecture](./copilot-instructions.md) | Design decisions | 15 min |

### Reference Docs
- [Java/Spring Patterns](.github/instructions/java-spring-patterns.instructions.md) — Backend conventions
- [Frontend Design](.github/instructions/frontend-design.instructions.md) — Anti-"AI slop" principles
- [CSS Utilities](.github/instructions/css-utilities.instructions.md) — Custom utility classes
- [Testing Skill](.github/skills/backend-testing/SKILL.md) — JUnit 5 patterns

---

## 🚀 Ready to Get Started?

### 🎮 Play the Game
```bash
cd socops && ./mvnw spring-boot:run
# → http://localhost:8080
```

### 📖 Learn Development
→ [**Read the Lab Guide** (50 min workshop)](workshop/GUIDE.md)

### 🤖 Build with AI
→ [**AI Quick Start** (.github/QUICKSTART.md)](./github/QUICKSTART.md)

### 💻 Dive into Code
→ [**Explore Architecture** (.github/copilot-instructions.md)](.github/copilot-instructions.md)

---

## 📋 Build & Test

```bash
cd socops

# Lint code (remove unused imports, format)
./mvnw spotless:apply

# Build application
./mvnw clean package

# Run tests (100% coverage!)
./mvnw test

# Start dev server (with hot reload)
./mvnw spring-boot:run
```

---

## 🤝 Contributing

This is an **open lab project** for learning AI-driven development with GitHub Copilot.

→ See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines

---

## 📜 License & Code of Conduct

- **License**: [See LICENSE](LICENSE)
- **Code of Conduct**: [Microsoft OSS](CODE_OF_CONDUCT.md)
- **Contributing**: [See CONTRIBUTING](CONTRIBUTING.md)
- **Security**: [See SECURITY.md](SECURITY.md)

---

## 🔗 Quick Links

| Resource | Link |
|----------|------|
| 🎮 Live Demo | https://copilot-dev-days.github.io/agent-lab-java/ |
| 📦 GitHub Repo | https://github.com/copilot-dev-days/agent-lab-java/ |
| 📚 Spring Boot Docs | https://spring.io/projects/spring-boot |
| 🧪 JUnit 5 Guide | https://junit.org/junit5/docs/current/user-guide/ |
| 🤖 GitHub Copilot | https://github.com/features/copilot |

---

## 💡 What's Next?

### For Players
- 🎯 Organize your next event
- 🌍 Customize prompts for your culture/team
- 📸 Share your SocOps moments

### For Developers
- 🚀 Extend with leaderboards
- 🎨 Design dark mode
- 🌐 Add real-time multiplayer
- 📱 Build native mobile app

### For AI Enthusiasts
- 🤖 Create custom agents
- 🧪 Experiment with TDD workflows
- 📖 Learn Copilot best practices
- 🔗 Build on this template

---

## 📞 Support

**Questions?** Check these first:
- 🔍 [QUICKSTART](.github/QUICKSTART.md) — Common workflows
- 📚 [Lab Guide](workshop/GUIDE.md) — Hands-on training
- 🐛 [Issues](https://github.com/copilot-dev-days/agent-lab-java/issues) — Report bugs
- 💬 [Discussions](https://github.com/copilot-dev-days/agent-lab-java/discussions) — Ask questions

---

<div align="center">

### 🎉 Ready to Break the Ice?

**[→ Start Playing (5 min)](http://localhost:8080)** | **[→ Learn Development (50 min)](workshop/GUIDE.md)** | **[→ AI Quick Start (5 min)](.github/QUICKSTART.md)**

---

**Made with ❤️ for community, learning, and fun.**

⭐ Star us on GitHub to stay updated!

</div>
