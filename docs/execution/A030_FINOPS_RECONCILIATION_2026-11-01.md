# A030 — Two-Provider FinOps / Effective-State Reconciliation

Date: 2026-11-01
Authority: Zippy Technology Intelligence A030
Status: EXECUTION DISPATCHED

## Goal

Produce one real, reproducible reconciliation from authorized provider evidence. This is the acceptance gate before additional Kiro Analytics dashboard work.

## Worker lanes

### Collector
- Use exactly two authorized providers/accounts.
- Capture source record IDs/timestamps, account generation, requested/served model, usage, cache/service tier, and billing evidence.
- Do not store credentials or raw secrets.

### Normalizer
Map each provider into:

configured preference → advertised catalog → entitlement → requested model → selected/allocated model → served model → tool/subagent/background usage → cache/service tier → billed evidence.

### Adversarial reviewer
Try to find:
- missing events flattened to zero;
- stale-account asynchronous results;
- list price mislabeled as settled spend;
- child/background calls omitted;
- requested model assumed equal to served model;
- provider credits/multipliers treated as invoice truth.

### Verifier
Run one fixed workload and emit:
- telemetry completeness: COMPLETE / PARTIAL / NON_BACKFILLABLE / UNKNOWN;
- cost disposition: SETTLED / ESTIMATED / UNKNOWN;
- requested-vs-served variance;
- provider-level and session-level totals;
- evidence receipt for every normalized row.

## Acceptance criteria

1. Missing telemetry is never zero.
2. No estimated cost is labeled settled.
3. Account generation is carried through asynchronous work.
4. Subagent/background usage is included when evidence exists.
5. Requested and served model identities remain separate.
6. Output can be consumed by ZippyMesh and ZippyCodeAudit.
7. One concise customer/operator report is generated from the same ledger.
8. No new generic dashboard feature work until this gate passes.

## Deliverables

- normalized ledger fixture;
- provider adapters or import path used for the pilot;
- reproducible command/runbook;
- variance report;
- evidence-linked summary;
- failure/unknown inventory.

## Local execution note

If COM10 or provider telemetry is inaccessible from the active agent, preserve this packet and record the exact missing access. Do not simulate a successful reconciliation.