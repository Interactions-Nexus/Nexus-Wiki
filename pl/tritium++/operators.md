---
title: Operatory
description: 
published: true
date: 2022-10-31T22:46:32.897Z
tags: 
editor: markdown
dateCreated: 2022-10-24T22:14:28.661Z
---

# Operatory

Interfejs API Nexusa i odpowiednie polecenia obsługują różne typy operatorów. Operatory umożliwiają wykonywanie obliczeń na przefiltrowanym zbiorze danych, podobnie jak w arkuszu kalkulacyjnym programu Excel.

Minimalne wymagane składniki identyfikatora URI dla operatora to:

````
commands/verb/noun/filter/operator
````

### `Filtr`

Aby wykonać operator, należy zastosować podstawowy filtr do zbioru danych, ponieważ musimy wyizolować składnik zwróconych danych, aby działał i zwracał.

Weź poniższą listę umów:

```
{
    "id": 33,
    "OP": "CREDIT",
    "for": "COINBASE",
    "txid": "01625b58e131e61813f77e8e97404cb587d780c7951b055b4f531f2a8ea5a63fc3c95f179ec26fa138e639143615a10961719ffb1b33dd98e64d0bf4d9fe50ae",
    "contract": 2,
    "to": "8BAv1H2YKfpaYC1RJMq9qjmMTiEV8DJiLpiKGqTY54wf2VPjznD",
    "amount": 208.833665,
    "token": "0",
    "ticker": "NXS"
},
{
    "id": 34,
    "OP": "CREDIT",
    "for": "COINBASE",
    "txid": "01b7291259fda66e8dbde6de502bd811894e42b6f2dd9fc684bdf87e9a3f0f224e16df72c491355547191af28f1cdd84bed0b522686de837f5b346593646f40f",
    "contract": 2,
    "to": "8BAv1H2YKfpaYC1RJMq9qjmMTiEV8DJiLpiKGqTY54wf2VPjznD",
    "amount": 205.705007,
    "token": "0",
    "ticker": "NXS"
},
```

Aby operować na naszym polu `amount`, musielibyśmy najpierw zastosować filtr:

````
commands/verb/noun/amount
````

To polecenie przygotuje teraz operatora, który można wywołać, kończąc URI:

````
commands/verb/noun/amount/sum
````

Powyższe polecenie zwróci obiekt JSON z naszym przefiltrowanym wynikiem:

````
{
    "amount": 414.53867,
}
````

### `Operatory`

W przypadku tego zestawu poleceń interfejsu API obsługiwane są następujące operatory:

[`array`](broken-reference) — Generuj listę wartości podanych ze zbioru przefiltrowanych wyników jako tablicę JSON.

[`count`](broken-reference) — Znajdź całkowitą liczbę wpisów zwróconych na danej liście JSON.

[`floor`](broken-reference) — Konwertuj wszystkie wartości w wyniku na liczby całkowite, usuwając ułamki dziesiętne.

[`max`](broken-reference) — Znajdź maksymalną wartość w danym zestawie i zwróć ją jako wynik.

[`mean`](broken-reference) — Oblicz średnią lub średnią wartość w zestawie przefiltrowanych wyników.

[`min`](broken-reference) — Znajdź minimalną wartość w podanym zestawie i zwróć ją jako wynik.

[`mode`](broken-reference) — Znajdź wartość z największą liczbą wystąpień w zestawie danych.

[`sum`](broken-reference) — oblicza sumę zestawu wartości uzyskanych na podstawie przefiltrowanych wyników.

**Przykład:**

````
finance/list/accounts/balance/sum
````

**Wynik:**

To polecenie zwróci sumę sald dla wszystkich rachunków:

````
{
    "balance": 333.376
}
````
