# Product Specification — SGH Productivity Center

## 1. Product statement

SGH Productivity Center is a private, single-user PWA for Kuba. It combines university planning, tasks, deadlines, learning sessions, grades, formalities, opportunities, and carefully controlled Google integrations in one calm operating system.

The product promise is simple:

> When Kuba opens the app, he immediately knows what to do next, what changed, and which decisions require his attention.

## 2. Primary outcomes

1. Eliminate uncertainty about the next useful action.
2. Keep SGH class, assignment, assessment, and material context connected.
3. Surface conflicts and consequences without deciding priorities for the user.
4. Turn screenshots, pasted messages, and files into reviewed update proposals.
5. Maintain one visible opportunity pipeline for events, recruitment, competitions, and SKN activity.
6. Produce useful daily and evening briefings.
7. Preserve trust through confirmation, provenance, and an audit history.

## 3. Non-goals for MVP

- Multi-user SaaS, teams, organizations, invitations, shared workspaces, or billing.
- LaureatEDU business management.
- Notion migration.
- Native Outlook SGH, university calendar, USOS, or OneDrive SGH API integration.
- Automated browser scraping of authenticated SGH portals.
- In-app speech recognition.
- Autonomous priority decisions that hide or discard important commitments.
- Automatic email sending or silent Google Calendar writes.
- Measuring detailed topic mastery for every subject.

## 4. User and operating context

- User: Kuba, first-year SGH student in Warsaw.
- Canonical timezone: `Europe/Warsaw`.
- UI language: Polish.
- Primary Google account: `jakub.wyszkowski6@gmail.com`.
- Academic source limitations: Outlook SGH, USOS, e-SGH, and the university calendar must be updated manually through user-provided content.
- SKN coverage: monitor all relevant clubs; prioritize SKN Biznesu, Klub Inwestora, and SKN Consultingu.
- Training template: Tuesday, Thursday, and Saturday, 05:30–07:00; flexible and user-editable.

## 5. Decision principles

### 5.1 User control

The system may recommend, compare, and propose. Kuba decides which deadline, study block, or event receives priority.

### 5.2 Confidence-aware automation

- High-confidence internal classification may happen automatically.
- Ambiguous interpretation creates a clarification item.
- External writes always require preview and confirmation.
- Destructive operations require explicit confirmation.

### 5.3 No invented facts

Unknown room, date, grade weight, deadline, or eligibility remains unknown. The UI must distinguish confirmed, inferred, and missing data.

### 5.4 One source of operational truth

The application database holds the normalized schedule, tasks, assessments, materials, and decisions. External systems remain source inputs or destinations, with provenance retained.

## 6. Information architecture

The fixed top bar contains:

- current context/title;
- global command/search entry;
- quick-add action;
- notifications/updates button with unread count;
- source-freshness status;
- compact user/settings menu.

The collapsible left navigation contains:

1. Dzisiaj
2. Inbox / Aktualizacje
3. Kalendarz
4. Nauka
5. Przedmioty
6. Oceny
7. Okazje
8. Pilne formalności
9. Codzienny Brief
10. Wieczorny Brief
11. Ustawienia i źródła

The app may expose a contextual assistant drawer from any route, but it must not permanently consume screen space.

## 7. Core screens

### 7.1 Dzisiaj (`/today`)

The initial route. It must answer, in order:

1. Co robię teraz?
2. Jakie są trzy priorytety?
3. Jakie są najbliższe zajęcia i sala?
4. Jaki jest najbliższy deadline?
5. Co się zmieniło lub wymaga decyzji?

Required modules:

- dominant Next Action card with start, snooze, replace, and explain actions;
- next class with time, course, building, room, and confidence/source;
- three user-approved or user-selectable priorities;
- nearest deadline;
- compact schedule strip;
- overdue summary linking to a separate overdue view/card;
- new updates indicator;
- important event/recruitment summary;
- source-check banner when SGH sources have not been confirmed today.

### 7.2 Inbox / Aktualizacje (`/updates`)

Unified queue for:

- imported screenshots, files, pasted messages, and emails;
- detected schedule changes;
- missing-date questions;
- calendar proposals;
- new opportunity items;
- room changes and cancellations;
- system warnings.

Each item displays source, received time, confidence, extracted facts, proposed destination, and actions: accept, edit, reject, ask later.

Unread items produce a red dot or count in navigation. Reading is not equivalent to accepting.

### 7.3 Calendar (`/calendar`)

Three synchronized views:

- day;
- week;
- agenda/list.

Shows classes, assessments, study sessions, events, training, and formalities. Conflicts are visible. Internal tentative items use a different visual state from confirmed Google Calendar events.

Google Calendar mutations require a diff-like preview: create/update/delete, title, date/time, target calendar, and collision warning. The default target is the primary calendar of `jakub.wyszkowski6@gmail.com`.

### 7.4 Study (`/study`)

Capabilities:

- list and calendar of planned sessions;
- Pomodoro/focus timer;
- total time by day, week, and course;
- attach materials and tasks to sessions;
- mark completed, partially completed, missed, or cancelled;
- proposal workflow for rescheduling missed work before its deadline;
- focus mode showing short messages such as „Schowaj telefon — teraz skupienie” or „Zamknij niepotrzebne karty”.

The app never silently moves a missed session. It proposes one or more viable slots and shows deadline impact.

### 7.5 Courses (`/courses`, `/courses/[id]`)

Course list and course workspace with:

- class pattern and occurrences;
- lecturer;
- tasks and deadlines;
- tests, projects, colloquia, and exams;
- materials;
- study sessions and accumulated time;
- notes about assessment rules;
- grade summary.

Progress measurement:

- mathematics may use a configurable skill/progress level;
- languages may show CEFR level such as B1;
- other courses do not require a mastery score in MVP.

### 7.6 Grades (`/grades`)

For each course show, where enough data exists:

- current weighted average;
- forecast final grade;
- result required on the remaining exam/assessment to achieve a selected target;
- missing weights or uncertain assumptions.

Calculations must expose their inputs. If weights do not sum to 100% or are unknown, forecast is marked incomplete rather than fabricated.

### 7.7 Opportunities (`/opportunities`)

One pipeline:

`wykryte → do przejrzenia → obserwowane → aplikuję/zapisany → zakończone → odrzucone`

Categories:

- startupy, hackathony i networking;
- edukacja inwestycyjna i rynek kapitałowy;
- konkursy ekonomiczne, inwestycyjne i finansowe;
- wydarzenia SGH and SKN activity;
- recruitment/program applications.

The system may explain fit and constraints but must not automatically decide whether an opportunity is “good.” Every item may include date, location/format, deadline, cost, eligibility, prizes, official URL, reason for relevance, tags, source, and last verification date.

Never duplicate an already reported item unless its status changed, a deadline is approaching, or the user explicitly requests a reminder.

### 7.8 Urgent formalities (`/formalities`)

Separate high-visibility list for administrative obligations such as BHP, library training, intellectual-property training, registrations, dean's-office matters, CNJO, and CWFIS.

Unknown deadlines remain visibly unknown and prompt source verification.

### 7.9 Daily Brief (`/brief/daily`)

Date-stamped page containing:

- next class and room;
- nearest deadline;
- three priorities;
- overdue count and link;
- important event/recruitment update;
- formalities requiring attention;
- source freshness;
- recommended first action.

It should be generated from current application data, not free-form guesswork.

### 7.10 Evening Brief (`/brief/evening`)

Contains:

- completed and missed work;
- time spent by category/course;
- unresolved updates;
- suggested rescheduling options;
- tomorrow's first commitments;
- a required 1–10 day rating with optional note.

### 7.11 Settings and Sources (`/settings/sources`)

Shows status and last confirmation for:

- USOS;
- e-SGH;
- Outlook SGH;
- Wirtualny Dziekanat;
- Google Calendar;
- Gmail;
- Google Drive;
- OneDrive SGH link.

The first app opening of each day displays a prominent source-check request until Kuba confirms the relevant SGH sources or explicitly postpones it. It should not reappear on every navigation action within the same day.

## 8. Global assistant and ingestion

The assistant accepts:

- natural-language text;
- pasted text/email;
- screenshot or image;
- PDF;
- PPTX;
- supported document attachments.

It does not accept voice directly in MVP. Kuba may dictate to ChatGPT externally, create text/PDF, and upload it.

The ingestion workflow is:

1. Receive source.
2. Extract candidate facts.
3. Match course/entity when possible.
4. Detect missing or contradictory data.
5. Create a human-readable proposal.
6. Ask for clarification if required.
7. Apply accepted internal changes.
8. Create separate external-write proposals if needed.
9. Store provenance and audit history.

Supported example commands:

- „W tym tygodniu zamień matematykę na podstawy prawa.”
- „Dołącz te notatki do środowej sesji mikroekonomii.”
- „Na tym zdjęciu jest nowy termin kolokwium.”
- „Odwołano jutrzejszą geografię.”
- „Nie zrobiłem matematyki, bo byłem zmęczony.”
- „Dodaj ten startupowy event o 18:00 do propozycji kalendarza.”
- „Dodaj to wydarzenie do obserwowanych.”
- „Jakie są trzy priorytety na teraz?”
- „Zaplanuj naukę do egzaminu od końcowego terminu.”
- „Stwórz plan przygotowań do tego kolokwium.”
- „Zaproponuj sesje, które pozwolą mi nadrobić ten materiał.”

## 9. Conflict behavior

### Multiple deadlines

Show all material deadlines, the available time, consequences, and viable plans. Ask Kuba to select the priority and what may be reduced or deferred.

### Missed study block

Show the missed block, remaining time before the deadline, and proposed alternative slots. Apply only after selection.

### Valuable event during study

Show the event and affected study session side by side. Offer keep study, attend event and reschedule, or dismiss event. The user chooses.

### Missing date

Ask a focused question. Do not create a fake or “best guess” date.

### Room change or cancellation

Create a high-priority update, unread indicator, and affected-calendar proposal. Preserve the old value in history.

## 10. Notifications

MVP channels:

- in-app notification center;
- PWA push when permission is granted;
- optional approved Google Calendar reminder.

Notification severities:

- info;
- action required;
- urgent;
- critical source staleness.

Use red only for urgent/action-required states, not for ordinary information.

## 11. Google integrations

### Gmail

- Analyze the connected personal account in a later integration phase.
- Classify high-confidence items and create internal proposals.
- Draft replies when requested.
- Never send automatically.
- LaureatEDU/business workflows remain outside MVP.

### Google Calendar

- Read availability and current commitments.
- Target the existing primary calendar; do not create a new calendar.
- Preview every write and require confirmation.
- Detect probable duplicates before creating events.

### Google Drive

- Optional destination or link source for materials.
- Do not make core app behavior depend on Drive availability.

## 12. File handling

- Store small app-managed files in Supabase Storage during MVP.
- Allow external URLs for OneDrive SGH or Google Drive.
- Accept PDFs and presentations as materials.
- Track filename, MIME type, size, course, related task/session, source, and upload time.
- Enforce configurable size limits and reject unsafe types.
- Do not duplicate a file when a link is sufficient.

## 13. Data freshness and provenance

Every externally derived fact may contain:

- source type;
- source reference;
- captured timestamp;
- user confirmation timestamp;
- confidence;
- superseded fact reference.

Priority when information conflicts:

1. latest user-confirmed update;
2. latest screenshot, email, or pasted SGH source;
3. imported `.ics`;
4. initial schedule screenshot;
5. general SGH program information.

## 14. Success metrics for personal use

- Kuba can identify the next action in under 10 seconds.
- No accepted calendar write occurs without confirmation.
- No ambiguous deadline is silently stored as confirmed.
- A missed study block can be rescheduled in three interactions or fewer.
- New critical SGH changes remain visibly unread until reviewed.
- Daily and evening brief pages are usable without opening other modules.

