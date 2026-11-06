---
name: "safe-retry-gate"
description: "Use when a state-changing action times out, disconnects, or returns an ambiguous result before a retry is considered. Reconcile a timed-out or ambiguous external action before repeating it, to reduce duplicate emails, uploads, submissions, and repository updates."
---

# Safe Retry Gate

After a timeout, establish whether the action already took effect before retrying.

Use this after an interrupted or unclear tool call that may have changed something. Ordinary read-only lookups usually do not need this workflow. Do not delay a clearly successful action just to produce a ledger.

## When to apply this workflow

Use when a state-changing action times out, disconnects, or returns an ambiguous result before a retry is considered. If the host makes this skill available, use it for matching work without waiting for a tag.

Before proposing or attempting a repeat, report whether the original action is confirmed succeeded, confirmed failed, or outcome unknown, with the evidence or gap. Pause the repeat while the outcome is unknown. Continue authorized work that does not depend on the unresolved result.

## Decide before repeating

1. Identify the exact intended action, destination, logical operation, observed error, and any receipt or operation reference. Keep the original user authorization in view.
2. Classify the call: read-only; explicitly retry-safe under the service's documented contract; or state-changing with a possible duplicate effect. A tool name or an agent's guess is not an idempotency guarantee.
3. Check the authoritative destination using already authorized read access. Match the relevant operation, version, recipient, or receipt; similar text alone may identify the wrong action.
4. Report one outcome: **confirmed succeeded**, **confirmed failed**, or **outcome unknown**, with the evidence and its scope. An empty search result is not proof of failure when indexing may lag or visibility is partial.
5. If success is confirmed, do not repeat it. If rejection before any side effect is established, a retry may be appropriate within the original permission and service rules. Otherwise retain uncertainty and explain what evidence is missing.

An explicitly documented idempotency mechanism can make an identical retry appropriate. Reuse its original key only within the documented scope and retention period. Do not reuse a key for a changed request. Two intentionally separate actions need separate logical operation identities even if their content is identical.

## Preserve the unresolved work

Before handing off, record the minimal operation reference, outcome, attempted destination, and next read-only reconciliation step. Do not turn a proposed resend into authorization. If observations conflict, stop and reconcile; choosing whichever status is convenient is unsafe.

Report the intended action, outcome, evidence, duplicate risk, and next action in a few lines. Do not collect message bodies, tokens, cookies, or unrelated account data for bookkeeping.

Read [the reconciliation playbooks](references/playbooks.md) for Gmail, GitHub, uploads, or browser forms. These are workflow guidance, not tested live-service adapters.

## Boundaries

This skill guides decisions; it does not intercept calls or guarantee exactly-once execution. Do not send, purchase, upload, delete, or broaden access merely to test a theory. Use synthetic examples when demonstrating the workflow.
