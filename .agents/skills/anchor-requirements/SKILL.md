---
name: anchor-requirements
description: Automatically trigger when user provides lengthy, complex, or multi-faceted requirements. Extracts, structures, and persists requirements into a tracked spec/checklist file to prevent context loss across multi-turn chats or sub-agents, and enforces rigorous acceptance verification.
---

# Skill: anchor-requirements

Convert long, complex user prompts into an immutable, file-backed "Task Contract" with trackable acceptance criteria.

## Trigger Heuristics (When to Act)

Proactively activate this skill when the user's prompt satisfies ANY of the following:
1. **High Complexity / Length**: Prompt contains ≥ 3 distinct functional requirements, or describes a complete feature/workflow.
2. **Explicit Edge Cases & Constraints**: User specifies precise constraints (e.g., performance limits, UI states, specific libraries, "do not touch X").
3. **Multi-Agent / Deep Workflow**: The task will likely require multiple tools, files, or sub-agent delegation.
4. **User Explicit Cue**: User says "here are the requirements", "plan this out", or pastes a dense PRD/issue.

## Artifact Convention

- **Default Path**: `.specs/{YYYY-MM-DD}-{kebab-task-name}.md` (or `specs/current-task.md` if single active task).
- **Format**: Markdown with persistent status checkboxes (`- [ ]` / `- [x]`).

## Processing Protocol (The 4 Steps)

### Step 1: Parse & Atomize (Compile to Spec)
Do not jump straight into coding. Parse the user's input into:
- **Core Objective**: 1-sentence goal.
- **Explicit Constraints**: Negative rules ("Do NOT do X", "Must use Y").
- **Atomized Acceptance Checklist**: Break big requirements down into discrete, binary-verifiable checklist items.
- **Unstated / Inferred Edge Cases**: Flag non-obvious traps (e.g., error states, empty states, auth timeouts).

### Step 2: Persist File & Notify User
Immediately write the file using the **Spec Template** below. Inform the user:
> *"I have anchored your detailed requirements into `{file_path}`. This will serve as our contract to prevent detail degradation across multi-turn chats and sub-agent delegations. Let me know if anything needs adjusting before I proceed."*

### Step 3: Sub-Agent Context Hand-off
Whenever spawning or delegating to a sub-agent:
- **Always inject the spec file path**: Instruct the sub-agent to read `.specs/...` first.
- Direct sub-agents to only report back completion against specific checklist IDs (e.g., `AC-01`, `AC-02`).

### Step 4: Verification Gate (Before Declaring "Done")
- **Never claim task completion without reading the spec file**.
- Perform an explicit audit pass: check each item in the file, toggle `- [ ]` to `- [x]`, and provide verification proof (test command, screenshot, or code diff).

---

## Spec File Template

When writing the file, use this structure strictly:

```markdown
# Spec Contract: {Task Title}

- **Created**: {YYYY-MM-DD HH:mm}
- **Status**: [In Progress | Completed | Blocked]
- **Target Files/Modules**: [List of relevant files]

## 1. Core Objective
{Brief 1-2 sentence summary of what success looks like}

## 2. Hard Constraints & Negative Rules (Non-negotiables)
- [ ] **C-01**: {e.g., Must not alter existing public API signatures}
- [ ] **C-02**: {e.g., Must maintain bundle size under X / No new external dependencies}

## 3. Atomized Acceptance Criteria (Checklist)
<!-- Each item MUST be concrete and verifiable -->
- [ ] **AC-01**: {Specific UI or functional requirement}
- [ ] **AC-02**: {Specific parameter handling / validation}
- [ ] **AC-03**: {Specific return type or state transition}
- [ ] **AC-04**: {Error handling: what happens on network failure/invalid input}

## 4. Edge Cases & Boundary Conditions
- {Edge Case 1: e.g., Concurrent requests}
- {Edge Case 2: e.g., Null/Undefined input handling}

## 5. Execution & Verification Log
<!-- Updated as the agent progresses -->
- [ ] Initial scaffolding
- [ ] Implementation
- [ ] Automated tests / manual verification
```

---

## Maintenance & Mid-Flight Changes

- **Requirement Drift**: If the user adds or modifies requirements mid-conversation, update the `.specs/` file **first**, then acknowledge the change.
- **Context Refresh**: If the conversation becomes long and context feels degraded, Agent must re-read the `.specs/` file to restore full fidelity.
