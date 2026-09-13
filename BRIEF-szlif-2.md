# BRIEF: szlif wizualny, runda druga (spis treści i karty)

Plik: `/Users/marcinsiwonia/projekty/claude-agenci-poradnik/index.html`. Zasady twarde jak poprzednio: polskie znaki, zero em-dash i en-dash, istniejące tokeny i klasy, animować tylko `transform`, `opacity` i kolory, każdy nowy element klikalny ma `:hover`, `:focus-visible`, `:active`, blok `prefers-reduced-motion` obejmuje nowości.

## Pomiary, które to wywołały
Hero ma 1086 px wysokości, z czego sam spis treści 407 px na desktopie. Na telefonie spis to kilka ekranów przewijania, zanim czytelnik dojdzie do pierwszej sekcji. Grupowanie zostaje, zmienia się gęstość.

## ZMIANA 1: spis na desktopie w dwóch kolumnach
Od szerokości około 900 px ułóż grupy spisu w dwóch kolumnach (CSS Grid, `grid-template-columns:1fr 1fr`, sensowny `gap`). Grupy mają się układać kolumnami tak, żeby wysokość obu kolumn była zbliżona. Cel liczbowy: spis poniżej 240 px wysokości przy 1440 px szerokości, przy zachowaniu czytelnych odstępów.

## ZMIANA 2: krótsze etykiety pigułek
Najdłuższe pigułki łamią rzędy i robią z grup przypadkowe kształty. Skróć teksty, zachowując numer i sens. Propozycje, możesz dobrać własne, byle krótsze i jednoznaczne:
- `01 · Co jest potrzebne` zostaje
- `03 · Claude Code w VS Code` na `03 · VS Code`
- `05 · Proste zadania na start` na `05 · Zadania na start`
- `07 · Pięć poziomów Claude` na `07 · Pięć poziomów`
- `10 · Najważniejsze funkcje` na `10 · Funkcje`
- `12 · Pętla i /goal` zostaje
- `16 · Narzędzia MCP` zostaje
- pozostałe przejrzyj i skróć te, które przekraczają około 22 znaków
Tytuły sekcji na stronie zostają bez zmian, skracasz wyłącznie pigułki.

## ZMIANA 3: spis zwinięty na telefonie
Na wąskich ekranach spis ma być domyślnie zwinięty, żeby nie zasłaniał wejścia w treść. Zrób to elementem `<details>` w konwencji strony (`details.trick` już jest, ale spis ma swój styl, więc użyj własnej, spójnej wersji bez kopiowania ramek akordeonu). W `summary` krótka etykieta, na przykład `Spis treści` plus liczba sekcji. W HTML `<details>` ma atrybut `open`, żeby bez JavaScriptu spis był w całości widoczny. Mały skrypt przy istniejących skryptach zamyka go, gdy `matchMedia('(max-width: 719px)')` pasuje, i otwiera z powrotem po przejściu na szeroki ekran. Na desktopie `summary` ma być ukryty, bo spis jest zawsze rozwinięty.

## ZMIANA 4: numery w kartach sekcji `#start`
Numery 01, 02, 03 w kartach są dziś ledwo widoczne i wyglądają jak artefakt. Wzmocnij je: kolor `var(--blue)`, wyraźniejszy rozmiar i waga, nadal drugoplanowe wobec nagłówka karty. Alternatywnie usuń je zupełnie, jeśli po próbie układ czyta się lepiej bez nich. Wybierz jedno i uzasadnij w podsumowaniu.

## Kontrola jakości (podaj liczby)
- Wysokość spisu i całego hero przy 1440 px oraz przy 390 px, przed i po zmianie.
- Liczba odsyłaczy w spisie nadal 22, wszystkie prowadzą do istniejących `id`.
- Brak poziomego przewijania przy 390 px i 1440 px.
- Zachowanie `<details>`: zamknięty przy 390 px, otwarty i bez widocznego `summary` przy 1440 px.
- `grep -n '—\|–' index.html` pusto, polskie znaki obecne, brak `transition:all`.
