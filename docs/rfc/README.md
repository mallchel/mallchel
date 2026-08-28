# RFC Process

RFCs exist to fix three specific problems the guild called out: no accountability, no
driver for initiatives once the discussion ends, and no shared "big picture." This
process is intentionally lightweight — it's meant to make it simple for any engineer
to raise a broad technical idea, not to build a bureaucracy around it.

An RFC is a GitHub Issue. There is no separate repo, no PR-to-merge-a-markdown-file
ceremony. If it later turns out to be an architecturally significant decision, it can
graduate into an [ADR](https://adr.github.io/madr/) (see "Relationship to ADRs" below).

## When do you need an RFC?

Open one if the change:

- touches more than one team or package,
- introduces a new architectural pattern or convention,
- takes significant engineering effort, or
- is hard/expensive to reverse once shipped.

Skip it for anything local, single-team, and easily reversible — just build it and
send a normal PR.

## Roles

| Role | Who | Responsibility |
| --- | --- | --- |
| **Initiator** | Anyone | Writes the RFC. Becomes the Technical Owner if it's accepted. |
| **TSC** | Fixed, named group (see guild announcement) | Validates, discusses, decides, and drives the RFC to a resolution — accepted, rejected, or needs changes. Owns the decision log. Helps sell tech debt work to EM/TL, and coordinates the tech roadmap by priority, handing tasks off to the owning teams. |
| **Facilitator** | One TSC member, assigned at triage | Single point of contact who keeps the discussion moving and makes sure it doesn't stall ("abandonment loop"). |
| **Technical Owner** | Initiator by default, or someone the TSC assigns if the RFC originated from the TSC itself | Assignee of the resulting Jira Epic. Owns delivery, knows the deadlines, sells the work to their EM/TL for roadmap capacity. |

The TSC reviews and drives; it does not silently inherit ownership of every accepted
idea. Every accepted RFC needs one named Technical Owner.

## Lifecycle

1. **Draft** — Initiator opens a GitHub Issue using the RFC template. Label:
   `rfc:draft`.
2. **Triage** — A TSC member claims it as facilitator within 2 business days. Label moves
   to `rfc:in-review`.
3. **Discussion** — Feedback happens in the issue thread and/or the bi-weekly guild
   meeting, same as today. The facilitator keeps a running decision log directly in the
   issue (edits to the top comment or a pinned summary comment) so the rationale is
   permanent and searchable later.
4. **Decision** — The facilitator posts the ruling in the issue: `accepted`, `rejected`,
   or `needs changes`, with the reasoning. Target: within 10 business days of entering
   `rfc:in-review`. If it needs more time, the facilitator posts why and sets a new date —
   the point is that it never just goes quiet.
5. **Execution** (accepted RFCs only):
   - Technical Owner is confirmed (initiator, or a TSC-assigned owner for
     TSC-originated initiatives).
   - TSC creates the Jira Epic and links it both ways: the Epic description links the
     GitHub Issue, and the Issue gets a comment with the Epic key.
   - The Epic assignee is set to the Technical Owner.
   - Issue is closed with a summary comment (decision + Epic link) and label
     `rfc:accepted`.

## Labels

`rfc:draft` → `rfc:in-review` → one of `rfc:accepted` / `rfc:rejected` /
`rfc:needs-changes`. Superseded RFCs get `rfc:superseded` with a link to the
replacement.

## Finding existing RFCs

Use GitHub's label search as the source of truth: `is:issue label:rfc` (add a status
label to narrow further). No separate index is maintained — a manually curated table
would just go stale.

## Relationship to ADRs

An RFC is the proposal-and-discussion phase. If the accepted RFC is an architecturally
significant, still-relevant-later decision, write it up as an ADR (see
[packages/e2e-tests/docs/decisions](../../packages/e2e-tests/docs/decisions) for the
convention this repo already uses) with a link back to the originating RFC issue. Not
every RFC needs one — only decisions worth explaining to someone reading the code in a
year.
