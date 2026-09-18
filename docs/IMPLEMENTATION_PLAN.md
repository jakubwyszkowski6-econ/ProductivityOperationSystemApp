# Implementation Plan

Build in reviewable phases. Do not advance through a gate merely because later work is technically possible.

## Phase 0 — Repository and decisions

### Deliverables

- private Git repository;
- Next.js App Router + TypeScript scaffold;
- selected package manager and committed lockfile;
- formatting, linting, typecheck, unit-test, and browser-test commands;
- `.env.example` with names only;
- documented route map and component boundaries;
- ADRs for framework, Supabase boundary, and integration adapters;
- fixture strategy;
- CI workflow for lint, typecheck, tests, and build.

### Rules

- Verify current stable library versions through Context7/current official docs.
- Do not create paid resources.
- Do not create live OAuth clients or a production database.
- Keep dependencies minimal.

### Gate

Codex reports the final structure and all validation commands. No feature work continues if the base build is broken.

## Phase 1 — Fixture-backed UX prototype

### Deliverables

- fixed top bar and collapsible sidebar;
- responsive dark design tokens;
- `/today` with representative Kuba fixtures;
- `/updates` with accepted, ambiguous, and urgent examples;
- `/courses/[id]` for one representative course;
- command/quick-add entry shell;
- source-check banner;
- unread notification marker;
- desktop and mobile browser verification;
- optional Figma capture/prototype for review.

### Out of scope

- Supabase project;
- live authentication;
- live AI parsing;
- Gmail/Calendar OAuth;
- production deployment.

### Gate: visual approval

Kuba approves navigation, information density, dashboard hierarchy, colors, and mobile behavior. Record requested changes before continuing.

## Phase 2 — Supabase foundation

### Preflight

1. Confirm Vercel CLI authentication and intended team/project.
2. Link the repo before running database or development scripts that depend on environment variables.
3. Verify required environment-key names without printing values.
4. Create a development Supabase project only after explicit confirmation.

### Deliverables

- Supabase Auth restricted to Kuba's account;
- schema and migrations for core entities;
- RLS and policy tests;
- private Storage bucket and policies;
- generated TypeScript database types;
- seed importer for known course/schedule fixtures;
- repository adapters replacing fixtures incrementally;
- audit logging.

### Gate: security review

- test anonymous denial and cross-user isolation;
- run Supabase advisors;
- confirm no service-role/secret key appears client-side;
- production build passes.

## Phase 3 — Core planning and manual SGH Sync

### Deliverables

- tasks, assessments, study sessions, materials, formalities;
- source freshness page;
- upload/paste ingestion UI;
- deterministic extraction contract and proposal model;
- clarification questions for missing dates/course matches;
- accept/edit/reject workflow;
- missed-session rescheduling proposals;
- grade calculations with incomplete-state handling;
- Daily Brief and Evening Brief;
- day rating.

Start with rule-based fixtures and mocked extraction responses. Add live model calls only after proposal and confirmation behavior is tested.

### Gate

Manual updates cannot mutate confirmed data without a visible proposal, and every accepted mutation has provenance.

## Phase 4 — AI interpretation

### Deliverables

- server-side AI adapter for text and supported files/images;
- schema-constrained extraction;
- confidence and missing-field outputs;
- prompt-injection resistant treatment of uploaded content as data;
- size/type limits and failure states;
- evaluation set derived from the example commands and ambiguous cases in the specs.

### Rules

- API keys server-side only.
- Uploaded content cannot override system/product policy.
- Model output is untrusted until schema validation and, where needed, user confirmation.
- No voice feature.

### Gate

The evaluation set passes agreed thresholds, and all ambiguous examples request clarification.

## Phase 5 — Google Calendar

### Deliverables

- separate Google OAuth owned by the app;
- read availability/current events;
- target existing primary calendar;
- preview/confirm create, update, and delete;
- duplicate detection;
- conflict display;
- idempotency and retry-safe external-action records.

### Gate

No external mutation occurs from an unconfirmed proposal. Provider failures are shown accurately and do not create silent duplicates.

## Phase 6 — Gmail and Drive

### Gmail

- read/classify relevant personal messages;
- create internal proposals;
- create drafts when requested;
- never send without separate confirmation.

### Google Drive

- optional material picker/linking or export destination;
- app remains functional without Drive;
- no dependency on OneDrive SGH API.

### Gate

Least-privilege scopes are documented and verified. Business/LaureatEDU mail remains excluded from MVP.

## Phase 7 — Opportunities and monitoring pipeline

### Deliverables

- full opportunity pipeline;
- import format for existing daily monitoring output;
- deduplication and status-change logic;
- three briefing categories;
- official-source and last-verified fields;
- daily/urgent presentation inside the app.

Direct autonomous web monitoring may remain external during MVP. The application must support importing or receiving its structured output.

### Gate

Previously reported items are not reintroduced as new without a material change or deadline reminder.

## Phase 8 — PWA, notifications, and deployment

### Deliverables

- installable PWA manifest and icons;
- safe service-worker/offline behavior for the shell;
- in-app notifications;
- optional push notifications;
- Vercel preview deployment;
- production environment variables;
- error boundaries and observability;
- backup/export path for core data.

### Gate

- end-to-end critical flows pass on desktop and Oppo/Android-sized mobile viewport;
- production build and preview are healthy;
- secrets and OAuth redirect URLs are audited;
- only then perform production deployment with explicit confirmation.

## Phase 9 — Post-MVP hardening

- accessibility audit;
- performance and bundle review;
- security review of auth, RLS, storage, file parsing, AI ingestion, and OAuth;
- data export/restore exercise;
- retrospective and `AGENTS.md` updates based on repeated failures;
- optional Figma design-system cleanup and Code Connect.

## Recommended initial dependency shape

Confirm current versions before installing:

- Next.js + React + TypeScript;
- Tailwind CSS;
- accessible component primitives/shadcn-style components;
- Supabase JS/SSR libraries when Phase 2 begins;
- schema validation (for example Zod);
- unit test runner;
- Playwright for browser tests;
- date/time library only if native/Temporal support is insufficient;
- icon library;
- no global state library until local/server state proves inadequate.

## Delivery rhythm

At the end of each phase, Codex must report:

1. outcome;
2. changed files;
3. checks run and results;
4. screenshots/preview route when relevant;
5. known limitations;
6. decisions required from Kuba;
7. explicit next phase — without starting it automatically when a review gate applies.

