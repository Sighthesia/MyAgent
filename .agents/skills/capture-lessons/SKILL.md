---
name: capture-lessons
description: Auto-invoke or suggest after resolving high-friction bugs, non-trivial debugging loops (>2 failed attempts), or discovering critical external workarounds/best practices via docs/search. Converts actionable experience into reusable project skills.
---

# Skill: capture-lessons

Transform painful debugging cycles, hidden tool traps, and non-obvious external solutions into structured, machine-searchable project skills.

## Trigger Heuristics (When to Act)

Proactively activate this skill when a task concludes and meets ANY of these conditions:
1. **Looping Debugging**: Fixed a stubborn bug after ≥ 2 failed attempts or architectural backtracking.
2. **External Knowledge Discovery**: The root cause or fix was found via web search, official GitHub issues/PRs, or obscure documentation (i.e., not naturally inferable from code context).
3. **Tool / Framework Trap**: Overcame a silent failure, undocumented API quirk, caching issue, or state-machine trap.
4. **Reusable Workflow Pattern**: Devised a novel verification or refactoring sequence that will benefit future sessions.

## Noise Filter (Do NOT Capture If)

- The bug was a simple typo, missing import, or trivial syntax error.
- The solution is project-specific business logic with zero recurrence potential.
- The root cause is not 100% verified (do not document speculative hacks).
- The solution already exists cleanly in standard framework documentation without nuance.

## Decision Flow

1. **Check Existing**: Search existing skills (`.skills/`, `.cursor/rules/`, or project skill directory) to avoid duplication.
2. **Route**:
   - **Extend**: If an existing skill covers the domain, append the new gotcha/edge-case to it.
   - **Create New**: If the pattern represents an isolated tool, technology, or workflow.
   - **Archive/Log**: If valuable for context but too project-specific, write to the task's PR/commit description or debugging log instead.

## Artifact Convention

- **Path**: `.skills/{kebab-case-topic}.md` (or your project's rule folder like `.cursor/rules/`).
- **Naming**: `{domain}-{action-or-trap}.md` (e.g., `playwright-react-hydration-wait.md`, `prisma-neon-connection-pool.md`).

## Generated Skill Schema

When writing or updating a skill, enforce the following markdown format:

```markdown
---
name: {domain}-{topic}
description: Concise summary of symptoms and when to apply this rule (max 2 lines).
---

# {Domain}: {Concise Topic Title}

## Context & Symptoms
- **Failure Cue**: Exact error message, silent failure behavior, or log pattern.
- **Trigger Scenario**: Under what specific environment, stack, or state this happens.

## The Gotcha (Root Cause)
- Why the intuitive approach failed (brief, 1-2 sentences).

## Prescribed Pattern (Solution)
- **Do**: Preferred code pattern, config, or CLI command.
- **Don't**: Intuitive anti-pattern that leads to the trap.

```code-snippet
// Minimal copy-pasteable example of the correct approach
```

## Verification
- How to verify the fix works (e.g., specific test command, health check).
```

## Execution Protocol

1. **Self-Check**: Evaluate the experience against the **Noise Filter**.
2. **Draft & Propose**: Inform the user:
   > *"We resolved a stubborn issue caused by [Root Cause]. I have synthesized this lesson into a new skill `[Skill Name]`. Would you like me to commit it to the project skills?"*
3. **Write**: Upon approval (or auto-save if in headless mode), write the file strictly following the **Generated Skill Schema**.
