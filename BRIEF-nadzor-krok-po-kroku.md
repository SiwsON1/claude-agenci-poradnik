# BRIEF: rozbudowa sekcji #nadzor o "kto ma co" i instrukcję krok po kroku

## Cel
W `/Users/marcinsiwonia/projekty/claude-agenci-poradnik/index.html` rozbuduj TYLKO sekcję `#nadzor` (Agent pilnuje agenta). Reszta strony bez zmian. Styl: istniejące komponenty i tokeny brandu (Montserrat, granat/blue/mint, karty, `.term`). Polskie diakrytyki wszędzie, zero em-dash (—) i en-dash (–).

## 1. Ujednolić interwał na 30 minut
W całej sekcji #nadzor zamień "co 10 minut" / "10m" na "co 30 minut" / "30m" (scenka, terminal, diagram, wszystkie wystąpienia W TEJ SEKCJI). Timestampy w istniejącym terminalu nadzoru zmień odpowiednio (np. 10:00 / 10:30 / 11:00).

## 2. Nowy blok "Kto ma co: cel czy pętla?" (po scence, przed istniejącym terminalem)
Dwie karty obok siebie (grid 2 kolumny, na mobile 1):
- Karta WYKONAWCA (Codex): badge mono "WYKONAWCA", tytuł "Dostaje /goal, czyli metę". Tekst: "Robi robotę aż do skończenia. Nie wraca co pół godziny, nie czeka na nikogo: cel ciągnie go do przodu, a on sam sprawdza po każdej turze, czy meta jest osiągnięta."
- Karta NADZORCA (Claude): badge mono "NADZORCA", tytuł "Dostaje /loop, czyli pętlę". Tekst: "Nie ma własnej mety. Ma wracać co 30 minut, porównać wynik z briefem i zareagować: doprecyzować polecenie, zawrócić wykonawcę na kurs albo dać znać Tobie."
Pod kartami callout (styl `.loop-back`): "A czemu nie na odwrót? Gdyby nadzorca dostał /goal, nie wiedziałby, kiedy zaglądać: cel nie mówi nic o rytmie. Gdyby wykonawca dostał /loop, kręciłby się w kółko co 30 minut zamiast dojechać do mety. Cel ciągnie robotę, pętla pilnuje rytmu."

## 3. Nowy blok "Ustaw to u siebie: 3 kroki" (po bloku z punktu 2)
Trzy kroki w stylu `.blocks`/`.block` z numerami, każdy z mini-terminalem `.term` (wariant kompaktowy):
- Krok 1: "Daj wykonawcy metę, nie listę kroków". Terminal (etykieta `TERMINAL · OKNO 1 · CODEX`):
  `> /goal przepisz 5 sekcji strony według briefu z pliku brief.md. Meta: wszystkie sekcje zgodne z makietą i bez błędów w konsoli`
  `plan: czytam brief, potem sekcja po sekcji`
- Krok 2: "Daj nadzorcy pętlę i konkretne pytania". Terminal (etykieta `TERMINAL · OKNO 2 · CLAUDE`):
  `> /loop 30m zajrzyj do Codexa: porównaj wynik z brief.md, wypisz co odbiega, w razie potrzeby doprecyzuj polecenie i zawróć go na kurs`
  `10:00 sekcje 1-2 zgodne z briefem, jadę dalej`
- Krok 3: "Reaguj tylko, gdy nadzorca Cię zawoła". Terminal (etykieta `TERMINAL · OKNO 2 · CLAUDE`):
  `10:30 Codex zmienił kolory poza briefem, doprecyzowałem polecenie`
  `11:00 wrócił na kurs, 5 z 5 sekcji gotowe. Meta osiągnięta, kończę pętlę`
  Pod terminalem zdanie: "Nadzorca kończy pętlę, gdy meta wykonawcy jest osiągnięta. Ty w tym czasie robisz swoje."

## 4. Spójność
- Istniejący blok "Jeden agent ma pętlę..." zostaje (ew. dopasuj 30 minut).
- Istniejący diagram i 3 zastosowania zostają.
- Sprawdź HTML, brak myślników, responsywność (karty 2 kolumny -> 1 na mobile).
