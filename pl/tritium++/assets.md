---
title: AKTYWA
description: API aktyw
published: true
date: 2022-11-11T23:21:02.047Z
tags: 
editor: markdown
dateCreated: 2022-10-24T22:27:57.050Z
---

# AKTYWA

Aktywo to zdefiniowana przez użytkownika struktura danych przechowywana w rejestrze obiektów należącym do profilu. Aktywa mogą zawierać jeden lub więcej fragmentów danych, a użytkownicy mogą definiować pola (nazwa, dane, typ, zmienność), w których dane są przechowywane. Interfejs API aktywów obsługuje formaty `readonly`, `raw`, `basic` i `JSON`, a użytkownik musi określić format.

Formaty `readonly` i `raw` są przydatne, gdy programiści chcą przechowywać dowolne dane, bez ponoszenia narzutu związanego z definiowaniem obiektu. Wartość zostanie podana z parametrem `data`. Format `readonly` nie może być aktualizowany i jest przechowywany w rejestrze tylko do odczytu. Format `raw` jest przechowywany w rejestrze surowym i umożliwia aktualizację danych.

Format `basic` umożliwia wywołującym zdefiniowanie aktywa w postaci prostych par 'key=value'. Zakłada, że ​​wszystkie wartości są przechowywane przy użyciu typu danych string. Pary 'key=value' można aktualizować.

Format `JSON` umożliwia wywołującym podanie szczegółowej definicji struktury danych dostarczania, z każdym polem zdefiniowanym z określonym typem danych i zmiennością. Elementy zdefiniowane za pomocą jednego ze złożonych formatów można aktualizować po ich początkowym utworzeniu.

API aktywów zapewnia również historię zmian wartości, a także historię własności elementu.

W pełni obsługiwany punkt końcowy finansowego identyfikatora URI jest następujący:

```
assets/verb/noun/filter/operator
```

Minimalne wymagane elementy identyfikatora URI to:

```
assets/verb/noun
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
[`tokenize`](#tokenize) — Aby reprezentować własność obiektu zasobu za pomocą obiektu tokenu.
[`transactions`](#transactions) - Lista wszystkich transakcji, które zmodyfikowały określony obiekt.
[`history`](#history) - Wygeneruj historię wszystkich ostatnich stanów.

---
&nbsp;

## Obsługiwane rzeczowniki (nouns)

Ten zestaw poleceń interfejsu API obsługuje następujące rzeczowniki:

[`asset`] - Rejestr obiektu zawierający obiekt aktywa.
[`raw`] - Rejestr obiektu zawierający surowy obiekt aktywa.
[`readonly`] — Rejestr obiektu zawierający obiekt aktywa tylko do odczytu.
[`any`] — Rzeczownik wyboru obiektu, który umożliwia mieszane aktywa.
[`schema`] - Rejestr obiektu zawierający obiekt aktywa zdefiniowany przez użytkownika.

---
&nbsp;

## Bezpośrednie punkty końcowe

Następujące polecenia są bezpośrednimi punktami końcowymi i dlatego nie obsługują powyższej struktury `verb` i `noun` dostępnej powyżej.

[`list/partial`](#list/partial) — Wyświetl szczegóły częściowej własności użytkowników dla tokenizowanych aktywów.

---
&nbsp;

## create <a href="#create" id="create"></a>

Utwórz nowy rejestr obiektów określony przez podany rzeczownik.

```
assets/create/noun
```

To polecenie obsługuje rzeczowniki `asset`, `readonly`, `raw` i `any`.

**create/asset**

Tworzy nowe aktywo w rejestrze obiektów.

**create/readonly**

Tworzy nowe aktywo w rejestrze tylko do odczytu.

**create/raw**

Tworzy nowe aktywo w nieprzetworzonym rejestrze.

**create/any**

Tworzy nowe aktywo określone przez parametr formatu.

### Parametry:

`pin` : Wymagany, jeśli **zablokowany**. `PIN` dla tego profilu.

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`name` : Opcjonalna dla **rzeczownika** `name` jako łańcuch zakodowany w _UTF-8_, który wygeneruje rejestr obiektu nazwy wskazujący na nowy obiekt.

`format` : Wymagany do **określenia** formatu użytego do zdefiniowania zasobu. Wartości mogą być `readonly`, `raw`, `basic` i `JSON`.

`data` : Wymagane, jeśli **format** jest `readonly` lub `raw`, umożliwia wywołującemu dodanie dowolnych danych do obiektu. Aktywa `readonly` nie mogą być aktualizowane. Wszystkie pozostałe pola są ignorowane.

`<fieldname>=<value>` : Opcjonalny dla **formatu** `basic`, wywołujący może podać pary 'key=value' dla każdej części danych do przechowywania w zasobie.

`json` : Jeśli **format** to `JSON`, to pole będzie zawierało definicję json zasobu jako tablicę obiektów JSON reprezentujących każde pole w obiekcie. Używa następującego formatu:

* `name`: Nazwa pola danych.
* `type` : Typ danych do użycia w tym polu. Wartości mogą być uint8, uint16, uint32, uint64, uint256, uint512, uint1024, string lub bytes.
* `value` : Domyślna wartość pola.
* `mutable` : Pole logiczne wskazujące, czy pole jest do zapisu (true), czy tylko do odczytu (false).
* `maxlength`: Dotyczy tylko pól łańcuchowych lub bajtowych, gdzie mutable=true, jest to maksymalna liczba znaków (bajtów), które mogą być przechowywane w polu. Jeśli nie podano parametru maxlength, wówczas domyślnym rozmiarem pola będzie długość wartości domyślnej, zaokrąglona w górę do najbliższych 64 bajtów.


> **NOTA:**
> Istnieje limit 1 KB na dane aktywa, które można zapisać w rejestrze, z wyłączeniem nazwy aktywa.
> Za utworzenie aktywa pobierana jest opłata w wysokości 1 NXS oraz dodatkowy 1 NXS za opcjonalną nazwę obiektu.
> {.is-info}


### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
{
    "success": true,
    "address": "87VmNhitFJv3WA3Yrovt9A3hts2MoXcfExyy9LiXyhK1sdThwYM",
    "txid": "01230bbc8f0d72aaaff13471e34520d17902290de9a1e5ce1f320f0883024e2d96e21b59a3e48b8d2b5ba2874e93d5d3b4f412e06dc92440c2e12682c958fe34"
}
[Completed in 4998.584942 ms]
```

#### Zwracane wartości:

`success` : Flaga logiczna wskazująca, że aktywo zostało pomyślnie zapisane.

`address` : Adres rejestru dla tego konta. Adres (lub nazwa, która hashuje się z tym adresem) jest potrzebny podczas tworzenia uznania lub obciążenia konta.

`txid` : Hash transakcji, która została wygenerowana dla tego tx. W przypadku użycia opcji -autotx to pole zostanie pominięte.

---
&nbsp;

## get <a href="#get" id="get"></a>

Pobiera informacje o zasobie określonym przez rzeczownik.

```
assets/get/noun
```

To polecenie obsługuje rzeczowniki `readonly`, `raw` i `asset`.

**get/asset**

Pobierz aktywo dla obiektu typu rejestru.

**get/readonly**

Pobierz aktywo dla typu rejestru tylko do odczytu.

**get/raw**

Pobierz aktywo dla rejestru typu raw.

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`name` : Wymagane do **określenia** nazwy aktywa. Nazwa powinna mieć format username:name (w przypadku nazw lokalnych) lub namespace::name (w przypadku nazw w przestrzeni nazw). Jest to opcjonalne, jeśli podano `address`.

`address` : Wymagany do **określenia** adresu rejestru aktywa. Jest to opcjonalne, jeśli podano `name`.

[`Sorting`](/pl/tritium++/sorting)

[`Filtering`](/pl/tritium++/filtering)

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
[
    {
        "owner": "b7392196b83aca438567558462cd0c5d982569c7cefa668500c4bf3e61a03b7a",
        "version": 1,
        "created": 1655279431,
        "modified": 1655279431,
        "type": "OBJECT",
        "Location": "Meta World ",
        "Owner Name": "John Doe",
        "Registration Details": "MRG/05/478564",
        "address": "87Wai2JoS4hNAEVXZVmejLS6pK21XQWKoLAkaep5aXFdrYnJJyk",
        "name": "local:Meta_World"
    }
]
[Completed in 2.838543 ms]
```

