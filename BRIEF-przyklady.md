# BRIEF: przykłady "jak to wygląda w praktyce" w poradniku index.html

## Cel
Rozbudowa `/Users/marcinsiwonia/projekty/claude-agenci-poradnik/index.html`. Strona ma zostać KOMPAKTOWA: podstawy widać od razu, głębsza wiedza w akordeonach. Do funkcji i kluczowych pojęć dodajemy realistyczne przykłady w formie mini-okna terminala (jak w VS Code). Przeczytaj cały plik przed edycją.

## 1. Komponent: mini-okno terminala (zrób raz, używaj wszędzie)
Dodaj do CSS jeden komponent `.term` w stylu granatowego bloku przykładu, który już jest w sekcji #wtracanie:
- Ciemne tło `#12224F` (jak `.trace`), zaokrąglenie i padding jak istniejące bloki.
- Nagłówek okna: trzy kropki (szare kółeczka CSS, bez kolorów mac, subtelnie) + etykieta mono np. `TERMINAL · VS CODE`.
- Zawartość mono (JetBrains Mono), 3-7 linii: linie użytkownika zaczynają się od `>` w kolorze teal `#1FD6B6`, linie agenta w jasnoszarym, komentarze w przygaszonym.
- Wersja kompaktowa do akordeonów: mniejszy padding i font ~13-14px, żeby nie rozdymać.
- Bez animacji pisania (strona scrollowana, ma być lekko).

## 2. Sekcja #funkcje (Dwanaście funkcji Claude Code)
W KAŻDYM z akordeonów funkcji dodaj na końcu treści mini-okno `.term` z realistycznym przykładem użycia: wpisana komenda/polecenie + 2-4 linie efektu. Akordeony zostają domyślnie zamknięte (kompaktowość zachowana). Przykłady dopasuj do opisu danej funkcji w akordeonie. Wzorce (dostosuj do faktycznej listy funkcji w pliku):
- Sub-agenci: `> przeszukaj wszystkie umowy i wypisz terminy wypowiedzenia` / `agent: uruchamiam 3 pomocników równolegle...` / `pomocnik 1: znalazłem 12 umów...` / `agent: gotowe, oto zbiorcze zestawienie.`
- /loop: `> /loop 10m sprawdź czy klient odpisał i przygotuj odpowiedź` / `10:00 sprawdzono, brak odpowiedzi` / `10:10 sprawdzono, brak odpowiedzi` / `10:20 klient odpisał! szykuję draft`
- /goal: `> /goal wszystkie testy przechodzą i strona ładuje się poniżej 2 s` / `plan: najpierw testy, potem szybkość` / `test: 3 z 40 nie przechodzą, poprawiam...` / `test: 40 z 40, ładowanie 1.8 s. Meta osiągnięta.`
- /compact, /clear, /init, statusline, worktrees, sterowanie z telefonu itd.: analogicznie, po jednym konkretnym przykładzie komendy i efektu.
Jeśli jakaś funkcja jest czysto opisowa i przykład terminalowy nie ma sensu, zamiast `.term` dodaj jednozdaniowy przykład "U nas: ..." w istniejącym stylu `.ex`.

## 3. Sekcja #petla (Pętla i /goal)
- Przy omówieniu /loop wstaw mini-okno `.term` z przykładem pętli (timeline 10:00/10:10/10:20 jak wyżej, może być inny use-case, np. monitorowanie wdrożenia).
- Przy omówieniu /goal wstaw mini-okno `.term` z przebiegiem: cel -> plan -> test nie przechodzi -> poprawka -> test przechodzi -> meta osiągnięta.
- Dopisz jedno zdanie wiążące: "Zapamiętaj różnicę: /loop wraca do zadania co jakiś czas, /goal nie odpuszcza, aż meta jest osiągnięta."

## 4. Sekcja #nadzor (Agent pilnuje agenta)
Dodaj mini-okno `.term` pokazujące jak to realnie wygląda: 
`> /loop 10m zajrzyj do Codexa: czy trzyma się briefu i czy nie utknął`
`10:00 Codex przepisał 2 z 5 sekcji, zgodnie z briefem`
`10:10 Codex utknął na galerii zdjęć, doprecyzowuję polecenie`
`10:20 wrócił na kurs, 4 z 5 sekcji gotowe`
Plus jedno zdanie: "Jeden agent ma pętlę (Claude z /loop), drugi ma cel (Codex z /goal). Pętla pilnuje, cel ciągnie robotę do przodu."

## 5. Sekcja #wtracanie
Już ma przykład rozmowy. Tylko ujednolić wygląd tego bloku z nowym komponentem `.term` (dodaj kropki i etykietę okna), treść zostaje.

## Zasady
- Cała treść po polsku z poprawnymi diakrytykami. ZERO em-dash (—) i en-dash (–), także w przykładach.
- Nie zmieniaj istniejących tekstów poza wskazanymi miejscami. Nie usuwaj niczego.
- Styl komend realistyczny ale prosty, zrozumiały dla laika (przykłady z życia agencji: klienci, strony, raporty, kampanie).
- Sprawdź po zmianach: HTML poprawny, wszystkie details domknięte, grep na — i – pusty.
