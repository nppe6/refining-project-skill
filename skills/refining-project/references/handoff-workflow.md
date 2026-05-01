# Persistent Handoff Workflow

Use this reference before creating or updating durable project review documents. The goal is to make a review resumable across interrupted sessions and new AI conversations without turning documentation into a giant archive.

## Core Rule

For any non-trivial project review, leave a target-project artifact behind unless the user explicitly asks for chat-only output.

The artifact should answer:

- What is this project?
- What was reviewed?
- What evidence supports the findings?
- What problems matter most?
- What should be fixed next?
- What has already been fixed or decided?
- What should a future AI agent avoid redoing?

## Where to Write

Prefer existing project conventions:

1. If the target project already has review, architecture, or planning docs, update the relevant existing document.
2. If it has `docs/`, use `docs/project-handoff.md` for the main handoff.
3. If the review is specifically about refactoring or optimization, use `docs/refining-project.md` or `docs/project-optimization.md` when a handoff doc does not exist.
4. If the target project has no docs directory and the user did not forbid new docs, create `docs/project-handoff.md`.
5. If writing docs is not appropriate, explain why and include a compact "handoff block" in the chat response that can be copied into the project later.

Use repo-relative links and paths inside generated documents.

## Recommended Document Split

Keep the documentation small and durable:

- `docs/project-handoff.md`: stable project overview, architecture, modules, reusable assets, risks, and next actions.
- `docs/project-optimization.md`: optional, when there is a substantial refactor or optimization plan.
- `docs/review-notes/<topic>.md`: optional, for deep evidence on one large topic such as auth, RBAC, database, or deployment.

Do not split documents just to look organized. Split only when the main handoff would become too long or when a topic will be worked independently.

## Main Handoff Size Discipline

Aim for a concise living document:

- Prefer tables for issues and next actions.
- Keep detailed code excerpts out unless they are essential.
- Link to files instead of copying large code blocks.
- Move long investigation notes into a separate topic file.
- Keep completed work summarized, not expanded forever.

## First Review Workflow

1. Search for existing handoff/review/optimization docs.
2. Build the project evidence map.
3. Produce the chat summary for the user.
4. Create or update the durable handoff document.
5. End the response by naming the document path and the highest-priority next actions.

## Follow-Up Optimization Workflow

When the user asks AI to implement fixes after a review:

1. Read the handoff/optimization document first.
2. Use its issue IDs or action IDs as the source of truth.
3. Update status as work progresses:
   - `Open`
   - `In Progress`
   - `Done`
   - `Deferred`
   - `Rejected`
4. Add new evidence when implementation reveals new facts.
5. Record decisions that change direction.
6. Keep next actions current.

Do not rewrite the whole document after every small edit. Update only the relevant sections.

## Suggested IDs

Use stable IDs so future sessions can refer to work precisely:

- `F-001`, `F-002`: findings or bugs.
- `A-001`, `A-002`: action items.
- `D-001`, `D-002`: decisions.
- `R-001`, `R-002`: risks.

Do not renumber existing IDs when adding new items.

## Minimal Action Queue

Every durable handoff should include a short action queue:

| ID | Priority | Status | Action | Evidence | Validation |
| --- | --- | --- | --- | --- | --- |

Priority can be `P0`, `P1`, `P2`, or `P3`.

## Decision Log

Record decisions when they affect future work:

| ID | Decision | Rationale | Date |
| --- | --- | --- | --- |

Examples:

- Keep Drizzle queries in services for now; do not add a global repository layer.
- Split session/RBAC logic before adding new business modules.
- Treat Redis/email/IP lookup as optional starter features.

## Example: Nest Starter Review Lessons

A real review of a Nest admin starter surfaced this pattern:

- The project was not over-layered; it was a runnable admin API template with a heavy feature set.
- Complexity came from fat services and mixed responsibilities, not from too many architectural layers.
- The most valuable output was an action queue:
  - Fix refresh-token SSO storage.
  - Fix permission creation undefined access.
  - Align role deletion permission codes.
  - Convert configuration values explicitly.
  - Make user list count use the same filter.
  - Avoid logging token-bearing responses.
- The missing piece was durable documentation. Without a handoff document, a later AI session would lose the evidence, priorities, and refactor direction.

Use this pattern when reviewing starter templates: separate "feature scope is heavy" from "architecture is over-abstracted", and preserve findings in a document before starting implementation.

## When Chat-Only Is Acceptable

Chat-only output is acceptable when:

- The user explicitly asks not to write files.
- The project is read-only or outside writable scope.
- The review is tiny and has no follow-up actions.
- The user only asks a quick question, not a handoff or optimization plan.

If chat-only is used, say so explicitly and include the reason.
