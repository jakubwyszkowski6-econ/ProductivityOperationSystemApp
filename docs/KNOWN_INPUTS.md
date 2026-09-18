# Known Inputs and Seed Context

This file records confirmed starting context. It is not a permanent source of truth for future SGH dates. Time-sensitive facts must be refreshed and carry provenance.

## 1. Owner and configuration

- User: Jakub “Kuba” Wyszkowski.
- Product name: SGH Productivity Center.
- Timezone: `Europe/Warsaw`.
- Locale/UI: Polish (`pl-PL`).
- Primary Google account and calendar: `jakub.wyszkowski6@gmail.com`.
- SGH email: `jw155473@student.sgh.waw.pl` — no direct integration available.
- App scope: private MVP for Kuba only.
- LaureatEDU: excluded from current scope.
- Notion: excluded from current scope.

## 2. SGH sources and quick links

- USOS: `https://usosweb.sgh.waw.pl/kontroler.php?_action=katalog2/index`
- Wirtualny Dziekanat: `https://dziekanat.sgh.waw.pl/?mtm_campaign=menu&mtm_kwd=Wirtualny-dziekanat`
- e-SGH: `https://e-sgh.pl/lms/drzewo_kursow.php`
- OneDrive SGH: `https://sghedu-my.sharepoint.com/?source=waffle`
- SGH address book: `https://ksiazka.sgh.waw.pl/?mtm_campaign=menu&mtm_kwd=Ksiazka-adresowa&lang=pl`
- SGH Library: `https://www.sgh.waw.pl/uczelnia/biblioteka`
- Niezbędnik: `https://n.e-sgh.pl/?mtm_campaign=menu&mtm_kwd=niezbednik`

Outlook SGH, university calendar, USOS, and e-SGH are manual-check sources. The app must not pretend to monitor them automatically.

## 3. Confirmed first-semester course context

The imported schedule snapshot contains these patterns; rooms are not confirmed and should remain unknown until updated:

| Course | Current known pattern |
|---|---|
| Language block, group 1 | Tuesday and Friday, 08:00–11:30 |
| Mikroökonomie I (FORUM) | Wednesday, 09:50–11:30 and 11:40–13:20 |
| Podstawy prawa | Thursday, 09:50–11:30 |
| Matematyka | Thursday, 11:40–13:20; Friday, 11:40–14:15 |
| Geografia ekonomiczna | Thursday, 13:30–15:10 |
| Wstęp do informatyki gospodarczej | Thursday, 15:20–17:00 |
| Proseminarium | Monday, 15:20–17:00; five dates beginning in November |
| Społeczna odpowiedzialność organizacji | e-learning; no fixed meeting time |

Known lecturer/rating snapshot:

- Paweł Węgrzyn — Geografia ekonomiczna — 4.5.
- Andrzej Stryjek — Matematyka — 4.1.
- Jürgen Wandel — Mikroökonomie I — 4.0.
- Łukasz Dąbrowski — Podstawy prawa — 4.4.
- Jan Misiuna — Proseminarium — rating unknown.
- Krystyna Polańska — Informatyka gospodarcza — 4.4.
- Language and e-learning lecturers — unknown.

Treat ratings as user-provided context, not an official SGH fact.

## 4. Formalities

The app should track but must not invent deadlines for:

- BHP training;
- library training;
- intellectual-property training;
- CNJO matters;
- CWFIS/WF registration;
- dean's-office matters;
- other e-SGH/Niezbędnik requirements.

## 5. SKN and activity priorities

Monitor broad SGH student-club opportunities with priority order:

1. SKN Biznesu;
2. Klub Inwestora;
3. SKN Consultingu.

Do not hide other SKN opportunities; priority affects ordering, not eligibility decisions.

## 6. Training template

- Tuesday 05:30–07:00.
- Thursday 05:30–07:00.
- Saturday 05:30–07:00.

This is flexible. The app may propose changes after a conflict but must not silently move training.

## 7. Opportunity monitoring specification

Source document: `handoff_monitoring_eventow_i_konkursow.pdf`, snapshot dated 17 September 2026.

The monitoring output is one Polish briefing at 19:00 Europe/Warsaw with up to three strong items per section and no weak filler:

### A — Startupy, hackathony i networking

Startup events, hackathons, demo days, pitch competitions, incubators, accelerators, and networking. Priority: SGH/Warsaw, Poland, online, then exceptional international opportunities accessible from Poland.

### B — Edukacja inwestycyjna i rynek kapitałowy

Events, webinars, training, conferences, study visits, and educational programs related to investing, markets, finance, development banking, and regulation.

### C — Konkursy ekonomiczne, inwestycyjne i finansowe

Only competitions with confirmed cash/non-cash prizes, internships, or meaningful professional benefits. Exclude high-school-only offers when Kuba is not eligible.

Required fields where published:

- name;
- exact date/time;
- location or format;
- application deadline;
- cost;
- eligibility;
- prizes for competitions;
- direct official URL;
- one sentence explaining relevance;
- labels such as PILNE, BEZPŁATNE, NOWOŚĆ, PRZYPOMNIENIE;
- star for the strongest item in a section.

Do not guess missing values. Confirm key facts at official sources. Do not repeat known items unless status changed or a deadline reminder is warranted.

Standing source groups:

- SGH calendar, CIVICA, CEMS, SGH news;
- Luma, Devpost, Eventbrite, Meetup, LinkedIn Events, Venture Café, CIC, 42 Warsaw, universities, incubators, and VC ecosystems;
- GPW, Fundacja GPW, KNF/CEDUR, BGK, NBP, PFR, PARP, KDPW, Ministry of Finance, Financial Ombudsman, BFG, CFA Society Poland;
- official competition pages and regulations.

Standing competition watchlist:

- Mistrz Wiedzy Ekonomicznej — SGH × Fundacja ERSTE;
- EY Financial Challenger;
- INDEX Investment Challenge — Fundacja GPW;
- CFA Institute Research Challenge Poland;
- ESGthon for Impact;
- additional eligible student competitions with meaningful prizes or CV value.

The app should import structured monitoring output and manage the pipeline. Direct autonomous browsing can remain external during MVP.

## 8. Known time-sensitive snapshot items

These items were previously reported and must not be reintroduced as new without fresh verification:

- Mistrz Wiedzy Ekonomicznej: online test 21–28 September 2026; final 23 October 2026.
- GPW Innovation Day: Future Makers: 22 September 2026.
- Warsaw Open Data Hackathon: 17–18 October 2026; previously reported deadline 1 October 23:59 or capacity limit.
- Dzień Edukacji Finansowej: 27 October 2026; program/registration required fresh verification.
- Philippe Aghion lecture at SGH: 29 October 2026, 11:30–13:30; previously reported Aula VII, building G.

This is snapshot data, not current truth. The app must show last verification time.

## 9. Supported input examples

Seed the prototype with examples such as:

- a confirmed room change;
- a cancelled class;
- an assessment announcement missing a date;
- a missed mathematics study block;
- an event-study conflict;
- a PDF attached to a study session;
- an urgent formality with unknown deadline;
- a new opportunity awaiting review;
- a draft calendar write awaiting confirmation.

## 10. File sources

Expected material types:

- PDF notes and instructions;
- PowerPoint or Canva-exported presentations;
- screenshots/images;
- pasted text and emails;
- tasks spoken to ChatGPT and then supplied to the app as text or PDF;
- links to OneDrive SGH or Google Drive files.

## 11. Input authority order

1. newest user-confirmed change;
2. newest screenshot/email/text supplied from SGH;
3. imported `.ics`;
4. original schedule screenshot;
5. general program information.

When equal-authority sources conflict, create a clarification item.

