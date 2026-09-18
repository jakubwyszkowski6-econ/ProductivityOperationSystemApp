# Design System — Linear × ChatGPT, dark and focused

## 1. Design intent

Combine Linear's compact product navigation, hierarchy, and keyboard efficiency with ChatGPT's calm conversational clarity. The result should feel like a serious personal operating system, not a student portal and not a marketing site.

Do not copy logos, brand marks, text, or exact proprietary screens. Use the references for interaction density, proportions, and hierarchy only.

## 2. App shell

### Fixed top bar

- Permanently visible; cannot be hidden.
- Height target: 48–56 px on desktop.
- Contains current section, command/search trigger, quick add, updates, source freshness, and user menu.
- Menus open into compact, grouped panels similar in density to Linear's expanded navigation.
- Avoid a wide marketing-navigation treatment.

### Collapsible left sidebar

- Expanded desktop width target: 232–264 px.
- Collapsed rail target: 52–64 px.
- Remembers user preference.
- Clear grouping: Today, Plan, Learn, Opportunities, Briefs, Settings.
- Active destination uses a quiet filled surface, not a bright colored block.
- Unread status uses a small red dot/count.

### Main content

- Constrain reading width for briefs and forms.
- Allow wider density for calendar, tables, and planning boards.
- Use drawers or modals for contextual detail rather than permanent competing panels.

## 3. Color tokens

Exact values may be tuned after visual review, but keep the semantic roles:

| Token | Initial value | Purpose |
|---|---:|---|
| `--bg-canvas` | `#090A0C` | global canvas |
| `--bg-sidebar` | `#0D0F12` | navigation |
| `--bg-surface` | `#121419` | cards and panels |
| `--bg-elevated` | `#181B21` | menus and dialogs |
| `--border-subtle` | `#252932` | low-contrast separators |
| `--text-primary` | `#F3F4F6` | primary text |
| `--text-secondary` | `#A3A8B3` | metadata |
| `--text-muted` | `#707784` | disabled/supporting text |
| `--accent` | `#7C8CF8` | restrained primary action |
| `--info` | `#60A5FA` | information |
| `--success` | `#34D399` | completed/healthy |
| `--warning` | `#F59E0B` | only meaningful warning |
| `--danger` | `#EF4444` | urgent/error/unread marker |

Yellow and orange must never become large decorative backgrounds. Red should remain rare enough to preserve urgency.

## 4. Typography

- Use Geist or another neutral UI sans-serif with Polish characters.
- Base size: 14–15 px desktop, 15–16 px mobile.
- Compact line height for controls; comfortable line height for briefs.
- Use size, weight, and spacing before color to create hierarchy.
- Avoid oversized marketing headings inside the product.

## 5. Spacing and geometry

- Base spacing unit: 4 px.
- Common gaps: 8, 12, 16, 24, 32 px.
- Border radius: 6–10 px. Avoid excessive pill shapes.
- Use subtle 1 px borders and restrained shadows.
- Cards exist only when grouping improves comprehension; do not wrap every row in a card.

## 6. Dashboard hierarchy

Desktop order:

1. next action / current focus;
2. three priorities and next deadline;
3. next class and compact timeline;
4. updates requiring decisions;
5. overdue/formalities/opportunity summaries.

Mobile order:

1. next action;
2. next class/deadline;
3. three priorities;
4. unread updates;
5. compact remainder behind progressive disclosure.

Do not show every metric simultaneously. The dashboard is an action surface, not an analytics wall.

## 7. Component patterns

### Next Action

- One dominant card or panel.
- Strong verb-led title.
- Explain “why now” in one sentence.
- Primary action: start/open.
- Secondary actions: postpone, replace, details.

### Update row

- Unread dot/count.
- Source icon and timestamp.
- Short factual headline.
- Confidence/status chip.
- Proposed action with accept/edit/reject controls.

### Conflict panel

- Side-by-side facts, not a hidden automatic resolution.
- Show collision and consequences.
- Present 2–3 viable options.
- Require explicit selection.

### Empty state

- Explain the next useful action.
- Do not use decorative illustrations by default.

### Focus mode

- Minimal screen, timer, current task, one short instruction.
- No opportunities feed, email count, or unrelated navigation while active.

## 8. Interaction behavior

- Global command palette via keyboard shortcut.
- Escape closes overlays.
- Enter confirms only when the action is safe and reversible.
- External writes use a dedicated confirmation step.
- Optimistic UI only for reversible internal changes.
- Loading uses skeletons without layout shift.
- Motion duration generally 120–220 ms.
- Respect `prefers-reduced-motion`.

## 9. Accessibility

- WCAG AA contrast for text and interactive states.
- Visible keyboard focus ring.
- Icons accompanied by accessible labels.
- Color is never the only status signal.
- Dialog focus trapping and restoration are required.
- Touch targets at least 44×44 px on mobile.

## 10. Figma workflow

Figma is an optional review layer:

1. Establish tokens and the app shell.
2. Prototype Today, Updates, and Course detail.
3. Review desktop and mobile.
4. Implement or refine the coded version.

If Figma write access is limited, continue with the coded prototype. Do not block the project on design-tool permissions.

## 11. Visual rejection criteria

Reject a design iteration when it:

- resembles a bright marketing landing page;
- uses large yellow/orange areas;
- hides the top bar;
- shows more than one competing primary action;
- permanently displays too many panels;
- requires horizontal scrolling on mobile;
- uses charts where a short number or list is clearer;
- treats every item as an equally prominent card;
- copies Linear or ChatGPT branding rather than adapting patterns.

