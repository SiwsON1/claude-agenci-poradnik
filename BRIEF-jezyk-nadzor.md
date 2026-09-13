# BRIEF: poprawa języka w sekcji #nadzor + dopisanie jak to uruchomić

## Zasada nadrzędna
Teksty podane niżej wklej DOSŁOWNIE, słowo w słowo. Nie parafrazuj, nie "ulepszaj", nie dodawaj od siebie. Zmiany TYLKO w sekcji `#nadzor` pliku `/Users/marcinsiwonia/projekty/claude-agenci-poradnik/index.html`. Struktura HTML i klasy zostają, wymieniamy treść i dodajemy jeden nowy blok.

## 1. Akapit wprowadzający (linia ~558, ten od "Scenka z naszej pracy...")
Zamień cały tekst akapitu na:
"Przykład: Codex dostaje duże zadanie, na przykład przepisanie kilku podstron. Claude co 30 minut sprawdza efekty jego pracy: czy wszystko jest zgodne z wytycznymi i czy Codex się gdzieś nie zaciął. Jeśli coś poszło nie tak, Claude poprawia polecenie i Codex wraca do właściwej wersji."

## 2. NOWY blok "Jak to uruchomić?" (wstaw zaraz po akapicie z punktu 1, przed kartami WYKONAWCA/NADZORCA)
Nagłówek pomocniczy w stylu istniejących podtytułów sekcji (jak "USTAW TO U SIEBIE: 3 KROKI"): "JAK TO URUCHOMIĆ?"
Pod nim akapit (zwykły `.blk`):
"Potrzebujesz dwóch okien terminala otwartych obok siebie. W pierwszym działa Codex, w drugim Claude Code. To dwa niezależne programy, ale pracują na tym samym folderze projektu, więc Claude widzi na bieżąco wszystkie pliki, które zmienia Codex. Nie piszą do siebie na czacie: nadzór polega na tym, że Claude co pół godziny zagląda w pliki i ocenia efekt."

## 3. Karta WYKONAWCA (linia ~561)
Tytuł karty: "Dostaje /goal, czyli cel do osiągnięcia" (kod /goal zostaje w <code>).
Tekst karty zamień na:
"Pracuje bez przerwy, aż skończy całe zadanie. Po każdym etapie sam sprawdza, czy warunek końca jest już spełniony."

## 4. Karta NADZORCA (linia ~562)
Tytuł karty: "Dostaje /loop, czyli powtarzane sprawdzanie" (kod /loop w <code>).
Tekst karty zamień na:
"Co 30 minut zagląda w pliki projektu i porównuje efekt z wytycznymi. Jeśli coś się nie zgadza, poprawia polecenie dla Codexa albo daje znać Tobie."

## 5. Callout "A czemu nie na odwrót?" (linia ~564)
Tekst po pogrubieniu zamień na:
"Cel mówi, co ma być zrobione, ale nie mówi, jak często sprawdzać postępy. Pętla wyznacza rytm sprawdzania, ale sama niczego nie kończy. Dlatego wykonawca dostaje cel, a nadzorca pętlę."

## 6. Kroki "Ustaw to u siebie: 3 kroki"
- Krok 1, tytuł: "Otwórz pierwsze okno i uruchom Codexa". Opis nad terminalem (jeśli jest): "Daj mu cel z jasnym warunkiem końca:". Zawartość terminala bez zmian, tylko w linii komendy zamień końcówkę "Meta: wszystkie sekcje zgodne z makietą i bez błędów w konsoli" na "Zadanie jest skończone, gdy wszystkie sekcje są zgodne z makietą i nie ma błędów w konsoli".
- Krok 2, tytuł: "Otwórz drugie okno i uruchom Claude Code". Linia komendy w terminalu zamień na:
"/loop 30m sprawdź postępy Codexa: porównaj jego pracę z plikiem brief.md, wypisz różnice, a jeśli trzeba, popraw polecenie"
- Krok 3, tytuł: "Zajmij się swoimi sprawami". Linie terminala zamień na:
"10:30 Codex zmienił kolory niezgodnie z briefem, poprawiłem polecenie"
"11:00 wszystko zgodne z briefem, 5 z 5 sekcji gotowych. Kończę pętlę"
Zdanie pod terminalem zamień na: "Claude sam zakończy pętlę, gdy zadanie Codexa będzie skończone. Odezwie się tylko wtedy, gdy coś będzie wymagało Twojej decyzji."

## 7. Duży terminal nadzoru (linie ~600-607)
Linie zamień na:
"> /loop 30m sprawdź postępy Codexa: czy praca jest zgodna z briefem i czy nic się nie zacięło"
"10:00 Codex przepisał 2 z 5 sekcji, wszystko zgodne z briefem"
"10:30 Codex zaciął się na galerii zdjęć, poprawiłem polecenie"
"11:00 znowu idzie do przodu, 4 z 5 sekcji gotowe"

## 8. Zdanie podsumowujące (linia ~609)
Zamień na: "<strong>Jeden agent ma pętlę</strong> (Claude z <code>/loop</code>), drugi ma cel (Codex z <code>/goal</code>). Cel pilnuje efektu końcowego, pętla pilnuje regularnej kontroli."

## Kontrola
Po zmianach w sekcji #nadzor nie może zostać żadne z: "Scenka", "na kurs", "zawraca", "zawróć", "ciągnie robotę", "pilnuje rytmu", "odjechał od briefu", "Meta osiągnięta", "własnej mety". Zero em-dash i en-dash. Diakrytyki poprawne.
