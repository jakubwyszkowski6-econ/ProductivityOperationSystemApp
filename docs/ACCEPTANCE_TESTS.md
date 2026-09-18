# Acceptance Tests

These scenarios define observable product behavior. Automate the stable paths with unit/integration tests and browser tests. Use deterministic fixtures before live integrations.

## A. App shell and dashboard

### A1 — First useful action

Given at least one scheduled class, task, or study block exists today, when the user opens `/today`, then one dominant next action appears above secondary modules and explains why it is recommended.

### A2 — Fixed navigation

When the user scrolls a long page, then the top bar remains visible. The left sidebar can collapse and its state persists.

### A3 — Mobile priority

At a common phone viewport, `/today` has no horizontal scrolling and shows next action, next class/deadline, three priorities, and unread updates before lower-priority content.

### A4 — Daily source check

Given SGH sources have not been confirmed today, the first app opening shows a prominent USOS/e-SGH/Outlook check prompt. After confirmation, normal navigation on the same day does not repeatedly show it.

## B. Manual SGH Sync

### B1 — Clear class-room change

Given a pasted message says that Friday mathematics moved to room 152 in building G, when it is parsed, then the app creates an update proposal showing old and new room, source, and affected occurrence. No mutation occurs before acceptance.

### B2 — Cancelled class

Given a screenshot clearly cancels tomorrow's geography, when accepted, then the occurrence becomes cancelled, a high-priority update is recorded, and any calendar change remains a separate confirmation step.

### B3 — Missing date

Given an email says “the colloquium has been moved” without a new date, then the ingestion item becomes `needs_clarification` and asks for the date. The app must not create a guessed assessment date.

### B4 — Ambiguous course

Given uploaded notes could match two courses, then the app asks which course to use before linking the material.

### B5 — Provenance

After an accepted change, the affected entity shows the source and confirmation time, and the audit log preserves the previous value.

## C. Tasks and study planning

### C1 — Missed study block

Given a planned mathematics block is marked missed, then the app shows available alternative slots before the related deadline. It does not automatically move the block.

### C2 — User-selected reschedule

When the user selects one proposed slot, then a new/updated study session is created and linked to the original missed session.

### C3 — Multiple deadlines

Given multiple important deadlines compete for insufficient time, then all deadlines and consequences remain visible and the app asks the user to select priorities. It does not silently hide or discard one.

### C4 — Event conflicts with study

Given a relevant startup event overlaps a study session, then the app presents keep study, attend and reschedule, or dismiss event. No choice is applied automatically.

### C5 — Study materials

Given a PDF is attached to a named study session, then it appears in both the session and its related course without duplication.

### C6 — Focus mode

When focus mode starts, unrelated feeds and notification counts are hidden, while the timer, current task, and one short focus instruction remain visible.

## D. Courses and grades

### D1 — Course workspace

Each course page can show schedule, lecturer, tasks, assessments, materials, sessions, total time, and known assessment rules.

### D2 — Incomplete weighting

Given assessment weights are unknown or incomplete, then the app labels the forecast incomplete and lists missing inputs instead of fabricating a final grade.

### D3 — Required exam score

Given valid current results, weights, and a target final grade, then the required remaining result is calculated with visible inputs and handles impossible targets explicitly.

### D4 — Measurement modes

Mathematics supports a configurable skill level, languages support CEFR such as B1, and ordinary courses do not show a mastery score by default.

## E. Opportunities

### E1 — Pipeline movement

An opportunity can move through detected, review, watching, applying/registered, completed, and rejected. Every move is reversible or auditable.

### E2 — Required competition fields

A competition is not presented as verified unless an official source confirms meaningful prizes or professional benefits.

### E3 — No duplicate briefing item

An already reported opportunity is not surfaced as new unless status, date, program, cost, availability, prize, or urgency changed.

### E4 — Event-study choice

Adding an event that conflicts with study creates a decision, not an automatic overwrite.

## F. Briefs and reviews

### F1 — Daily brief

The dated Daily Brief contains next class/room, nearest deadline, three priorities, overdue count, key opportunity/formality, source freshness, and first action based on stored data.

### F2 — Evening brief

The Evening Brief contains completed/missed items, time spent, unresolved updates, tomorrow's first commitment, proposed recovery actions, and a 1–10 rating control.

### F3 — Rating validation

Values outside 1–10 cannot be saved.

## G. Google integrations

### G1 — Calendar preview

Given a proposed event, before any provider call the user sees title, date/time, target calendar, reminders, and conflicts. Only explicit confirmation executes the write.

### G2 — Primary calendar

The default target is the existing primary calendar belonging to `jakub.wyszkowski6@gmail.com`. No new SGH calendar is created.

### G3 — Duplicate protection

When a materially similar calendar event already exists, creation is blocked or requires explicit duplicate confirmation.

### G4 — Draft but do not send

When the user requests an email response, the app may prepare a draft. It must never send without a distinct confirmation action.

### G5 — Integration failure

If an external write fails, the app shows failure, retains the internal proposal, and does not claim success or create a duplicate retry silently.

## H. Notifications and freshness

### H1 — Unread marker

A new room change, cancellation, assessment date, or urgent formality creates an unread red dot/count. Opening the list alone does not resolve the underlying action.

### H2 — Source states

Source status supports current, check recommended, and stale. The timestamp is visible.

### H3 — Unknown deadline

An urgent formality with unknown deadline stays visible and prompts verification without inventing a date.

## I. Security and privacy

### I1 — Anonymous access

Anonymous clients cannot read or mutate user data or private materials.

### I2 — Cross-user isolation

A second test user cannot read, update, or delete the first user's rows or storage objects.

### I3 — No client secrets

Production build output and browser network/config inspection contain no service-role key, Google client secret, OpenAI secret, or private token.

### I4 — RLS updates

Update policies enforce both ownership of the existing row and ownership of the updated row.

### I5 — Audit trail

Accepted agent proposals, calendar writes, cancellations, and destructive file actions have durable audit records.

## J. Quality gates

Before a phase is accepted:

- lint passes;
- TypeScript check passes;
- relevant unit/integration tests pass;
- production build passes;
- browser tests pass for affected paths;
- desktop and mobile layouts are reviewed;
- no secret is committed;
- known skipped checks are reported explicitly.

