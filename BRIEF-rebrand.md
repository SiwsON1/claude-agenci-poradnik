# BRIEF: restyling poradnika index.html do aktualnego brandbooka Netim (nowa.netim.pl)

## Cel
Podnieść wizualnie `/Users/marcinsiwonia/projekty/claude-agenci-poradnik/index.html` do poziomu i stylu nowej strony nowa.netim.pl. TREŚĆ, struktura sekcji, akordeony, kotwice TOC i cała zawartość ZOSTAJĄ BEZ ZMIAN. Zmieniamy wyłącznie warstwę wizualną (CSS + drobne elementy markupu typu logo w topbarze i dekor hero). Przeczytaj cały index.html przed edycją.

## Tokeny brandu (źródło: child-theme nowa.netim.pl, plik home-v2.css)
Podmień istniejące zmienne CSS na:
```
--granat:#050a30; --blue:#1e5e9f; --mint:#80dfa0; --sky:#26a7f0; --deep:#0c4190;
--koral:#f86464; --lime:#caff7e; --turq:#00e19c; --white:#ffffff;
--bg-soft:#f1f4fb; --bg-paper:#fafbff; --bg-dark:#03061f; --ink-soft:#1a2046;
--mute:#5b6385; --line:#d8defa; --line-d:#1e2553;
--ease-out:cubic-bezier(.23,1,.32,1); --ease-inout:cubic-bezier(.77,0,.175,1);
--r-md:16px; --r-lg:22px;
```
Mapowanie ze starych: `#12224F` (navy) -> `--granat`; teal `#12B79B`/`#1FD6B6` -> na JASNYCH tłach `--blue` (kontrast!), na CIEMNYCH blokach `--mint`; miętowe tła `#E4F7F1`/`#F2FBF8` -> `--bg-soft`/`--bg-paper`; szare linie -> `--line`.

## Typografia
- Google Fonts: zamień Carlito na `Montserrat:ital,wght@0,300..900;1,300..900`. JetBrains Mono zostaje dla mono.
- Nagłówki sekcji: Montserrat 800, granat, letter-spacing lekko ujemny (-0.5px do -1px na dużych rozmiarach).
- Body: Montserrat 400/500, kolor `--ink-soft`, line-height 1.6-1.7.
- Eyebrow (obecne `.sec-no`): Montserrat 800 12px, uppercase, `letter-spacing:.14em`, kolor `--blue`, przed tekstem kropka 7px w `--mint` (pseudo-element, wyrównana do środka).
- Etykiety mono (np. nagłówki mini-terminali, tagi PL/EN) zostają w JetBrains Mono.

## Hero (góra strony)
- Tło: `radial-gradient(ellipse 60% 50% at 20% 0%, rgba(38,167,240,.16), transparent 60%), radial-gradient(ellipse 50% 40% at 85% 20%, rgba(128,223,160,.12), transparent 60%), linear-gradient(180deg, var(--granat), var(--bg-dark))`. Tekst hero biały, akcent "Claude Code" w `--mint` albo `--sky`.
- Dekor: sygnet Netim w wersji outline jako duży, subtelny element po prawej stronie hero, maskowany `radial-gradient(ellipse 72% 72% at center,#000 34%,transparent 96%)`, opacity niskie (0.14-0.2). SVG sygnetu skopiuj inline z pliku `/Users/marcinsiwonia/projekty/nowa-netim/child-theme/parts/main-nav.php` (symbol `#netim-sygnet-outline`; przeczytaj ten plik i przenieś ścieżki SVG 1:1).
- Badge nad tytułem ("CLAUDE CODE + AGENCI"): pill `border-radius:999px`, tło rgba biel 8%, border rgba biel 18%, tekst mono albo Montserrat 700 uppercase, jasny.
- Pigułki TOC w hero: na ciemnym tle: border `rgba(255,255,255,.22)`, tekst jasny, hover tło `rgba(255,255,255,.08)` + translateY(-1px); focus-visible outline `--sky`.

## Topbar
- Logo: inline SVG logo mark z `main-nav.php` (symbol `#netim-logo-mark`) + wordmark: `NETIM` Montserrat 800 + pod spodem lub obok `GROUP` Montserrat 500 9px `letter-spacing:.64em`. Skopiuj strukturę i proporcje z headera strony (main-nav.php okolice linii 71-75).
- Topbar biały, cienka linia dolna `--line`, tekst meta po prawej w `--mute`.

## Karty i komponenty (wszystkie istniejące)
- Karty (`.term-card`, karty wideo, karty agentów, bloki): tło `--white` lub `--bg-paper`, border `1px solid --line`, radius `--r-lg`, cień warstwowy: `0 1px 0 rgba(5,10,48,.04), 0 20px 40px -20px rgba(5,10,48,.18)`. Hover (tam gdzie karta jest klikalna, np. karty wideo): `translateY(-3px)` + cień mocniejszy `0 30px 70px -30px rgba(5,10,48,.45)`, transition tylko transform i box-shadow 200ms var(--ease-out).
- Akordeony `details.trick`: summary z hoverem (tło `--bg-soft`), marker rozwijania w `--blue`, focus-visible outline `--sky`. Otwarty akordeon: lewa krawędź 3px `--mint`.
- Mini-terminale `.term`: tło `--granat`, border `1px solid --line-d`, radius `--r-md`, prompt `>` w `--mint`, timestampy/komentarze w `--sky` lub przygaszone, tekst `#dfe5ff`. Cień jak karty.
- Callouty (`.loop-back` itp.): tło `--bg-soft`, lewa krawędź `--mint` albo `--blue`, radius `--r-md`.
- Diagramy (`.cyc-flow`, SVG pętli): boxy border `--line`, aktywne/wyróżnione tło `--bg-soft` z borderem `--blue`, strzałki `--blue`, etykiety tak/nie: tak `--turq` lub `--mint` (ciemniejszy wariant dla kontrastu na białym: użyj `--blue` jeśli mint nieczytelny), nie `--koral`.
- Linki tekstowe: `--blue`, underline offset 3px, hover `--deep`; focus-visible outline `--sky`.
- Tagi PL/EN i `.tag`: pill, mono 11px, tło `--bg-soft`, kolor `--blue`.
- Obrazki/screenshoty jeśli są: radius `--r-md` + cień `0 44px 90px -46px rgba(5,10,48,.5)` tylko dla dużych.

## Sekcje
- Naprzemienne tła sekcji: `--white` i `--bg-paper` (subtelnie), separatory `--line`.
- Sekcja finałowa/memowa: może dostać ciemne tło `--granat` z jasnym tekstem jako klamra z hero (jeśli łatwe bez ruszania treści; jeśli nie, zostaw jasną).
- Animacja `.reveal` zostaje (rise), timing na `var(--ease-out)`.

## Zasady twarde
- Animować TYLKO transform/opacity/box-shadow. Zero `transition: all`.
- Każdy interaktywny element: `:hover` + `:focus-visible` + `:active` (dla klikalnych `scale(.97)` lub translateY).
- `prefers-reduced-motion: reduce`: wyłącz translacje.
- Kontrast: nigdy `--mint` jako tekst na białym (za jasny). Na białym akcenty tekstowe = `--blue`/`--deep`.
- Zero em-dash i en-dash w ewentualnych nowych tekstach (nie dodawaj tekstów).
- HTML/CSS poprawne, strona ma działać bez JS-owych zmian (istniejący JS reveal zostaje).
- Mobile: strona już jest responsywna; zachowaj media queries, sprawdź że nowe style nie psują wąskich szerokości (karty w 1 kolumnie itd.).
