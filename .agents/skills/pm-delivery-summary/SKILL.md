---
name: pm-delivery-summary
description: Enforce this format for all final summaries and task handoffs. Treats the user as a busy Product Manager by suppressing low-level code walkthroughs and throttling verbosity. Focuses strictly on deliverables, deviations, key mechanics, and actionable user steps.
---

# Skill: pm-delivery-summary

Deliver concise, low-cognitive-load conclusions tailored for a Product Manager. Suppress implementation trivia; prioritize business/design outcomes and next actions.

## Core Mindset (The PM Rule)

- **Default Persona**: Assume the user is a **busy Product Manager** who cares about *what was achieved, what broke/deviated, and what they need to do next*.
- **The Escape Hatch**: Only provide line-by-line code explanations or verbose architectural dissertations if the user explicitly asks: *"Show me the code"*, *"Explain how you implemented X"*, or *"As a developer..."*.
- **Progressive Disclosure**: Never dump everything in one go. Keep the final response short and scannable (< 300 words). If the user has doubts, let them follow up.

## Strict Negative Constraints (What NOT to Do)

- ❌ **No File-by-File Walkthroughs**: Do NOT write "First I modified `User.ts`, then I imported `service.ts`...".
- ❌ **No Long Code Blocks**: Max 5 lines of code/config in the final summary (unless specifically requested).
- ❌ **No Log Dumps**: Never paste raw terminal output or stack traces into the final handoff.
- ❌ **No Filler / Fluff**: Avoid generic pleasantries ("I hope this helps! Feel free to ask...").

## Self-Check Gate (Before Outputting)

Before emitting the final message, run this internal check:
1. *Can the user finish reading this on half a mobile/terminal screen without scrolling?*
2. *Did I leak implementation details (variables, class names, file trees) instead of product impact?*
3. *Are the action items unmistakably prominent?*

If too long, **cut 40% of the words** before sending.
