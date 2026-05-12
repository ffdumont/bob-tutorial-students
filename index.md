---
layout: default
---

# Best practices for IBM Bob

> Source: *Getting Started with IBM Bob*, Markus Eisele (v1.2.0)

Bob is an AI partner for the software development lifecycle. The premise is blunt: code is text, software is a system. Writing code has never been easier; designing systems, changing them safely, and keeping them valuable over time still is.

Bob's mental model has three parts, kept separate on purpose:

- **Intent** — what you are trying to achieve
- **Evidence** — what actually exists in the repo
- **Judgment** — what should be done

Mixing them produces confident code that solves the wrong problem.

---

## Contracts before code

The exact diff Bob writes is not the durable artefact — on a re-run, Bob may take a different but still reasonable path. What stays is the contract: how the team recognises a correct outcome even when the implementation varies.

A useful contract names six things:

- task intent
- success condition
- non-goals
- preserved constraints
- verification method
- stop condition

Contract shape changes with the job:

- **Feature** — acceptance criteria
- **Bug** — a failing test that turns green, plus the guarantee that adjacent behavior stays intact
- **Modernization** — preserved behavior; existing tests should still pass; intentional changes are named, not smuggled in
- **Security work** — threat reduction plus no new exposure
- **Documentation** — accuracy against shipped behavior, not wording that sounds plausible

A worked contract for a modernization task:

> *"Modernize AuthenticationService to Java 21 style while preserving all existing login, token refresh, and audit behavior. No public API changes. All existing tests must pass unchanged. Stop if the refactor requires a behavior change we cannot explain in the PR."*

### ML/DL workflow examples

**Fraud detection with imbalanced dataset** (multi-conversation workflow):

```
Conversation 1 (0.2 BC): Dataset Analysis
Contract: "Analyze imbalance in credit card fraud dataset. Dataset: 284,807
transactions, 492 frauds (0.17%). Recommend sampling strategies without loading
full data. Success: clear recommendation with trade-offs. Stop if analysis
requires loading full dataset."

Conversation 2 (0.8 BC): Sampling Implementation
Contract: "Implement 3 techniques: SMOTE, undersampling, hybrid. Create
evaluation script with F1, AUC-ROC, precision, recall. Success: all three
methods working, evaluation script runs. Stop if any method requires > 1GB memory."

Conversation 3 (0.5 BC): Threshold Optimization
Contract: "Optimize decision threshold for recall > 0.90 while maximizing
precision. Success: threshold found, documented trade-offs. Stop if recall
cannot reach 0.90."

Total: ~1.5 BC
```

**Real-time emotion recognition** (architecture → implementation → optimization):

```
Conversation 1 (0.3 BC): Architecture Planning
Contract: "Design CNN for emotion recognition. Constraints: 48×48 input, 7 classes,
inference < 50ms. Success: architecture diagram with layer specs and estimated
latency. Stop if estimated latency > 50ms."

Conversation 2 (1.0 BC): Pipeline Implementation
Contract: "Implement video pipeline with profiling. Measure latency: capture,
preprocess, inference, display. Success: working pipeline with per-stage timing.
Stop if total latency > 100ms."

Conversation 3 (0.7 BC): Optimization
Contract: "Optimize bottlenecks. Target: latency < 100ms end-to-end. Success:
latency under target, documented optimizations. Stop if optimization requires
model architecture changes."

Total: ~2.0 BC
```

The right moment to write the contract is before execution, not after a good-looking diff appears.

*See Ch.7 (Contracts Before Code).*

---

## Orient, bound, plan — then act

The canonical operating loop has six beats: **Orient → Bound → Plan → Act → Verify → Explain** (OBPAVE).

**Orient** — Bob reads the repo, related files, tests, history. Modes Ask and Plan are read-only; this beat happens before anything lands on disk.

**Bound** — name what is allowed: in-scope files, out-of-scope changes, required approvals, environment limits, stop conditions. Confidence is not the same thing as authorization.

**Plan** — Bob proposes a path. A useful plan names what will change, why, what might break, what stays unchanged, and how the result will be verified. During this beat nothing is generated on disk — the split between planning and execution is deliberate.

**Act** — execute only the approved slice. Execution should feel mechanical: predictable, boring. Surprises belong in planning, while you can still change your mind.

**Verify** — check behavior, not motion. Tests, diff review, manual inspection, preserved-behavior checks, acceptance criteria.

**Explain** — leave behind evidence someone else can review later. Task history, PR description, ticket, short ADR, release notes.

The loop runs at two scales: an **inner loop** (the immediate task) and an **outer loop** (shared rules, modes, review habits across the team). The **evidence ledger** — plans, findings, task history, diffs, verification notes — connects them so one task becomes organizational learning instead of isolated chat output.

*See Ch.3 (The Agentic SDLC), Ch.4.3 (Why Bob Separates Planning from Execution).*

---

## Signal versus noise

Context is a budget, not a dump. Two requests with the same intent can land very differently depending on what sits in the window:

| High signal | Low signal |
|---|---|
| Exact file snippet and explicit goal | Paraphrased code and vague intent |
| Actual stack trace or terminal output | Memory of an error "somewhere in utils" |
| One mission per thread | Several unrelated goals in one chat |
| Current docs or specs for the API you mean | Assumptions from outdated free-form recall |

Grounding habits:

- Mention exact files and line ranges when you can
- Don't paraphrase code from memory when `@` can fetch the real text
- Paste real stack traces or use `@terminal` / `@problems`
- Keep one clear outcome per task thread
- Link authoritative docs or specs when the answer must match an external contract
- Don't treat earlier chat turns like durable memory across sessions — re-ground with mentions when it matters

ML/DL-specific grounding examples:

| High signal | Low signal |
|---|---|
| *"Bob, analyze schema and first 100 rows of @data/fraud.csv"* | *"Bob, analyze @data/fraud.csv"* (284K rows) |
| *"Bob, design CNN for 48×48 input, 7 classes, inference < 50ms"* | *"Bob, design a CNN for emotion recognition"* |
| *"Bob, reduce latency from 80ms to < 50ms in @pipeline.py:45-120"* | *"Bob, improve the model performance"* |
| *"Bob, implement SMOTE for 0.17% minority class, target F1 > 0.85"* | *"Bob, fix the imbalanced dataset"* |

Most "hallucinations" are context debt: a missing constraint, a missing source of truth, a missing test expectation, a business rule that never entered the task.

*See Ch.6.3 (Signal Versus Noise), Ch.6.5 (Grounding Habits), Ch.6.12 (Most Hallucinations Are Context Debt).*

---

## Point Bob at the truth

Typing `@` attaches workspace artefacts on purpose. Recipe: precise `@` mentions, exact error text (or `@terminal` / `@problems`), and a one-sentence goal.

- `@/path/file` — exact file contents; on large files use a line range, e.g. `@/path/File.java:80-120`
- `@/path/folder` — sibling files; folder mentions are non-recursive
- `@problems` — diagnostics from the Problems panel
- `@terminal` — build or CLI output as evidence
- `@git-changes` or a commit hash — when reasoning about diffs, commits, or uncommitted work
- `@` plus a URL — external docs or specs anchor the reply

Office files look small on disk and explode in the window: `.xlsx`, `.docx`, `.pptx` drag in sheets, revision metadata, slide masters, speaker notes, hidden ranges. Filter rows, hide unused sheets, export bounded CSVs.

Explicit file and folder `@` mentions bypass `.bobignore` and `.gitignore` when fetching text. `.bobignore` keeps secrets, keys, and noisy paths out of routine reads; explicit `@` is the override when you intend to pull a path through.

*See Ch.6.4 (Point Bob at the Truth: context mentions), Ch.6.7 (Large spreadsheets, documents, and slides).*

---

## Set up your team memory

### Write what "normal" means here

Three layers hold team memory together:

- **Modes** cap what Bob may do for a chat
- **Slash commands** drop in ready-made prompts — `.bob/commands/` (team) or `~/.bob/commands/` (personal)
- **Rules and project briefs** hold the slower-moving stuff — `AGENTS.md`, `.bob/rules/`, and other repo-local text that says what "normal" means here

`AGENTS.md` is the short map that points people at the rest. `.bob/rules/` holds constraints that should hold every turn. Both are read whenever Bob plans, both are reviewed like code, both are owned in the repo.

*See Ch.15.1 (Two Levers You Did Not Have to Author), Ch.15.6 (Choose the Right Memory Layer).*

### Climb the permission ladder

Agent permissions are a ladder, not a binary switch:

1. Read files and explain
2. Summarize and plan
3. Edit files
4. Run tests
5. Run shell commands
6. Use network
7. Use MCP tools
8. Touch shared environments
9. Prepare production changes
10. Execute production changes

Climb only when the task justifies it; never several rungs at once because the model sounds confident.

Pick the mode before polishing the sentence:

- **Ask** — explanations without edits
- **Plan** — strategy before commits
- **Code** — when the repo and shell are enough
- **Advanced** — when you need browser, MCP, or skills
- **Orchestrator** — for work that genuinely spans specialties; coordinates subtasks rather than forcing one mode to pretend it owns everything

Cycle modes with `⌘.` (macOS) or `Ctrl.` (Windows/Linux).

YOLO mode (everything auto-approved) lets shell, files, and network run without a human pause — fast until one injected prompt acts at machine speed. Turn off blanket auto-approval for shell, outbound network, and infrastructure-changing tools. Allowlisting a command name does not stop hostile flags on the same binary; the risk is rarely the binary alone, it is the arguments.

*See Ch.11.3 (Approvals, YOLO Mode, and "Safe" Commands), Ch.11.4 (The Permission Ladder), Ch.15.2 (Finding Commands and Switching Mode).*

### Shell access through Code mode

Code and Advanced modes can run shell — rung 5 of the permission ladder. The posture from the rest of the ladder applies: keep arguments visible, prefer per-action approvals over executable-only allowlists, and remember that the risk lives in the arguments rather than the binary name.

*See Ch.11.4 (The Permission Ladder).*

### MCP and enterprise integration

MCP connects Bob to external systems and is part of your attack surface.

- Configuration lives in `~/.bob/mcp_settings.json` (user) and `.bob/mcp.json` (project). Treat these like production integration configs; review them in pull requests; do not commit long-lived secrets as plain strings.
- The `alwaysAllow` list runs named tools without an approval prompt — a small YOLO. Keep it empty for anything that writes, runs commands, or touches sensitive systems.
- Put MCP behind a gateway with vault-issued, short-lived credentials.
- Downstream systems should see the developer's identity (On-Behalf-Of), not an overpowered shared service account.

Each MCP server is a bridge into another system — credentials, scopes, and silent tool runs deserve the same skepticism as shipping a new microservice dependency. `arabold/docs-mcp-server` is a useful pattern for indexing versioned documentation so answers ground on current versions instead of static training priors.

*See Ch.11.8 (MCP and Enterprise Integration), Ch.6.15 (Docs MCP server).*

### Rules and project briefs

`AGENTS.md` and `.bob/rules/` hold the slower-moving steering text, read whenever Bob plans. AGENTS.md is the short map; rules are the constraints that should hold every turn. Both are reviewed like code and committed with the repo.

Match the memory layer to the use case:

- **Slash commands** — repeat asks you want one keystroke away
- **Modes** — posture and permissions for whole threads
- **Rules** — constraints that should hold every turn
- **Skills** — multi-step flows with tools and review expectations baked in
- **AGENTS.md** — the short map that points people at the rest

*See Ch.15.6 (Choose the Right Memory Layer).*

### Skills: workflows you trigger with words

Skills are workflows someone already packaged — reviews, migration checks, doc passes. Using them does not mean editing `SKILL.md` directly; it means phrasing the task so Bob matches the skill description.

- Advanced mode is required; skills assume the broad tool surface
- One activation per chat — matching uses your words plus the skill text; if nothing fits, you get a generic answer
- Resolution order: project `.bob/skills/...` beats the same name globally, then `~/.bob/skills/`, plus whatever extensions install
- Name the deliverable in the ask — *"security review of `src/api/auth.ts`"* or *"release notes for the last twenty commits"* — rather than *"help with this file"*

Skill lifecycle:

1. Notice repeated work or repeated confusion
2. Capture the current best workflow in plain language
3. Turn it into a skill, command, mode, or rule only after the pattern is stable enough to be worth sharing
4. Test it on real examples
5. Document when to use it and when not to
6. Review it like code
7. Retire it when the team or product changes

A stale skill is not neutral — it is an outdated habit with better packaging.

*See Ch.15.3 (Skills: Packaged Workflows You Trigger With Words), Ch.15.4 (Skills Are Team Habits in Package Form), Ch.15.5 (The Skill Lifecycle).*

### Orchestrator and helper flows

For work that genuinely spans specialties, **Orchestrator mode** coordinates subtasks rather than packing everything into one mode. It is not "all tools in one blind bundle" — it routes subtasks to bounded contexts.

Some installs also expose **helper agents or split flows** for exploration. Where available, they keep the main thread receiving short cited findings instead of carrying the whole exploration in the same window.

*See Ch.11.7 (Modes, Ignore Files, and Checkpoints), Ch.15.2 (Finding Commands and Switching Mode), Ch.6.14 (Session Handoff and Long Threads).*

### How custom assets are distributed

Custom modes, rules, skills, and slash commands are distributed through the same `.bob/...` directories used for personal use. Team-shared assets live in the repo (`.bob/commands/`, `.bob/skills/`, `.bob/rules/`, `AGENTS.md`); personal ones live under `~/.bob/`. Extensions and admin tooling can install additional assets that resolve below the project-level ones in the lookup order.

*See Ch.15.1 (Two Levers You Did Not Have to Author), Ch.15.3 (Skills: Packaged Workflows You Trigger With Words).*

---

## Ask, and let Bob ask back

### Read the codebase through Bob

Bob mirrors patterns already in the repo when it answers, so newcomers feel house style through repetition. Useful asks:

- *"Analyze this service and explain what it does"*
- *"Explain this pattern"*
- *"What does this code do?"*
- *"What would happen if I change this method signature?"*

The last one produces an impact analysis. For a service whose method is called in several places, Bob returns something like:

> *This method is called by: UserController (3 places), AdminService (1 place), UserEventHandler (2 places). Changing the signature would require updating all 6 call sites.*

Cheap rehearsal beats fixing six call sites after the fact.

Start in Ask mode for read-only exploration.

*See Ch.13.5 (Using Bob for Onboarding and Knowledge Transfer).*

### Let Bob refuse to invent scope

Bob does not edit the repo without a checkpoint; the checkpoint forces clarity. A canonical example, applied to a Quarkus greeting endpoint: the user types *"Add validation to the greeting endpoint."* Bob's first reply refuses to invent scope and offers options:

- Validate that the name parameter is not null or empty
- Validate name length (e.g. min 2, max 50 characters) and format (only letters and spaces)
- Add comprehensive validation: non-null, length constraints, character restrictions, and sanitization
- Show me the current endpoint code so I can suggest appropriate validation

Pick an option and the intent tightens enough to plan against.

The same pattern shows up in modernization, where Bob asks about behavior boundaries before drafting a plan:

> - *Should I preserve the synchronous audit logging behavior, or is it okay to make it asynchronous?*
> - *Should I preserve the "email failures don't block" behavior, or should we add retry logic?*
> - *Should I add pagination to list queries, or keep the current behavior?*
> - *What Java version are we targeting?*

These questions are about behavior boundaries, not line noise.

*See Ch.4.5 (Why Bob Asks Before It Acts), Ch.8.2 (Defining Intent Clearly), Ch.10.4 (Preserving Behavior While Refactoring).*

---

## Keep the window honest

### Reset before you argue

Escalation rule for when context goes bad: if a second correction still misses, treat it as context drift — restart with a smaller, cleaner context set instead of arguing in place.

Stop Conditions — moments to pause:

- Bob repeats itself without adding evidence
- The plan changes without new information
- You cannot explain the diff in plain language
- The window is crowded with stale or conflicting material
- You are asking Bob to compensate for unclear intent
- The tool asks for broader permissions than the task deserves
- Approval has become mechanical because you are tired

The reliable fix is usually not arguing longer; it is reset context and re-ground. Often the fix is a new chat with a tiny, honest context set.

*See Ch.6.10 (When Context Goes Bad: Poisoning), Ch.12.9 (Stop Conditions).*

### Context is a budget, not a dump

The window is on the order of 200K tokens, large but shared. System rules, chat history, `@` attachments, and tool output all draw from the same pool. Auto-condense (when the product summarises older turns) is cited around 140K; the hard cap is in the same ballpark as the headline window size.

Cost optimization techniques:
- Use Plan mode first (cheaper, read-only exploration)
- Reset conversations when context becomes crowded
- Use precise `@` mentions instead of folder-level includes
- Avoid loading full datasets — work with schemas and samples
- Isolate expensive exploration in separate threads

The **Context Pack** is the smallest bounded evidence Bob needs for one task:

- task intent
- relevant files
- known constraints
- tests or expected behavior
- related ticket or customer scenario
- non-goals
- stop condition

Ship a packet another reviewer could follow — not a brain dump.

#### Context Pack examples for ML/DL projects

**Reinforcement Learning project:**
```markdown
✅ Include:
- Environment wrapper (@envs/traffic_env.py)
- Agent architecture (@agents/ppo_agent.py)
- Reward function (@utils/reward.py)
- Config (@config/rl_config.yaml)

❌ Exclude:
- Replay buffers, checkpoints, logs, full simulation files

Estimated cost: 0.3-0.5 BC per conversation
```

**Computer Vision real-time project:**
```markdown
✅ Include:
- Model architecture (@models/emotion_cnn.py)
- Pipeline (@utils/video_pipeline.py)
- Benchmark (@tests/benchmark.py)
- Config (@config/model_config.yaml)

❌ Exclude:
- Full dataset, trained models, video frames, logs

Estimated cost: 0.4-0.6 BC per conversation
```

**Imbalanced dataset project:**
```markdown
✅ Include:
- Dataset schema and statistics
- Sampling strategy (@utils/sampling.py)
- Evaluation metrics (@utils/metrics.py)
- Sample of minority class (100 rows max)

❌ Exclude:
- Full dataset (use summary statistics instead)
- All trained model checkpoints

Estimated cost: 0.2-0.4 BC per conversation
```

Healthy chat checklist:

- **Before** — one goal per task, direct `@` where possible, exact errors from Problems or terminal
- **During** — watch token pressure, review iteratively, keep folder scope tight
- **Before you leave** — write a handoff note (commit it when the team tracks decisions in Git)
- **Hard no** — no secrets in chat, no huge raw Office dumps, no pretending yesterday's chat is permanent memory

*See Ch.6.1 (Why Context Is a Budget, Not a Dump), Ch.6.8 (What "200k Tokens" Means), Ch.6.13 (The Context Pack), Ch.6.16 (Healthy Chat Checklist).*

### Isolate exploration in helper flows

When broad exploration risks crowding the window, isolate it in a helper flow so the main thread only receives short findings. Where the install exposes helper agents or split flows, use them; otherwise run exploration in a separate task and reference its short, cited findings from the main thread.

*See Ch.6.14 (Session Handoff and Long Threads).*

### Snapshot before writes land

Before file changes, Bob can save a checkpoint — a restore point for that task:

- **Restore files** rolls files back and keeps the chat
- **Restore files and task** rolls files back and trims later messages when the thread went wrong

Checkpoints complement Git — they do not replace commits.

*See Ch.5.5 (What Bob Never Touches Unless You Approve It), Ch.11.7 (Modes, Ignore Files, and Checkpoints).*

### Hand off, don't resume

Before switching topics or abandoning a long thread, capture a small handoff artefact — typically a Markdown file under `docs/` — and use it as the anchor for the next task.

Template:

```markdown
docs/handoff-[feature].md

## Goal
## Decisions
## Files touched
## Open questions

Use only what we agreed.
Stop. Do not implement yet.
```

Adjacent patterns: ADR stubs (constraints, chosen approach, rejected alternatives) and repro/runbook notes (exact commands, expected versus actual, minimum `@` set). Stop paying window rent for work you no longer need in view.

*See Ch.6.14 (Session Handoff and Long Threads).*

---

## Beyond the IDE side panel

Bob is centred on the IDE side panel with human approval at each step. The sections below cover surfaces and posture choices that come into play when the workflow leaves the side panel.

### Bob Shell: preface only

Bob's product surface includes Bob Shell alongside the IDE side panel. Practitioner habits for piped, non-interactive invocation (structured output flags, streaming, scripting) live in the IBM Bob product reference rather than in the habits collected here.

*See preface.*

### Parallel sessions: outside the book

Patterns for running multiple Bob sessions concurrently — worktrees, parallel agents, isolated VMs, writer/reviewer pairs — are not part of the practitioner habits collected here. The IDE-side-panel posture assumes one thread, one human approver at a time.

### One plan over many files

For multi-file work, Bob's pattern is coordinated planning. Bob analyses blast radius first — *"What files will be affected if I modernize UserService?"* — and proposes a single coordinated plan spanning every affected file. Orchestrator mode is built for work that genuinely spans specialties.

The impact analysis shape Bob returns:

> - **Files that must change** — UserService.java (primary target), UserServiceTest.java (tests need updates for new patterns)
> - **Files that might need changes** — UserController.java (if method signatures change), UserEventHandler.java (if event handling changes)
> - **Files that should not change** — UserRepository.java, EmailService.java, AuditLogger.java (interfaces stay the same)
> - **Recommendation** — keep UserService interface unchanged; refactor internal implementation only

That is blast-radius mapping: what must move, what might move, what should stay put. One reviewable plan, one audit trail.

*See Ch.10.5 (Coordinating Multi-File Changes), Ch.15.2 (Finding Commands and Switching Mode).*

### Fast until it is not

YOLO mode (everything auto-approved) lets shell, files, and network run without a human pause. Hybrid setups sometimes auto-approve "low-risk" steps; this breaks down for the terminal, where the risk is rarely the binary name alone but the arguments. Recommendations:

- Turn off blanket auto-approval for shell, outbound network, and infrastructure-changing tools unless proven controls exist
- Prefer granular prompts per action
- Do not rely on executable-only allowlists until full command lines are validated — or keep those paths manual

*See Ch.11.3 (Approvals, YOLO Mode, and "Safe" Commands).*

---

## Anti-patterns when using Bob

Seven recurring anti-patterns:

| Anti-pattern | Fix |
|---|---|
| **The Copy-Paste Developer** — shipping Bob's diff without reading it | Read, run, and be ready to justify every line you keep |
| **The Approval Bot** — rubber-stamping plans that look confident | Question scope, alternatives, and failure modes before every approve |
| **The Context-Free Requester** — pinging "fix it" with no `@` mentions or exemplars | Ground the task in files and constraints before asking for edits |
| **The Blame Shifter** — blaming the model when prod misbehaves | Own outcomes from tools you authorised |
| **The Black Box User** — using Bob off-thread, leaving teammates to guess how code appeared | Put intent, plans, and tool use where reviewers already look — commits, PRs, tickets |
| **The Shortcut Seeker** — asking for answers to skip building mental models | Use explanations as teaching aids; verify claims against the repo |
| **The Production Experimenter** — pointing automation at prod without staging or review | Same guardrails as any privileged change: review, staging, humans on approvals, tight MCP and auto-approve posture |

### Budget-conscious pitfalls for students and constrained teams

Five common mistakes that waste tokens unnecessarily:

| Pitfall | Cost Impact | Fix |
|---|---|---|
| **Loading Full Datasets** — *"Bob, analyze @data/creditcard.csv"* (284K rows) | ~0.3 BC wasted | Analyze schema and first 100 rows only; use summary statistics |
| **Long Argumentative Conversations** — continuing to correct Bob in the same crowded thread | ~0.5 BC wasted | Reset after 2 failed corrections; start fresh with clearer context |
| **Vague Intent** — *"Bob, improve the model"* without measurable targets | ~0.2 BC wasted | Specify exact metrics: *"reduce latency from 80ms to < 50ms"* |
| **Skipping Plan Mode** — jumping straight to Code mode without exploration | ~0.5 BC wasted | Use Plan mode first (cheaper, read-only), then execute in Code mode |
| **Including Unnecessary Files** — *@entire_project_folder* instead of targeted mentions | ~0.1-0.2 BC wasted | Use *@specific_file:line_range* or list only relevant files |

**Total potential savings per project:** 1.6-2.7 BC through disciplined context management.

Five situations where reaching for Bob first is the wrong move:

- Learning something new — let Bob tutor after you have felt the edges
- Prototyping — don't let the first polished answer lock the design
- Emergencies — chat latency and judgment should not get between you and the pager
- Problems you don't understand — analyse until the failure mode is named, then automate fixes
- Architectural decisions — ownership stays with people who will maintain the consequences

*See Ch.12.7 (Anti-Patterns When Using Bob), Ch.12.8 (When to Stop Using Bob).*

---

## Keep Bob boring

Excitement in an assistant means variance, and for production work the opposite is what you want.

Four-week ramp:

- **Week 1 — Analysis only.** Read-only work: *"Analyze this service and explain what it does"*, *"Explain why this test is failing"*, *"What would break if I change this method?"* Goal: evidence before keystrokes.
- **Week 2 — Add code review.** Run `/review` before every commit; read findings; fix what you agree with; document what was found.
- **Week 3 — Add planning.** Define clear intent; ask Bob to create a plan; review the plan; approve and execute.
- **Week 4 — Full workflow.** Analysis → plan → execute → review as one rhythm.

If week four still feels foreign, stay on week three longer.

When Bob shines the most: changing unfamiliar code; coordinating complex multi-file changes; maintaining consistency with team conventions; catching issues early through review and security-oriented passes; learning and knowledge transfer.

How to keep Bob boring:

- Use consistent workflows — pick a few paths and run them until muscle memory shows up
- Document patterns — modes, rules, and conventions belong in writing, not folklore
- Review and improve regularly — once a month: what worked, what felt flaky, what one tweak would remove the most thrash
- Share with your team — shared habits beat isolated brilliance
- Resist the temptation to be clever — creative prompting is fun for demos; boring prompting ships

*See Ch.17 (The Bob Mindset), Ch.18 (Keeping Bob Boring).*

---

## Related resources

- *Getting Started with IBM Bob*, Markus Eisele (v1.2.0) — source for the chapter references above
- **IBM Bob documentation** — Modes, Skills, Slash commands, Context mentions, Context window management, Security guidance
- **OWASP Top 10 for LLM Applications (2025)** — shared vocabulary with security and audit (LLM01 prompt injection through LLM10 unbounded consumption); Bob aligns its threat model with this taxonomy