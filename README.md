# Bootstrap IA — Advanced AI-Powered Project Generation for Cursor

A comprehensive ruleset and workflow system that transforms Cursor into an advanced project generation and development engine. Bootstrap IA goes beyond coding standards — it provides a complete methodology for AI-assisted software engineering.

## What is Bootstrap IA?

Bootstrap IA combines three layers of intelligence:

1. **Core Workflow Rules** — A structured methodology for AI-driven project creation (discovery → architecture → scaffolding → implementation → quality gates → iteration).
2. **Global Quality Rules** — Universal coding standards that apply to every project regardless of tech stack.
3. **Technology-Specific Rules** — Best practices for 18+ programming languages and frameworks.

When you drop these rules into a project, Cursor becomes a senior engineer that:
- Plans before coding (architecture, data model, API contracts).
- Scaffolds projects with proper structure, tooling, and configuration.
- Implements features as vertical slices with tests.
- Validates quality at every step (security, performance, accessibility).
- Iterates and refines based on feedback.

## Compatibility

| Tool | File | Format |
|------|------|--------|
| **Cursor** | `.cursor/rules/*.mdc` | MDC with YAML frontmatter |
| **Claude Code** | `CLAUDE.md` | Markdown (project root) |
| **OpenCode / Agents** | `AGENTS.md` | Markdown (project root) |

## Rules Overview

### Core Rules (AI Workflow & Project Generation)

These rules define HOW the AI approaches project creation and development.

| Rule | Description |
|------|-------------|
| `core-workflow` | Master workflow: discovery → architecture → scaffold → implement → validate → iterate |
| `core-planning` | Requirements analysis, scoping, acceptance criteria, task breakdown |
| `core-architecture` | Architecture patterns, data modeling, API design, system design decisions |
| `core-scaffolding` | Project structure generation, tooling setup, configuration files |
| `core-implementation` | Vertical slices, incremental delivery, coding patterns, error-first development |
| `core-quality-gates` | Validation checkpoints: functionality, security, performance, accessibility |
| `core-iteration` | Feedback loops, refactoring triggers, technical debt management |
| `core-agent-orchestration` | Multi-agent patterns, prompt strategies, context management for Cursor |
| `core-devops` | CI/CD pipelines, deployment strategies, monitoring, secrets management |
| `core-tech-stack` | Technology selection framework, stack recommendations by project type |
| `core-ux-design` | UX/UI design principles, forms, loading states, accessibility, responsive design |

### Global Rules (Always Apply)

Universal coding standards for every project.

| Rule | Description |
|------|-------------|
| `global-clean-code` | Naming, functions, readability, simplicity |
| `global-error-handling` | Fail fast, meaningful errors, logging |
| `global-security` | Input validation, secrets, auth, common vulnerabilities |
| `global-testing` | Test structure, coverage, mocking |
| `global-git-conventions` | Commits, branches, PR workflow |
| `global-documentation` | Code comments, API docs, ADRs |
| `global-performance` | Bottlenecks, caching, async, payloads |
| `global-solid-principles` | SOLID, DRY, KISS, YAGNI |
| `global-project-structure` | File organization, module boundaries |
| `global-code-review` | Review checklist and feedback guidelines |

### Technology-Specific Rules

Activated automatically when working with matching file types.

| Rule | Globs | Description |
|------|-------|-------------|
| `specific-typescript` | `**/*.ts, **/*.tsx` | Strict types, patterns, nullability |
| `specific-react` | `**/*.tsx, **/*.jsx` | Components, hooks, state, performance |
| `specific-nextjs` | `**/*.tsx, **/*.ts` | App Router, server components, data fetching |
| `specific-python` | `**/*.py` | PEP 8, type hints, pytest, project structure |
| `specific-nodejs` | `**/*.js, **/*.ts` | Async, error middleware, API design, logging |
| `specific-css-tailwind` | `**/*.css, **/*.scss, **/*.tsx` | Utilities, responsive, accessibility |
| `specific-sql-database` | `**/*.sql, **/*.prisma` | Schema, queries, migrations, ORM |
| `specific-docker` | `Dockerfile, docker-compose*` | Multi-stage, security, compose |
| `specific-rust` | `**/*.rs` | Ownership, error handling, idiomatic patterns |
| `specific-go` | `**/*.go` | Error handling, concurrency, project layout |
| `specific-vue` | `**/*.vue, **/*.ts` | Composition API, Pinia, performance |
| `specific-csharp` | `**/*.cs` | .NET patterns, async, LINQ, nullable, DI |
| `specific-java` | `**/*.java` | Modern Java 17+, Spring, Optional, streams |
| `specific-dart` | `**/*.dart` | Dart 3 / Flutter, null safety, state management |
| `specific-c` | `**/*.c, **/*.h` | Memory safety, defensive programming, portability |
| `specific-cpp` | `**/*.cpp, **/*.hpp, **/*.cc` | RAII, smart pointers, modern C++17/20/23 |
| `specific-api-rest` | `**/api/**, **/routes/**` | URL design, HTTP methods, response format |
| `specific-markdown` | `**/*.md` | Markdown layout, headings, links |

## Usage

### Quick Start — Full Bootstrap

Copy the entire ruleset into your project:

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/bootstrap-IA.git

# Copy all rules to your project
cp -r bootstrap-IA/.cursor/ /path/to/your-project/.cursor/

# Copy agent entrypoints
cp bootstrap-IA/AGENTS.md /path/to/your-project/
cp bootstrap-IA/CLAUDE.md /path/to/your-project/
```

### Cherry-Picking Rules

Copy only the rules you need:

```bash
# Core workflow rules only (AI project generation)
cp bootstrap-IA/.cursor/rules/core-*.mdc /path/to/your-project/.cursor/rules/

# Global quality rules only
cp bootstrap-IA/.cursor/rules/global-*.mdc /path/to/your-project/.cursor/rules/

# Specific tech rules (pick what you need)
cp bootstrap-IA/.cursor/rules/specific-typescript.mdc /path/to/your-project/.cursor/rules/
cp bootstrap-IA/.cursor/rules/specific-react.mdc /path/to/your-project/.cursor/rules/
cp bootstrap-IA/.cursor/rules/specific-nextjs.mdc /path/to/your-project/.cursor/rules/
```

### Using with Cursor

1. Copy the rules into your project's `.cursor/rules/` directory.
2. Open the project in Cursor.
3. Start a conversation — the AI will automatically follow the workflow.
4. For new projects, begin with: *"I want to build [description]. Let's start with discovery and planning."*

### Using with Claude Code

Place `CLAUDE.md` at your project root. Claude Code reads it automatically.

### Using with OpenCode / Other Agents

Place `AGENTS.md` at your project root.

## Workflow Example

Here's how Bootstrap IA transforms a typical conversation:

**Without Bootstrap IA:**
> "Build me a todo app" → AI immediately dumps 500 lines of code in one go.

**With Bootstrap IA:**
> "Build me a todo app" → AI follows the workflow:
> 1. **Discovery**: Asks about features, users, constraints.
> 2. **Architecture**: Proposes stack, data model, API design.
> 3. **Scaffolding**: Creates project structure, config, tooling.
> 4. **Implementation**: Builds feature by feature with tests.
> 5. **Quality gates**: Validates security, performance, accessibility.
> 6. **Iteration**: Refines based on review.

## Customization

Each `.mdc` rule file has YAML frontmatter you can modify:

```yaml
---
description: What this rule does
globs: "**/*.ts"       # File pattern (specific rules only)
alwaysApply: false     # Set to true to always apply
---
```

### Adjusting the Workflow

- **Lighter workflow**: Remove `core-devops.mdc` and `core-quality-gates.mdc` for smaller projects.
- **Backend only**: Remove `core-ux-design.mdc` and frontend-specific rules.
- **Different stack**: Edit `core-tech-stack.mdc` with your preferred technologies.

## File Structure

```
bootstrap-IA/
├── README.md                    # This file
├── AGENTS.md                    # Entrypoint for OpenCode / agents
├── CLAUDE.md                    # Entrypoint for Claude Code
├── .gitignore
└── .cursor/
    └── rules/
        ├── core-workflow.mdc            # Master workflow
        ├── core-planning.mdc            # Project planning
        ├── core-architecture.mdc        # Architecture decisions
        ├── core-scaffolding.mdc         # Project scaffolding
        ├── core-implementation.mdc      # Implementation strategy
        ├── core-quality-gates.mdc       # Quality validation
        ├── core-iteration.mdc           # Iterative refinement
        ├── core-agent-orchestration.mdc # AI agent patterns
        ├── core-devops.mdc              # CI/CD & infrastructure
        ├── core-tech-stack.mdc          # Technology selection
        ├── core-ux-design.mdc           # UX/UI design
        ├── global-*.mdc                 # 10 global quality rules
        └── specific-*.mdc              # 18 tech-specific rules
```

## Contributing

1. Fork the repository.
2. Create a feature branch: `feat/add-xyz-rule`.
3. Add or modify rules following the existing format.
4. Submit a PR with a description of the changes.