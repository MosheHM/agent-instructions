# AI Agent Instructions Repository

A comprehensive collection of specialized agent instruction files for various AI coding assistants and productivity tools. These instructions help you get the most out of Claude Code, GitHub Copilot, Google Gemini CLI, and other AI assistants.

## 📚 Repository Structure

```
agents/
├── code/                    # Software development agents
│   ├── senior-software-architect.md
│   ├── ui-frontend-developer.md
│   ├── python-backend-developer.md
│   ├── nodejs-backend-developer.md
│   ├── devops-cicd-engineer.md
│   ├── code-reviewer.md
│   ├── code-refactorer.md
│   └── security-researcher.md
├── content/                 # Content creation agents
│   ├── technical-writer.md
│   ├── copywriter.md
│   └── content-strategist.md
└── organization/           # Productivity & organization agents
    ├── email-manager.md
    ├── calendar-manager.md
    └── productivity-assistant.md
```

## 🎯 Available Agents

### Code Development Agents
- **Senior Software Architect** - System design, architecture patterns, technical decisions
- **UI/Frontend Developer** - React, Vue, Angular, TypeScript, responsive design
- **Python Backend Developer** - FastAPI, Django, Flask, APIs, databases
- **Node.js Backend Developer** - Express, NestJS, TypeScript, real-time apps
- **DevOps CI/CD Engineer** - Docker, Kubernetes, Terraform, GitHub Actions
- **Code Reviewer** - Critical code analysis, security, performance review
- **Code Refactorer** - Clean code, technical debt reduction, optimization
- **Security Researcher** - Vulnerability detection, OWASP Top 10, security audits

### Content Creation Agents
- **Technical Writer** - Documentation, API docs, tutorials, user guides
- **Copywriter** - Marketing copy, landing pages, email campaigns
- **Content Strategist** - Content planning, SEO, audience research

### Organization & Productivity Agents
- **Email Manager** - Inbox management, email drafting, communication
- **Calendar Manager** - Schedule optimization, meeting coordination
- **Productivity Assistant** - Task management, GTD, goal setting

## 🚀 How to Use These Instructions

### With Claude Code

Claude Code supports custom instructions through project-level configuration.

#### Method 1: Using Custom Instructions (Recommended)

1. **Open your project in Claude Code**

2. **Create or edit `.claude/instructions`:**
   ```bash
   mkdir -p .claude
   ```

3. **Add agent instructions to your project:**
   ```bash
   # Copy the specific agent file content
   cat agents/code/python-backend-developer.md >> .claude/instructions
   ```

4. **Or reference it directly in your instructions:**
   ```markdown
   # .claude/instructions

   You are a Python Backend Developer. Follow the guidelines in:
   agents/code/python-backend-developer.md

   Additional project-specific context:
   - We use FastAPI and PostgreSQL
   - Follow PEP 8 style guide
   - Minimum 80% test coverage required
   ```

5. **Claude Code will automatically load these instructions** for your project

#### Method 2: Custom Slash Commands

Create custom slash commands for different agents:

```bash
# Create slash command directory
mkdir -p .claude/commands
```

```bash
# Create a command file
echo "Act as a Senior Software Architect. Review this code and provide architectural feedback.

$(cat agents/code/senior-software-architect.md)" > .claude/commands/architect.md
```

Now use `/architect` in Claude Code to activate this agent.

#### Method 3: Dynamic Agent Switching

```markdown
# .claude/instructions

# Available Agents
You can switch between different specialized agents. When the user requests:

- "switch to architect mode" → Load agents/code/senior-software-architect.md
- "review my code" → Load agents/code/code-reviewer.md
- "security audit" → Load agents/code/security-researcher.md
- "refactor this" → Load agents/code/code-refactorer.md

[Include summaries of each agent's role]
```

### With GitHub Copilot

GitHub Copilot doesn't support custom instructions directly, but you can use these files effectively:

#### Method 1: Inline Comments

```python
# @copilot Following the guidelines from agents/code/python-backend-developer.md
# Requirements:
# - Use type hints
# - Add docstrings
# - Implement proper error handling
# - Follow Python best practices

def create_user(email: str, password: str) -> User:
    """
    Create a new user with hashed password.
    """
    # Copilot will generate code following these guidelines
```

#### Method 2: Copilot Chat

In VS Code Copilot Chat, paste agent instructions:

```
@workspace I'm working as a Python Backend Developer following these guidelines:

[Paste relevant sections from agents/code/python-backend-developer.md]

Please help me create a secure authentication endpoint.
```

#### Method 3: GitHub Copilot Instructions (Beta)

If you have access to Copilot instructions (GitHub Copilot for Business):

1. **Create `.github/copilot-instructions.md`:**
   ```markdown
   # Copilot Instructions

   When writing Python code, follow the guidelines in agents/code/python-backend-developer.md:
   - Always use type hints
   - Include docstrings for all public functions
   - Implement proper error handling
   - Use parameterized queries for databases
   ```

2. **Reference agent files:**
   ```markdown
   See agents/code/ for detailed role-specific guidelines.
   ```

#### Method 4: VS Code Workspace Settings

```json
// .vscode/settings.json
{
  "github.copilot.advanced": {
    "customInstructions": "Follow the Python Backend Developer guidelines from agents/code/python-backend-developer.md. Always include type hints, docstrings, and proper error handling."
  }
}
```

### With Google Gemini CLI

Google Gemini CLI supports system instructions and context files.

#### Method 1: Using System Instructions

```bash
# Set agent as system instruction
gemini chat --system-instruction="$(cat agents/code/python-backend-developer.md)"
```

#### Method 2: Create Alias for Each Agent

```bash
# Add to your ~/.bashrc or ~/.zshrc

alias gemini-architect='gemini chat --system-instruction="$(cat ~/agents/code/senior-software-architect.md)"'
alias gemini-python='gemini chat --system-instruction="$(cat ~/agents/code/python-backend-developer.md)"'
alias gemini-review='gemini chat --system-instruction="$(cat ~/agents/code/code-reviewer.md)"'
alias gemini-security='gemini chat --system-instruction="$(cat ~/agents/code/security-researcher.md)"'
```

Usage:
```bash
gemini-python "Help me create a FastAPI endpoint for user authentication"
```

#### Method 3: Context Files

```bash
# Create a context file that includes agent instructions
cat agents/code/python-backend-developer.md > /tmp/agent-context.txt
echo "\n\nCurrent Project Context:" >> /tmp/agent-context.txt
echo "- Using FastAPI and PostgreSQL" >> /tmp/agent-context.txt
echo "- Python 3.11+" >> /tmp/agent-context.txt

gemini chat --context-file=/tmp/agent-context.txt
```

#### Method 4: Interactive Mode with Instructions

```bash
# Start Gemini in interactive mode
gemini chat

# Then paste the agent instructions in your first message:
> I want you to act as a Python Backend Developer. Follow these guidelines:
> [Paste content from agents/code/python-backend-developer.md]
>
> Now help me create a user authentication system.
```

#### Method 5: Gemini CLI Config File

Create a config file for different agents:

```yaml
# ~/.config/gemini/agents.yaml

agents:
  python:
    system_instruction_file: "~/agents/code/python-backend-developer.md"
  architect:
    system_instruction_file: "~/agents/code/senior-software-architect.md"
  reviewer:
    system_instruction_file: "~/agents/code/code-reviewer.md"
```

## 📖 Usage Examples

### Example 1: Code Review Workflow

#### With Claude Code:
```bash
# Use slash command
/review

# Or in chat:
"Please review this code following the code reviewer guidelines"
```

#### With Gemini CLI:
```bash
gemini-review "Review this authentication function:
$(cat src/auth.py)"
```

### Example 2: Architecture Discussion

#### With Claude Code:
```
Switch to architect mode and help me design a microservices architecture for an e-commerce platform.
```

#### With Copilot Chat:
```
@workspace Acting as a Senior Software Architect (see agents/code/senior-software-architect.md), help me design a scalable architecture for handling 1M+ users.
```

### Example 3: Security Audit

#### With Gemini CLI:
```bash
gemini-security "Audit this API endpoint for security vulnerabilities:
$(cat src/api/users.py)"
```

### Example 4: Content Creation

#### With Claude Code:
```bash
# Load content agent
cat agents/content/technical-writer.md >> .claude/instructions

# Then request:
"Create API documentation for our REST endpoints"
```

## 🔧 Customization

### Adapting Agents to Your Stack

Create project-specific versions:

```bash
# Copy agent to your project
cp agents/code/python-backend-developer.md .claude/agents/

# Edit to add project-specific details
nano .claude/agents/python-backend-developer.md
```

Add your project specifics:
```markdown
# Python Backend Developer

[Original content...]

## Project-Specific Guidelines

**Tech Stack:**
- FastAPI 0.104+
- PostgreSQL 15
- Redis for caching
- Docker for containerization

**Code Standards:**
- Use `ruff` for linting
- Type hints required (mypy strict mode)
- pytest with 80%+ coverage
- All endpoints must have OpenAPI docs

**Project Structure:**
- Follow the repository structure in /docs/architecture.md
- Use dependency injection pattern
- Repository pattern for data access
```

### Combining Multiple Agents

```markdown
# .claude/instructions

# Multi-Agent System

## Primary Agent: Full-Stack Developer
You combine skills from:
- Frontend: agents/code/ui-frontend-developer.md
- Backend: agents/code/python-backend-developer.md
- DevOps: agents/code/devops-cicd-engineer.md

## Review Process
After writing code:
1. Self-review using agents/code/code-reviewer.md
2. Security check using agents/code/security-researcher.md
3. Suggest refactoring using agents/code/code-refactorer.md
```

## 🎨 Creating Your Own Agent Instructions

Use this template:

```markdown
# [Agent Name]

## Role Description
[Clear description of the agent's expertise and focus]

## Core Responsibilities
- [Primary responsibility 1]
- [Primary responsibility 2]
- [Primary responsibility 3]

## Key Competencies
- **[Skill Area 1]**: [Details]
- **[Skill Area 2]**: [Details]

## Best Practices
[List of best practices the agent should follow]

## Code Examples / Templates
[Provide examples of good outputs]

## Communication Style
[How the agent should communicate]

## Example Use Cases
- [Use case 1]
- [Use case 2]
```

## 📊 Agent Selection Guide

Choose the right agent for your task:

| Task | Recommended Agent |
|------|------------------|
| System design & architecture | Senior Software Architect |
| Building React components | UI/Frontend Developer |
| Creating REST APIs | Python/Node.js Backend Developer |
| CI/CD pipeline setup | DevOps CI/CD Engineer |
| Code review & quality | Code Reviewer |
| Cleaning up legacy code | Code Refactorer |
| Security assessment | Security Researcher |
| Writing documentation | Technical Writer |
| Marketing content | Copywriter |
| Content planning | Content Strategist |
| Email management | Email Manager |
| Schedule optimization | Calendar Manager |
| Task organization | Productivity Assistant |

## 💡 Tips for Best Results

### 1. Be Specific
```
❌ "Write some code"
✅ "Acting as a Python Backend Developer, create a secure REST API endpoint for user registration with email validation and password hashing"
```

### 2. Provide Context
```
Include project context:
- Tech stack
- Coding standards
- Constraints
- Requirements
```

### 3. Reference Agent Explicitly
```
"Following the Security Researcher guidelines, audit this authentication code for vulnerabilities"
```

### 4. Combine Agents When Needed
```
"First, act as an Architect to design the system.
Then, as a Backend Developer, implement the API.
Finally, as a Code Reviewer, review the implementation."
```

### 5. Iterate and Refine
```
1. Initial implementation
2. Code review
3. Refactoring
4. Security audit
5. Final review
```

## 🤝 Contributing

Want to add more agents or improve existing ones?

1. Fork this repository
2. Create a new agent file following the template
3. Add it to the appropriate category
4. Update this README
5. Submit a pull request

## 📝 License

This repository is open source and available under the MIT License.

## 🌟 Popular Combinations

### Full Stack Development
- UI/Frontend Developer
- Python/Node.js Backend Developer
- Code Reviewer

### Security-First Development
- Backend Developer (Python/Node.js)
- Security Researcher
- Code Reviewer

### DevOps & Infrastructure
- Senior Software Architect
- DevOps CI/CD Engineer
- Security Researcher

### Content & Documentation
- Technical Writer
- Copywriter
- Content Strategist

### Productivity Suite
- Email Manager
- Calendar Manager
- Productivity Assistant

## 📞 Support

- Issues: [GitHub Issues](https://github.com/yourusername/agent-instructions/issues)
- Discussions: [GitHub Discussions](https://github.com/yourusername/agent-instructions/discussions)

## 🔄 Updates

This repository is actively maintained. Check back for:
- New specialized agents
- Updated best practices
- Additional AI tool integrations
- Community contributions

---

**Last Updated:** 2025-01-09

Made with ❤️ for the AI-assisted development community
