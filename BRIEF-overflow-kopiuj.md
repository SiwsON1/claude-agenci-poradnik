# BRIEF: naprawa rozjeżdżania okienek terminala + przyciski kopiowania w sekcji przykładów

Plik: `/Users/marcinsiwonia/projekty/claude-agenci-poradnik/index.html`.
Zasady twarde jak poprzednio: polskie znaki diakrytyczne, zero em-dash i en-dash, tylko istniejące klasy i tokeny, bez nowych bibliotek, nic istniejącego nie kasować.

## ZADANIE 1 (najważniejsze): okienka terminala rozpychają układ

Pomiar Playwrightem na żywym pliku:
- viewport 390 px: cała strona przewija się w bok o 935 px, dwanaście okienek `.term` wystaje poza `.wrap`, rekordzista o 935 px.
- viewport 1440 px: strona przewija się w bok o 83 px, wystają cztery okienka, w tym `TERMINAL · OKNO 1 · CODEX` w starej sekcji `#nadzor` o 273 px.

Przyczyna: `.term` leży w komórce siatki (`.block` ma `display:grid`), a komórka siatki ma domyślnie `min-width:auto`, więc zamiast przyciąć zawartość i pozwolić `.term` przewijać się wewnątrz (`overflow-x:auto` już tam jest), rozpycha całą kolumnę.

Napraw systemowo, dla całej strony, nie tylko dla nowych sekcji:
- Komórkom siatki, w których siedzą okienka, ustaw `min-width:0` (dotyczy potomków `.block`, a jeśli podobny układ jest gdzie indziej, na przykład `.tcol` albo `.blocks`, dołóż tam też).
- `.term` ma dostać `max-width:100%`.
- Nie zmieniaj `overflow-x:auto` ani `white-space:nowrap` poza tym, co opisano w zadaniu 3.

Warunek odbioru, sprawdź go sam po zmianie: po naprawie `document.documentElement.scrollWidth` równa się `clientWidth` przy szerokości 390 px i 1440 px, czyli strona nie przewija się w bok, a żadne `.term` nie wystaje poza prawą krawędź swojego `.wrap`. Okienka mają się przewijać wewnętrznie, jeśli komenda jest dłuższa niż kolumna.

## ZADANIE 2: przyciski kopiowania także w sekcji `#przyklady`
Dodaj przycisk `.term-copy` do każdego okienka `.term.term-sm` w sekcji `#przyklady`, dokładnie tak jak w `#instalacja` i `#pierwsza-sesja` (ten sam styl, ten sam `data-copy` bez znaku zachęty). Te polecenia mają być do wzięcia jednym kliknięciem, bo po to są.

## ZADANIE 3: zawijanie na telefonie obejmuje też nowe okienka
Reguła z `@media(max-width:719px)`, która zawija `.term-line` w okienkach z przyciskiem kopiowania, ma objąć również sekcję `#przyklady`. Jeśli obecna reguła celuje w konkretne sekcje, przepnij ją na okienka zawierające `.term-copy`, żeby działała wszędzie tam, gdzie jest komenda do skopiowania.

## ZADANIE 4: dwie drobne poprawki
- Przycisk kopiowania w trybie awaryjnym pokazuje `Zaznacz i skopiuj` i tak już zostaje. Ma wracać do napisu `Kopiuj` po 2 sekundach, tak samo jak `Skopiowano`.
- W sekcji `#vscode`, w kroku 1, słowa `Mac` i `Windows` na początku zdań o instalacji mają być pogrubione (`<b>`), żeby dało się na pierwszy rzut oka znaleźć swój system. Treści nie zmieniaj.

## Kontrola jakości (wypisz wynik każdego punktu)
- Zmierz i podaj `scrollWidth` oraz `clientWidth` dla 390 px i 1440 px po naprawie. Mają być równe.
- Podaj liczbę okienek `.term` wystających poza `.wrap` w obu szerokościach. Ma być zero.
- Liczba przycisków `.term-copy` na stronie i potwierdzenie, że każdy `data-copy` zawiera samą komendę.
- `grep -n '—\|–' index.html` pusto, polskie znaki obecne, HTML domknięty.
