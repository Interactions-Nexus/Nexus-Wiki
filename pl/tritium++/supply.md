---
title: PODAŻ
description: API podaży
published: true
date: 2022-11-16T23:43:31.974Z
tags: 
editor: markdown
dateCreated: 2022-10-24T22:29:40.457Z
---

# PODAŻ

Interfejs Supply API udostępnia funkcje wspierające wymagania dotyczące przeniesienia własności, typowe dla procesu łańcucha dostaw. Pozycjom w łańcuchu dostaw można nadać wartość, a wartość ta może być aktualizowana w czasie. Dostarczany interfejs API obsługuje formaty `readonly`, `raw`, `basic` i `JSON`, a użytkownik musi określić format.

Formaty `readonly` i `raw` są przydatne, gdy programiści chcą przechowywać dowolne dane, bez ponoszenia narzutu związanego z definiowaniem obiektu. Wartość zostanie podana z parametrem `data`. Format `readonly` nie może być aktualizowany i jest przechowywany w rejestrze tylko do odczytu. Format `raw` jest przechowywany w rejestrze surowym i umożliwia aktualizację danych.

Format `basic` umożliwia wywołującym zdefiniowanie aktywa w postaci prostych par klucz=wartość. Zakłada, że wszystkie wartości są przechowywane przy użyciu typu danych string. Pary klucz=wartość można aktualizować. . Format `JSON` umożliwia wywołującym podanie szczegółowej definicji struktury danych dostarczania, z każdym polem zdefiniowanym z określonym typem danych i zmiennością. Elementy zdefiniowane za pomocą jednego ze złożonych formatów można aktualizować po ich początkowym utworzeniu.

Supply API zapewnia również historię zmian wartości, a także historię własności elementu.

W pełni obsługiwany punkt końcowy identyfikatora URI dostawy jest następujący:

```
supply/verb/noun/filter/operator
```

Minimalne wymagane elementy identyfikatora URI to:

```
supply/verb/noun
```

---
&nbsp;

## Obsługiwane czasowniki (verbs)

Poniższe czasowniki są obecnie obsługiwane przez ten zestaw poleceń interfejsu API:

[`create`](#create) - Generuje nowy obiekt obsługiwanego typu.
[`get`](#get) - Pobierz obiekt obsługiwanego typu.
[`list`](#list) - Lista wszystkich obiektów posiadanych przez danego użytkownika.
[`update`](#update) - Aktualizuj określony obiekt.
[`transfer`](#transfer) - Transfer określonego rejestru obiektów.
[`claim`](#claim) - Roszczenie własności rejestru obiektów.
[`history`](#history) - Wygeneruj historię wszystkich ostatnich stanów.
[`transactions`](#transactions) - Lista wszystkich transakcji, które zmodyfikowały określony obiekt.

---
&nbsp;

## Obsługiwane rzeczowniki (nouns)

Ten zestaw poleceń interfejsu API obsługuje następujące rzeczowniki:

[`item`] - Rejestr obiektów zawierający obiekt pozycji.
[`raw`] - Rejestr obiektów zawierający surowy obiekt.
[`readonly`] - Rejestr obiektów zawierający obiekt tylko do odczytu.
[`any`] — Rzeczownik wyboru obiektu, który pozwala na mieszanie elementów.

---
&nbsp;

## create <a href="#create" id="create"></a>

Utwórz nowy rejestr obiektów określony przez podany rzeczownik.

```
supply/create/noun
```

To polecenie obsługuje tylko rzeczowniki `item`, `raw`, `readonly` i `any`.

##### create/item

Tworzy nowy element w rejestrze obiektów.

##### create/raw

Tworzy nowy element w surowym rejestrze.

##### create/readonly

Tworzy nowy element w rejestrze tylko do odczytu.

##### create/any

Tworzy nowy element określony przez parametr formatu.

### Parametry:

`pin` : Wymagany, jeśli **zablokowany**. `PIN` dla tego profilu.

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`name` : Opcjonalna nazwa identyfikująca aktywo. Jeśli zostanie podany, obiekt Nazwa zostanie również utworzony w lokalnej przestrzeni nazw użytkowników, umożliwiając dostęp do aktywa/pobieranie go według nazwy. Jeśli nazwa nie zostanie podana, aktywo będzie wymagało dostępu/pobrania za pomocą jego 256-bitowego adresu rejestru.

`format` : Wymagany do **określenia** formatu użytego do zdefiniowania aktywa. Wartości mogą być `readonly`, `raw`, `basic` i `JSON`.

`data` : Wymagane, jeśli **format** to `readonly` lub `raw`, wtedy to pole zawiera dane zakodowane szesnastkowo, które mają być przechowywane w tym aktywie. Aktywa `readonly` nie mogą być aktualizowane w trybie tylko do odczytu. Wszystkie pozostałe pola poprzedzające są ignorowane.

`<fieldname>=<value>` : Jeśli format to `basic`, wywołujący może podać dodatkowe pary = dla każdej części danych do przechowywania w aktywie. Jeśli format to `JSON`, to pole będzie zawierało definicję json aktywa jako tablicę obiektów JSON reprezentujących każde pole w obiekcie. Używa następującego formatu:

* `name`: Nazwa pola danych.
* `type` : Typ danych do użycia w tym polu. Wartości mogą być uint8, uint16, uint32, uint64, uint256, uint512, uint1024, string lub bytes.
* `value` : Domyślna wartość pola.
* `mutable` : Pole logiczne wskazujące, czy pole jest do zapisu (true), czy tylko do odczytu (false).
* `maxlength`: Dotyczy tylko pól łańcuchowych lub bajtowych, gdzie mutable=true, jest to maksymalna liczba znaków (bajtów), które mogą być przechowywane w polu. Jeśli nie podano parametru maxlength, wówczas domyślnym rozmiarem pola będzie długość wartości domyślnej, zaokrąglona w górę do najbliższych 64 bajtów.


> **NOTA:**
> W rejestrze obowiązuje limit 1 KB danych pozycji, które mogą zostać zapisane, z wyłączeniem nazwy pozycji.
> Opłata wynosi 1 NXS za utworzenie przedmiotu oraz dodatkowy 1 NXS za opcjonalną nazwę obiektu.
{.is-info}

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
{
    "success": true,
    "address": "87PUYqzvL73Ta81VfNMWuNyVjAqy3ZzE2iiX6FawibeNY56XC1u",
    "txid": "012d0190164584f6174c0c5b1cfa7c155a7faeb453b050ee4cc520681b47e52402d9aab5cdf327ee614752c4f40647d4bd3b32364db19da2bacb83c5f71a9144"
}
[Completed in 4970.165011 ms]
```

#### Zwracane wartości:

`success` : Flaga logiczna wskazująca, że ​​element został pomyślnie zapisany.

`address` : Adres rejestru dla tego nowo utworzonego elementu. Adres (lub nazwa, która hashuje się z tym adresem) jest potrzebny podczas tworzenia uznania lub obciążenia konta.

`txid` : Identyfikator (hash) transakcji, która zawiera utworzony obiekt.

---
&nbsp;

## get <a href="#get" id="get"></a>

Pobiera informacje dla pojedynczego elementu dla typu określonego przez rzeczownik.

```
supply/get/noun
```

To polecenie obsługuje rzeczowniki `item`, `raw`, `readonly` i `any`.

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`name` : Wymagane do **określenia** nazwy elementu. Nazwa powinna mieć format username:name (w przypadku nazw lokalnych) lub namespace::name (w przypadku nazw w przestrzeni nazw). Jest to opcjonalne, jeśli podano `address`.

`address` : Wymagane do **określenia** adresu rejestru elementu. Jest to opcjonalne, jeśli podano `name`.

[`Sorting`](/pl/tritium++/sorting)

[`Filtering`](/pl/tritium++/filtering)

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
[
    {
        "owner": "b7a57ddfb001d5d83ab5b25c0eaa0521e6b367784a30025114d07c444aa455c0",
        "version": 1,
        "created": 1656664801,
        "modified": 1656665317,
        "type": "OBJECT",
        "ABW": "DH0001222145565",
        "Address": "Marks street, PO Box:7887",
        "Item": "Samsung Watch",
        "address": "87wQAJ6nTWqVhGB423mKqtAJyF4B6S5WUXMqzYQWRcH9rJZxZup",
        "name": "local:Item0002"
    }
]
[Completed in 34.175112 ms]
```

#### Zwracane wartości:

`owner` : Hash nazwy użytkownika profilu właściciela.

`version` : Wersja serializacji transakcji.

`created` : Sygnatura czasowa systemu UNIX, kiedy element został utworzony.

`modified` : Sygnatura czasowa systemu UNIX, kiedy element był ostatnio modyfikowany.

`type` : Typ rejestru. Może to być OBJECT, RAW, READONLY.

`<fieldname>=<value>` : Para klucz-wartość dla każdego fragmentu danych przechowywanych w elemencie.

`data` : Dane przechowywane w obiekcie elementu nieprzetworzonego lub tylko do odczytu.

`address` : Adres rejestru elementu.

`name` : Nazwa identyfikująca element.

---
&nbsp;

## list <a href="#list" id="list"></a>

Pobiera listę wszystkich obiektów elementów należących do profilu określonego przez rzeczownik.

```
supply/list/noun
```

To polecenie obsługuje rzeczowniki `item`, `raw`, `readonly` i `any`.

##### list/items

Wyświetla listę wszystkich pozycji dla typu rejestru obiektów.

##### list/readonly

Wyświetla listę wszystkich pozycji dla typu rejestru tylko do odczytu.

##### list/raw

Wyświetla listę wszystkich pozycji dla surowego typu rejestru.

##### list/any

Wyświetla listę wszystkich pozycji dla obsługiwanych typów rejestrów.

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`where` : Tablica klauzul do **filtrowania** wyników JSON. Więcej informacji na temat filtrowania wyników z metod API /list/xxx można znaleźć w sekcji `Queries`.

[`Sorting`](/pl/tritium++/sorting)

[`Filtering`](/pl/tritium++/filtering)

[`Operators`](/pl/tritium++/operators)

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
[
    {
        "owner": "b7a57ddfb001d5d83ab5b25c0eaa0521e6b367784a30025114d07c444aa455c0",
        "version": 1,
        "created": 1656664801,
        "modified": 1656665317,
        "type": "OBJECT",
        "ABW": "DH0001222145565",
        "Address": "Marks street, PO Box:7887",
        "Item": "Samsung Watch",
        "address": "87wQAJ6nTWqVhGB423mKqtAJyF4B6S5WUXMqzYQWRcH9rJZxZup",
        "name": "local:Item0002"
    },
    {
        "owner": "b7a57ddfb001d5d83ab5b25c0eaa0521e6b367784a30025114d07c444aa455c0",
        "version": 1,
        "created": 1656662631,
        "modified": 1656663298,
        "type": "OBJECT",
        "ABW": "FED456315463135",
        "Address": "Avenue street, PO Box:4587",
        "Item": "Mobile Holder",
        "address": "87nyrW2TiKX9gZwRi61q3JNoVQK3GGTpZxBJBwR634au1A8Arc3",
        "name": "local:Item0001"
    }
]
[Completed in 34.175112 ms]
```

#### Zwracane wartości:

`owner` : Hash nazwy użytkownika profilu właściciela.

`version` : Wersja serializacji transakcji.

`created` : Sygnatura czasowa systemu UNIX, kiedy element został utworzony.

`modified` : Sygnatura czasowa systemu UNIX, kiedy element był ostatnio modyfikowany.

`type` : Typ rejestru. Może to być OBJECT, RAW, READONLY.

`<fieldname>=<value>` : Para klucz-wartość dla każdego fragmentu danych przechowywanych w elemencie.

`data` : Dane przechowywane w obiekcie elementu nieprzetworzonego lub tylko do odczytu.

`address` : Adres rejestru elementu.

`name` : Nazwa identyfikująca element.

---
&nbsp;

## update <a href="#update" id="update"></a>

Ta metoda zapewnia użytkownikowi możliwość aktualizacji danych obiektu określonych przez rzeczownik.

```
supply/update/noun
```

To polecenie obsługuje tylko rzeczowniki `item` i `raw`.

##### update/item

Spowoduje to zaktualizowanie wartości danych elementu w formacie basic i JSON.

##### update/raw

Spowoduje to aktualizację wartości danych dla rejestru pozycji surowych.

### Parametry:

`pin` : Wymagane w przypadku uwierzytelnienia. `PIN` dla tego profilu.

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`name` : Wymagane do **zidentyfikowania** elementu do aktualizacji według nazwy. Jest to opcjonalne, jeśli podano `address`.

`address` : Wymagane do **zidentyfikowania** elementu do aktualizacji według adresu rejestru. Jest to opcjonalne, jeśli podano `name`.

`format` : Wymagany do **określenia** formatu aktywa do aktualizacji. Wartości mogą być `readonly`, `raw`, `basic` i `JSON`.

`data`: Wymagane, jeśli **format** to `raw`, umożliwia wywołującemu aktualizację obiektu danych.

`<fieldname>=<value>` : Wymagane dla **formatu** `basic`. Wywołujący może podać pary klucz=wartość, aby zaktualizować każdy fragment danych elementu.

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
{
    "success": true,
    "txid": "01947f824e9b117d618ed49a7dd84f0e7c4bb0896e40d0a95e04e27917e6ecb6b9a5ccfba7d0d5c308b684b95e98ada4f39bbac84db75e7300a09befd1ac0999"
}
[Completed in 18533.182336 ms]
```





