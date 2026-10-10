---
name: research-and-reuse
description: Eliminates passivity toward web/GitHub search. Mandates proactive searching for mature open-source implementations, official docs, and existing solutions before tackling complex designs or debugging stubborn errors. Prioritizes reusing battle-tested patterns over reinventing the wheel.
---

# Skill: research-and-reuse

Overcome model search-reluctance. Enforce an "Open-Source-First, Search-Before-Inventing" mandate for non-trivial engineering tasks.

## The Prime Directive (Anti-NIH Rule)

> **"Never invent from scratch in an isolated silo what the open-source community has already solved and battle-tested."**

Do not treat web/GitHub search as an "optional last resort" after failing. Treat it as a **first-class intelligence gathering step** before writing code or when stuck.

---

## Mandatory Search Gates (搜索硬性门禁)

You **MUST** invoke web search tools before proceeding if the task hits ANY of these gates:

### Gate 1: Complex Design / Subsystem Gate (禁止闭门造轮子)
- **Scenarios**: Implementing auth flows, file upload/chunking, distributed locks, retry/backoff, rate limiting, state machine synchronization, or data streaming.
- **Required Action**: Search how reputable open-source projects or popular libraries implement this pattern. Prefer adopting standard libraries, official recipes, or canonical GitHub patterns over bespoke hand-rolled code.

### Gate 2: The "Stubborn Error / Trap" Gate (禁止瞎猜盲改)
- **Scenarios**: 
  - Any error message containing a framework-specific error code or silent failure.
  - The first attempt to fix a bug failed.
  - Unexplained runtime quirks, hydration mismatches, version conflicts, or build tool failures.
- **Required Action**: Freeze code edits immediately. Copy the exact error signature and search GitHub Issues, StackOverflow, or release discussions.

### Gate 3: Fast-Moving Ecosystem Gate (警惕知识滞后)
- **Scenarios**: Involving modern or rapidly iterating frameworks (e.g., Next.js App Router, Tailwind v4, Vite, Deno, Bun, AI/LLM SDKs, cloud APIs).
- **Required Action**: Verify current API signatures and breaking changes against latest official documentation or GitHub repos. Do not rely solely on pre-trained memory.

---

## High-Hit-Rate Search Tactics (高级搜索指令)

When calling search tools, do not use vague conversational queries. Construct high-signal, engineer-level queries:

| 场景 | 推荐搜索查询范式 (Search Query Formula) |
| :--- | :--- |
| **搜错误/踩坑** | `"[Exact Error Text]"` `[Framework Name]` `site:github.com` OR `site:stackoverflow.com` |
| **搜开源方案** | `best practice [Tech Stack] [Feature]` OR `github repo [Feature] [Language]` |
| **搜架构/模式** | `how does [Famous Project] handle [Problem]` (e.g., `how does Prisma handle connection pool neon`) |
| **搜最新变更** | `[Library Name] [New Version] migration guide breaking changes` |

---

## Evaluation & Reuse Rules (如何甄别与复用)

1. **Prefer Battle-Tested over Ad-hoc**: If a mature, active, lightweight library exists for the problem (e.g., `p-limit` for concurrency, `zod` for validation, `ms` for time parsing), **recommend installing it** instead of writing 100 lines of brittle custom logic.
2. **Cite the Source**: When adopting an open-source architecture, recipe, or workaround, briefly mention the source (e.g., *"参考了 [开源项目名] 的经典重试策略/官方 Issue #1234 的解决方案"*).
3. **Verify License & Dependency Weight**: Avoid dragging in bloated, unmaintained, or GPL-restrictive packages for tiny utilities. If the package is heavy, extract and adapt the core algorithm/snippet directly from its open-source repository.

---

## Strict Negative Constraints (红线行为)

- ❌ **No Brute-Force Guessing**: Strictly forbidden to modify code blindly for >2 iterations without searching for the error string.
- ❌ **No Over-Engineering**: Do not handcraft complex utility libraries from memory when standard community solutions exist.
- ❌ **No Passive Waiting**: Never ask the user *"Did you encounter this before?"* without having searched GitHub issues and docs first.
