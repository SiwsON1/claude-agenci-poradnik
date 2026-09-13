# BRIEF: domknięcie ścieżki startowej w index.html (cztery zadania)

Plik: `/Users/marcinsiwonia/projekty/claude-agenci-poradnik/index.html`.
Zasady twarde, obowiązują wszędzie poniżej:
- Polskie znaki diakrytyczne w całym nowym tekście (ą ć ę ł ń ó ś ź ż).
- ZERO em-dash i en-dash. Przecinek, kropka, dwukropek, nawias.
- Tylko klasy, które już są w arkuszu strony: `.wrap`, `.sec-head`, `.sec-no`, `.sec-title`, `.sec-intro`, `.blocks`/`.block`/`.num`, `.terms`/`.term-card` (etykieta w `<span class="m">`), `.term`/`.term-sm`/`.term-bar`/`.term-dots`/`.term-title`/`.term-line` (znak zachęty w `<span class="u">&gt;</span>`), `.tricks`/`.tacc`/`details.trick`/`.d`, `.note`, `.loop-back`, `.mono`, `.reveal`. Bez nowych bibliotek, bez obrazków, bez nowego systemu wizualnego.
- Ton warsztatowy, dla osoby nietechnicznej z agencji (SEO, marketing, obsługa klienta). Akapity do 65 słów. Zero zwrotów typu "warto pamiętać", "kluczowe znaczenie", "podsumowując".
- Niczego istniejącego nie kasuj i nie przepisuj poza tym, co wprost opisano niżej.

---

## ZADANIE 1: przycisk kopiowania przy komendach

Problem: `.term-line` ma `white-space:nowrap`, więc na telefonie komenda `curl -fsSL https://claude.ai/install.sh | bash` jest ucięta, a to komenda do wklejenia.

- W każdym okienku `.term.term-sm` w sekcjach `#instalacja` i `#pierwsza-sesja` dodaj na końcu paska `.term-bar` przycisk `<button class="term-copy" type="button" data-copy="...">Kopiuj</button>`. W `data-copy` wchodzi sama komenda, bez znaku `>` i bez linii zaczynających się od "wynik:". Gdy okienko ma dwie komendy po kolei, rozdziel je znakiem nowej linii.
- Styl: mały, monospace, jasny tekst na przezroczystym tle, obramowanie `var(--line-d)`, zaokrąglenie spójne z `.term-sm`, `margin-left:auto`. Obowiązkowe stany `:hover`, `:focus-visible`, `:active`. Animuj tylko kolor, `transform` albo `opacity`, nigdy `transition:all`.
- JS przy istniejących skryptach na końcu pliku: jedna delegacja zdarzeń na `document`, `navigator.clipboard.writeText(btn.dataset.copy)`, po sukcesie napis zmienia się na `Skopiowano` i wraca po 2 sekundach. Gdy schowek odmówi (strona otwarta z pliku lokalnego), zaznacz tekst komendy przez `document.createRange` i pokaż `Zaznacz i skopiuj`. Bez bibliotek, bez `alert`. Kod ma nie rzucać błędu, gdy na stronie nie ma żadnego przycisku.
- Dodaj `gap` do `.term-bar`, żeby przycisk nie sklejał się z tytułem.

## ZADANIE 2: komenda widoczna w całości na telefonie

W `@media(max-width:719px)` dla okienek z przyciskiem kopiowania ustaw `.term-line{ white-space:pre-wrap; overflow-wrap:anywhere; }`, z lekkim wcięciem zawiniętych wierszy, żeby było widać, że to ta sama komenda. Nie zmieniaj zachowania `.term-line` w pozostałych sekcjach strony.

## ZADANIE 3: pobranie samego VS Code i trafienie do swojego folderu

### 3a. Sekcja `#vscode`
W `.blocks` dodaj NOWY krok jako pierwszy, a dotychczasowe kroki 1-4 przenumeruj na 2-5 (zmieniasz tylko cyfry w `.num`, treść kroków zostaje).

Nowy krok 1, nagłówek `Pobierz i zainstaluj VS Code`:
- Edytor jest darmowy, pobierasz go z `code.visualstudio.com` (link `target="_blank" rel="noopener"`), strona sama rozpoznaje system i podpowiada właściwą wersję. Kto ma VS Code od wcześniej, zaczyna od kroku drugiego.
- Mac: pobrany plik po otwarciu pokazuje ikonę programu. Przeciągasz Visual Studio Code do folderu Programy i uruchamiasz stamtąd.
- Windows: wybierz wersję User Installer, bo nie wymaga uprawnień administratora. Uruchamiasz plik .exe i klikasz przez instalator, który sam dopisuje edytor do systemu.
- Jedno zdanie na koniec: przy pierwszym uruchomieniu VS Code proponuje pakiet z polskimi nazwami przycisków. Zostaw angielskie, jeśli chcesz, żeby nazwy zgadzały się z tym poradnikiem.

### 3b. Sekcja `#instalacja`
Dodaj akordeon (`.tricks`/`.tacc`/`details.trick`) pod blokami, nagłówek `Jak trafić do swojego folderu w terminalu`:
- Komenda `cd` znaczy "przejdź do folderu". Po niej podajesz ścieżkę.
- Na Macu nie musisz jej przepisywać: wpisz `cd`, zrób spację i przeciągnij folder z Findera prosto do okna terminala, ścieżka wpisze się sama. Potem Enter.
- Na Windowsie kliknij folder prawym przyciskiem i wybierz kopiowanie ścieżki, potem wklej ją po `cd`.
- Komenda `pwd` na Macu albo `cd` bez niczego na Windowsie pokazuje, gdzie właściwie jesteś.

## ZADANIE 4: nowa sekcja z prostymi zadaniami na start

Wstaw NOWĄ sekcję `<section id="przyklady" class="reveal">` między `#pierwsza-sesja` a `#klopoty`. Numer `.sec-no`: `05 · przykłady`. Wszystkie następne sekcje przenumeruj (dotychczasowe 05-21 stają się 06-22) i zaktualizuj pigułki `.toc` w hero: dopisz `05 · Proste zadania na start` i popraw numery pozostałych pozycji.

Tytuł sekcji: `Proste zadania na start: pięć rzeczy, które możesz zlecić w pierwszym tygodniu`.
Intro: przykłady są dla osoby, która nie pisze kodu. Każde zadanie dotyczy plików, które i tak masz na dysku. Zacznij na kopii folderu, żeby spokojnie sprawdzić, jak agent pracuje.

Pięć bloków (`.blocks`, `.num` 1-5). Każdy: nagłówek `<h4>`, jedno zdanie po co to, okienko `.term.term-sm` z poleceniem wpisanym po polsku jak do człowieka (z `<span class="u">&gt;</span>`) i jedno zdanie, co dostajesz na wyjściu. Tytuły okienek w `.term-title` w konwencji strony (na przykład `TERMINAL · PORZĄDKI W PLIKACH`).

Tematy, treść dopracuj sam, ale trzymaj sens:
1. Porządki w plikach ze zdjęciami. Polecenie w stylu: zmień nazwy zdjęć w folderze zdjecia na opisowe, po polsku bez ogonków, słowa oddzielone myślnikami, zachowaj kolejność. Efekt: nazwy, które da się rozpoznać po roku i które rozumie Google.
2. Liczenie w tabeli. Polecenie: w pliku raport.csv policz sumę kliknięć dla każdego miesiąca i zapisz wynik do pliku podsumowanie.csv. Efekt: gotowa tabela bez ręcznego klikania w arkuszu.
3. Wyciąganie konkretów z dokumentu. Polecenie: przeczytaj plik brief-klienta.pdf i wypisz w punktach, o co klient prosi i czego zabrania. Efekt: lista zadań zamiast dwudziestu stron do przeczytania.
4. Przeczesanie folderu z notatkami. Polecenie: przejrzyj wszystkie pliki w folderze notatki i zbierz z nich jedną listę rzeczy do zrobienia, z nazwą pliku przy każdej pozycji. Efekt: jedno miejsce zamiast dwudziestu plików.
5. Prosta strona z pliku tekstowego. Polecenie: zrób z pliku cennik.md jedną stronę HTML z tabelą i otwórz ją w przeglądarce, żebym zobaczył wynik. Efekt: widoczny rezultat po kilku minutach, bez znajomości HTML.

Pod blokami dodaj porównanie dobrego i słabego polecenia, w dwóch kartach `.term-card` w `.terms`:
- karta z etykietą `polecenie za ogólne`: przykład "ogarnij mi te pliki" i zdanie, czemu to nie działa (agent zgaduje, co znaczy ogarnij, i robi coś innego niż myślisz).
- karta z etykietą `polecenie konkretne`: ten sam zamiar rozpisany na co, gdzie i po czym poznasz koniec, plus zdanie, że warunek końca jest tym, co zamienia życzenie w zadanie.

Na koniec `.loop-back` ze zdaniem, że pełne nawyki pisania poleceń są w dalszej sekcji o promptowaniu, a tu chodzi tylko o pierwsze wejście.

---

## Kontrola jakości (wypisz wynik każdego punktu)
- Numeracja `.sec-no` ciągła od 01 do 22, pigułki `.toc` zgodne z numerami i z istniejącymi `id` (sprawdź każdy href).
- Kroki w `#vscode` numerowane 1-5 bez luk.
- `grep -n '—\|–' index.html` nie zwraca nic.
- Polskie znaki obecne w nowym tekście (brak form "moze", "wiecej", "czesc", "reszte").
- Każdy `data-copy` zawiera dokładnie to, co w okienku jest komendą, bez `>` i bez linii "wynik:".
- HTML domknięty: zgadza się liczba `<section>`, `<details>`, `<div>`.
