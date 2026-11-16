---
name: triage
description: "Triage sched-prod requests into the issue tracker. Merge or close what is already settled, and mark every open issue agent-ready or needs-human. Use when new requests arrive or issues are unmarked."
---

You work alone. Nobody answers questions during a run. A person decides only through a needs-human issue.

Sources of truth: `specs/` (rules, cite them by id: AUT-1, AUT-2, AUT-3, PRD-n, DES-n, ADR-n) and `README.md` (issue format, labels, close reasons, body templates, the collector command).

### Principles
- **Settled first.** Before you create or mark work, ask whether something already settles the request: an issue that asks the same, shipped work, a spec that forbids it, or a later request that withdraws it. If so, close it with its reason and cite the key, spec id or request id.
- **Done means someone shipped it.** A close that no person made, or that nothing confirms, is not done. Reopen it as needs-human.
- **Two-way door: agent-ready.** The change adds to what is there, can be undone, stays inside the specs, and a test can show it works and what must not happen (AUT-1).
- **One-way door: needs-human.** A client relies on the current behaviour, it touches pricing, invoices or terms, or it deletes or rewrites stored data (AUT-2). An unclear request, or two requests that conflict, is also a one-way door.
- **When in doubt, needs-human.** A wrong needs-human costs a person minutes. A wrong agent-ready ships on its own.
- **Specs beat loud requests.** Urgency does not change a mark.
- **Nothing gets lost.** Every request id ends up in the `sources` of exactly one issue.

### Steps
1. Run the collector (README.md) so new requests are filed.
2. Read every issue, open and closed, and group requests that ask for the same thing.
3. Merge: keep the backlog issue (or the oldest request), add each request id to its `sources`, and close the others as duplicate with `duplicate-of:`. Remove the `sources` line from the closed duplicate.
4. Close what is settled, with the README's reason. Mark every open issue with exactly one of agent-ready or needs-human, and write its body from the README template (needs-human reads as AUT-3 says).
5. When a new request changes an issue you marked before, triage that issue again.
6. Run the collector once more, then check: every open issue has exactly one mark, no closed issue has one, and every request id is in exactly one `sources`.

For each issue, ask: Could an agent ship this without asking anyone? Who is hurt if the mark is wrong, and can we undo it?
