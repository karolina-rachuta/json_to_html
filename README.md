![Coders-Lab-1920px-no-background](https://user-images.githubusercontent.com/30623667/104709387-2b7ac180-571f-11eb-9b94-517aa6d501c9.png)

# Kilka ważnych informacji

Przed przystąpieniem do rozwiązywania zadań przeczytaj poniższe wskazówki

## Jak zacząć?

1. Stwórz [*fork*](https://guides.github.com/activities/forking/) repozytorium z zadaniami.
2. Sklonuj fork repozytorium (stworzony w punkcie 1) na swój komputer. Użyj do tego komendy `git clone adres_repozytorium`
Adres możesz znaleźć na stronie forka repozytorium po naciśnięciu w guzik "Clone or download".
3. Rozwiąż zadania i skomituj zmiany do swojego repozytorium. Użyj do tego komend `git add nazwa_pliku`.
Jeżeli chcesz dodać wszystkie zmienione pliki użyj `git add .` 
Pamiętaj że kropka na końcu jest ważna!
Następnie skommituj zmiany komendą `git commit -m "nazwa_commita"`
4. Wypchnij zmiany do swojego repozytorium na GitHubie.  Użyj do tego komendy `git push origin main`
5. Stwórz [*pull request*](https://help.github.com/articles/creating-a-pull-request) do oryginalnego repozytorium, gdy skończysz wszystkie zadania.

Poszczególne zadania rozwiązuj w odpowiednich plikach.

### Poszczególne zadania rozwiązuj w odpowiednich plikach.

**Repozytorium z ćwiczeniami zostanie usunięte 2 tygodnie po zakończeniu kursu. Spowoduje to też usunięcie wszystkich forków, które są zrobione z tego repozytorium.**


# JSON to HTML parser - część 1

Plik `index.js` jest głównym plikiem Twojej aplikacji. Oznacza to, że aby ją uruchomić musisz wpisać w konsoli `node index.js`. Już za chwilę uruchomienie naszej aplikacji będzie odrobinę bardziej skomplikowane, ponieważ stworzymy komendy przy użyciu narzędzi jakich dostarcza nam moduł `commander` i dodamy do nich różne opcje.
Wtedy będziemy mogli używać `npm run -lt ol-list`, `npm run -lt li-list` lub `npm run table` (sprawdź w skryptach w pliku `package.json`).

Pamiętaj, że nie musisz trzymać wszystkich rozwiązań w jednym pliku. W trakcie wykonywania zadania, dostaniesz podpowiedzi gdzie mogłyby się znaleźć, niektóre funkcje czy zmienne.

## Zadanie 1

W pliku `variables.js` umieść i wyeksportuj absolutne ścieżki do plików, które będą nam potrzebne do rozwiązania zadania tj. pliki html, pliki z danymi wejściowymi i domyślny plik z danymi wyjściowymi:

- common/templates/basic_html_template.html
- list/templates/ol_basic_template.html
- list/templates/ol_template.html
- list/templates/ul_basic_template.html
- list/templates/ul_template.html
- table/templates/table_basic_template.html
- table/templates/table_template.html

- list/input/list_basic.json
- list/input/list.json
- table/input/table_basic.json
- table/input/table.json

- output/result.html

Zaimportuj je w pliku `index.js` i sprawdź czy mają poprawne wartości.

## Zadanie 2:

W pliku `utils.js` zaimplementuj i wyeksportuj trzy funkcje:

- `getHTMLTemplate(fileName)` - która odczyta podany w parametrze plik (wartością domyślną powinien być plik w lokalizacji `common/templates/basic_html_template.html`, a dokładnie nasza wyeksportowana wcześniej zmienna) i zwróci jego zawartość (**async/await i obsługa błędów!**)
- `fillTemplateWithData(template, title, body)`- kiedy zajrzysz do pliku w lokalizacji `common/templates/basic_html_template.html` zobaczysz dwa bardzo charakterystyczne ciągi znaków. tj `__title__` oraz `__body__`. Są to miejsca, w które wstawimy nasze dane. Oznacza to, że zmienna `template`, to nic innego jak zwrócony w funkcji `getHTMLTemplate` string zawierający nasze placeholdery tj `__title__` oraz `__body__`. Używając metod ze `String.prototype` zamień `__title__` na to co zostało przekazane w zmiennej `title`, a `__body__` na to co zostało przekazane w zmiennej `body`. Zwróć wygenerowany w ten sposób string.
- `saveOutputHTML(dataToSave, fileName)` - która zapisze do podanego w drugim parametrze pliku (wartością domyślną powinien być plik w lokalizacji `output/result.html`, a dokładnie nasza wyeksportowana wcześniej zmienna) dane z pierwszego parametru.

Zaimportuj te funkcje do pliku `index.js` i przetestuj ich działanie, w taki sposób, aby do wygenerowanego pliku trafił taki kod HTML:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>My first generated HTML</title>
  </head>
  <body>
    It's quite fun!
  </body>
</html>
```

Brawo! Udało Ci się właśnie wygenerować pierwszy HTML z podstawionymi danymi. Na tym właśnie będzie polegało parsowanie danych z pliku JSON do pliku HTML. Zacznijmy od list.

## Zadanie 3

W pliku `utils.js` stwórzmy jeszcze jedną funkcję `getInputData(fileName)` (wartością domyślną powinien być plik w lokalizacji `list/input/list_basic.json`, a dokładnie nasza wyeksportowana wcześniej zmienna), która pobiera dane z pliku `json`, parsuje je za pomocą metody `JSON.parse`, a na końcu zwraca.

Otwórz teraz plik `list_basic.json`. Jak się pewnie domyślasz jest to plik z danymi, które pomogą nam zasilić listę i uzupełnić nią nasz HTML.

## Zadanie 4

W pliku `list-utils.js` w katalogu list stworzymy teraz dwie funkcje:

- `getListTemplate(fileName)`, która zwróci nam zawartość podanego w parametrze pliku (wartością domyślną powinien być plik w lokalizacji `list/templates/ul_basic_template.html`, a dokładnie nasza wyeksportowana wcześniej zmienna)
- `fillListTemplateWithDataBasic(template, objectToFillData)`, która zwróci nam uzupełniony pobranymi w poprzednim ćwiczeniu danymi template. Dane jakimi zasilimy naszą funkcję będą w następującym formacie:

```json
[
  {
    "id": 1,
    "data": "Red Dead Redemption II"
  }
]
```

Będzie to tablica z obiektami o atrybutach `id` i `data`, możemy więc po niej iterować.

Zwróć uwagę jak wygląda template listy, którego będziemy używać:

```html
<ul>
  <li>__data1__</li>
  <li>__data2__</li>
  <li>__data3__</li>
  <li>__data4__</li>
  <li>__data5__</li>
</ul>
```

Jak już się pewnie domyślasz, ciągi znaków od `__data1__` do `__data5__` to miejsca, które wypełnimy danymi z tablicy obiektów. Póki co nie musisz się martwić, miejsc jest pięć i naszych obiektów też. Dobrze byłoby natomiast gdyby `id` obiektu zgadzało się z numerem w placeholderze.

## Zadanie 5

Stwórzmy nową funkcję `basicListPath` w pliku `paths.js` w katalogu `paths` i wykorzystajmy wszystkie stworzone przez nas wcześniej funkcje do implementacji programu w którym:

1. Odczytasz dane wejściowe z pliku `list\input\list_basic.json`.
2. Odczytasz template listy i uzupełnij ją wcześniej pobranymi danymi wejściowymi z kroku pierwszego.
3. Odczytasz podstawowy template html, uzupełnisz go w `__title__` wpisując "My favorite games", a w `__body__` podasz uzupełnioną w kroku drugim listę.
4. Zapiszesz plik html do `result.html`. Pamiętaj o konstrukcji `async/await` i obsłudze błędów.

Udało nam się właśnie wygenerować poprawny HTML z uzupełnioną o nasze ulubione gry listą.

## Zadanie 6

Zostało nam jeszcze kilka rzeczy do zrobienia. Po pierwsze dobrze by było gdyby cała nasz program umieszczony została w komendzie (użyj do tego modułu `commander`) i wywoływana była w następujący sposób: `node index.js list`.

## Zadanie 7

Zwróć uwagę, że w katalogu `list/templates` są pliki zarówno dla listy uporządkowanej jak i nieuporządkowanej. W akcji komendy dodajmy opcję `type`, która pozwoli użytkownikowi zdefiniować, którą listę chce wygenerować, Jeśli użytkownik poda opcję inną niż `ul/ol` wykorzystaj wartość domyślną tj `ul`. W funkcji `basicListPath` przekaż parametr ze ścieżką do pliku template listy.

Dodaj też opcję `title` do uruchamiania naszego programu. Opcja ta będzie przyjmować tytuł Twojego pliku html (zastąp nim placeholder `__title__`).

## Zadanie 8 - dla chętnych

W katalogu templates znajdują się także pliki bez słowa basic w nazwie. Zajrzyjmy do jednego z nich:

```html
<ul>
  __list__
</ul>
```

Teraz zamiast pojedynczych elementów listy, będziemy zastępować placeholder `__list__`. Oznacza to że strukturę:

```json
[
  {
    "id": 1,
    "data": "A"
  },
  {
    "id": 2,
    "data": "B"
  }
]
```

musimy zamienić na `<li>A</li>\r\n<li>B</li>\r\n` dla systemu Windows lub `<li>A</li>\r\n<li>B</li>\n` dla systemów Linux oraz macOS. Dzięki użyciu `\r\n` lub `\n` pomiędzy elementami zapewniamy przeniesienie każdego elementu listy do nowej linii, co trochę ułatwi nam czytanie wygenerowanego przez nas pliku HTML.

Jeśli chcemy zapewnić generyczne, działające na każdej platformie rozwiązanie wystarczy użyć `const nl = (process.platform === 'win32' ? '\r\n' : '\n')` i wstawić w następujący sposób `<li>A</li>\r\n<li>B</li>${nl}`.

W pliku `list-utils.js` stwórz nową funkcję `fillListTemplateWithData` przy pomocy, której uzupełnisz template listy odpowiednimi danymi.

W pliku `paths.js` stwórz nową funkcję `listPath`. Wykorzystaj w niej nowy sposób generowania danych (stworzona `fillListTemplateWithData`) oraz plik wejściowy `list.json`. Zmodyfikuj plik z danymi wejściowymi i zobacz czy wszystko działa.


# JSON to HTML parser - częśc 2

Krok po kroku udało nam się stworzyć prosty parser, który pobiera dane z pliku i wypełnia nimi listę w HTML. Kolejną strukturą danych, którą możemy wygenerować jest tablica. Spróbujmy więc rozszerzyć nasz parser o komendę `table`, parsującą dane na na tabelę.

# Zadanie 1

Postępując analogicznie jak w przypadku listy stwórz parser, który pozwoli na przekształcenie odpowiedniej struktury danych na tabelę.

1. Używając modułu `commander` stwórz komendę `table` z opcją `title`, która uruchomi odpowiednią akcję i wygeneruje tabelę z danymi w pliku HTML z odpowiednim tytułem.
2. W pliku `table-utils.js` stwórz dwie funkcje, jedną, która odczytuje template z pliku, a drugą, która podmienia placeholdery na odpowiednie dane. Możesz zacząć od kroku pośredniego i na początek wykorzystać `table/template/table_basic_template.html` oraz dane z pliku `table/input/table_basic.json`).
3. W pliku `path.js` stwórz funkcję `basicTablePath` i wygeneruj poprawny, uzupełniony danymi HTML.
4. Dopisz odpowiednie funkcje, które pozwalają na parsowanie `table/template/table_template.html` z dowolną strukturą danych wejściowych (np. dane z pliku `table/input/table.json`).
5. Pamiętaj o podmianie odpowiednich ścieżek!
6. Wykorzystaj metody z pliku `utils.js`, a także stwórz analogiczne funkcje do tych z `list-utils.js` w pliku `table-utils.js`.
7. Stwórz odpowiednie funkcje w pliku `path.js` podobne do tych jakie stworzyliśmy w przypadku parsera listy.


# JSON to HTML parser - część 3

# Zadanie 1.

W pliku `watch.js` napisz prosty watcher (`fs.watchFile(...)`), który będzie obserwował zmiany w folderze output tj. tym, w którym generujemy nasze pliki html. Żeby niczego nie nadpisać, po każdej zmianie, niech plik `result.html` będzie kopiowany do tymczasowo stworzonego folderu, z nową, losowo wygenerowaną nazwą. Przed zakończeniem procesu i wyjściem z aplikacji za pomocą Ctrl + C (`proces.on('SIGINT',...)`) usuń tymczasowy folder i zawarte w nim pliki.

Rozwiąż to zadanie korzystając z eventów!

Plik uruchomisz za pomocą `node watch.js`.
