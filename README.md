# Dokumentacja projektu **SŁÓWKA**

## Spis treści

  - [Autor](#autor)
  - [Geneza powstania](#geneza-powstania)
  - [Wprowadzenie](#wprowadzenie)
  - [Struktura projektu](#struktura-projektu)
  - [Lokalizacja oraz wykorzystane technologie](#lokalizacja-oraz-wykorzystane-technologie)
  - [Elementy HTML/PHP](#elementy-htmlphp)
    - [Plik `index.html`](#plik-indexhtml)
    - [Plik `log.php`](#plik-logphp)
    - [Plik `reg.php`](#plik-regphp)
    - [Plik `lobby.php`](#plik-lobbyphp)
    - [Plik `game.php`](#plik-gamephp)
    - [Plik `scoreboard.php`](#plik-scoreboardphp)
    - [Plik `updateStats.php`](#plik-updatestatsphp)
  - [Elementy JavaScript](#elementy-javascript)
    - [Plik `game.js`](#plik-gamejs)
    - [Plik `popup.js`](#plik-popupjs)
  - [Konstrukcja CSS](#konstrukcja-css)
  - [Zawartość folderu `media`](#zawartość-folderu-media)
  - [Konstrukcja bazy danych](#konstrukcja-bazy-danych)


## Autor

Tomasz Papierowski, IV sem. Inf, spec. Aplikacje Internetowe i Mobilne

## Geneza powstania

Projekt realizujący zaliczenie przedmiotu "Języki znacznników i skryptowe" 2-go roku Informatyki Uniwersytetu Morskiego w Gdyni na wydziałe Elektrycznym

## Wprowadzenie

**SŁÓWKA** to prosta gra logiczna polegająca na odgadnięciu nieznanego, 5-literowego słowa. Odgadywanie odbywa się poprzez wpisywanie różnych słów do tabelki. Pierwsze wpisane słowo zawsze musi być losowe, od następnego wprowadzonego słowa gra może ukazać podpowiedzi. Jeżeli dowolna litera słowa wpisanego na pozycji *n* jest taka sama jak litera słowa szukanego na tej samej pozycji, to zostaje ona zaznaczona kolorem zielonym. Jeżeli dowolna litera słowa wpisanego występuje w słowie szukanym, ale na innej pozycji niż została wpisana, to zostaje ona zaznaczona kolorem żółtym. Jeżeli dowolna litera nie występuje w szukanym słowie, to zostaje ona zaznaczona kolorem szarym. Użytkownik posiada 6 prób odgadnięcia słowa. Gra kończy się w momencie, kiedy poszukiwany wyraz zostanie poprawnie wprowadzony lub kiedy skończy się ilość prób. Po poprawny odgadnięciu słowa gracz otrzymuje punkt, który wpływa na pozycjonowanie na globalnej tablicy wyników. Przed rozpoczęciem gry wymagana jest rejestracja, która umożliwia przchowywanie wyników poszczególnych graczy oraz organizację tabeli wyników.

## Struktura projektu

```
projekt/
├── css/
│   ├── gameStyle.css
│   ├── indexStyle.css
│   ├── lobbyStyle.css
│   ├── logStyle.css
│   ├── regStyle.css
│   └── scoreboardStyle.css
├── media/
│   ├── bg.png
│   └── favicon.ico
├── script/
│   ├── game.js
│   └── popup.js
├── game.php
├── index.html
├── lobby.php
├── log.php
├── README.md
├── reg.php
├── scoreboard.php
└── updateStats.php
```

## Lokalizacja oraz wykorzystane technologie

Projekt umieszczony jest na stronie hostingowej *webd.pl* pod domeną *graslow2.webd.pro*. Struktura projektu na hostingu jest taka sama jak w/w *Struktura programu*. Do projektu zostały wykorzystane następujące technologie:
- HTML - interfejs / konstrukcja strony po stronie użytkownika
- CSS - konfiguracja części wizualnej
- JS - konfiguracja części logicznej
- PHP - komunikacja z bazą danych

## Elementy HTML/PHP

### Plik `index.html`

Plik służy za stronę powitalną projektu. Na środku znajduje się animowany napis ***SŁÓWKA***. Pod napisem widoczne są dwa przyciski, czyli ***LOGOWANIE*** oraz ***REJESTRACJA***.

Znacznik `<h1 id="mainTitle">` przechowuje sześć znaczników `<span id="letterSpanX"></span>`, które odpowiadają za wyświetlenie animowanego napisu strony.

Znacznik `<div class="button-container">` przechowuje dwa przyciski, które służą do przemieszczenia się do logowania/rejestracji.

### Plik `log.php`

Plik służy do obsługi logowania na stronę. Na środku znajduje się animowany napis ***LOGOWANIE***. Pod napisem widnieje przestrzeń służąca do wprowadzenia danych użytkownika oraz przycisk realizujący zapytanie do bazy SQL.

Znacznik `<h1 id="mainTitle">` przechowuje dziewięć znaczników `<span id="letterSpanX"></span>`, które odpowiadają za wyświetlenie animowanego napisu strony.

Znacznik `<form method="POST">` przechowuje cały formularz logowania włącznie z przyciskiem wysyłającym zapytanie w celu weryfikacji, czy użytkownik widnieje w bazie SQL.

Znacznik `<p id='errorDrop'><?php echo $errorMessage; ?></p>` służy jako kontener do wyświetlania błędów przy próbie zalogowania.

Znaczniki `<h2 id="moveToReg"> Nie masz jeszcze konta? </h2>` oraz `<a href="reg.php" id="moveToRegBtn">Rejestracja</a>` odpowiadają za przekierowanie użytkownika do panelu rejestracji.

Umieszczony na początku pliku kod PHP jest aktywowany po naciśnięciu przycisku logowania. Pobierane są dane wpisane przez użytkownika. Nastepnie następuje połączenie z bazą w celu sprawdzenia, czy występuje w niej użytkownik oraz czy podane przez niego hasło jest prawidłowe. Jeżeli wszystko się zgadza, użytkownik przenoszony jest do pliku `lobby.php` oraz tworzona jest sesja logowania. Jeżeli nie - program przekazuje stosowny komunikat.

### Plik `reg.php`

Plik służy do obsługi rejestracji na stronie. Na środku znajduje się animowany napis ***REJESTRACJA***. Pod napisem widnieje przestrzeń służąca do wprowadzenia danych użytkownika oraz przycisk realizujący zapytanie do bazy SQL.

Znacznik `<h1 id="mainTitle">` przechowuje jedenaście znaczników `<span id="letterSpanX"></span>`, które odpowiadają za wyświetlenie animowanego napisu strony.

Znacznik `<form method="POST">` przechowuje cały formularz rejestracji włącznie z przyciskiem wysyłającym zapytanie w celu weryfikacji, czy użytkownik może zostać utworzony.

Znacznik `<p id='errorDrop'><?php echo $errorMessage; ?></p>` służy jako kontener do wyświetlania błędów przy próbie rejestracji.

Znacznik `<p id='accountCreate'><?php echo $successMessage; ?></p>` służy jako kontener do wyświetlenia informacji o powodzeniu tworzenia konta.

Znaczniki `<h2 id="moveToLog"> Masz już konto? </h2>` oraz `<a href="log.php" id="moveToLogBtn">Logowanie</a>` odpowiadają za przekierowanie użytkownika do panelu logowania.

Umieszczony na początku pliku kod PHP jest aktywowany po naciśnięciu przycisku rejestracji. Pobierane są dane wpisane przez użytkownika. Hasło wpisane przez użytkownika sprawdzane jest pod względem kryteriów silnego hasła oraz poprawności powtórnego wpisana hasła. Nastepnie następuje połączenie z bazą w celu sprawdzenia, czy przypadkiem nie występuje w niej użytkownik o podanym loginie. Jeżeli wszystko się zgadza, użytkownik jest tworzony wraz z zapisem do bazy danych. Jeżeli nie - program przekazuje stosowny komunikat

### Plik `lobby.php`

Plik służy jako całościowe lobby projektu. W głównej części widoczny jest komunikat witający użytkownika oraz dwa przyciski - *Rozegraj grę* oraz *Tabela wyników*, które przenoszą w stosowne miejsce. W górnej części ekranu widoczny jest animowany napis ***SŁÓWKA***. W dolnej części ekranu występują dwa przyciski - *Wyloguj* oraz *Jak grać?*.

Znacznik `<h1 id="mainTitle">` przechowuje sześć znaczników `<span id="letterSpanX">S</span>`, które odpowiadają za wyświetlenie animowanego napisu strony.

Znacznik `<div id="welcome">` służy do przywitania gracza. Pobiera zawarty w sesji login, który wykorzystuje do wystosowania wiadomości *Witaj, x!*.

Znacznik `<div class="button-container">` przechowuje dwa przyciski, które służą do przemieszczenia się do gry/tablicy wyników.

Znacznik `<form method="POST">` przechowuje dwa przyciski, które służą do wylogowania oraz podpowiedzi jak grać. Po naciśnięciu przycisku *Wyloguj* przerywana jest sesja logowana, a gracz zostaje cofnięty do pliku `index.html`. Po naciśnięciu przycisku *Jak grać* wyświetla się *pop-up* z podpowiedzia jak wygląda rozgrywka.

Znacznik `<div id="popup">` przechowuje całą strukturę *pop-up* informującą jak grać.

### Plik `game.php`

Plik jest główną częścią całego projektu. W głównej części widoczna jest szachownica w którą gracz wpisuje swoje próby. Po wpisaniu słowa i zatwierdzeniu go za pomocą *Enter* program odpowiednio zakolorowuje konkretne litery. W górnej części ekranu widoczny jest animowany napis ***SŁÓWKA***. W dolnej części ekranu występują dwa przyciski - *Powrót do lobby* oraz *Jak grać?*.

Znacznik `<h1 id="mainTitle">` przechowuje sześć znaczników `<span id="letterSpanX">S</span>`, które odpowiadają za wyświetlenie animowanego napisu strony.

Znacznik `<div id="game-board"></div>` służy jako kontener przechowywujący całą planszę gry. Bazowo plansza przystosowana jest pod rozmiar 5x6, jednak jej wymiar jest możliwy do zmiany w pliku `game.js`.

Znacznik `<p id="message"></p>` służy do przekazywania komunikatów o grze.

Znacznik `<script>` umieszczony pod planszą jest znacznikiem pomocniczym, który przekazuje niezbędne parametry do pliku `game.js`.

Znacznik `<form method="POST">` przechowuje dwa przyciski, które służą do powrotu do lobby oraz podpowiedzi jak grać. Po naciśnięciu przycisku *Powrót do lobby* gra zostaje przerwana, a gracz zostaje cofnięty do pliku `lobby.php`. Po naciśnięciu przycisku *Jak grać* wyświetla się *pop-up* z podpowiedzia jak wygląda rozgrywka.

Znacznik `<div id="popup">` przechowuje całą strukturę *pop-up* informującą jak grać.

### Plik `scoreboard.php`

Plik służy do wyświetlenia tablicy wyników graczy. W głównej cześci widoczna jest tabelka wraz z możlwiością jej modyfikowania, który przedstawia obecne pozycjonowanie graczy na podstawie rekordów umieszczonych w bazie danych. Tabelę można dostosować pod ilość wyświetlanych rekordów (od 1 do 10) oraz pod jedno z trzech dostępnych kryteriów - *Wygrane gry*, *Rozegrane gry*, *% wygranych*. W górnej części ekranu widoczny jest animowany napis ***SŁÓWKA***. W dolnej części ekranu występują dwa przyciski - *Powrót do lobby* oraz *Jak grać?*.

Znacznik `<h1 id="mainTitle">` przechowuje sześć znaczników `<span id="letterSpanX">S</span>`, które odpowiadają za wyświetlenie animowanego napisu strony.

Znacznik `<form method="POST" class="limit-form">` służy do dostosowania tabelki pod własne wymagania. Możliwa jest zmiana ilości wyświetlanych rekordów oraz sposób sortowania.

Znacznik `<table>` zawiera całą strukturę wyświetlanej tabeli.

Znacznik `<form method="POST">` przechowuje dwa przyciski, które służą do powrotu do lobby oraz podpowiedzi jak grać. Po naciśnięciu przycisku *Powrót do lobby* gra zostaje przerwana, a gracz zostaje cofnięty do pliku `lobby.php`. Po naciśnięciu przycisku *Jak grać* wyświetla się *pop-up* z podpowiedzia jak wygląda rozgrywka.

Znacznik `<div id="popup">` przechowuje całą strukturę *pop-up* informującą jak grać.

### Plik `updateStats.php`

Plik służy do aktualizacji statusu użytkownika po zakończonej grze. Jeżeli użytkownik wygra rozgrywkę, rekord `gamesWon` oraz `gamesPlayed` zostaje zwiększony o jeden. Jeżeli użytkownik przegra rozgrywkę, tylko rekord `gamesPlayed` zostaje zwiększony.

## Elementy JavaScript

### Plik `game.js`

Plik odpowiada za całościową obsługę rozgrywki umieszczonej w pliku `game.php`.

Zmienna `const WORD_LENGTH = 5;` określa długość słów, które będą wprowadzane przez użytkownika. Jej zmiana spowoduje wydłużenie/skrócenie planszy w lini poziomej. Przy obecnym założeniu bazy danych zmiana ta może uniemożliwić rozgrywkę, jednak zmieniając wartość zmiennej na *n* oraz dodając do bazy słowa o długości *n* możliwa jest bezproblemowa rozgrywka.

Zmienna `const MAX_GUESSES = 6;` określa ilość prób, które posiada użytkownik na odgadnięcie hasła. Jej zmiana jest możliwa niezależnie, nie powoduje utworzenia problemów związanych z rozgrywką.

Pętla `for (let r = 0; r < MAX_GUESSES; r++)` odpowada za tworzenie całej planszy rozgrywki. Plansza tworzona jest na podstawie wartości zmiennnych `WORD_LENGTH` oraz `MAX_GUESSES`.

Funkcja `function handleKey(e)` odpowaiad za obsługę zdarzenia jakim jest naciśnięcie przycisku przez użytkownika. Jeżeli zostanie nacisnięty przycisk *Backspace*, to cofnięta zostanie ostatnio wprowadzona litera. Jeżeli zostanie naciśnięty przycisk *Enter*, to zostanie sprawdzona poprawność słowa. Warunek `if (/^[a-zA-ZĄĆĘŁŃÓŚŹŻąćęłńóśźż]$/.test(e.key) && currentGuess.length < WORD_LENGTH)` obsługuję wprowadzanie liter do tabelki.

Funkcja `function updateBoard()` odpowiada za aktualizowanie widoku planszy gry w oparciu o aktualne próby gracza. Pętla `for (let i = 0; i < WORD_LENGTH; i++)` odpowiada za przeanalizowanie każdej z litery w danym wierszu, ustawieniu tekstu w każdej komórce oraz jego zamianie na wielką literę.

Funkcja `function showError(text)` służy do wyświetlania komunikatu w momencie, kiedy użytkownik wprowadzi za krótkie słowa. Parametr `setTimeout(() => message.classList.remove("visible"), 2000);` ogranicza czas wyświetlania błędu.

Funkcja `function showMessage(text)` służy do wyświetlania informacji o wygranej lub przegraniej przez użytkownika.

Funkcja `function checkGuess()` sprawdza, czy podane przez użytkownika słowo jest takie same jak słowo poszukiwane. Pierwsza umieszczona pętla `for (let i = 0; i < WORD_LENGTH; i++)` służy do zakolorowania komórki na zielono w momencie, kiedy litera słowa szukanego na pozycji *n* jest taka sama jak litera słowa wpisanego na pozycji *n*. Druga pętla służy do zakolorowania komórki na żółto w momencie, kiedy litera słowa szukanego jest taka sama jak litera słowa wpisanego, ale jej pozycja jest inna. Trzecia pętla zakolorowuje komrkę na szarno w momencie, kiedy litera wpisana nie występuje w słowie szukanym. Warunek `if (guess === TARGET_WORD)` sprawdza, czy słowo szukane jest takie same jak słowo wpisane. Jeżeli tak, gracz wygrywa. Warunek `if (currentRow >= MAX_GUESSES)` sprawdza, czy użytkownikowi nie skończyły się próby. Jeżeli tak, gracz przegrywa. Funkcja `function sendGameResult(win)` służy do przesłania informacji o wygranej/przegranej gracza.

## Plik `popup.js`

Plik służy jak obsługa okienka pop-up wykorzystywanego do informowania gracza jak wygląda rozgrywka.

Zmienna `const popup` pobiera element z plików .php zawierający konstrukcję pop-upa.

Zmienna `const openBtn` pobiera element jakim jest przycisk otwierania pop-upa.

Zmienna `const closeBtn` pobiera element jakim jest przycisk zamknięcia pop-upa.

Warunek `if (openBtn && popup && closeBtn)` sprawdza, czy wszystkie elementy istnieją. 

Wydarzenie `openBtn.addEventListener("click", (e) =>` odpowiada za obsługę przycisku otwierającego.

Wydarzenie `closeBtn.addEventListener("click", () =>` odpowiada za obsługę przycisku zamykającego.

## Konstrukcja CSS

Arkusz stylów dla każdego z pliku jest zbliżony, co utrzymuje cały projekt w jednej kompozycji.
 
Głównym elementem powtarzającym się na każdej stronie jest animowany napis o treści *Słówka*, *Logowanie* lub *Rejestracja*. Sposób wykonania animacji jest identyczny, polega na rozróżnieniu każdej z liter słowa z osobna. Po najechaniu na dowolną literę dochodzi do wykonania `transition`, który odpowiada za delikatną zmianę położenia w pozycji pionowej oraz nadanie odpowiedniego koloru. Wyjątkiem zawsze jest druga litera słowa, która kieruje się odwrotnie niż pozostałe litery

Dla plików `lobby.php`, `game.php` oraz `scoreboar.php` dodatkowow została zaimplementowana animacja ciągłego przeskakiwania liter oraz ich zmian kolorów. Utworzone jest to za pomocą wykorzystania `@keyframes bounceColorX`, który odpowiada za zmianę położenia oraz koloru.

Stylistyka obramowań opiera się na zastosowania gradientu przechodzącego z koloru niebieskiego do koloru różowego. Z racji na brak natwynego wsparcia ustawienia gradientu jako kolor obramowania, zostało zastosowane `border-image`. 

Wszystkie przyciski funckyjne również otrzymały podświetlenie/obramowanie związane z w/w gradientem w celu zachowania spójności kompozycji 

Dla plików `lobby.php`, `game.php` oraz `scoreboar.php` dodatkowow został zaimplemetowany pop-up informujący o sposóby gry. Po naciśnięciu stosownego przycisku wyskakuje okienko z prawej strony z pełną instrukcją rozgrywki.

## Zawartość folderu `media`

Folder przechowuje dodatkowe elementy wykorzystywane na stronie. Znajduje się w nim plik `bg.png`, który jest wykorzystywany jako tło dla każdego z plików. Dodatkowo znajduje się w nim plik `favicon.ico`, który jest wyświetlany jako ikona strony na pasku w przeglądarce

## Konstrukcja bazy danych

Baza opiera się o *phpMyAdmin* dostępnym na hostingu *webd.pl*. W bazie zawarte są dwie tabele:
- `users` - tabela przechowująca informacjo o użytkownikach:
  - **id**, int, AI - identyfikator użytkownika
  - **login**, varchar(50) - login użytkownika
  - **password**, char(60) - zahashowane hasło użytkownika
  - **gamesPlayed**, int - ilość rozegranych gier przez użytkownika
  - **gamesWon**, int - ilość wygranych gier przez użytkownika
- `words` - tebale przechowująca listę możliwych słów w grze:
  - **id**, int, AI - identyfikator słowa
  - **word**, varchar(5) - słowo
