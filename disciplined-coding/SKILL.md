---
name: disciplined-coding
description: Apply disciplined software-engineering behavior before and during code changes by surfacing assumptions and ambiguity, choosing the simplest sufficient implementation, keeping diffs surgical, and defining and verifying success criteria. Use for implementing features, fixing bugs, refactoring, reviewing changes, or any task that modifies an existing codebase where correctness, scope control, and minimal complexity matter.
---

# Disciplined Coding

Optimize for the smallest verified change that satisfies the user's actual goal. Apply all four principles throughout the task.

## 1. Think Before Coding

- Read the relevant code, tests, repository instructions, and surrounding contracts before editing.
- State assumptions that materially affect the implementation.
- When a request has multiple plausible interpretations, present the meaningful alternatives and their consequences. Ask before proceeding if the choice materially changes behavior, scope, risk, or architecture.
- For low-impact ambiguity, choose the least-invasive interpretation, state it briefly, and continue.
- Surface contradictions, missing information, and uncertainty instead of hiding them.
- Push back when the request conflicts with the codebase, creates avoidable risk, or has a materially simpler solution. Explain the tradeoff concisely.
- Stop and ask when confusion prevents a safe, correct implementation.

## 2. Apply Simplicity First

- Write the minimum code needed to meet the stated requirements.
- Add no speculative features, extension points, configurability, or flexibility.
- Avoid abstractions for single-use logic. Prefer direct code and established project patterns.
- Add error handling only for realistic failure modes and existing contract boundaries.
- Reuse existing concepts before introducing new layers, types, helpers, or dependencies.
- If the implementation is substantially larger than the problem requires, simplify it before finishing.

Use this test: Would an experienced maintainer consider the solution overcomplicated for the stated requirement? If yes, reduce it.

## 3. Make Surgical Changes

- Change only files and lines required by the user's request.
- Preserve unrelated code, comments, formatting, naming, and behavior.
- Do not refactor adjacent code merely because it could be improved.
- Match the local style and architecture unless changing them is part of the request.
- Remove imports, variables, functions, tests, or comments only when the current change makes them obsolete.
- Leave pre-existing dead code in place unless the user asks to remove it. Mention relevant unrelated issues separately.
- Review the final diff and ensure every changed line traces directly to the request or to verification of it.

## 4. Execute Toward Verifiable Goals

- Translate the request into observable success criteria before implementation.
- For a bug fix, first reproduce the failure with a focused test when feasible, then make it pass.
- For validation or behavior changes, write or update tests that demonstrate the requested cases when feasible.
- For refactoring, establish that behavior passes before and after the change.
- For multi-step work, state a brief plan in this form:

  1. `[Step]` -> verify: `[specific check]`
  2. `[Step]` -> verify: `[specific check]`

- Work until the criteria are satisfied. Run focused checks first, then broader checks proportional to the risk.
- If a check cannot be run, state exactly what remains unverified and why.
- Stop when the requested goal is met; do not expand the task with optional improvements.

## Report the Result

Lead with the outcome. Summarize the material changes, verification performed, and any remaining limitation or risk. Mention assumptions only when they affected the result.
