---
title: Szablon API Tritium++
description: Szablon API Tritium++
published: true
date: 2022-10-31T22:25:58.885Z
tags: 
editor: markdown
dateCreated: 2022-10-24T22:01:37.905Z
---

# Szablony

Wiele z obecnych poleceń dostępnych w API działa na ogólnym kodzie szablonowym, który umożliwia wstawianie dowolnego typu obiektu bez potrzeby powtarzania funkcji do obsługi każdego typu obiektu. Poniższa lista ogólnych punktów końcowych zawiera domyślne parametry, które mogą być przydatne poza każdym zestawem poleceń.

### `Zakres`

Poniższe szablony nie przekraczają zakresu lokalnego, co oznacza, że ​​zwrócą wyniki pochodzące z wewnętrznych usług indeksowania, które wymagają logowania i autoryzacji. Zestaw danych zwrócony z tych szablonów jest przechowywany w Logicznej Bazie Danych, a zatem dostarcza tylko dane lokalne do identyfikatora profilu, co oznacza, że `historia` i `transakcje` pokażą tylko zdarzenia, które miały miejsce w profilu, który wygenerował indeksy po zalogowaniu.

### `Czasowniki`

Poniższa lista czasowników to szablony w interfejsach API Nexusa. Chociaż akcja ma charakter ogólny (tj. Lista, pobierz, utwórz), implementacje tych działań będą zgodne z pewną semantyką lub obowiązkowymi parametrami niezależnie od rzeczownika (zasobu).

* `list`
  * Pobiera posortowaną listę obiektów lub danych
  * Sortowanie jest oparte na wieku transakcji/obiektu, domyślnie zawsze od najnowszego do najstarszego. Niektóre metody list obsługują dodatkowe pola sortowania.
  * Wspólne parametry:
    * `order` : Kolejność wyników. Wartości mogą być `desc` (domyślnie) lub `asc`
    * `limit` : Liczba rekordów do zwrócenia, domyślnie 100. `limit=none` jest dozwolone.
    * `page`: Umożliwia zwracanie wyników według strony (licząc od zera). Np. przekazanie page=1 zwróci drugi zestaw (limit) transakcji. Wartość domyślna to 0, jeśli nie została podana.
    * `offset` : Alternatywa dla `page`, offset może być użyty do zwrócenia zestawu (limit) wyników z określonego indeksu.
    * `verbose` : aby wskazać szczegółowość zwracanych danych. Wartości mogą być `default`, `summary`, lub `detail`
* `get`
  * Pobiera pojedynczy obiekt lub fragment danych
  * Obsługiwane parametry:
    * `verbose` : aby wskazać szczegółowość zwracanych danych. Wartości mogą być `default`, `summary`, lub `detail`
* `create`
  * Tworzy pojedynczy zasób lub obiekt.
  * Wspólne parametry:
    * `format` : wskazuje format danych dostarczanych do stworzenia pozycji/obiektu (jeśli dotyczy). Wartości mogą być `basic`, `raw`, i `JSON`
    * `scheme` : ustawia typ klucza, który ma być użyty dla danej transakcji. Wartości mogą być `falcon` lub `brainbpool`
* `update`
  * Aktualizuje pojedynczy zasób lub obiekt.
  * Wspólne parametry:
    * `format` : wskazuje format danych dostarczanych do stworzenia pozycji/obiektu (jeśli dotyczy). Wartości mogą być `basic`, `raw`, `standard`, i `JSON`
    * `scheme` : ustawia typ klucza, który ma być użyty dla danej transakcji. Wartości mogą być `falcon` lub `brainbpool`
* `transfer`
  * Przenosi pojedynczy zasób lub obiekt do profilu innego użytkownika
  * Wspólne parametry:
    * `address`: adres obiektu do przeniesienia
    * `recipient`: identyfikator profilu obiektu odbierającego sigchain.
    * `scheme` : ustawia typ klucza, który ma być użyty dla danej transakcji. Wartości mogą być `falcon` or `brainbpool`
* `claim`
  * Zajmuje pojedynczy zasób lub przedmiot z danego transferu
  * Wspólne parametry:
    * `address`: adres przedmiotu reklamacji
    * `txid`: identyfikator transakcji przelewu, którego żądamy.
    * `scheme` : ustawia typ klucza, który ma być użyty dla danej transakcji. Wartości mogą być `falcon` lub `brainbpool`
* `history`
  * Lista historii zmian stanu dla danego obiektu.
  * Wspólne parametry:
    * `address`: adres obiektu do przeglądania historii.
    * `order` : Kolejność wyników. Wartości mogą być `desc` (domyślnie) lub `asc`
    * `limit` : Liczba rekordów do zwrócenia, domyślnie 100. `limit=none` jest dozwolone.
    * `page`: Umożliwia zwracanie wyników według strony (licząc od zera). Np. przekazanie page=1 zwróci drugi zestaw (limit) transakcji. Wartość domyślna to 0, jeśli nie została podana.
    * `offset` : Alternatywa dla `page`, offset może być użyty do zwrócenia zestawu (limit) wyników z określonego indeksu.
    * `verbose` : aby wskazać szczegółowość zwracanych danych. Wartości mogą być `default`, `summary`, lub `detail`
* `transactions`
  * Wymień wszystkie transakcje, które zmodyfikowały dany rejestr.
  * Wspólne parametry:
    * `address`: adres obiektu do przeglądania transakcji.
    * `order` : Kolejność wyników. Wartości mogą być `desc` (domyślnie) lub `asc`
    * `limit` : Liczba rekordów do zwrócenia, domyślnie 100. `limit=none` jest dozwolone.
    * `page`: Umożliwia zwracanie wyników według strony (licząc od zera). Np. przekazanie page=1 zwróci drugi zestaw (limit) transakcji. Wartość domyślna to 0, jeśli nie została podana.
    * `offset` : Alternatywa dla `page`, offset może być użyty do zwrócenia zestawu (limit) wyników z określonego indeksu.
    * `verbose` : aby wskazać szczegółowość zwracanych danych. Wartości mogą być `default`, `summary`, lub `detail`

<details>

<summary></summary>



</details>