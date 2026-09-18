# MASTER PROMPT

## PROMPT DO WKLEJENIA

You are starting the implementation of **SGH Productivity Center**, a private single-user productivity PWA for Kuba. The repository contains the authoritative project documents.

Read all of these files before proposing implementation work:

- `@AGENTS.md`
- `@docs/PRODUCT_SPEC.md`
- `@docs/DESIGN_SYSTEM.md`
- `@docs/DATA_MODEL.md`
- `@docs/ACCEPTANCE_TESTS.md`
- `@docs/IMPLEMENTATION_PLAN.md`
- `@docs/KNOWN_INPUTS.md`

Treat those files as the source of truth. If they appear to conflict, apply this precedence:

1. `AGENTS.md` for safety, scope, and engineering workflow.
2. `PRODUCT_SPEC.md` for product behavior.
3. `DESIGN_SYSTEM.md` for UX and visual decisions.
4. `DATA_MODEL.md` for persistence and security.
5. `ACCEPTANCE_TESTS.md` for observable completion criteria.
6. `IMPLEMENTATION_PLAN.md` for sequencing.
7. `KNOWN_INPUTS.md` for seed data and contextual facts.

Work in Plan mode first. Do not implement the entire product in one pass.

Your first assignment is limited to **Phase 0 and Phase 1** from `IMPLEMENTATION_PLAN.md`:

1. Inspect the workspace and confirm the instruction files loaded.
2. Identify any true blocker. Do not ask about details already decided in the documents.
3. Verify current stable framework and library guidance through Context7 before choosing versions.
4. Propose the repository structure and the smallest reasonable dependency set.
5. Scaffold the application.
6. Build a responsive, fixture-backed UI shell covering the core navigation and the Today dashboard.
7. Implement the first visual versions of Today, Updates/Inbox, and one Course detail view.
8. Add representative seed fixtures for Kuba's current SGH context.
9. Add the smallest relevant automated tests and run lint, typecheck, tests, and production build.
10. Start a local preview when possible and verify desktop and mobile layouts with browser automation.
11. Stop at the visual approval checkpoint. Do not create a Supabase project, production database, Google OAuth credentials, Gmail integration, calendar writes, or a production deployment yet.

Hard constraints:

- This is a private product for one user. Do not build organizations, teams, roles, invitations, billing, or public registration.
- The UI language is Polish. Code, schema, and engineering documentation may be English.
- The visual style combines Linear's information density and navigation with ChatGPT's calm, understandable interaction model. Do not copy trademarks, logos, or proprietary content.
- Keep the permanent top bar visible. The left navigation may collapse. Use dark neutral colors; yellow, orange, and red are semantic accents only.
- The screen must make the next action obvious and avoid presenting every module at once.
- Do not add voice recognition to the app.
- Do not guess missing SGH data. Mark it unknown and provide a manual update path.
- External actions such as calendar writes and sending email always require a preview and explicit user confirmation.
- Use adapters and mock data for integrations until their implementation phase.
- Never expose Supabase service-role keys, Google client secrets, OpenAI keys, or other secrets to the browser.
- Do not deploy or create paid resources without explicit confirmation.

Before editing files, return a concise execution plan containing:

- chosen architecture and why;
- proposed routes and component boundaries;
- dependency list;
- fixture strategy;
- verification commands;
- the exact screens delivered at the Phase 1 checkpoint.

After presenting the plan, proceed unless a genuine blocker requires user input. At completion, report:

- files changed;
- routes implemented;
- tests and commands run with results;
- known limitations;
- the local preview URL or exact run command;
- the specific visual decisions that need Kuba's approval before Phase 2.

