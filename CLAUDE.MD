# Claude Code - Project Context

This is the **Claude Code** repository, Anthropic's official agentic coding CLI tool that helps developers write code faster through natural language commands.

## Project Overview

**Claude Code** is an AI-powered terminal tool that:
- Understands codebases and executes routine tasks
- Explains complex code through natural language
- Handles git workflows automatically
- Supports extensible plugins for custom commands and agents
- Integrates with IDEs and GitHub

**Official Documentation**: https://docs.anthropic.com/en/docs/claude-code/overview

## Repository Structure

```
claude-code/
├── .claude/                    # Claude configuration
│   └── commands/              # Custom slash commands
│       ├── dedupe.md          # Find duplicate GitHub issues
│       ├── oncall-triage.md   # Triage GitHub issues
│       └── commit-push-pr.md  # Commit, push, and open PR
│
├── docs/                      # Documentation
│   ├── onboarding/           # Team onboarding guides
│   │   ├── README.md         # Main onboarding guide
│   │   ├── quick-reference.md
│   │   └── faq.md
│   └── scenarios/            # Scenario-based documentation (Korean)
│       ├── 01-초기-실행-흐름.md
│       ├── 02-기능-개발-워크플로우.md
│       ├── 03-도구-실행과-보안-훅.md
│       ├── 04-병렬-에이전트-실행.md
│       └── 05-Git-작업-워크플로우.md
│
├── plugins/                   # Plugin system
│   ├── agent-sdk-dev/        # Agent SDK development tools
│   ├── code-review/          # Code review functionality
│   ├── commit-commands/      # Git commit automation
│   ├── explanatory-output-style/  # Output styling
│   ├── feature-dev/          # Feature development workflow
│   ├── learning-output-style/     # Learning mode output
│   ├── pr-review-toolkit/    # PR review tools
│   └── security-guidance/    # Security best practices
│
├── examples/                  # Example projects
├── scripts/                   # Build and utility scripts
├── CHANGELOG.md              # Version history
├── README.md                 # Main readme
├── SECURITY.md              # Security policy
└── code-flow-story.md       # Detailed code flow documentation (Korean)
```

## Key Components

### 1. Plugin System

Plugins extend Claude Code with custom commands, agents, and hooks. Each plugin contains:
- **Commands** (`commands/*.md`): Slash commands like `/feature-dev`
- **Agents** (`agents/*.md`): Specialized AI agents for specific tasks
- **Hooks** (`hooks/*.md`): Event-driven scripts
- **README.md**: Plugin documentation

**Key Plugins:**
- `feature-dev`: 7-phase feature development workflow with parallel agents
- `commit-commands`: Git automation commands
- `pr-review-toolkit`: Comprehensive PR review agents
- `code-review`: Code quality analysis
- `security-guidance`: Security best practices

### 2. Agent Types

Specialized agents for different tasks:
- **code-explorer**: Explores codebase, traces code flow, analyzes architecture
- **code-architect**: Designs system architecture
- **code-reviewer**: Reviews code quality, finds bugs, checks security
- **pr-test-analyzer**: Analyzes PR tests
- **type-design-analyzer**: Reviews type system design
- **silent-failure-hunter**: Finds silent failure patterns

### 3. Hook System

Hooks execute automatically on events:
- **SessionStart**: Runs when Claude Code session starts
- **PreToolUse**: Runs before tool execution (security checks)
- **PostToolUse**: Runs after tool execution (formatting, linting)

### 4. Slash Commands

Custom commands available in this repository:
- `/dedupe`: Find duplicate GitHub issues
- `/oncall-triage`: Triage critical GitHub issues
- `/commit-push-pr`: Commit changes, push, and create PR

## Development Guidelines

### Code Style
- Use TypeScript for type safety
- Follow existing code patterns and conventions
- Keep functions focused and single-purpose
- Write clear, descriptive commit messages

### Security
- Never commit secrets or credentials
- Use security hooks to validate changes
- Follow OWASP top 10 guidelines
- Avoid command injection, XSS, SQL injection

### Git Workflow
1. Develop on feature branches (prefix: `claude/`)
2. Write descriptive commit messages
3. Use `/commit-push-pr` for automated git operations
4. Keep commits atomic and focused

### Testing
- Test all changes before committing
- Run linters and formatters
- Verify security hooks pass
- Check for breaking changes

## Common Workflows

### Adding a New Plugin
1. Create directory in `plugins/`
2. Add `README.md` with plugin description
3. Create subdirectories: `commands/`, `agents/`, `hooks/`
4. Document each command and agent in markdown
5. Test plugin functionality

### Creating a Slash Command
1. Create markdown file in `.claude/commands/`
2. Define command behavior and parameters
3. Document usage examples
4. Test command execution

### Developing a New Agent
1. Create agent file in plugin's `agents/` directory
2. Define agent's purpose and capabilities
3. Specify tools the agent can use
4. Document expected inputs and outputs

### Writing Documentation
- Use clear, concise language
- Include code examples
- Add usage scenarios
- Keep formatting consistent
- Support both English and Korean (for scenarios)

## Important Files

- **CHANGELOG.md**: Track version history and breaking changes
- **SECURITY.md**: Security reporting guidelines
- **code-flow-story.md**: Detailed walkthrough of feature-dev workflow (Korean)
- **docs/onboarding/README.md**: Comprehensive onboarding guide for new users
- **plugins/README.md**: Plugin system documentation

## Package Information

- **Package Name**: `@anthropic-ai/claude-code`
- **Platform**: Node.js 18+
- **Install**: `npm install -g @anthropic-ai/claude-code`
- **Usage**: Run `claude` in project directory

## Data & Privacy

Claude Code collects:
- Usage data (code acceptance/rejections)
- Conversation data
- User feedback via `/bug` command

See [data usage policies](https://docs.anthropic.com/en/docs/claude-code/data-usage) for details.

## Resources

- **Documentation**: https://docs.anthropic.com/en/docs/claude-code/overview
- **Issues**: https://github.com/anthropics/claude-code/issues
- **Discord**: https://anthropic.com/discord (Claude Developers Discord)
- **Feedback**: Use `/bug` command within Claude Code

## Architecture Notes

### Feature Development Flow (feature-dev)
1. **Phase 1: Discovery** - Understand requirements
2. **Phase 2: Codebase Exploration** - 3 parallel code-explorer agents
3. **Phase 3: Clarifying Questions** - Resolve ambiguities
4. **Phase 4: Architecture Design** - Present 3 approaches
5. **Phase 5: Implementation** - Build the feature
6. **Phase 6: Quality Review** - 3 parallel code-reviewer agents
7. **Phase 7: Summary** - Document results

### Parallel Agent Execution
- Multiple agents run concurrently for efficiency
- Each agent has specific expertise and tools
- Results aggregate for comprehensive analysis
- Color-coded badges identify agent types (yellow, blue, green)

### Security Model
- PreToolUse hooks validate dangerous operations
- Commands requiring approval are flagged
- Per-session warnings prevent alert fatigue
- Security guidance plugin provides best practices

## Special Considerations

- All scenario documentation in `docs/scenarios/` is in Korean
- Code flow story (`code-flow-story.md`) is a narrative-style technical doc in Korean
- Onboarding documentation supports multilingual team members
- Plugin system is designed for extensibility
- Git operations follow strict branch naming (prefix: `claude/`)

## Contributing

When contributing to this repository:
1. Read existing documentation thoroughly
2. Follow established patterns and conventions
3. Test changes across multiple scenarios
4. Update documentation for any new features
5. Use `/commit-push-pr` for consistent git workflow
6. Ensure security hooks pass before committing

## Current State

- Active development repository
- Multiple merged PRs for documentation improvements
- Comprehensive onboarding and scenario documentation
- Well-structured plugin system
- Active community on Discord

---

**This file was created to provide context for Claude when working in this repository. Update it as the project evolves.**
