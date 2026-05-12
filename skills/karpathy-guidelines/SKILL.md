---
name: karpathy-guidelines
description: Behavioral guidelines to reduce common LLM coding mistakes. Covers thinking before coding, simplicity, surgical changes, goal-driven execution, root-cause decisions, surfacing conflicts, failing loud, using the model only for judgment calls, and checkpointing multi-step work.
license: MIT
---

# Karpathy Guidelines

Behavioral guidelines to reduce common LLM coding mistakes, derived from [Andrej Karpathy's observations](https://x.com/karpathy/status/2015883857489522876) on LLM coding pitfalls.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- Don't assume I know exactly what I want. If my motivation or goal is unclear, pause and clarify it with me.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler or better approach exists, say so directly. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Before adding new code, read exports, callers, and shared utilities in the surrounding area first.
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you don't understand why existing code is structured the way it is, ask before adding to it.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

Tests must encode WHY behavior matters, not just WHAT it does. A test that can't fail when business logic changes is misleading.

## 5. Root-Cause Decisions

**Fix causes, not symptoms. Every decision answers "why."**

- Identify root causes before proposing fixes. A workaround is a flag for follow-up, not a fix.
- Before deciding, review the existing design and weigh trade-offs.
- Focus on what matters. Strip details that don't affect the decision.

## 6. Reserve the model for judgment calls

**Use Claude for classification, drafting, summarization, and extraction. Not for routing, retries, or deterministic transforms.**

- If plain code can answer the question, plain code answers the question.
- Don't delegate decisions that simple logic can decide.
- Every unnecessary model call for a deterministic decision adds cost and latent flakiness.

## 7. Surface conflicts, don't average them

**When two existing patterns contradict, don't blend them. Pick one and flag the other.**

- Choose the more recent or more tested pattern, explain why, and flag the other for cleanup.
- Code that tries to satisfy two contradictory rules is worse than either alone.

## 8. Fail loud

**"Completed" is wrong if anything was skipped. "Tests pass" is wrong if any were skipped. Default to surfacing uncertainty.**

- If you can't be sure something worked, say so explicitly.
- Surface skipped records, suppressed errors, and unverified edge cases.
- Silent success is the most expensive kind of failure.

## 9. Checkpoint after every significant step

**For multi-step tasks: summarize what was done, what's verified, and what's left before continuing.**

- Don't continue from a state you can't describe back.
- If you lose track, stop and restate before proceeding.
- Checkpoints catch drift early — one wrong turn shouldn't cascade into the remaining steps.

---

**These guidelines are working if:** fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, clarifying questions come before implementation rather than after mistakes, and you hear about problems before they compound.
