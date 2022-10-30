---
title: Przegląd API Tritium++
description: Przegląd
published: true
date: 2022-10-30T22:58:33.259Z
tags: 
editor: markdown
dateCreated: 2022-10-24T22:00:16.489Z
---

# ⚙ Przegląd Tritium++

## Omówienie interfejsu API Nexusa

Nexus udostępnia kilka interfejsów API, które umożliwiają użytkownikom i programistom łatwą interakcję z funkcjami stosu oprogramowania Nexus. Każdy interfejs API jest logicznie pogrupowanym zbiorem metod, które oddziałują z określoną częścią stosu (np. księgą, rejestrami), według obszaru funkcjonalnego (konta, aktywa, tokeny) lub według konkretnego przypadku użycia w branży (zaopatrzenie, muzyka).

### `Protokół`

Serwer API używa protokołu `HTTP` i obsługuje zarówno metody żądania **`GET`**, jak i **`POST`**.

API używa **`JSON`** (JavaScript Object Notation) jako podstawowego mechanizmu transportu danych zarówno dla danych wejściowych, jak i wyjściowych. Jednak serwer API obsługuje również żądania zakodowane w adresie URL (**`application/x-www-form-urlencoded`**).

### `Port`

Domyślnie serwer API działa na porcie 8080. Można to zmienić, ustawiając `apiport=xxxx` w nexus.conf lub uruchamiając demona z parametrem `-apiport=xxxx`.

### `Bezpieczeństwo`

Interfejs API Nexusa korzysta ze schematu uwierzytelniania `HTTP Basic`. Wymaga to od wywołującego ustawienia nagłówka HTTP `Authorization` z wartością `Basic <credentials>` z częścią `<credendtials>`ustawioną na `apiuser:apipassword` i zakodowane `base64`. Po stronie serwera API uwierzytelnianie jest konfigurowane poprzez dodanie `apiuser=<nazwa użytkownika>` i `apipassword=<hasło>` do nexus.conf.\
**UWAGA**: Jeśli chcesz całkowicie wyłączyć uwierzytelnianie, możesz to zrobić, ustawiając `apiauth=0` w pliku nexus.conf

Uzupełnieniem mechanizmu uwierzytelniania jest implementacja szyfrowania `SSL` (`HTTPS`). Domyślnie serwer API jest uruchamiany z wyłączonym SSL. Aby go włączyć, dodaj `apissl=1` do swojego nexus.conf

### `Sesje wieloużytkownikowe`

Interfejs API Nexusa można skonfigurować tak, aby działał w trybie wielu użytkowników, co pozwala na jednoczesne logowanie wielu łańcuchów sygnatur i jednoczesne korzystanie z interfejsu API. Tę funkcję można włączyć, ustawiając `multiuser=1` w nexus.conf (domyślnie wyłączone). Gdy włączony jest tryb wielu użytkowników, początkowa odpowiedź logowania będzie zawierać wartość identyfikatora sesji. Ten identyfikator sesji musi być następnie uwzględniony we wszystkich kolejnych wywołaniach interfejsu API do punktów końcowych, które wymagają zalogowania się użytkownika.

### `Punkt końcowy`

Każdy punkt końcowy interfejsu API można wywołać za pomocą następującej semantyki:

**`<api>/<verb>/<noun>`**

e.g.

```
http://127.0.0.1:8080/ledger/get/block
```

**UWAGA**: URI są zawsze pisane małymi literami.

### `Obsługa błędów`

W przypadku, gdy wywołanie API zakończy się błędem, obiekt JSON zostanie zwrócony w następującym formacie:

```
{
    "error" :
    {
        "code" : -123,
        "message" : "An error has occurred"
    }
}
```

## Kody błędów DSL

| Kod | Wiadomość                                                                     |
| ---- | ---------------------------------------------------------------------------- |
| 1    | Błąd składni zapytania: zduplikowane symbole wieloznaczne niedozwolone   |
| 2    | Błąd składni zapytania: dla typu \[typename] dozwolone są tylko operatory '=' i '!=' |
| 3    | Błąd składni zapytania: zniekształcona klauzula where w \[clause] |
| 4    | Błąd składni zapytania: należy użyć = bez dodatkowych znaków |
| 5    | Błąd składni zapytania: należy użyć '(and)' do mieszania instrukcji AND/OR |
| 6    | Błąd składni zapytania: brak operatora logicznego dla grupy |
| 7    | Błąd składni zapytania: pusta klauzula where w \[clause] |
| 8    |
| 9    |

## Kody błędów API

| Kod | Wiadomość |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| -1 | Metoda niedostępna: \[message] |
| -2 | Nie znaleziono metody: \[message] |
| -3 | Metoda została przestarzała w wersji \[version]: \[message] |
| -4 | Nie znaleziono API (nazwa API) |
| -5 | Obiekt niedostępny: \[message] |
| -6 | content-type \[content type] nie jest obsługiwany |
| -7 | Nieobsługiwany typ \[typ] dla parametrów. |
| -8 | Nie można wyodrębnić adresu wejściowego |
| -9 | Sesja (session) nie istnieje |
| -10 | Nieprawidłowy identyfikator ID sesji |
| -11 | Użytkownik niezalogowany |
| -12 | Błędne lub brakujące kodowanie obiektów dla \[type] |
| -13 | Nie znaleziono obiektu |
| -14 | Nieprawidłowy adres URL żądania |
| -15 | Obiekt nie jest kontem ani tokenem |
| -16 | Konto nie zostało odblokowane dla transakcji |
| -17 | Nie udało się utworzyć transakcji |
| -18 | Nieprawidłowy format dla standardowego \[name] |
| -19 | Pole \[name] nie istnieje w obiekcie |
| -20 | Pole \[name] jest tylko do odczytu i nie może być aktualizowane |
| -21 | Rozmiar pola \[name] przekracza maksymalną długość \[size] |
| -22 | Pole \[name] to zarezerwowana nazwa pola |
| -23 | Standard obiektu \[name] niedostępny dla polecenia |
| -24 | Nie znaleziono zleceń dla rynku |
| -25 | Nieważna umowa zlecenia rynkowego: message |
| -26 | Nieprawidłowy parametr \[from], \[type] wymaga poprawnego tokena |
| -27 | Nieprawidłowe kodowanie base64 |
| -28 | Brakujący parametr \[name] w poleceniu |
| -29 | Określono nieobsługiwany format \[type] |
| -30 | Operacje nie zostały wykonane |
| -31 | Księga nie może podpisać transakcji |
| -32 | Nie udało się zaakceptować |
| -33 | Nieprawidłowa lub brakująca nazwa/adres |
| -34 | Nie znaleziono aktywa |
| -35 | Nieprawidłowy parametr \[key=type], oczekiwano \[type] |
| -36 | Nieobsługiwany typ \[name] dla polecenia |
| -37 | Brak nazwy/adresu tokena |
| -38 | Brak nazwy/adresu aktywa |
| -39 | Brak name\_from / address\_from |
| -40 | Nie znaleziono poprzedniej transakcji |
| -41 | Nieprawidłowy identyfikator transakcji |
| -42 | Brak ważnych debetów do kupienia od |
| -43 | Brak ważnych umów w tx |
| -44 | Transakcja nie powiodła się |
| -45 | Brak name\_to / address\_to |
| -46 | Brakująca kwota |
| -47 | Brak ceny |
| -48 | Nie znaleziono tokena |
| -49 | Nieobsługiwany typ nazwy/adresu |
| -50 | Brak txid |
| -51 | Brak dostępnych kont tokenowych dla odbiorcy |
| -52 | Nie ma więcej dostępnych kont do debetu |
| -53 | Brak name / address rachunku do zasilenia |
| -54 | Brak name\_proof / address\_proof do zasilenia |
| -55 | Musi mieć co najmniej dwóch odbiorców, aby obciążyć dowolny |
| -56 | Nieprawidłowe user-type enum \[value]  |
| -57 | Nieprawidłowy parametr \[name] |
| -58 | Pusty parametr \[name] |
| -59 | Konto do zasilenia nie jest kontem NXS |
| -60 | \[name] poza zakresem \[max] |
| -61 | Konto dowodowe jest przeznaczone dla innego tokena niż token aktywów |
| -62 | Transakcja Coinbase wydobyta przez innego użytkownika |
| -63 | Nie można pobrać domyślnego konta NXS do zasilenia |
| -64 | Brak konta odbiorcy name\_to / address\_to |
| -65 | Obiekt nie jest kontem |
| -66 | Nie można używać zagregowanych nazw pól z operacjami |
| -67 | -safemode następna niezgodność hash, transmisja zakończona |
| -68 | Zbyt mała kwota |
| -69 | Niewystarczające środki |
| -70 | Nie znaleziono konta trust |
| -71 | Nazwa pola \[name] nie istnieje |
| -72 | Rejestr nie jest kontem trust |
| -73 | Konto trust nie jest kontem NXS |
| -74 | Nie znaleziono rejestrów |
| -75 | Wartość \[key=value] przekracza rozmiar zbioru danych \[size] |
| -76 | Nie można ustawić stawki dla konta trust do czasu transakcji Genesis |
| -77 | Niewystarczające saldo konta trust, aby dodać do stakowania |
| -78 | Stawka niezmieniona |
| -79 | getblockhash wymaga uruchomienia demona z flagą -indexheight |
| -80 | Brak wysokości |
| -81 | \[command] nie może używać parametru \[name] w połączeniu z \[name] |
| -82 | Numer bloku poza zakresem |
| -83 | Nie znaleziono bloku |
| -84 | Brak hash lub wysokości |
| -85 | getblock według wysokości wymaga uruchomienia demona z flagą -indexheight |
| -86 | Brak hash lub txid |
| -87 | Nieprawidłowa lub nieznana transakcja |
| -88 | Brak lub pusta nazwa |
| -89 | Nieprawidłowy register\_address |
| -90 | Namespace już istnieje |
| -91 | Brak nazwy / register\_address |
| -92 | Nie znaleziono nazwy |
| -93 | Brak nazwy namespace |
| -94 | Nieprawidłowa namespace |
| -95 | Namespace nie istnieje: \[namespace] |
| -96 | Nie można utworzyć nazwy w \[namespace], której nie jesteś właścicielem |
| -97 | Obiekt o tej nazwie już istnieje w namespace |
| -98 | Obiekt o tej nazwie już istnieje dla tego użytkownika |
| -99 | Nie znaleziono transakcji przelewu