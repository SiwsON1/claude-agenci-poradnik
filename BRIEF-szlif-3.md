# BRIEF: szlif wizualny, runda trzecia (wyrównanie spisu i dwie etykiety)

Plik: `/Users/marcinsiwonia/projekty/claude-agenci-poradnik/index.html`. Zasady twarde bez zmian.

## ZMIANA 1: grupy spisu wyrównane w rzędach
Na zrzucie przy 1440 px widać, że spis rozkłada się kolumnami, nie rzędami: lewa kolumna trzyma grupy 1 i 3, prawa grupy 2, 4 i 5. Przez to etykiety grup startują na różnych wysokościach (pierwsza lewa etykieta wypada o kilkadziesiąt pikseli wyżej niż pierwsza prawa) i cały spis wygląda na złożony przypadkiem.

Przestaw układ tak, żeby grupy szły rzędami: grupa 1 i 2 w pierwszym rzędzie, 3 i 4 w drugim, 5 w trzecim. Etykiety sąsiadujących grup mają leżeć na tej samej linii. Użyj `grid-template-columns:1fr 1fr` z `align-items:start` i jednolitym odstępem między rzędami, bez `grid-auto-flow: column` i bez `column-count`. Ostatnia grupa zostaje w lewej kolumnie i nie rozciąga się na całą szerokość.

Sprawdź pomiarem: górne krawędzie etykiet grup 1 i 2 różnią się o mniej niż 2 px, tak samo grup 3 i 4.

## ZMIANA 2: dwie etykiety skrócone za mocno
- `09 · W trakcie` nie mówi nic komuś, kto nie zna sekcji. Sekcja nazywa się "Wtrącaj się, kiedy agent pracuje". Daj etykietę, która to oddaje, w granicach 22 znaków.
- `06 · Potknięcia` bez kontekstu brzmi jak nazwa działu, a nie jak pomoc przy problemach. Sekcja to "Coś nie działa: pięć typowych potknięć". Popraw podobnie.
Pozostałych etykiet nie ruszaj.

## Kontrola jakości (podaj liczby)
- Różnica w pionie górnych krawędzi etykiet sąsiadujących grup przy 1440 px.
- Wysokość spisu i hero przy 1440 px oraz 390 px.
- 22 odsyłacze, wszystkie cele istnieją, najdłuższa etykieta poniżej 23 znaków.
- Brak poziomego przewijania przy 390 px i 1440 px.
- `grep -n '—\|–' index.html` pusto, polskie znaki obecne.
