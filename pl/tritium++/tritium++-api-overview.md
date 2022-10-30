---
title: Przegląd API Tritium++
description: Przegląd
published: true
date: 2022-10-30T22:13:00.131Z
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
| 3    | Błąd składni zapytania: zniekształcona klauzula where w \[klauzula] |
| 4    | Błąd składni zapytania: należy użyć = bez dodatkowych znaków. |
| 5    | Błąd składni zapytania: należy użyć '(' i ')' do mieszania instrukcji AND/OR |
| 6    | Błąd składni zapytania: brak operatora logicznego dla grupy |
| 7    | Błąd składni zapytania: pusta klauzula where w \[klauzula] |
| 8    |
| 9    |
