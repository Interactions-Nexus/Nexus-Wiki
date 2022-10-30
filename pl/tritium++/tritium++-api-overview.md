---
title: Przegląd API Tritium++
description: Przegląd
published: true
date: 2022-10-30T22:28:40.916Z
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
| -31 | Błąd księgi