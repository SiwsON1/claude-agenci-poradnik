# BRIEF: rozbudowa poradnika index.html o 3 nowe sekcje

## Zasady ogólne
- Plik: `/Users/marcinsiwonia/projekty/claude-agenci-poradnik/index.html`. Przeczytaj go w całości przed edycją.
- Styl 1:1 z istniejącą stroną: te same klasy i komponenty (`.wrap`, `.sec-head`, `.sec-no`, `.sec-title`, `.sec-intro`, akordeony `details.trick`, `.tricks/.tcol`, `.blocks/.block/.num`, `.terms/.term`, `.cyc-flow/.cyc-box/.cyc-arr`, `.loop-back`, `.reveal`). NIE wymyślaj nowego systemu wizualnego, nie dodawaj nowych fontów.
- Cała treść po polsku z poprawnymi znakami diakrytycznymi. ZERO em-dash (—) i en-dash (–). Ton jak reszta strony: warsztatowy, obrazowy, dla laika.
- Po dodaniu sekcji: zaktualizuj pigułki TOC (`.toc`) o nowe anchory we właściwej kolejności ORAZ przenumeruj `.sec-no` wszystkich sekcji tak, żeby numeracja szła po kolei.
- Niczego istniejącego nie usuwaj ani nie skracaj.

## Sekcja A: "Wtrącaj się, kiedy agent pracuje" (id="wtracanie")
Miejsce: PO sekcji `#tricki` (po linii ~310), PRZED `#funkcje`.
Treść:
- Intro (`.sec-intro`): Agent pracuje kilka minut sam. Nie musisz czekać do końca, żeby coś dopowiedzieć. Piszesz w trakcie, a wiadomość wpada między jego krokami.
- Przykładowa wymiana pokazana w bloku przykładu w stylu strony (mono, jak `.ex` w akordeonach albo prosty ciemny blok):
  agent: Przeglądam pliki kampanii...
  agent: Porównuję wyniki miesiąc po miesiącu...
  ty (w trakcie): btw pomiń marzec, tam były błędne dane
  agent: Jasne, pomijam marzec i liczę dalej.
- Trzy karty albo bloki (`.blocks` z `.num` 1-3):
  1. Dopisek to kierownica. Piszesz w trakcie, agent koryguje kurs bez zatrzymywania roboty.
  2. Esc to hamulec. Twardy stop, gdy idzie w złą stronę. Praca zrobiona do tej pory zostaje.
  3. Analogia: jak kucharz przy garach. Nie gasisz kuchni, żeby powiedzieć: mniej soli.
- Na końcu callout (`.loop-back`): odsyłacz, że jeden akordeon o Escape jest też w sekcji z trikami, a tu jest pełny obraz.

## Sekcja B: "Agent pilnuje agenta" (id="nadzor")
Miejsce: PO sekcji `#petla` (po linii ~457), PRZED `#czesci`.
Treść:
- Intro: W /goal kontroler sprawdza pracownika po każdej turze. Ale ten sam pomysł działa też szerzej: osobny agent nadzorca, który cyklicznie zagląda wykonawcy przez ramię.
- Scenka z naszej pracy (opisowo): Codex dostaje długą robotę, na przykład przepisanie sekcji strony. Claude dostaje pętlę: co 10 minut sprawdź co zrobił Codex, czy nie utknął i czy nie odjechał od briefu. Gdy coś jest nie tak: poprawia brief i zawraca wykonawcę na kurs.
- Diagram poziomy w stylu `.cyc-flow`: [CLAUDE nadzorca] -> zagląda co 10 minut -> [CODEX wykonawca] -> postęp i wynik -> (strzałka powrotna do nadzorcy). Jeśli `.cyc-flow` nie uniesie strzałki powrotnej, zrób dwa rzędy bloków z opisami strzałek tekstowo.
- Bloki albo akordeony z 3 zastosowaniami:
  1. Długa robota bez dryfu: nadzorca łapie moment, gdy wykonawca kręci się w kółko.
  2. Jeden pisze, drugi recenzuje: każdy większy kawałek kodu przechodzi przez drugiego agenta, zanim trafi do klienta.
  3. Rutyny: nadzór można ustawić przez /loop albo harmonogram, działa też gdy nie patrzysz.
- Callout (`.loop-back`): To nie science fiction, tylko /loop + drugi agent. Wszystko z klocków, które już znasz z tej strony.

## Sekcja C: "Chcesz więcej? Materiały wideo" (id="wideo")
Miejsce: PO sekcji `#prompt` (po linii ~639), PRZED `#mem`.
UWAGA: to sekcja z POLECANYMI FILMAMI do nauki (linki do YouTube), nie o przetwarzaniu wideo.
Treść: lista 5 pozycji w stylu kart `.terms/.term` (albo prostej listy w stylu strony), każda z: badge PL/EN (może być `.tag` albo mono etykieta), tytuł jako link `<a href>` otwierany w nowej karcie, jedno zdanie po co oglądać:
1. PL: Claude Code dla początkujących: jak zacząć krok po kroku. https://www.youtube.com/watch?v=RgG784JZ7o4 (dobry start bez technicznego tła)
2. PL: Claude Code: Poradnik Dla Początkujących. https://www.youtube.com/watch?v=RL3szsL72ow (podstawy pracy w terminalu i pierwsze zadania)
3. PL: 26 Funkcji Claude Code i Codex w 20 Minut. https://www.youtube.com/watch?v=fGqMoa-UMto (szybka mapa funkcji)
4. EN: Full Claude Code Tutorial for Non-Technical Beginners (2026). https://www.youtube.com/watch?v=bqJzIWAEn40 (cały proces od zera, krok po kroku)
5. EN: Claude Code Subagents: Complete Guide to Parallel Agents. https://www.vibecodingacademy.ai/blog/claude-code-subagents-complete-guide (artykuł: jak myśleć o pomocnikach i pracy równoległej)

## Kontrola jakości
- HTML poprawny, wszystkie details/summary domknięte.
- TOC działa (anchory się zgadzają), numeracja sekcji ciągła.
- Zero — i – w całym pliku (sprawdź grepem, także w nowych fragmentach).
- Klasa `.reveal` na nowych sekcjach jak na pozostałych.
