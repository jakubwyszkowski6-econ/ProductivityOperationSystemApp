# AGENTS.md — SGH Productivity Center

## Mission

Build a reliable private productivity PWA for Kuba. The product should tell him what matters now, keep SGH data organized, and surface choices without taking consequential decisions for him.

## Authoritative documents

Read before substantial work:

- `docs/PRODUCT_SPEC.md`
- `docs/DESIGN_SYSTEM.md`
- `docs/DATA_MODEL.md`
- `docs/ACCEPTANCE_TESTS.md`
- `docs/IMPLEMENTATION_PLAN.md`
- `docs/KNOWN_INPUTS.md`

Do not silently reinterpret confirmed product decisions. Record proposed changes in the final summary and ask before changing scope.

## Product boundaries

- One private user only. No teams, organizations, invitations, billing, public sign-up, or generalized SaaS architecture.
- Polish UI and user-facing copy. English is acceptable in code, schema, tests, and developer documentation.
- Europe/Warsaw is the canonical timezone.
- LaureatEDU, Notion, direct Outlook SGH integration, direct USOS scraping, and direct OneDrive SGH API access are out of the MVP.
- No in-app voice recognition in the MVP.
- Never guess dates, rooms, assessment rules, or deadlines. Preserve `unknown` and request clarification.
- The user makes priority tradeoffs. The app explains conflicts and proposes options; it does not silently choose what the user should abandon.

## Required behavior

- External writes require preview and explicit confirmation: Google Calendar changes, email sends, and destructive file operations.
- Email automation may classify and draft, but never send automatically.
- Calendar integration targets the primary calendar of `jakub.wyszkowski6@gmail.com`; do not create a separate SGH calendar unless the user later changes this decision.
- Manual SGH Sync accepts text, screenshots, images, PDFs, presentations, and pasted email content.
- Ambiguous inputs must create a clarification request, not a confident mutation.
- All accepted changes receive provenance and an audit-log entry.

## Engineering defaults

- Use a current stable Next.js App Router release with TypeScript. Verify versions and APIs through current documentation or Context7 before implementation.
- Prefer Server Components by default; use Client Components only for interactive boundaries.
- Default to the Node.js runtime unless a feature clearly needs Edge.
- Use Tailwind CSS and accessible primitives such as shadcn/ui, with Lucide-style icons or another consistent open icon set.
- Use Supabase for Postgres, Auth, and Storage after the visual prototype is accepted.
- Use Vercel for preview and production deployment after local verification.
- Keep integrations behind typed adapters so fixture mode, test mode, and live mode share the same domain interfaces.
- Pin dependencies, commit the lockfile, and avoid adding packages that duplicate platform capabilities.

## Supabase security

- Enable RLS on every table exposed through the Data API.
- Authorize rows with ownership predicates such as `auth.uid() = user_id`; `TO authenticated` alone is insufficient.
- UPDATE policies require both `USING` and `WITH CHECK`.
- Never use user-editable metadata for authorization.
- Never expose service-role or secret keys to the client.
- Prefer security-invoker views. Do not add `SECURITY DEFINER` merely to bypass permission errors.
- Storage policies must cover the intended operations; replacement/upsert requires INSERT, SELECT, and UPDATE.
- Run Supabase advisors before accepting schema work.

## UX rules

- Fixed top navigation; collapsible left sidebar; no permanently open third rail.
- Default dark neutral theme. Bright yellow/orange/red only for semantic status or small icons.
- Avoid visual clutter, excessive cards, gradients, decorative charts, and large empty marketing layouts.
- One dominant next-action area on Today. Secondary information should be grouped and progressively disclosed.
- New or changed information uses a red dot/count and a clear Updates destination.
- Keyboard navigation, visible focus states, reduced-motion support, and WCAG AA contrast are required.
- Mobile views must preserve priority and action clarity rather than merely stacking desktop cards.

## Work sequencing

- Follow `docs/IMPLEMENTATION_PLAN.md` and its approval gates.
- Do not create live databases, OAuth clients, or deployments during the fixture-backed UI phase.
- Do not run database migrations or the development server until project linkage and required environment-key names are verified.
- Use Figma as an optional review surface, not a blocker. The coded prototype remains authoritative unless the user explicitly approves a Figma revision.

## Verification

For every meaningful implementation change:

1. Run formatter/lint.
2. Run TypeScript checks.
3. Run the smallest relevant unit or integration tests.
4. Run a production build.
5. For UI changes, verify desktop and mobile with browser automation and capture evidence.
6. Check the relevant scenarios in `docs/ACCEPTANCE_TESTS.md`.
7. Review the diff for secrets, scope creep, destructive operations, and regressions.

Do not claim completion if a required check was skipped. Report the skipped check and reason.

## Change discipline

- Preserve existing user changes and unrelated files.
- Prefer small, reviewable increments.
- Keep fixtures deterministic.
- Add migrations through the approved Supabase workflow only after schema review.
- Keep `.env.local` and all credentials out of Git. Maintain `.env.example` with names only.
- Ask before adding a production dependency, creating a paid resource, changing an approved data model, or broadening the app beyond Kuba.

## Definition of done

A task is done only when the requested behavior exists, relevant tests pass, the build succeeds, the user-facing flow is verified, and limitations are explicitly reported.

