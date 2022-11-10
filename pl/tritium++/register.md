---
title: REJESTR
description: API rejestru
published: true
date: 2022-11-10T23:43:10.642Z
tags: 
editor: markdown
dateCreated: 2022-10-29T09:58:35.680Z
---

# REJESTR

Register API zapewnia dostęp do danych rejestru, co pozwala na prezentację informacji z całej sieci. W pełni obsługiwany punkt końcowy identyfikatorów URI profili jest następujący:

````
register/verb/noun/filter/operator
````

Minimalne wymagane składniki identyfikatora URI to:

````
register/verb/noun
````

## Obsługiwane czasowniki (verbs)

Następujące czasowniki są obecnie obsługiwane przez ten zestaw poleceń interfejsu API:

[`get`](#get) - Pobierz obiekt obsługiwanego typu.
[`list`](#list) - Lista wszystkich obiektów należących do danego użytkownika.
[`history`](#history) — Generuje historię wszystkich ostatnich stanów.
[`transactions`](#transactions) — Lista wszystkich transakcji, które zmodyfikowały określony obiekt.

---
&nbsp;

## Obsługiwane rzeczowniki (nouns)

W tym zestawie poleceń interfejsu API obsługiwane są następujące rzeczowniki:

[`crypto`] - Rejestr obiektu, który przechowuje hashe klucza publicznego.
[`object`] - Rejestr obiektu zawierający strukturę danych zdefiniowaną przez użytkownika.
[`raw`] - Rejestr obiektów typu raw.
[`readonly`] - Rejestr obiektów typu tylko do odczytu.
[`any`] - Rzeczownik wyboru obiektu umożliwiający mieszanie kont różnych tokenów.

---
&nbsp;

## Obsługiwane API/rzeczownik
###### API finansów:

[`finance:account`] - Rejestr obiektów zawierający identyfikator tokena i saldo.
[`finance:trust`] — Rejestr obiektów zawierający identyfikator tokena, saldo i zaufanie.
[`finance:token`] - Rejestr obiektów zawierający identyfikator tokena, saldo, podaż i liczby dziesiętne.

###### API nazw:

[`names:local`] - Rejestr obiektów zawierający nazwy lokalne.
[`names:global`] - Rejestr obiektów zawierający nazwy globalne.
[`names:namespaces`] - Rejestr obiektów zawierający przestrzenie nazw.
###### API faktur:

[`invoices:invoice`] — Rejestr obiektów zawierający faktury.
[`invoices:outstanding`] — Rejestr obiektów zawierający zaległe faktury.
[`invoices:paid`] — Rejestr obiektów zawierający opłacone faktury.
[`invoices:cancelled`] — Rejestr obiektów zawierający anulowane faktury.

###### API aktywów:

[`assets:asset`] - Rejestr obiektów zawierający obiekt aktywów.
[`assets:raw`] — Rejestr obiektów zawierający surowy obiekt zasobu.
[`assets:readonly`] - Rejestr obiektów zawierający obiekt zasobu tylko do odczytu.

###### API podaży:

[`supply:item`] - Rejestr obiektów zawierający obiekt item.
[`supply:raw`] - Rejestr obiektów zawierający surowy obiekt.
[`supply:readonly`] - Rejestr obiektów zawierający obiekt pozycji tylko do odczytu.

---
&nbsp;

## get <a href="#get" id="get"></a>

Pobiera informacje o pojedynczym obiekcie dla typu określonego przez noun lub API:noun

````
register/get/noun
````

To polecenie obsługuje wszystkie rzeczowniki.

````
register/get/API:noun
````

To polecenie obsługuje wszystkie API:nouns.

**get/crypto**

Pobiera informacje o określonym rejestrze obiektów kryptograficznych profilu.

**get/object**

Pobiera informacje o określonym rejestrze obiektów.

**get/readonly**

Pobiera informacje dla określonego rejestru tylko do odczytu.

**get/raw**

Pobiera informacje dla określonego rejestru surowego.

**get/append**

Pobiera informacje o określonym rejestrze dołączania.

### Parametry:

`name` : Wymagane do **identyfikacji** nazwy konta/zaufania/tokena. Nazwa powinna być w formacie username:name (dla nazw lokalnych) lub namespace::name (dla nazw w przestrzeni nazw). Jest to opcjonalne, jeśli podano `address`.

`address` : Wymagany do **identyfikacji** adresu rejestrowego konta/zaufania/tokena. Jest to opcjonalne, jeśli podano `name`.

[`Sorting`](/pl/tritium++/sorting)

[`Filtering`](/pl/tritium++/filtering)

---
&nbsp;

## list <a href="#list" id="list"></a>

Ta metoda daje użytkownikowi możliwość bezpośredniego dostępu do danych rejestru obiektów określonych przez rzeczownik i nie wymaga logowania.

````
register/list/noun
````

To polecenie obsługuje wszystkie rzeczowniki.

````
register/list/API:noun
````

To polecenie obsługuje wszystkie API:nouns.

**list/crypto**

Zwraca listę wszystkich rejestrów obiektów kryptograficznych.

**list/object**

Zwraca listę wszystkich rejestrów obiektów.

**list/readonly**

Zwraca listę wszystkich rejestrów tylko do odczytu.

**list/raw**

Zwraca listę wszystkich nieprzetworzonych rejestrów.

**list/append**

Zwraca listę wszystkich rejestrów dołączających.

