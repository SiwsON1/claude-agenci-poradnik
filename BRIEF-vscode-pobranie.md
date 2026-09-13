# BRIEF: dołóż krok pobrania i instalacji samego VS Code

Plik: `/Users/marcinsiwonia/projekty/claude-agenci-poradnik/index.html`, sekcja `<section id="vscode">`. Reszty strony nie ruszaj.
Zasady: polskie znaki diakrytyczne, zero em-dash i en-dash, tylko klasy z istniejącego arkusza, ton dla laika, akapity do 65 słów.

## Problem
Sekcja zakłada, że czytelnik ma już VS Code i od razu każe mu instalować rozszerzenie. Ktoś, kto edytora nigdy nie widział, zatrzymuje się w tym miejscu.

## Co zrobić
W bloku `.blocks` w sekcji `#vscode` dodaj NOWY krok jako pierwszy, a dotychczasowe kroki 1-4 przenumeruj na 2-5 (same cyfry w `.num`, treść bez zmian).

Nowy krok 1, nagłówek `<h4>Pobierz i zainstaluj VS Code</h4>`, a w treści:
- Zdanie wstępne: edytor jest darmowy, pobierasz go ze strony code.visualstudio.com (link `<a href="https://code.visualstudio.com/" target="_blank" rel="noopener">`), gdzie strona sama rozpoznaje Twój system i podpowiada właściwą wersję. Kto ma VS Code od wcześniej, zaczyna od kroku drugiego.
- Dwa krótkie akapity albo dwie pozycje w stylu strony, jeden na Maca, drugi na Windowsa:
  - Mac: pobiera się plik, który po otwarciu pokazuje ikonę programu. Przeciągasz Visual Studio Code do folderu Programy (Applications) i uruchamiasz go stamtąd.
  - Windows: wybierz wersję User Installer, bo nie wymaga uprawnień administratora. Uruchamiasz pobrany plik .exe i klikasz przez instalator. Instalator sam dopisuje edytor do systemu, więc potem komenda `code .` działa w każdym oknie terminala.
- Na końcu kroku jedno zdanie: przy pierwszym uruchomieniu VS Code proponuje pakiet z polskimi nazwami przycisków. Zostaw angielskie, jeśli chcesz, żeby nazwy zgadzały się z tym poradnikiem i z dokumentacją.

Jeśli układ dwóch systemów wygląda lepiej jako dwa okienka albo dwie karty w stylu strony, użyj komponentów, które już są w arkuszu (`.term-card` w `.terms`, albo zwykłe akapity z pogrubionym słowem Mac i Windows). Nie wymyślaj nowych klas i nie dodawaj obrazków.

## Kontrola jakości
- Kroki w `#vscode` numerowane 1-5 bez luk, treść dotychczasowych kroków nietknięta.
- `grep -n '—\|–' index.html` pusto.
- Polskie znaki obecne, link z `target="_blank" rel="noopener"`.
- HTML domknięty.
