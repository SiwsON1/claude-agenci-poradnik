# BRIEF: rozbudowa poradnika index.html o blok startowy dla totalnego laika

## Cel
Dodać na POCZĄTKU poradnika pięć nowych sekcji, które prowadzą kogoś, kto nigdy nie otwierał terminala, od zera do pierwszej działającej sesji Claude Code, w tym instalacji w VS Code. Dziś strona zaczyna się od "Pięciu poziomów", czyli od mapy, ale nikt nie wie, jak w ogóle zacząć.

## Zasady ogólne (twarde)
- Plik: `/Users/marcinsiwonia/projekty/claude-agenci-poradnik/index.html`. Przeczytaj go W CAŁOŚCI przed edycją.
- Styl 1:1 z istniejącą stroną. Używaj TYLKO klas, które już są w pliku: `.wrap`, `.sec-head`, `.sec-no`, `.sec-title`, `.sec-intro`, `.tricks`/`.tacc`/`details.trick`/`.d`, `.blocks`/`.block`/`.num`, `.terms`/`.term-card` (z `<span class="m">`), `.term`/`.term-sm`/`.term-bar`/`.term-dots`/`.term-title`/`.term-line` (z `<span class="u">&gt;</span>`), `.loop-back`, `.note`, `.three`, `.reveal`, `.mono`, `.ex`.
  NIE twórz nowego systemu wizualnego, nie dodawaj fontów, nie dodawaj bibliotek. Jeśli potrzebujesz drobnej korekty wyglądu, dopisz maksymalnie kilka reguł do istniejącego `<style>`, spójnych z tokenami (var(--blue), var(--mint), granat).
- Cała treść po polsku z pełnymi znakami diakrytycznymi (ą, ć, ę, ł, ń, ó, ś, ź, ż). Brak ogonków = robota do wyrzucenia.
- ZERO em-dash (—) i en-dash (–) w całym pliku. Przecinek, kropka, dwukropek, nawias. Sprawdź grepem po edycji.
- Ton: warsztatowy, obrazowy, dla laika, bez żargonu. Każde pojęcie techniczne tłumacz przy pierwszym użyciu jednym zdaniem (terminal, folder projektu, rozszerzenie, panel).
- Akapity krótkie, do 65 słów. Zero zwrotów typu "warto pamiętać", "w dzisiejszych czasach", "kluczowe znaczenie", "podsumowując".
- Niczego istniejącego nie usuwaj, nie skracaj i nie przepisuj.

## Gdzie wstawić
Wszystkie pięć sekcji idzie PRZED istniejącą sekcją `<section id="poziomy">` (dziś "01 · mapa"), w kolejności A, B, C, D, E.

Po dodaniu:
1. Przenumeruj `.sec-no` WSZYSTKICH sekcji na stronie, żeby numeracja szła ciągiem od 01 do 21 (nowe zajmują 01-05, dotychczasowe "01 · mapa" staje się "06 · mapa" itd., opisowa część po kropce zostaje bez zmian).
2. Przebuduj pigułki TOC (`.toc` w hero) tak, żeby zawierały nowe anchory na początku i zachowały resztę we właściwej kolejności z nowymi numerami.
3. Dopisz jedno zdanie do `.lede` w hero albo dopisz krótkie zdanie, że poradnik zaczyna się od instalacji od zera. Nie przepisuj całego lede.

## Sekcja A: id="start" | "Zanim zaczniesz: co jest potrzebne"
Intro: Claude Code to nie strona internetowa, tylko program, który działa na Twoim komputerze i ma dostęp do plików w jednym folderze, który mu wskażesz. Instalacja zajmuje kilkanaście minut i nie wymaga umiejętności programowania.

Trzy bloki (`.blocks`, `.num` 1-3):
1. Konto. Potrzebny płatny plan Claude: Pro, Max, Team albo Enterprise. Darmowy plan Claude.ai nie daje dostępu do Claude Code. Alternatywnie konto w Anthropic Console, rozliczane za zużycie.
2. Komputer. macOS od wersji 13, Windows 10 (aktualizacja 1809) lub nowszy, albo Linux. Minimum 4 GB pamięci i stałe połączenie z internetem.
3. Piętnaście minut. Nic nie trzeba konfigurować ręcznie, instalator robi wszystko sam, a logowanie odbywa się przez przeglądarkę.

Dalej akordeony (`.tricks` z `.tacc`, `details.trick`) tłumaczące trzy pojęcia dla kogoś, kto ich nie zna:
- "Co to jest terminal": czarne okno, w którym piszesz polecenia zamiast klikać. Na Macu nazywa się Terminal i znajdziesz go przez Spotlight (Cmd + spacja, wpisz "Terminal"). Na Windowsie to PowerShell, w menu Start. Nic nie zepsujesz, dopóki nie wpisujesz komend, których nie rozumiesz.
- "Co to jest folder projektu": Claude widzi tylko ten folder, który mu otworzysz, i wszystko w środku. Nie ma dostępu do reszty dysku. Dlatego zawsze zaczynasz od przejścia do folderu z robotą.
- "Czy to bezpieczne": zanim agent zmieni plik albo uruchomi komendę, pyta o zgodę (zależnie od trybu uprawnień, opisanego w sekcji o VS Code). Pierwsze dni pracuj na kopii folderu, nie na jedynym egzemplarzu.

## Sekcja B: id="instalacja" | "Instalacja krok po kroku"
Intro: Jedna komenda wklejona do terminala. Instalator sam pobiera program i sam się aktualizuje w tle.

Bloki (`.blocks`, `.num`) z okienkami terminala (`.term term-sm`, tytuł w `.term-title`):
1. "Mac albo Linux": otwórz Terminal i wklej. Okno terminala z tytułem `TERMINAL · MAC` i linią:
   `curl -fsSL https://claude.ai/install.sh | bash`
2. "Windows": otwórz PowerShell (nie CMD, poznasz po tym, że linia zaczyna się od `PS C:\`) i wklej. Okno z tytułem `POWERSHELL · WINDOWS` i linią:
   `irm https://claude.ai/install.ps1 | iex`
   Pod spodem zdanie: na Windowsie warto doinstalować Git for Windows (https://git-scm.com/downloads/win), bo daje agentowi pełniejszy zestaw komend. Bez niego też zadziała.
3. "Sprawdź, czy się udało": okno terminala z tytułem `TERMINAL · SPRAWDZENIE` i dwiema liniami:
   `claude --version` (ma wypisać numer wersji, na przykład `2.1.211 (Claude Code)`)
   `claude doctor` (wypisuje diagnostykę instalacji i ustawień, gdy coś jest nie tak)
4. "Pierwsze uruchomienie i logowanie": przejdź do folderu z projektem i wpisz `claude`. Okno terminala z tytułem `TERMINAL · PIERWSZY START` i liniami:
   `cd ~/projekty/moja-strona`
   `claude`
   Opis: przy pierwszym uruchomieniu otworzy się przeglądarka z logowaniem do konta Claude. Potwierdzasz i wracasz do terminala.

Na końcu `.note` albo `.loop-back`: kto nie chce terminala w ogóle, może zacząć od aplikacji Claude Desktop na Maca i Windowsa, która daje to samo w oknie z przyciskami. Terminal i tak przyda się później, przy pracy w kilku sesjach naraz.

## Sekcja C: id="vscode" | "Claude Code w VS Code: wersja z oknem zamiast terminala"
Intro: VS Code to darmowy edytor kodu od Microsoftu (do pobrania z code.visualstudio.com). Claude Code ma do niego oficjalne rozszerzenie i to jest najwygodniejszy sposób pracy, bo widzisz rozmowę i pliki obok siebie, a zmiany dostajesz do zatwierdzenia w formie porównania przed i po.

Wymaganie w `.note`: VS Code w wersji 1.94 lub nowszej, do tego to samo konto Claude co wyżej. Klucz API nie jest potrzebny.

Bloki (`.blocks`, `.num` 1-4):
1. "Zainstaluj rozszerzenie": w VS Code naciśnij Cmd + Shift + X (Mac) albo Ctrl + Shift + X (Windows), wpisz w wyszukiwarkę "Claude Code", wybierz pozycję od wydawcy Anthropic i kliknij Install. Jeśli po instalacji nic się nie pojawia, zrestartuj VS Code.
2. "Otwórz panel": w prawym górnym rogu edytora pojawia się ikona iskry (Spark). Klikasz i po prawej otwiera się panel rozmowy. Ikona iskry jest też na lewym pasku, na liście sesji. Panel można przeciągnąć w dowolne miejsce okna.
3. "Zaloguj się": przy pierwszym otwarciu panelu klikasz Sign in i potwierdzasz w przeglądarce. Potem pokazuje się lista "Learn Claude Code" z zadaniami na rozgrzewkę.
4. "Otwórz folder z robotą": File, Open Folder, wskazujesz katalog projektu. Claude pracuje w tym, co otwarte w edytorze.

Dalej akordeony (`.tricks`/`.tacc`) z tym, co daje panel:
- "Tryby uprawnień, czyli ile agent może sam": klikasz wskaźnik trybu pod polem tekstowym. Auto: klasyfikator sam przepuszcza większość działań, bez pytania o każde. Manual: agent pyta przed każdą zmianą pliku i przed większością komend. Plan: najpierw opisuje, co zamierza, czeka na akceptację, a plan otwiera się jako dokument, w którym możesz dopisać uwagi. Edit automatically: zmienia pliki bez pytania.
- "Pokazywanie plików agentowi": wpisujesz `@` i kawałek nazwy pliku albo folderu, reszta się podpowiada. Zaznaczony w edytorze fragment kodu agent widzi sam, a Option + K (Mac) albo Alt + K (Windows) wstawia do polecenia odnośnik z numerami linii, na przykład `@app.ts#5-10`. Obrazek wklejasz do pola ze schowka.
- "Porównanie przed i po": w trybie Manual każda zmiana pliku pokazuje się jako zestawienie starej i nowej wersji obok siebie. Możesz przyjąć, odrzucić albo napisać, co zrobić inaczej.
- "Wracanie do starych rozmów": przycisk historii sesji na górze panelu. Sesje mają automatyczne tytuły, można je przemianować i archiwizować, a nieużywane po dwóch tygodniach same trafiają do archiwum.
- "Drobiazgi, które oszczędzają nerwy": Shift + Enter robi nową linię bez wysyłania wiadomości. Pod polem widać, ile pamięci rozmowy zostało. Rozszerzenie działa też w edytorach zbudowanych na VS Code, na przykład Cursor.

Na końcu `.loop-back`: rozszerzenie nosi w sobie własną kopię programu na potrzeby panelu. Jeśli chcesz dodatkowo wpisywać `claude` w terminalu wbudowanym w VS Code, zostaw przy tym instalację z sekcji drugiej. Jedno drugiemu nie przeszkadza.

## Sekcja D: id="pierwsza-sesja" | "Pierwsze dziesięć minut: co napisać na start"
Intro: Program działa, konto podpięte, folder otwarty. Teraz najprostsza ścieżka, żeby zobaczyć, o co chodzi, bez ryzyka popsucia czegokolwiek.

Bloki (`.blocks`, `.num` 1-4), każdy z okienkiem terminala pokazującym realne polecenie:
1. "Poproś o rozpoznanie terenu": `> opisz mi, co jest w tym folderze i do czego służy ten projekt`. Nic nie zmienia, a Ty sprawdzasz, czy agent w ogóle widzi to, co powinien.
2. "Zbuduj pamięć projektu": `> /init`. Agent przegląda projekt i zapisuje plik CLAUDE.md z notatkami, które czyta przy każdym następnym uruchomieniu. Raz zrobione, działa zawsze.
3. "Daj małe, konkretne zadanie": `> popraw literówki w pliku oferta.md i pokaż mi, co zmieniłeś`. Małe zadanie na start uczy więcej niż duże, bo widać cały przebieg.
4. "Zamknij i wróć później": `> /clear` czyści rozmowę bez zamykania programu, a `claude --continue` wraca do ostatniej sesji w tym folderze.

Na końcu `.loop-back` odsyłający do sekcji z wtrącaniem się w trakcie pracy i do sekcji o promptowaniu: co napisać, gdy agent idzie w złą stronę, jest dalej na tej stronie.

## Sekcja E: id="klopoty" | "Coś nie działa: pięć typowych potknięć"
Format: `.terms` z kartami `.term-card`, w `<span class="m">` krótka etykieta objawu, w `<b>` przyczyna, w `<p>` co zrobić.
1. etykieta "command not found: claude" | przyczyna: terminal nie zna jeszcze nowej komendy | rada: zamknij okno terminala i otwórz nowe, komenda dopisuje się przy starcie. Jeśli dalej nie działa, uruchom instalację jeszcze raz i sprawdź `claude doctor`.
2. etykieta "logowanie nie przechodzi" | przyczyna: darmowy plan albo złe konto | rada: Claude Code wymaga planu Pro, Max, Team, Enterprise albo konta Console. Sprawdź, na które konto zalogowała się przeglądarka, bo bierze to zalogowane jako pierwsze.
3. etykieta "panel w VS Code pusty" | przyczyna: rozszerzenie wystartowało przed instalacją | rada: Command Palette (Cmd + Shift + P albo Ctrl + Shift + P), komenda "Developer: Reload Window". Jeśli to nie pomaga, zrestartuj cały edytor.
4. etykieta "agent nie widzi pliku" | przyczyna: plik leży poza otwartym folderem | rada: Claude sięga tylko do folderu, który mu otworzyłeś. Otwórz folder wyżej albo skopiuj plik do środka.
5. etykieta "agent poszedł w złą stronę" | przyczyna: polecenie było za ogólne albo brakowało w nim warunku końca | rada: Escape zatrzymuje pracę natychmiast, a to, co zrobił do tej pory, zostaje. Dopisz, co ma być gotowe i czego ma nie ruszać, i puść jeszcze raz.

Pod kartami `.note`: pełną listę komend i ustawień trzyma oficjalna dokumentacja pod adresem https://code.claude.com/docs (po angielsku). Link ma się otwierać w nowej karcie.

## Kontrola jakości przed oddaniem
- HTML poprawny, wszystkie `<details>`, `<section>`, `<div>` domknięte.
- Numeracja `.sec-no` ciągła 01-21, TOC zgadza się z anchorami (sprawdź każdy href z id w pliku).
- `grep -n '—\|–' index.html` ma nie zwracać nic.
- Polskie znaki diakrytyczne obecne w całym nowym tekście (sprawdź, czy nie ma "moze", "wiecej", "czesc").
- Klasa `.reveal` na nowych sekcjach, tak jak w pozostałych.
- Wszystkie linki zewnętrzne z `target="_blank" rel="noopener"`.
