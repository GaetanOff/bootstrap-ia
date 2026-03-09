# AGENTS.md — Bootstrap IA: Advanced AI-Powered Project Generation

> This file is the entrypoint for OpenCode and other agent-compatible editors.
> It aggregates all rules from Bootstrap IA: workflow, quality, and technology-specific.

---

## Core Workflow Rules

### Master Workflow

Follow this phased approach for every project — never skip phases:

1. **Discovery**: understand requirements, users, constraints, acceptance criteria.
2. **Architecture**: choose patterns, design data model, define API contracts, select tech stack.
3. **Scaffolding**: generate project structure, set up tooling, configure linter/formatter/tests.
4. **Implementation**: build feature by feature as vertical slices with tests.
5. **Quality Gates**: validate functionality, security, performance, accessibility.
6. **Iteration**: refine based on feedback, refactor, optimize, update docs.

Never start coding before completing Discovery and Architecture. Present trade-offs explicitly.

### Planning

- Decompose into epics → features → user stories → tasks.
- Define MVP scope. Cut ruthlessly — ship less, ship better.
- Write acceptance criteria: Given [precondition] When [action] Then [expected outcome].
- Plan vertical implementation: data layer → business logic → API → UI → tests → docs.
- Start with foundational features (auth, data model), then core flows, then polish.

### Architecture

- Document every decision: Context → Options → Trade-offs → Decision → Consequences.
- Choose pattern based on needs: monolith (MVP), modular monolith (growing), microservices (large teams), serverless (event-driven).
- Design data model first: entities, relationships, invariants. Normalize for writes, denormalize for reads.
- Define API contracts before implementation. Design for backward compatibility.
- Plan cross-cutting concerns upfront: logging, error handling, config, health checks, rate limiting.

### Scaffolding

- Organize by feature/domain, not by file type. Colocate related files.
- Set up: package manager, linter, formatter, type checker, test runner, git hooks.
- Create: README.md, .env.example, .gitignore, Dockerfile (if needed), CI pipeline.
- First commit: structure + config + deps + smoke test + README.

### Implementation

- Build vertical slices: complete one feature through all layers before starting the next.
- Implement error/edge cases alongside the happy path, not after.
- Every commit should leave the project in a working state.
- Use feature flags for incomplete features. Deploy to staging frequently.

### Quality Gates

Per feature:
- All acceptance criteria met (happy + error paths).
- Edge cases handled. Error messages are user-friendly.
- No linter errors. No hardcoded values. No dead code.
- Unit + integration tests pass. Coverage ≥80% on business logic.
- Security: input validated, auth enforced, no secrets in code.
- Performance: no N+1 queries, paginated lists, optimized assets.
- Accessibility: semantic HTML, keyboard nav, WCAG AA contrast.

### Iteration

- Compare output against requirements. Fix blockers → improvements → polish.
- Refactor when: duplication ≥3 places, functions >40 lines, files >300 lines.
- Refactor in dedicated commits. Green → refactor → green.
- Profile before optimizing. Measure baseline → change → measure again.
- Update README, API docs, ARCHITECTURE.md after changes.

### Agent Orchestration

- Reference specific files with @ mentions. Break large tasks into focused conversations.
- Be specific in prompts: mention stack, constraints, existing patterns.
- Multi-step approach: design first → implement → test → refine.
- Request self-review: security audit, edge cases, performance, conventions.
- Don't accept first output blindly — review, then ask for improvements.

### DevOps

- CI pipeline minimum: install → lint → type check → unit tests → build → integration tests.
- Use environment variables for all config. Never use production data in dev.
- Containerize services. Multi-stage builds, pin versions, non-root user.
- Monitor with three pillars: logs (structured), metrics (RED/USE), traces (OpenTelemetry).
- Automate backups. Document disaster recovery plan.

### Technology Selection

- Evaluate: fitness, maturity, ecosystem, community, team expertise, scalability, cost.
- SaaS web app: Next.js + React + TypeScript + Tailwind + PostgreSQL + Prisma.
- API backend: Fastify/Hono + TypeScript + PostgreSQL + Zod + Vitest.
- Mobile: React Native + Expo or Flutter.
- CLI: Go (Cobra) or Rust (Clap).
- Always pin dependency versions. Use lockfiles. Audit regularly.

### UX Design

- Clarity over cleverness. Consistency. Feedback on every action. Forgiveness.
- Every interactive element: default, hover, focus, active, disabled, loading states.
- Forms: label every input, inline validation, appropriate input types.
- Design empty states and error states. Provide a path forward from every error.
- Mobile-first responsive. Touch targets ≥44px. WCAG AA contrast.

---

## Global Rules

### Clean Code Fundamentals

- Use descriptive, intention-revealing names. Booleans: `is`, `has`, `should`, `can` prefix.
- Functions: verb phrases, under 20 lines, max 3 parameters, single level of abstraction.
- Prefer early returns / guard clauses over deep nesting.
- No magic numbers or strings — extract to named constants.
- Delete dead code. Don't comment it out.
- Write the simplest code that works. Avoid premature abstraction (Rule of Three).
- Prefer composition over inheritance.

### Error Handling

- Fail fast: validate at boundaries, reject bad data early.
- Never swallow errors silently. Use specific error types with contextual messages.
- Catch at the appropriate level. Clean up resources in `finally` / `defer` / `with`.
- Log at correct severity (debug, info, warn, error). Include correlation IDs.
- Never log sensitive data (passwords, tokens, PII).

### Security

- Never trust user input. Validate and sanitize at system boundaries.
- Use parameterized queries — never concatenate user input into SQL.
- Never hardcode secrets in source code. Use env vars or a secrets manager.
- Hash passwords with bcrypt/scrypt/argon2. Validate authorization server-side on every request.
- Keep dependencies up to date. Run security audits regularly.

### Testing

- Follow Arrange-Act-Assert. One behavior per test. Descriptive test names.
- Test pyramid: 70% unit, 20% integration, 10% E2E.
- Tests must be deterministic. No shared mutable state between tests.
- Test edge cases: empty, null, boundary values, error paths.
- Mock external dependencies, not internal logic.

### Git Conventions

- Conventional Commits: `<type>(<scope>): <description>`. Types: feat, fix, refactor, docs, test, chore, perf, ci.
- Imperative mood, lowercase, no period, max 72 chars subject line.
- One logical change per commit. Keep PRs small (<400 lines diff).
- Branch naming: `feat/<ticket>-description`, `fix/<ticket>-description`.
- Never commit secrets, `.env`, or build artifacts.

### Documentation

- Code should be self-documenting. Comments explain **why**, not **what**.
- Document public APIs: purpose, parameters, return values, exceptions.
- Every project needs: README.md, .env.example, architecture overview.
- Record significant decisions as ADRs (Architecture Decision Records).

### Performance

- Measure first, optimize second. Algorithmic improvements beat micro-optimizations.
- Watch for N+1 queries, unnecessary re-renders, main thread blocking, large payloads.
- Cache at the right layer with proper invalidation.
- Use async I/O, parallel execution, connection pooling.
- Paginate list endpoints. Lazy-load non-critical resources.

### SOLID Principles

- **SRP**: One reason to change per module/class/function.
- **OCP**: Open for extension, closed for modification.
- **LSP**: Subtypes must be substitutable for their base types.
- **ISP**: Don't force clients to depend on methods they don't use.
- **DIP**: Depend on abstractions, not concrete implementations. Inject dependencies.
- **DRY**: Extract duplicated logic, but wait for 3 occurrences before abstracting.
- **KISS/YAGNI**: Simplest solution wins. Don't build what you don't need yet.

### Project Structure

- Organize by feature/domain, not by file type. Colocate related files.
- Flat structure — max 3-4 levels deep. Each directory has one clear purpose.
- Define module boundaries. Expose public APIs, hide internals. No circular dependencies.

### Code Review

- Self-review every diff before submitting. No debug code or console logs.
- Review for: correctness, security, maintainability, performance, test coverage.
- Give specific feedback. Distinguish blockers from suggestions. Ask questions, don't demand.

---

## Technology-Specific Rules

### TypeScript

- Enable `strict: true`. Avoid `any` — use `unknown` + type guards.
- Prefer `interface` for extendable shapes, `type` for unions/intersections.
- Use discriminated unions for state modeling. Use `readonly` for immutable data.
- Use optional chaining (`?.`) and nullish coalescing (`??`). Prefer explicit null checks over `!`.
- Use `import type` for type-only imports.

### React

- Functional components only. One per file. Keep JSX under ~50 lines.
- Destructure props. Follow Rules of Hooks. One effect per concern.
- Start with local state, lift up only when needed. Don't store derived state.
- Memoize with `useMemo`/`useCallback` only when measurably needed.
- Don't use array index as `key`. Don't mutate state directly.

### Next.js (App Router)

- Default to Server Components. Push `"use client"` boundary as low as possible.
- Fetch data in Server Components with `async/await`. Use `loading.tsx` and `error.tsx`.
- Use Server Actions for mutations. Validate with Zod.
- Use `<Image>` and `<Link>` components. Implement `generateMetadata` for SEO.

### Python

- Follow PEP 8 (Black/Ruff formatter). Type hints on all function signatures.
- Use dataclasses/Pydantic for structured data. Context managers for resources.
- Catch specific exceptions. Use `logging`, not `print()`.
- Use `pytest` with fixtures and parametrize. `pyproject.toml` for config.

### Node.js

- Always `async/await`. Never forget `await`. Use `Promise.all()` for parallel ops.
- Centralized error middleware. Custom error classes. Consistent error response shapes.
- Validate requests with Zod/Joi. Use structured logging (pino/winston).
- Handle graceful shutdown. Use connection pooling.

### CSS & Tailwind

- Use utility classes directly. Extract to components, not `@apply`.
- Mobile-first responsive: default → `sm:` → `md:` → `lg:`.
- Use `cn()` / `clsx` for conditional classes. Group classes logically.
- Ensure WCAG AA contrast. Support `prefers-reduced-motion`.

### SQL & Database

- Parameterized queries always. Never `SELECT *` in application code.
- Add `NOT NULL` by default. Use `created_at`/`updated_at` timestamps.
- One atomic change per migration. Migrations must be reversible.
- Watch for N+1 queries. Use transactions for atomic operations.

### Docker

- Multi-stage builds. Minimal base images. Pin versions.
- Order layers by change frequency. Don't run as root.
- Use `.dockerignore`. Set `HEALTHCHECK`. Scan for vulnerabilities.

### Rust

- Prefer borrowing over cloning. Use `Result<T, E>` for recoverable errors.
- Use `thiserror` (libraries) / `anyhow` (apps). Avoid `unsafe` unless justified.
- Use iterators/combinators. Derive `Debug`, `Clone`, `PartialEq`.
- Run `clippy` and `rustfmt` in CI.

### Go

- Follow `gofmt`. Always check returned errors. Wrap with `%w` for context.
- Accept interfaces, return structs. Keep interfaces small (1-2 methods).
- Use `context.Context` for cancellation. Manage goroutine lifecycles.
- Table-driven tests. Minimize external dependencies.

### Vue.js 3

- Use `<script setup>` + Composition API. `ref()` for primitives, `reactive()` for objects.
- Extract logic into composables (`useXxx`). Use `computed()` for derived state.
- Use Pinia for state management. Lazy-load routes.
- Use `defineProps<T>()` and `defineEmits<T>()` for type safety.

### C#

- Follow .NET naming: `PascalCase` public, `_camelCase` private fields, `I` prefix for interfaces.
- Use records for immutable DTOs. Use `sealed` on classes not designed for inheritance.
- Always `async/await` — never `.Result` or `.Wait()`. Pass `CancellationToken` through call chains.
- Use `ValueTask<T>` for hot paths. Use `ConfigureAwait(false)` in library code.
- Enable nullable reference types (`<Nullable>enable</Nullable>`). Use pattern matching and switch expressions.
- Constructor injection for DI. `IOptions<T>` for config. Validate options at startup.
- LINQ: `Any()` over `Count() > 0`. Avoid multiple enumeration of `IEnumerable<T>`.

### Java

- Use modern Java (17+): records, sealed classes, pattern matching, switch expressions, text blocks.
- Use `Optional<T>` as return type for absent values — never as field or parameter.
- `Objects.requireNonNull()` for fail-fast. Try-with-resources for all `AutoCloseable`.
- Use `List.of()`, `Map.of()`, `Set.of()` for immutable collections. Streams for transformations.
- Constructor injection (Spring). `@Valid` for input validation. `@RestControllerAdvice` for errors.
- JUnit 5 + Mockito + AssertJ. `@SpringBootTest` only for integration tests.

### Dart & Flutter

- Follow official Dart style. `dart format` enforced. `PascalCase` types, `camelCase` variables, `_prefix` private.
- Embrace sound null safety. Avoid `!` assertion — handle null explicitly. Prefer `final` by default.
- Use sealed classes (Dart 3) + pattern matching for exhaustive state modeling.
- Use `const` constructors for widgets. Extract widgets into classes, don't nest deeply.
- Riverpod/Bloc/Provider for state (pick one). Separate logic from UI.
- `async/await` for Futures. Always handle errors. Use `mocktail` for testing.

### C

- Every `malloc`/`calloc` must have a matching `free`. Check for `NULL` on allocation.
- Set pointers to `NULL` after freeing. Use `sizeof(*ptr)` for allocation size.
- Use bounded functions: `snprintf` over `sprintf`, `fgets` over `gets`.
- Track buffer sizes alongside pointers. Guard against integer overflow.
- Use `goto cleanup` pattern for multi-resource functions.
- Return error codes: `0` success, negative for errors. `const` everything possible.
- Use `<stdint.h>` fixed-size types. Compile with `-Wall -Wextra -Werror`.
- Run sanitizers (`-fsanitize=address,undefined`) and static analysis (cppcheck, clang-tidy).

### C++

- Never raw `new`/`delete`. Use `std::make_unique` (default), `std::make_shared` (shared ownership only).
- RAII for every resource. Pass `T&`/`const T&` to functions, not smart pointers (unless transferring ownership).
- Use `std::optional`, `std::variant`, `std::string_view`, structured bindings, `constexpr`.
- Use `std::span<T>` for non-owning contiguous views. `std::expected<T,E>` (C++23) for error handling.
- Mark everything `const`: variables, references, member functions. `noexcept` on move ops and destructors.
- Prefer STL containers and `<algorithm>` / `<ranges>`. Reserve vector capacity when known.
- `std::mutex` + `std::scoped_lock` for shared data. `std::atomic` for simple counters.
- Compile with `-Wall -Wextra -Wpedantic -Werror`. Use clang-tidy with Core Guidelines.

### REST API Design

- Nouns for resources, plural: `/users`, `/orders`. Shallow nesting (max 2-3 levels).
- Correct HTTP methods and status codes. Consistent response envelope.
- Version APIs (`/api/v1/`). Paginate all list endpoints. Rate limit everything.
- Document with OpenAPI/Swagger.
