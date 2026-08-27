---
name: hard-cut
description: "Enforce a hard-cut product policy when a change intentionally replaces existing product behavior or internal architecture: keep one canonical runtime implementation and remove compatibility, fallback, adapter, and dual-behavior code unless transition support is explicitly requested or required by a verified external contract. Use for changes to persisted state, startup recovery, routing, contracts, configuration, schemas or enums, feature flags, and architecture where new canonical behavior supersedes old behavior. Do not use merely because a task touches these areas without replacing behavior."
---

# Hard-Cut Policy

## Overview

Apply a hard-cut policy when new behavior supersedes old behavior. Keep one canonical runtime codepath, distinguish runtime compatibility from one-time data conversion, and preserve verified external contracts and user-owned data.

## Operating Rules

- Identify the canonical target behavior from the user request, acceptance criteria, current contracts, authoritative documentation, and relevant tests before removing alternatives. Surface material conflicts or ambiguity before implementation.
- Delete compatibility bridges, fallback paths, dual reads or writes, adapter layers, old enum aliases, legacy route parsing, and silent coercions from the primary runtime codepath.
- Treat historical local state as non-authoritative only after verifying that it is ephemeral or rebuildable, or that the user authorized invalidating it.
- Separate runtime compatibility from one-time data conversion. Use a forward or offline migration when needed to preserve valid data while keeping one canonical runtime format.
- Do not destroy, reset, rewrite, or abandon user-owned, shared, or production data without explicit authorization.
- Check whether public APIs, deployed clients, storage and retention requirements, versioned protocols, or deployment constraints create a concrete compatibility requirement. Preserve transition support only when that requirement is explicitly requested or verified; do not infer it from silence.
- Do not add compatibility for hypothetical stale clients, version skew, downgrades, unknown consumers, or future migration needs. Require concrete evidence that such support is needed.
- Implement the hard cut directly. Do not introduce migration frameworks, transition orchestration, compatibility abstractions, or telemetry solely for removed behavior when a simple replacement or documented reset is sufficient.
- Update contracts, validation, flags, constants, and configuration in one canonical location. Do not preserve parallel policy logic.
- Fail fast with actionable diagnostics when state, inputs, or contracts do not match the canonical format. Do not silently mutate or delete invalid state.
- Prefer explicit operator or user recovery steps over runtime fallback logic.

## Decision Test

1. Identify the canonical target behavior and the evidence that makes it authoritative.
2. Determine whether explicit instructions or verified external contracts require transition support.
3. Classify affected state as ephemeral, rebuildable, user-owned, shared, or production data.
4. If no transition requirement exists, remove the old path and keep only the canonical runtime behavior. Report invalidated state and required recovery steps.
5. If transition support is required, keep it narrow and temporary. Record its rationale, owner, exit condition, and exact deletion criteria in the final summary or PR body. Link an existing ADR or task when available; never invent one.

## Review Checklist

- Remove obsolete runtime migration and fallback code after any required one-time conversion is complete.
- Collapse duplicated validation or policy logic into one source of truth.
- Replace silent fallback with an explicit error, assertion, or recovery instruction.
- Prefer actionable invalid-state diagnostics over best-effort parsing or coercion.
- Remove obsolete tests, fixtures, documentation, flags, telemetry, and identifiers associated only with the old path.
- Search for old identifiers and behavior branches, then run the relevant tests.
- Report affected persisted state, conversion or recovery steps, and any unavoidable temporary compatibility code in the final summary or PR body.
