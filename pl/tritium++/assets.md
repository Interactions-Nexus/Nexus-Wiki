---
title: AKTYWA
description: API aktyw
published: true
date: 2022-11-12T23:00:47.864Z
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

#### Zwracane wartości:

`owner` : Hash nazwy użytkownika profilu właściciela.

`version` : Wersja serializacji transakcji.

`created` : Sygnatura czasowa systemu UNIX, kiedy aktywo zostao utworzone.

`modified` : Sygnatura czasowa systemu UNIX, kiedy aktywo było ostatnio modyfikowane.

`type` : Typ rejestru aktywów. Może to być OBJECT, RAW lub READONLY.

`data` : Dane przechowywane w surowym lub tylko do odczytu aktywie zasobów.

`<fieldname>=<value>` : Para klucz-wartość dla każdego elementu danych przechowywanego w aktywie.

`address`: Adres rejestru aktywa.

`name` : Nazwa identyfikująca aktywo.

---
&nbsp;

## list <a href="#list" id="list"></a>

Pobiera listę wszystkich obiektów aktywów należących do profilu określonego przez rzeczownik.

```
assets/list/noun
```

To polecenie obsługuje rzeczowniki `asset`, `readonly`, `raw` i `any`.

**list/assets**

Wyświetla listę wszystkich aktywów dla typu rejestru obiektów.

**list/readonly**

Wyświetla listę wszystkich aktywów dla typu rejestru tylko do odczytu.

**list/raw**

Wyświetla listę wszystkich aktywów dla surowego typu rejestru.

**list/any**

Wyświetla listę wszystkich aktywów dla wszystkich obsługiwanych typów rejestrów.

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`where` : Tablica klauzul do **filtrowania** wyników JSON. Więcej informacji na temat filtrowania wyników z metod API /list/xxx można znaleźć w sekcji `Zapytania`.

[`Sorting`](/pl/tritium++/sorting)

[`Filtering`](/pl/tritium++/filtering)

[`Operators`](/pl/tritium++/operators)

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
        "Location": "Margoa",
        "Owner Name": "Ageon",
        "Registration Details": "MRG/05/478564",
        "address": "87Wai2JoS4hNAEVXZVmejLS6pK21XQWKoLAkaep5aXFdrYnJJyk",
        "name": "local:Asset2"
    }
]
[Completed in 2.838543 ms]
```

#### Zwracane wartości:

`owner` : Hash nazwy użytkownika profilu właściciela.

`version` : Wersja serializacji transakcji.

`created` : Sygnatura czasowa systemu UNIX, kiedy aktywo zostało utworzone.

`modified` : Sygnatura czasowa systemu UNIX, kiedy aktywo było ostatnio modyfikowane.

`type` : Typ rejestru aktywów. Może to być OBJECT, RAW lub READONLY.

`data` : Dane przechowywane w surowym lub tylko do odczytu obiekcie aktywa.

`<fieldname>=<value>` : Para klucz-wartość dla każdego elementu danych przechowywanego w aktywie.

`address`: Adres rejestru aktywa.

`name` : Nazwa identyfikująca aktywo.

---
&nbsp;

## update <a href="#update" id="update"></a>

Ta metoda zapewnia użytkownikowi możliwość aktualizacji danych obiektu określonych przez rzeczownik.

```
assets/update/noun
```

To polecenie obsługuje tylko rzeczowniki `asset` i `raw`.

**update/asset**

Spowoduje to zaktualizowanie wartości danych dla aktywa w formacie podstawowym i JSON.

**update/raw**

Spowoduje to zaktualizowanie wartości danych dla rejestru pozycji surowych.

### Parametry:

`pin` : Wymagany, jeśli **zablokowany**. `PIN` dla tego profilu.

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`name` : Wymagane do **określenia** nazwy aktywa. Nazwa powinna mieć format username:name (w przypadku nazw lokalnych) lub namespace::name (w przypadku nazw w przestrzeni nazw). Jest to opcjonalne, jeśli podano `address`.

`address` : Wymagany do **określenia** adresu rejestru aktywa. Jest to opcjonalne, jeśli podano `name`.

`format` : Wymagany do **określenia** formatu aktywa do aktualizacji. Wartości mogą być `readonly`, `raw`, `basic` i `JSON`.

`data` : Wymagane, jeśli **format** jest `readonly` lub `raw`, umożliwia dzwoniącemu aktualizację obiektu danych.

`<fieldname>=<value>` : Opcjonalny dla **formatu** `basic`, wywołujący może podać pary 'key=value', aby zaktualizować każdy fragment danych dla zasobu.

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
{
    "success": true,
    "txid": "01947f824e9b117d618ed49a7dd84f0e7c4bb0896e40d0a95e04e27917e6ecb6b9a5ccfba7d0d5c308b684b95e98ada4f39bbac84db75e7300a09befd1ac0999"
}
[Completed in 18533.182336 ms]
```

#### Zwracane wartości:

`success` : Flaga logiczna wskazująca, że aktywo zostało pomyślnie zapisane.

`txid` : Hash transakcji, która została wygenerowana dla tego tx. W przypadku użycia opcji -autotx to pole zostanie pominięte.

---
&nbsp;

## transfer <a href="#transfer" id="transfer"></a>

Spowoduje to zainicjowanie przeniesienia własności określonego rzeczownika.

```
assets/transfer/noun
```

To polecenie obsługuje rzeczowniki `asset`, `raw` i `readonly`.

**transfer/asset**

Spowoduje to zainicjowanie transferu aktywa do odbiorcy.

**transfer/raw**

Spowoduje to zainicjowanie transferu surowego aktywa do odbiorcy.

**transfer/readonly**

Spowoduje to zainicjowanie transferu aktywa tylko do odczytu do odbiorcy.

### Parametry:

`pin` : Wymagany, jeśli **zablokowany**. `PIN`dla tego profilu.

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`name` : Wymagane do **określenia** nazwy aktywa. Nazwa powinna mieć format username:name (w przypadku nazw lokalnych) lub namespace::name (w przypadku nazw w przestrzeni nazw). Jest to opcjonalne, jeśli podano `address`.

`address` : Wymagany do **określenia** adresu rejestru aktywa. Jest to opcjonalne, jeśli podano `name`.

`recipient` : Wymagany do **zidentyfikowania** konta odbiorcy. Może to być nazwa użytkownika profilu lub hash genesis.

`expires` : Opcjonalne pole umożliwia dzwoniącym określenie **wygaśnięcia** transakcji transferu. Wartość wygaśnięcia to liczba sekund od czasu utworzenia transakcji, po której odbiorca nie może już odebrać transakcji. Z drugiej strony, gdy stosujesz wygaśnięcie transakcji, nie możesz anulować transakcji, dopóki nie upłynie czas wygaśnięcia. Jeśli opcja wygasa jest ustawiona na 0, transakcja nigdy nie wygaśnie, przez co nadawca nie będzie mógł nigdy anulować transakcji. W przypadku pominięcia zostanie zastosowany domyślny okres wygaśnięcia wynoszący 7 dni (604800 sekund).

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
{
    "success": true,
    "address": "87VmNhitFJv3WA3Yrovt9A3hts2MoXcfExyy9LiXyhK1sdThwYM",
    "txid": "01bc48f80792fd4b97d43555d5993f0edfb0998ab14bcf159404f52e34a64abd6769f61014f006703100aa040a27aca65227133b2b5a71617efac3bc5640e361"
}
[Completed in 4998.999748 ms]
```

#### Zwracane wartości:

`success` : Flaga logiczna wskazująca, że transfer aktywa zakończył się pomyślnie.

`address` : Adres rejestru dla tego aktywa.

`txid` : Identyfikator (hash) transakcji, która obejmuje przeniesienie aktywa.

---
&nbsp;

## claim <a href="#claim" id="claim"></a>

Ta metoda przejmie prawo własności do aktywa, aby zakończyć odpowiednią transakcję przeniesienia.

```
assets/claim/noun
```

To polecenie obsługuje rzeczowniki `asset`, `raw` i `readonly`.

**claim/asset**

Aktywa, które zostały przeniesione, muszą zostać odebrane przez odbiorcę. Ta metoda tworzy transakcję roszczenia.

**claim/raw**

Surowe aktywa, które zostały przeniesione, muszą zostać odebrane przez odbiorcę. Ta metoda tworzy transakcję roszczenia.

**claim/readonly**

Przeniesione aktywa tylko do odczytu muszą zostać odebrane przez odbiorcę. Ta metoda tworzy transakcję roszczenia.

### Parametry:

`pin` : Wymagany, jeśli **zablokowany**. `PIN` dla tego profilu.

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`txid` : Wymagany **identyfikator transakcji** (hash) transakcji przeniesienia aktywów, dla której żądane jest żądanie.

`name`: Opcjonalne pole pozwala użytkownikowi **zmienić nazwę** przedmiotu, gdy jest on odbierany. Domyślnie nazwa jest kopiowana od poprzedniego właściciela i tworzony jest rekord Nazwa dla elementu w Twojej przestrzeni nazw użytkownika. Jeśli masz już obiekt o tej nazwie, musisz podać nową nazwę, aby zgłoszenie się powiodło.

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
{
    "success": true,
    "txid": "01f35304d41d00b002ca02d3bd9cf6cfeb134f5c454d4b6f5a355e35ffc557cfb3756834f3cf5cbeaf98da6773adcaaeca80154d15e449d4876ddf35c0b895cf"
}
[Completed in 4978.949420 ms]
```

#### Zwracane wartości:

`success` : Flaga logiczna wskazująca, że roszczenie do aktywa powiodło się.

`txid` : Identyfikator (hash) transakcji, która obejmuje żądane aktywo.

---
&nbsp;

## tokenize <a href="#tokenize" id="tokenize"></a>

Ta metoda tokenizuje aktywo w zamienne tokeny, które reprezentują własność.

```
assets/tokenize/noun
```

To polecenie obsługuje tylko rzeczownik `asset`.

### Parametry:

`pin` : Wymagany, jeśli **zablokowany**. `PIN` dla tego profilu.

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`name` : Wymagane do **zidentyfikowania** nazwy aktywa, który ma być tokenizowany. Nazwa powinna mieć format username:name (w przypadku nazw lokalnych) lub namespace::name (w przypadku nazw w przestrzeni nazw). Jest to opcjonalne, jeśli podano `address`.

`address` : Wymagane do **określenia** adresu rejestru aktywów, które mają być tokenizowane. Jest to opcjonalne, jeśli podano `name`.

`token` : Wymagany do **zidentyfikowania** tokenu w celu stokenizacji aktywa. Może to być nazwa (dla nazw globalnych), username:tokenname (dla nazw lokalnych) lub adres rejestru tokena.


> **NOTA:** Utwórz token przed użyciem interfejsu API tokenizacji.
{.is-info}


### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
{
    "success": true,
    "txid": "01f35304d41d00b002ca02d3bd9cf6cfeb134f5c454d4b6f5a355e35ffc557cfb3756834f3cf5cbeaf98da6773adcaaeca80154d15e449d4876ddf35c0b895cf"
}
[Completed in 4978.949420 ms]
```

#### Zwracane wartości:

`success` : Flaga logiczna wskazująca, że tokenizacja aktywa zakończyła się pomyślnie.

`txid` : Identyfikator (hash) transakcji, która obejmuje żądane aktywo.

---
&nbsp;

## history <a href="#history" id="history"></a>

Spowoduje to pobranie historii zmian w aktywie, w tym zarówno danych, jak i własności.

```
assets/history/noun
```

To polecenie obsługuje rzeczowniki `asset`, `raw`, `readonly` i `any`.

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`name` : Wymagane do **określenia** nazwy aktywa. Nazwa powinna mieć format username:name (w przypadku nazw lokalnych) lub  namespace::name (w przypadku nazw w przestrzeni nazw). Jest to opcjonalne, jeśli podano `address`.

`address` : Wymagany do **określenia** adresu rejestru zasobu. Jest to opcjonalne, jeśli podano `name`.

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
        "created": 1656614448,
        "modified": 1656614448,
        "type": "OBJECT",
        "Assetname": "Bugatti Veyron",
        "Chassis_No": "BV45648784634546",
        "Purchased Date": "22/06/2022",
        "Engine_No": "BVE54864660",
        "Owner": "John Doe",
        "Registration_No": "DL01EK0001",
        "address": "88NcYcKtMTRwtwDgfXFkZ4TbrHvkRGzsQkqVZco77Hqx1WRgCyi",
        "name": "local:Asset0001",
        "action": "CREATE"
    }
]
[Completed in 0.870644 ms]
```

#### Zwracane wartości:

Wartość zwracana to tablica obiektów JSON dla każdego wpisu w historii nazw:

`owner` : Hash nazwy użytkownika profilu właściciela.

`version` : Wersja serializacji transakcji.

`created` : Sygnatura czasowa systemu UNIX podczas tworzenia konta.

`modified` : Sygnatura czasowa systemu UNIX, kiedy nazwa została zaktualizowana.

`type` : Typ rejestru. Może to być OBJECT, RAW lub READONLY.

`<fieldname>=<value>` : Jeśli format jest podstawowy, wywołujący może podać dodatkowe pary dla każdej części danych do zapisania w zasobie.

`data` : Dane przechowywane w nieprzetworzonym lub tylko do odczytu obiekcie aktywa.

`address` : Adres rejestru obiektu nazwy.

`name`: Nazwa obiektu.

`action` : Akcja, która miała miejsce - CREATE | MODIFY | TRANSFER | CLAIM.

---
&nbsp;

## transactions <a href="#transactions" id="transactions"></a>

Spowoduje to wyświetlenie wszystkich transakcji dla określonego rzeczownika.

```
assets/transactions/noun
```

To polecenie obsługuje wszystkie rzeczowniki.

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`name` : Wymagane do **identyfikacji** aktywa. Jest to opcjonalne, jeśli podano `address`.

`address` : Wymagany do **określenia** adresu rejestru aktywa. Jest to opcjonalne, jeśli podano `name`.

`verbose` : Opcjonalne, określa, ile danych transakcji ma zostać uwzględnionych w odpowiedzi. Obsługiwane wartości to:

* `default` : summary
* `summary` : type, version, sequence, timestamp, blockhash, confirmations, contracts
* `detail` : Wszystko  z summary + genesis, nexthash, prevhash, pubkey, signature

[`Sorting`](/pl/tritium++/sorting)

[`Filtering`](/pl/tritium++/filtering)

[`Operators`](/pl/tritium++/operators)

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
[
    {
        "txid": "0167d11ebea68f68e2c6591a9d94c236a60c312cf70d596492002a3e4d9a95a4f4e859c498fa6ac17c56cb4db1043abacdfd44f669112641fc4add15bb3efefa",
        "type": "tritium user",
        "version": 4,
        "sequence": 4,
        "timestamp": 1656614805,
        "blockhash": "9b2c063b2e8766ce9b55c5b75524b13c12c7006e0c67423dbfe1539ed4f62cd0c764f63fbbc6cb41ab9fc785ce6f88ae92e6a82e3151c4c956fa65eac524db3e1922bdced7bdd4cd97a4563dd21f011a310d062440300b2a7532fe21f6df55c7e3ba9046a982b99af97acddd768569d3cf5368cb91dcb0138cf5af7f1a6f391b",
        "confirmations": 95,
        "contracts": [
            {
                "id": 0,
                "OP": "TRANSFER",
                "address": "88NcYcKtMTRwtwDgfXFkZ4TbrHvkRGzsQkqVZco77Hqx1WRgCyi",
                "recipient": "8Dnn5LUeffcRCqZLpboCHnzw5AkfwzkM5hjVScjSDHVKhFpVzCB",
                "tokenized": true
            }
        ]
    },
    {
        "txid": "01e4eff49cadbd887511c6302d5fe8e89ead4caa87bcec2dfd55e18cb201a8fc8db9726571d3bebe554a81f579b22e2794a0e86756be326f362964e95ab28f23",
        "type": "tritium user",
        "version": 4,
        "sequence": 2,
        "timestamp": 1656614448,
        "blockhash": "e9b46f5dcf3c321f8a2dc672a6c47a5c6b763bc9d1f001722bc446b186afda3566f04cc739253696a3f232e036bc273ca68c18d84213186a1317d246ec86a165ba152838a2eca4425c19472dc8fb1b762f4413c5a633c4fef5494378b9858da34129dcd5bc556110c1e79aa42f01f8bae6f4938a6e87a63b6d30e2ee6025d507",
        "confirmations": 97,
        "contracts": [
            {
                "id": 0,
                "OP": "CREATE",
                "address": "88NcYcKtMTRwtwDgfXFkZ4TbrHvkRGzsQkqVZco77Hqx1WRgCyi",
                "type": "OBJECT",
                "standard": "NONSTANDARD",
                "object": {
                    "Assetname": " Bugatti Veyron",
                    "Chassis_No": "BV45648784634546",
                    "Purchased Date": "22/06/2022",
                    "Engine_No": "BVE54864660",
                    "Owner": "John Doe",
                    "Registration_No": "DL01EK0001"
                }
            }
        ]
    }
]
[Completed in 3.128134 ms]
```







