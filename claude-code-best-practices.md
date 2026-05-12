# Best practices for Claude Code

> Source: https://code.claude.com/docs/en/best-practices

Claude Code is an agentic coding environment. Unlike a chatbot that answers questions and waits, Claude Code can read your files, run commands, make changes, and autonomously work through problems while you watch, redirect, or step away entirely.

This changes how you work. Instead of writing code yourself and asking Claude to review it, you describe what you want and Claude figures out how to build it. Claude explores, plans, and implements.

Most best practices are based on one constraint: **Claude's context window fills up fast, and performance degrades as it fills.**

---

## Give Claude a way to verify its work

Include tests, screenshots, or expected outputs so Claude can check itself. This is the single highest-leverage thing you can do.

Claude performs dramatically better when it can verify its own work — run tests, compare screenshots, validate outputs.

| Strategy | Before | After |
|---|---|---|
| Provide verification criteria | "implement a function that validates email addresses" | "write a validateEmail function. example test cases: user@example.com is true, invalid is false, user@.com is false. run the tests after implementing" |
| Verify UI changes visually | "make the dashboard look better" | "[paste screenshot] implement this design. take a screenshot of the result and compare it to the original. list differences and fix them" |
| Address root causes, not symptoms | "the build is failing" | "the build fails with this error: [paste error]. fix it and verify the build succeeds. address the root cause, don't suppress the error" |

---

## Explore first, then plan, then code

Separate research and planning from implementation to avoid solving the wrong problem. Use **plan mode** to separate exploration from execution.

### The four phases

**1. Explore** — Enter plan mode. Claude reads files and answers questions without making changes.
```
read /src/auth and understand how we handle sessions and login.
also look at how we manage environment variables for secrets.
```

**2. Plan** — Ask Claude to create a detailed implementation plan.
```
I want to add Google OAuth. What files need to change?
What's the session flow? Create a plan.
```
> Press `Ctrl+G` to open the plan in your text editor for direct editing before Claude proceeds.

**3. Implement** — Switch out of plan mode and let Claude code, verifying against its plan.
```
implement the OAuth flow from your plan. write tests for the
callback handler, run the test suite and fix any failures.
```

**4. Commit** — Ask Claude to commit with a descriptive message and create a PR.
```
commit with a descriptive message and open a PR
```

> Planning is most useful when you're uncertain about the approach, when the change modifies multiple files, or when you're unfamiliar with the code being modified. If you could describe the diff in one sentence, skip the plan.

---

## Provide specific context in your prompts

The more precise your instructions, the fewer corrections you'll need.

| Strategy | Before | After |
|---|---|---|
| Scope the task | "add tests for foo.py" | "write a test for foo.py covering the edge case where the user is logged out. avoid mocks." |
| Point to sources | "why does ExecutionFactory have such a weird api?" | "look through ExecutionFactory's git history and summarize how its api came to be" |
| Reference existing patterns | "add a calendar widget" | "look at how existing widgets are implemented on the home page... follow the pattern to implement a new calendar widget..." |
| Describe the symptom | "fix the login bug" | "users report that login fails after session timeout. check the auth flow in src/auth/, especially token refresh..." |

---

## Provide rich content

- Reference files with `@` instead of describing where code lives
- Paste images directly (copy/paste or drag and drop)
- Give URLs for documentation and API references
- Pipe in data: `cat error.log | claude`
- Let Claude fetch what it needs via Bash commands, MCP tools, or file reads

---

## Configure your environment

### Write an effective CLAUDE.md

Run `/init` to generate a starter `CLAUDE.md` file, then refine over time. It is read at the start of every conversation.

```markdown
# Code style
- Use ES modules (import/export) syntax, not CommonJS (require)
- Destructure imports when possible (eg. import { foo } from 'bar')

# Workflow
- Be sure to typecheck when you're done making a series of code changes
- Prefer running single tests, and not the whole test suite, for performance
```

**Include ✅**
- Bash commands Claude can't guess
- Code style rules that differ from defaults
- Testing instructions and preferred test runners
- Repository etiquette (branch naming, PR conventions)
- Architectural decisions specific to your project
- Developer environment quirks (required env vars)
- Common gotchas or non-obvious behaviors

**Exclude ❌**
- Anything Claude can figure out by reading code
- Standard language conventions Claude already knows
- Detailed API documentation (link to docs instead)
- Information that changes frequently
- Long explanations or tutorials
- File-by-file descriptions of the codebase
- Self-evident practices like "write clean code"

CLAUDE.md files can be placed in:
- `~/.claude/CLAUDE.md` — applies to all sessions
- `./CLAUDE.md` — project root, check into git
- `./CLAUDE.local.md` — personal project-specific notes (add to `.gitignore`)
- Parent/child directories for monorepos

### Configure permissions

Three ways to reduce approval interruptions:
- **Auto mode** — a classifier reviews commands and blocks only risky ones
- **Permission allowlists** — permit specific tools you know are safe (`/permissions`)
- **Sandboxing** — OS-level isolation for filesystem and network access

### Use CLI tools

Tell Claude Code to use CLI tools like `gh`, `aws`, `gcloud`, and `sentry-cli` when interacting with external services. They are the most context-efficient way to interact with external services.

### Connect MCP servers

Run `claude mcp add` to connect external tools like Notion, Figma, or your database.

### Set up hooks

Use hooks for actions that must happen every time with zero exceptions. Unlike CLAUDE.md instructions which are advisory, hooks are deterministic.
- `"Write a hook that runs eslint after every file edit"`
- `"Write a hook that blocks writes to the migrations folder"`

### Create skills

Create `SKILL.md` files in `.claude/skills/` to give Claude domain knowledge and reusable workflows.

```markdown
---
name: api-conventions
description: REST API design conventions for our services
---
# API Conventions
- Use kebab-case for URL paths
- Use camelCase for JSON properties
- Always include pagination for list endpoints
```

### Create custom subagents

Define specialized assistants in `.claude/agents/` that Claude can delegate to for isolated tasks.

```markdown
---
name: security-reviewer
description: Reviews code for security vulnerabilities
tools: Read, Grep, Glob, Bash
model: opus
---
You are a senior security engineer. Review code for:
- Injection vulnerabilities (SQL, XSS, command injection)
- Authentication and authorization flaws
- Secrets or credentials in code
```

### Install plugins

Run `/plugin` to browse the marketplace. Plugins bundle skills, hooks, subagents, and MCP servers into a single installable unit.

---

## Communicate effectively

### Ask codebase questions

Ask Claude questions you'd ask a senior engineer:
- How does logging work?
- How do I make a new API endpoint?
- What edge cases does CustomerOnboardingFlowImpl handle?
- Why does this code call foo() instead of bar() on line 333?

### Let Claude interview you

For larger features, have Claude interview you first:

```
I want to build [brief description]. Interview me in detail using the AskUserQuestion tool.

Ask about technical implementation, UI/UX, edge cases, concerns, and tradeoffs.
Keep interviewing until we've covered everything, then write a complete spec to SPEC.md.
```

---

## Manage your session

### Course-correct early and often

- **Esc** — stop Claude mid-action, context is preserved
- **Esc + Esc** or `/rewind` — restore previous conversation and code state
- **"Undo that"** — have Claude revert its changes
- `/clear` — reset context between unrelated tasks

> If you've corrected Claude more than twice on the same issue in one session, run `/clear` and start fresh with a more specific prompt.

### Manage context aggressively

- Use `/clear` frequently between tasks
- Run `/compact <instructions>` for more control (e.g., `/compact Focus on the API changes`)
- Customize compaction behavior in CLAUDE.md
- Use `/btw` for quick questions that don't need to stay in context

### Use subagents for investigation

```
Use subagents to investigate how our authentication system handles token
refresh, and whether we have any existing OAuth utilities I should reuse.
```

### Rewind with checkpoints

Every action Claude makes creates a checkpoint. Double-tap Escape or run `/rewind` to open the rewind menu. Checkpoints persist across sessions.

### Resume conversations

- `claude --continue` — pick up the most recent session
- `claude --resume` — choose from a list of sessions
- Use `/rename` to give sessions descriptive names

---

## Automate and scale

### Run non-interactive mode

```bash
# One-off queries
claude -p "Explain what this project does"

# Structured output for scripts
claude -p "List all API endpoints" --output-format json

# Streaming for real-time processing
claude -p "Analyze this log file" --output-format stream-json
```

### Run multiple Claude sessions in parallel

- **Worktrees** — separate CLI sessions in isolated git checkouts
- **Desktop app** — manage multiple local sessions visually
- **Claude Code on the web** — sessions on cloud infrastructure in isolated VMs
- **Agent teams** — automated coordination with shared tasks and a team lead

**Writer/Reviewer pattern:**

| Session A (Writer) | Session B (Reviewer) |
|---|---|
| Implement a rate limiter for our API endpoints | Review the rate limiter implementation in @src/middleware/rateLimiter.ts |
| Here's the review feedback: [output]. Address these issues. | — |

### Fan out across files

```bash
for file in $(cat files.txt); do
  claude -p "Migrate $file from React to Vue. Return OK or FAIL." \
    --allowedTools "Edit,Bash(git commit *)"
done
```

### Run autonomously with auto mode

```bash
claude --permission-mode auto -p "fix all lint errors"
```

---

## Avoid common failure patterns

| Pattern | Fix |
|---|---|
| **The kitchen sink session** — mixing unrelated tasks | `/clear` between unrelated tasks |
| **Correcting over and over** — context polluted with failed approaches | After two failed corrections, `/clear` and write a better initial prompt |
| **The over-specified CLAUDE.md** — important rules get lost in the noise | Ruthlessly prune. Delete what Claude already does correctly |
| **The trust-then-verify gap** — plausible-looking implementation without edge case handling | Always provide verification (tests, scripts, screenshots) |
| **The infinite exploration** — Claude reads hundreds of files | Scope investigations narrowly or use subagents |

---

## Related resources

- [How Claude Code works](https://code.claude.com/docs/en/how-claude-code-works) — the agentic loop, tools, and context management
- [Extend Claude Code](https://code.claude.com/docs/en/extend-claude-code) — skills, hooks, MCP, subagents, and plugins
- [Common workflows](https://code.claude.com/docs/en/common-workflows) — step-by-step recipes for debugging, testing, PRs, and more
- [CLAUDE.md](https://code.claude.com/docs/en/claude-md) — store project conventions and persistent context
