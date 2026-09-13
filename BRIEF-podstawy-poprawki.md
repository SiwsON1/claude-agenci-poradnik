# BRIEF: trzy poprawki w nowych sekcjach index.html (po przeglądzie zrzutów)

Plik: `/Users/marcinsiwonia/projekty/claude-agenci-poradnik/index.html`. Dotyczy wyłącznie sekcji `#instalacja`, `#pierwsza-sesja` i `#klopoty`, które właśnie dodałeś. Reszty strony nie ruszaj.
Zasady te same co poprzednio: polskie znaki diakrytyczne, zero em-dash i en-dash, klasy i tokeny z istniejącego arkusza, bez nowych bibliotek.

## Poprawka 1: przycisk kopiowania przy komendach
Problem: `.term-line` ma `white-space:nowrap`, więc na telefonie komenda `curl -fsSL https://claude.ai/install.sh | bash` jest ucięta. To komenda, którą laik ma wkleić, więc musi dać się wziąć jednym kliknięciem.

Zrób:
- W każdym okienku `.term.term-sm` w sekcjach `#instalacja` i `#pierwsza-sesja` dodaj w prawym rogu paska tytułu (`.term-bar`) przycisk `<button class="term-copy" type="button" data-copy="...">Kopiuj</button>`, gdzie `data-copy` zawiera samą komendę do wklejenia, bez znaku zachęty `>` i bez linii zaczynających się od "wynik:". Jeśli okienko ma dwie komendy do wklejenia po kolei (na przykład `cd ...` i `claude`), w `data-copy` daj obie rozdzielone znakiem nowej linii.
- W okienkach z liniami "wynik:" kopiuj TYLKO komendy.
- Styl przycisku: mały, monospace, jasny tekst na przezroczystym tle, obramowanie `var(--line-d)`, zaokrąglenie jak `.term-sm`, `margin-left:auto` żeby dosunąć do prawej. Stany `:hover`, `:focus-visible` i `:active` obowiązkowo, animować tylko `transform` i `opacity` albo kolory, nigdy `transition:all`.
- JS na końcu pliku, przy istniejących skryptach: jedna delegacja zdarzeń na `document`, `navigator.clipboard.writeText(btn.dataset.copy)`, po sukcesie tekst przycisku zmienia się na `Skopiowano` i wraca do `Kopiuj` po 2 sekundach. Gdy API schowka odmówi (strona z pliku lokalnego w części przeglądarek), fallback: zaznacz tekst komendy przez `document.createRange` i pokaż na przycisku `Zaznacz i skopiuj`. Bez bibliotek, bez `alert`.
- Do `.term-bar` dodaj `gap` bez zmiany istniejącego wyglądu tytułu, żeby przycisk nie sklejał się z etykietą.

## Poprawka 2: komenda widoczna w całości na telefonie
W obrębie okienek, które dostały przycisk kopiowania, komenda ma się zawijać zamiast uciekać poza ekran. Dodaj do arkusza regułę tylko dla wąskich ekranów (`@media(max-width:719px)`), która w tych okienkach ustawia `.term-line{ white-space:pre-wrap; overflow-wrap:anywhere; }`. Zawinięte dalsze wiersze mają mieć lekkie wcięcie, żeby było widać, że to ta sama komenda. Nie zmieniaj zachowania `.term-line` w pozostałych sekcjach strony.

## Poprawka 3: szósta karta w sekcji "Coś nie działa"
Problem: pięć kart w siatce dwukolumnowej zostawia pustą dziurę w prawym dolnym rogu.
Dopisz szóstą kartę `.term-card` w tej samej konwencji co pozostałe (etykieta objawu w `<span class="m">`, przyczyna w `<b>`, rada w `<p>`), o tym, że agent nie pamięta poprzedniej rozmowy:
- etykieta: `agent nie pamięta poprzedniej rozmowy`
- przyczyna: każde uruchomienie startuje z pustą głową
- rada: `claude --continue` wraca do ostatniej rozmowy w tym folderze, a `/clear` czyści bieżącą, gdy chcesz zacząć od nowa. Ustalenia, które mają przetrwać na stałe, zapisz przez `/init` w pliku CLAUDE.md, bo ten plik agent czyta przy każdym starcie.
Karta ma iść przed blokiem `.note` z linkiem do dokumentacji.

## Kontrola jakości
- Sprawdź `grep -n '—\|–' index.html` (ma być pusto) i obecność polskich znaków w nowym tekście.
- Sprawdź, że `data-copy` każdego przycisku zawiera dokładnie to, co widać w okienku jako komenda, bez `>` i bez linii "wynik:".
- Sprawdź, że nowy JS nie rzuca błędu, gdy na stronie nie ma żadnego przycisku kopiowania.
- HTML domknięty, liczba kart w `#klopoty` wynosi 6.
