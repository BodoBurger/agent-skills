---
name: hard-cut
description: "Enforce a hard-cut policy when a change replaces old behavior with one canonical implementation. Remove obsolete compatibility, fallback, adapter, and dual-behavior code unless transition support is explicitly requested or required by a verified external contract. Use only when existing behavior is actually superseded, not merely because a task touches configuration, schemas, routing, contracts, or architecture."
---

# Hard-Cut Policy

Keep one canonical runtime path when new behavior supersedes old behavior. Preserve valid user-owned data and verified external contracts without carrying unnecessary compatibility code.

## Operating Rules

- Identify the canonical target behavior from the request and the minimum relevant evidence. Inspect broader contracts, documentation, or tests only when needed to resolve material uncertainty or risk.
- Remove compatibility bridges, fallback paths, dual reads or writes, adapter layers, aliases, legacy parsing, and silent coercions that exist only for the superseded behavior.
- Do not add compatibility for hypothetical stale clients, version skew, downgrades, unknown consumers, or future migration needs. Require concrete evidence.
- Distinguish runtime compatibility from one-time data conversion. Use a focused conversion only when valid persisted data must be preserved.
- Do not destroy, reset, rewrite, or abandon user-owned, shared, or production data without explicit authorization.
- Preserve transition support only when explicitly requested or required by a verified external contract, deployed client, protocol, storage requirement, or deployment constraint.
- Keep required transition support narrow and temporary; avoid migration frameworks, compatibility abstractions, orchestration, or telemetry when a simple cutover is sufficient.
- Keep contracts, validation, flags, constants, and configuration canonical. Do not preserve parallel policy logic.
- Prefer explicit errors or documented recovery steps over runtime fallback or best-effort coercion.

## Decision Test

1. What is the canonical target behavior?
2. Is transition support explicitly requested or required by concrete evidence?
3. Does affected persisted state require preservation or conversion?
4. If not, remove the old runtime path and keep only the canonical implementation.
5. If transition support is required, keep only the minimum needed and state its rationale and deletion condition.

## Verification

- Verify the changed behavior with the smallest relevant checks first.
- Search for old identifiers or branches only when they are directly related to the removed behavior.
- Run broader tests or inspect broader repository context only when the change risk justifies it.
- Remove obsolete tests, fixtures, docs, flags, telemetry, and identifiers only when they exist solely for the removed path.
- Report any invalidated state, required conversion or recovery steps, and unavoidable temporary compatibility code.
