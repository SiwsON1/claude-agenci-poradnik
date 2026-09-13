# BRIEF: szlif wizualny poradnika (cztery zmiany)

Plik: `/Users/marcinsiwonia/projekty/claude-agenci-poradnik/index.html`.
Zasady twarde: polskie znaki diakrytyczne, zero em-dash i en-dash, tylko istniejące tokeny kolorów i fonty ze strony, bez nowych bibliotek. Animować wyłącznie `transform`, `opacity`, kolory i `clip-path`, nigdy `transition:all`, nigdy właściwości układu. Każdy nowy element klikalny ma `:hover`, `:focus-visible` i `:active`. Blok `@media (prefers-reduced-motion: reduce)` na końcu arkusza musi obejmować też to, co dodasz.

## Kontekst
Strona ma 34 330 px wysokości i 22 sekcje. Po dołożeniu bloku startowego spis treści w hero to 22 jednakowe pigułki w czterech rzędach, bez struktury, a pierwsze pięć sekcji ma identyczny rytm: nagłówek, pionowa lista numerowanych bloków, okienko terminala. Zmiany poniżej mają to rozbić, nie przebudowywać strony.

## ZMIANA 1: spis treści w hero pogrupowany tematycznie

Zamiast jednej płaskiej listy 22 pigułek zrób pięć grup, każda z małą etykietą nad swoim rzędem pigułek. Etykieta w stylu istniejącego `.sec-no` albo `.term-title`: mono, wersaliki, mały rozmiar, kolor przygaszony względem pigułek, bez ozdobników. Pigułki zostają takie jak są (`.toc a`), zmienia się tylko grupowanie i odstępy.

Podział sekcji na grupy (numery zgodne z obecną numeracją):
- 01-06: sekcje start, instalacja, vscode, pierwsza-sesja, przyklady, klopoty. Etykieta o sensie "zaczynasz od zera".
- 07-10: poziomy, tricki, wtracanie, funkcje. Etykieta o sensie "codzienna praca".
- 11-15: agent, petla, nadzor, czesci, sdk. Etykieta o sensie "jak to działa w środku".
- 16-19: mcp, skille, predkosc, nasze. Etykieta o sensie "narzędzia i nasze wdrożenia".
- 20-22: prompt, wideo, mem. Etykieta o sensie "na koniec".
Nazwy grup dobierz sam, krótkie, po polsku, dwa albo trzy słowa, bez wielkich słów.

Odstęp między grupami wyraźnie większy niż między pigułkami w grupie, żeby podział był widoczny bez linii i ramek. Na telefonie grupy układają się jedna pod drugą i nadal się nie rozjeżdżają.

## ZMIANA 2: pasek postępu czytania

Cienki pasek (2-3 px) przyklejony do górnej krawędzi okna, pokazujący, ile strony zostało. Kolor `var(--mint)`, pod spodem nic (żadnego tła), `pointer-events:none`, nad treścią ale pod ewentualnym paskiem górnym strony.

Zrób to bez JavaScriptu, animacją sterowaną przewijaniem:
```
animation: nazwa linear;
animation-timeline: scroll();
```
z `transform-origin:left` i skalowaniem w poziomie od 0 do 1. Całość obuduj `@supports (animation-timeline: scroll())`, żeby w przeglądarkach bez tej funkcji pasek po prostu się nie pojawiał (nie rób zapasowego wariantu na JS). Przy `prefers-reduced-motion: reduce` pasek ma zniknąć.

## ZMIANA 3: sekcja `#start` na trzy karty obok siebie

Dziś to pionowa lista `.blocks` z numerami 1-3 (Konto, Komputer, Piętnaście minut), a zaraz po niej idą trzy kolejne sekcje w tym samym układzie. Przełam ten rytm: przenieś te trzy pozycje do układu trzech kart obok siebie, korzystając z istniejącej klasy `.three` (na wąskich ekranach i tak zwija się do jednej kolumny). Treść zostaje bez zmian, numery możesz zachować jako duży znak wewnątrz karty albo pominąć, jeśli układ czyta się lepiej bez nich. Akordeony pod spodem (terminal, folder projektu, bezpieczeństwo) zostają.

Karty mają mieć stan `:hover` spójny z `.term-card` na stronie (delikatne uniesienie i mocniejszy cień), bez nowych kolorów.

## ZMIANA 4: wejście bloków z opóźnieniem kaskadowym

Bloki w `.blocks` i karty w `.terms` pojawiają się dziś wszystkie naraz razem z `.reveal`. Dodaj kaskadę: kolejne elementy w obrębie jednego kontenera wchodzą z opóźnieniem 40-60 ms względem poprzedniego, maksymalnie do szóstego elementu (dalej bez dodatkowego opóźnienia, żeby dół sekcji nie czekał). Zrób to czystym CSS na `:nth-child`, bez dotykania skryptu obsługującego `.reveal`. Przy `prefers-reduced-motion: reduce` opóźnienia mają zniknąć.

## Kontrola jakości (wypisz wynik każdego punktu)
- Zmierz Playwrightem (`NODE_PATH=/Users/marcinsiwonia/projekty/agent-lab/node_modules node _pomiary/<skrypt>.cjs`): brak poziomego przewijania strony przy 390 px i 1440 px, żaden `.term` nie wystaje poza `.wrap`.
- Spis treści: 22 odsyłacze, każdy prowadzi do istniejącego `id`, podzielone na 5 grup.
- `grep -n '—\|–' index.html` pusto, polskie znaki obecne.
- Brak `transition:all` w pliku, brak animacji na właściwościach układu.
- Blok `prefers-reduced-motion` obejmuje pasek postępu i kaskadę.
- HTML domknięty, skrypty bez błędów.
