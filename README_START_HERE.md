# SGH Productivity Center — instrukcja uruchomienia w Codex

Ten pakiet jest kompletną specyfikacją prywatnej aplikacji Kuby. Nie trzeba dopisywać kolejnego długiego opisu projektu. Brakujące bieżące dane SGH będą później dostarczane agentowi jako aktualizacje, a nie jako zmiana fundamentów produktu.

## Zawartość pakietu

- `AGENTS.md` — trwałe zasady pracy Codexa. Ten plik musi być w katalogu głównym repozytorium.
- `MASTER_PROMPT.md` — dokładna pierwsza wiadomość do wklejenia w nowym czacie Codexa.
- `docs/PRODUCT_SPEC.md` — funkcje, ekrany, reguły zachowania i zakres MVP.
- `docs/DESIGN_SYSTEM.md` — system wizualny inspirowany Linear i ChatGPT.
- `docs/DATA_MODEL.md` — model bazy Supabase, bezpieczeństwo i pliki.
- `docs/ACCEPTANCE_TESTS.md` — kryteria uznania funkcji za działające.
- `docs/IMPLEMENTATION_PLAN.md` — kolejność budowy i bramki jakości.
- `docs/KNOWN_INPUTS.md` — potwierdzone dane startowe, portale i ograniczenia integracji.

## Zalecany sposób użycia

1. Utwórz pusty folder lub prywatne repozytorium GitHub o nazwie `sgh-productivity-center`.
2. Skopiuj do niego zawartość tego pakietu, zachowując strukturę folderów.
3. Upewnij się, że `AGENTS.md` znajduje się dokładnie w katalogu głównym repozytorium.
4. Otwórz ten katalog w Codexie.
5. Rozpocznij **nowy czat/sesję**. Codex wczytuje `AGENTS.md` przy uruchomieniu sesji, dlatego nie używaj starego czatu rozpoczętego przed dodaniem pliku.
6. Włącz tryb Plan, jeśli jest dostępny (`/plan` lub odpowiedni przełącznik).
7. Otwórz `MASTER_PROMPT.md`, skopiuj całą sekcję „PROMPT DO WKLEJENIA” i wklej ją jako pierwszą wiadomość.
8. Nie wklejaj osobno całej treści pozostałych dokumentów. Prompt odwołuje się do nich przez `@docs/...`, więc Codex przeczyta je bez duplikowania kontekstu.
9. Do pierwszego zadania pozwól Codexowi wykonać wyłącznie Fazę 0 i Fazę 1 z planu. Najpierw zaakceptuj wygląd oraz nawigację, dopiero później bazę i integracje.

## Jeśli zaczynasz bez lokalnego repozytorium

Możesz załączyć ZIP do nowego czatu Codexa i napisać:

> Rozpakuj załączony pakiet do nowego katalogu `sgh-productivity-center`, zachowaj strukturę plików i zatrzymaj się. Nie implementuj aplikacji w tej sesji.

Następnie otwórz powstały katalog jako repozytorium i rozpocznij nową sesję. To konieczne, aby repozytoryjny `AGENTS.md` został automatycznie wczytany.

## Pliki wizualne

Sześć wcześniej przekazanych screenshotów Linear, ChatGPT i OneDrive nie jest wymaganych do startu — ich istotne cechy zapisano w `DESIGN_SYSTEM.md`. Przy pierwszej iteracji UI możesz je dodatkowo przeciągnąć do czatu i dopisać:

> Traktuj załączone obrazy wyłącznie jako referencje układu i gęstości informacji. Nie kopiuj znaków towarowych, logo ani treści Linear/ChatGPT.

## Jakich integracji używać

Włączone i potrzebne: GitHub, Supabase, Vercel, Gmail, Google Calendar, Google Drive, Figma i Context7.

Nie podłączaj na potrzeby MVP: Notion, Outlook, Outlook Calendar, SharePoint, Todoist, TickTick, Asana ani ClickUp.

Połączenia ChatGPT z Gmail i Google Calendar nie stają się automatycznie połączeniami nowej aplikacji. Własna aplikacja otrzyma później oddzielne Google OAuth. Do czasu tej fazy używaj danych testowych i adapterów integracyjnych.

## Co wpisać później

Po akceptacji prototypu używaj krótkich poleceń, np.:

- „Kontynuuj Fazę 2 z `@docs/IMPLEMENTATION_PLAN.md`. Najpierw pokaż plan migracji Supabase.”
- „Zmień wyłącznie dashboard według komentarzy; nie modyfikuj modelu danych.”
- „Uruchom testy z `@docs/ACCEPTANCE_TESTS.md` dla przepływu ręcznego SGH Sync.”
- „Przed wdrożeniem wykonaj security review RLS, Storage i sekretów.”

## Czego nie robić

- Nie proś Codexa jednym poleceniem o zbudowanie wszystkich faz naraz.
- Nie twórz od razu produkcyjnego OAuth Gmail/Calendar.
- Nie pozwalaj na automatyczne wysyłanie e-maili ani zapisy do kalendarza bez podglądu i potwierdzenia.
- Nie wklejaj haseł, kodów MFA, ciasteczek, kluczy API ani tokenów do czatu lub repozytorium.
- Nie dodawaj funkcji wieloużytkownikowych, zespołów, organizacji, zaproszeń ani płatności.

## Kiedy MVP jest gotowe

MVP jest gotowe dopiero wtedy, gdy:

1. użytkownik po otwarciu aplikacji widzi następne działanie;
2. może ręcznie przekazać zmianę SGH tekstem, obrazem lub plikiem;
3. każda niepewna lub zewnętrzna zmiana wymaga potwierdzenia;
4. zadania, zajęcia, deadline'y, sesje nauki i okazje są spójne;
5. testy akceptacyjne przechodzą;
6. aplikacja działa na komputerze i telefonie jako PWA;
7. sekrety nie znajdują się w kliencie ani repozytorium.

