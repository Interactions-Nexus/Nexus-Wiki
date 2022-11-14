---
title: NAZWY
description: API nazw
published: true
date: 2022-11-14T23:12:48.456Z
tags: 
editor: markdown
dateCreated: 2022-10-24T22:28:47.994Z
---

# NAZWY

Nazwy i przestrzenie nazw to specjalne rodzaje rejestrów obiektów, które są używane jako lokalizatory innych rejestrów obiektów w łańcuchu bloków. Kiedy rejestr obiektów jest tworzony po raz pierwszy (na przykład aktywo), wywołujący może podać nazwę rejestru. Jeśli podano nazwę, tworzony jest również rejestr obiektu Nazwa z jego adresem rejestru na podstawie skrótu nazwy. Obiekt Name posiada również pole adresu, które jest wypełniane adresem rejestru (aktywa, tokena, konta itp.), na który „wskazuje” nazwa. W ten sposób obiekty mogą być pobierane według nazwy, najpierw mieszając nazwę, aby uzyskać adres obiektu Nazwa, pobierając obiekt Nazwa, a następnie używając zapisanego w nim adresu, aby pobrać rejestr obiektów. Nazwa jest więc najlepiej traktowana jako nazwany indeks do rejestrów obiektów.

System nazewnictwa `TAO` (TNS) umożliwia tworzenie obiektów Nazw w jednym z trzech różnych kontekstów — `local`, `namespaced`, `global` i będzie własnością profilu. Nazwy muszą być unikalne w ramach profilu, w którym zostały zdefiniowane.

## Nazwy lokalne (local)
Nazwy lokalne to nazwy utworzone w kontekście profilu użytkownika. Aby użyć nazwy lokalnej, musisz poprzedzić nazwę nazwą użytkownika właściciela oddzieloną pojedynczym dwukropkiem, np. bob:savings. Jest to równoznaczne z powiedzeniem „spójrz na wszystkie Nazwy zarejestrowane w profilu bob i znajdź jedno o nazwie savings, a następnie zobacz, na jaki rejestr obiektów wskazuje”. Może istnieć tylko jedna Nazwa o nazwie savings w sig chain bob, ale inny użytkownik alice może również utworzyć lokalną nazwę o nazwie savings.

## Nazwy z przestrzenią nazw (namespaced)
Nazwy w przestrzeni nazw to nazwy utworzone w kontekście `namespace`, która sama w sobie jest globalnie unikalnym słowem kluczowym. Przestrzenie nazw umożliwiają użytkownikom nadawanie przyjaznych dla użytkownika nazw rejestrów obiektów bez konieczności ujawniania nazwy użytkownika. Jest to przydatne ze względu na prywatność, ale także umożliwia powiązanie nazw z firmą lub innym znaczącym kontekstem. Aby użyć nazwy z przestrzenią nazw, musisz poprzedzić nazwę przestrzenią nazw oddzieloną podwójnym dwukropkiem, np. `bobscoffeeshop::payments`. W tym przykładzie bob najpierw zarejestrowałby przestrzeń nazw `bobscoffeeshop` i utworzył konto do otrzymywania `payments` (które można nazwać czymkolwiek). Następnie tworzy Nazwę z name=payments, namespace=bobscoffeeshop i adres=(adres rejestracyjny konta). Od tego momentu każdy może używać nazwy `bobscoffeeshop::payments` i zostanie ona rozwiązana na adres rejestracyjny konta. Aby uniknąć przyklepywania nazw, rejestracja nazwy przestrzeni nazw wiąże się z wysoką opłatą (1000 NXS). Jednak po zarejestrowaniu tworzenie Nazw w tej przestrzeni nazw kosztuje tylko 1 NXS.

## Nazwy globalne (global)
Nazwy globalne nie wymagają nazwy użytkownika ani prefiksu przestrzeni nazw i dlatego są globalnie unikalne. Będą one prawdopodobnie zarezerwowane dla przypadków użycia, w których konieczna jest zwięzła, niepowtarzalna nazwa, na przykład symbol tokena `ticker`. Aby uniknąć niepotrzebnego przyklepywania nazw, globalne nazwy pociągają wysoką opłatę (2000 NXS).

Interfejs Names API umożliwia dzwoniącym dostęp do `Names` i `Namespaces` oraz zarządzanie nimi. Nazwy mogą być tworzone tak, aby „wskazywały” dowolny adres rejestru, niezależnie od tego, czy dzwoniący jest właścicielem rejestru, czy nie. Jest to przydatne na przykład, jeśli ktoś poda Ci adres rejestrowy konta NXS do otrzymywania płatności i chcesz dodać do niego przyjazną Nazwę do wykorzystania w przyszłości.

Przestrzenie nazw można przenosić do innych łańcuchów sygnatur, otwierając możliwość kupna i sprzedaży przestrzeni nazw na rynku wtórnym (podobnie jak nazwy domen internetowych). `Global Names` i `Names`, które zostały utworzone w ramach `namespace`, mogą być również przenoszone do innych łańcuchów sygnatur. Nie można przenosić nazw lokalnych.

W pełni obsługiwany punkt końcowy identyfikatora URI nazw jest następujący:

```
names/verb/noun/filter/opertor
```

Minimalne wymagane elementy identyfikatora URI to:

```
/names/verb/noun
```
---
&nbsp;

## Obsługiwane czasowniki (verbs)

Poniższe czasowniki są obecnie obsługiwane przez ten zestaw poleceń interfejsu API:

[`create`](#create) - Generuje nowy obiekt obsługiwanego typu.
[`get`](#get) - Pobierz obiekt obsługiwanego typu.
[`list`](#list) - Lista wszystkich obiektów posiadanych przez danego użytkownika.
[`update`](#update)- Aktualizuj rejestr obiektów.
[`transfer`](#transfer)- Przeniesienie własności rejestru obiektów.
[`claim`](#claim) - Roszczenie własności rejestru obiektów.
[`history`](#history) - Wygeneruj historię wszystkich ostatnich stanów.
[`transactions`](#transactions) - Lista wszystkich transakcji, które zmodyfikowały określony obiekt.

---
&nbsp;

## Obsługiwane rzeczowniki (nouns)

Ten zestaw poleceń interfejsu API obsługuje następujące rzeczowniki:

[`name`] - Rejestr obiektów zawierający nazwę obiektu.
[`namespace`] - Rejestr obiektów zawierający obiekt przestrzeni nazw.
[`global`] - Rejestr obiektów rozpoznawany globalnie w sieci.
[`local`] - Rejestr obiektów, który jest rozpoznawany tylko w kontekście profilu użytkownika.
[`any`] — Rzeczownik wyboru obiektu, który pozwala rzeczownikom o różnych nazwach.

---
&nbsp;

## create <a href="#create" id="create"></a>

Spowoduje to utworzenie nowego rejestru obiektów określonego przez podany rzeczownik.

```
names/create/noun
```

To polecenie obsługuje nazwy i rzeczowniki przestrzeni nazw.

##### create/name

Spowoduje to utworzenie nowej nazwy lokalnej lub nazwy w przestrzeni nazw lub nazwy globalnej.

##### create/namespace

Spowoduje to utworzenie nowej przestrzeni nazw.

> **NOTA**: Przestrzenie nazw mogą zawierać tylko małe litery, cyfry i kropki (.).
{.is-info}


### Parametry:

`pin` : Wymagany, jeśli **zablokowany**. PIN do autoryzacji transakcji.

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

##### create/name

`name` : Nazwa wymagana do **utworzenia** obiektu, na który ta nazwa będzie wskazywać. Nazwa może zawierać dowolne znaki, ale nie może zaczynać się od dwukropka :

`namespace` : Opcjonalne pole pozwala dzwoniącym **określić** przestrzeń nazw, w której ma zostać utworzona nazwa. Jeśli przestrzeń nazw jest podana, wywołujący musi być również właścicielem przestrzeni nazw. tj. nie możesz utworzyć nazwy w czyjejś przestrzeni nazw. Jeśli przestrzeń nazw pozostanie pusta (domyślnie), nazwa zostanie utworzona w lokalnej przestrzeni nazw użytkownika (chyba że zostanie wyraźnie oznaczona jako globalna).

`global` : Opcjonalne, boolowskie pole wskazuje, że Nazwa powinna zostać utworzona w globalnej przestrzeni nazw, czyli będzie globalnie unikalna. Jeśli obiekt wywołujący ustawi to pole na wartość true, parametr przestrzeni nazw jest ignorowany.

`address` : Opcjonalny, 256-bitowy **adres rejestru** w systemie szesnastkowym obiektu, na który będzie wskazywać ta nazwa.

##### create/namespace

`namespace` : Nazwa wymagana do **utworzenia** obiektu przestrzeni nazw. Skrót nazwy określi adres rejestru.

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
{
    "success": true,
    "address": "8LBEGF1Yo3UR2HPtVVokZMpmAespLfDdPdt99cpKiFJ7VSufsJ5",
    "txid": "01dc4d11a9b3418832796ad6c9ca90ba18897b0ec24be44667f0fb0172481775925fa5fc568d54d8cac1e18a81beb552cbbb8cf242210a70233a79355e5a056f"
}
[Completed in 4981.591417 ms]
```

#### Zwracane wartości:

`success`: Flaga logiczna wskazująca, że ​​nazwa lub przestrzeń nazw została pomyślnie utworzona.

`address` : Adres rejestru dla utworzonej nazwy lub przestrzeni nazw. Jest to nazwa lub przestrzeń nazw, która jest mieszana z tym adresem.

`txid` : Identyfikator (hash) transakcji, która zawiera nazwę lub utworzenie przestrzeni nazw.

---
&nbsp;

## get <a href="#get" id="get"></a>

Pobiera informacje o obiekcie określone przez podany rzeczownik.

```
names/get/noun
```

To polecenie obsługuje rzeczowniki `name`, `namespace`, `global` i `local`.

##### get/name

Spowoduje to pobranie określonego obiektu nazwy.

##### get/namespace

Spowoduje to pobranie określonego obiektu przestrzeni nazw.

##### get/global

Spowoduje to pobranie określonego obiektu nazwy globalnej.

##### get/local

Spowoduje to pobranie określonego obiektu nazwy lokalnej.

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

[`Sorting`](/pl/tritium++/sorting)

[`Filtering`](/pl/tritium++/filtering)

##### get/name, get/global, get/local

`name` : Wymagane do **zidentyfikowania** nazwy obiektu name. Nazwa powinna być w formacie nazwa (dla nazw lokalnych i globalnych), username:name (dla nazw lokalnych) lub namespace::name (dla nazw w przestrzeni nazw). Jest to opcjonalne, jeśli podano `address`.

`address` : Wymagane do **określenia** zarejestrowanego adresu nazwy. Jest to opcjonalne, jeśli podano `name`.

##### get/namespace

`namespace` : Wymagane do **zidentyfikowania** przestrzeni nazw. Jest to opcjonalne, jeśli podano `address`.

`address` : Wymagane do **zidentyfikowania** adresu rejestru przestrzeni nazw. Jest to opcjonalne, jeśli podano `namespace`.

### Wyniki:

#### Wartość zwracana Obiekt JSON:

##### get/name

```
{
    "owner": "b7fa11647c02a3a65a72970d8e703d8804eb127c7e7c41d565c3514a4d3fdf13",
    "version": 1,
    "created": 1656571493,
    "modified": 1656571493,
    "type": "OBJECT",
    "register": "8BJ747ASK45oU7UC5e2dePXeMviskmU1t5Kd4iyKLdSiCgKtLcJ",
    "name": "Block_Token",
    "namespace": "",
    "address": "8HeR7kxrk9zsAcEAqaQaD2juMnZ73m4WDb4sW16pW93qd7i2Q3G"
}
[Completed in 0.418167 ms]
```

##### get/namespace

```
{
    "owner": "b7fa11647c02a3a65a72970d8e703d8804eb127c7e7c41d565c3514a4d3fdf13",
    "version": 1,
    "created": 1654698239,
    "modified": 1654698239,
    "type": "OBJECT",
    "namespace": "valkyrie",
    "address": "8LBEGF1Yo3UR2HPtVVokZMpmAespLfDdPdt99cpKiFJ7VSufsJ5"
}
[Completed in 0.174417 ms]
```

#### Zwracane wartości:

`owner` : Hash nazwy użytkownika profilu właściciela.

`version` : Wersja serializacji nazwy.

`created` : Sygnatura czasowa systemu UNIX podczas tworzenia nazwy.

`modified` : Sygnatura czasowa systemu UNIX, kiedy nazwa była ostatnio modyfikowana.

`type` : Typ rejestru aktywów. Może to być OBJECT, RAW lub READONLY.

`register` : Adres rejestru obiektu, na który wskazuje ta nazwa lub przestrzeń nazw.

`name` : Nazwa identyfikująca rejestr obiektów.

`namespace` : Nazwa identyfikująca przestrzeń nazw lub przestrzeń nazw, w której nazwa została utworzona. W przypadku nazw globalnych zostanie ustawiona wartość ~~GLOBAL~~.

`address`: Adres rejestrowy Nazwy.

---
&nbsp;

## list <a href="#list" id="list"></a>

Pobiera listę wszystkich szczegółów obiektu określonych przez rzeczownik.

```
names/list/noun
```

To polecenie obsługuje wszystkie rzeczowniki.

##### list/name

Spowoduje to odzyskanie wszystkich obiektów nazw.

##### list/namespace

Spowoduje to odzyskanie wszystkich obiektów przestrzeni nazw.

##### list/global

Spowoduje to odzyskanie wszystkich globalnych obiektów nazw.

##### list/local

Spowoduje to pobranie wszystkich obiektów nazw lokalnych.

##### list/any

Spowoduje to odzyskanie wszystkich obsługiwanych obiektów.

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`where` : Tablica klauzul do **filtrowania** wyników JSON. Więcej informacji na temat filtrowania wyników z metod API /list/xxx można znaleźć pod adresem [`Queries`](/pl/tritium++/queries).

[`Sorting`](/pl/tritium++/sorting).

[`Filtering`](/pl/tritium++/filtering)

[`Operators`](/pl/tritium++/operators)

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
[
    {
        "owner": "b7fa11647c02a3a65a72970d8e703d8804eb127c7e7c41d565c3514a4d3fdf13",
        "version": 1,
        "created": 1656571493,
        "modified": 1656571493,
        "type": "OBJECT",
        "register": "8BJ747ASK45oU7UC5e2dePXeMviskmU1t5Kd4iyKLdSiCgKtLcJ",
        "name": "EPS-Token",
        "namespace": "",
        "address": "8HeR7kxrk9zsAcEAqaQaD2juMnZ73m4WDb4sW16pW93qd7i2Q3G"
    },
    {
        "owner": "b7fa11647c02a3a65a72970d8e703d8804eb127c7e7c41d565c3514a4d3fdf13",
        "version": 1,
        "created": 1656571181,
        "modified": 1656571181,
        "type": "OBJECT",
        "register": "8DS2qGLhuEC2reKrzxyWaXXwtVq2KmGWGQCWKBQwrCQc4XS2b8V",
        "name": "EPS",
        "namespace": "~GLOBAL~",
        "address": "8H5tcBwU31FBTzokw3gDhz7e1k3mGytk26MBbKeAfjJbFHoXo7Y"
    }
]
[Completed in 0.781230 ms]
```

#### Zwracane wartości:

Wartość zwracana to tablica obiektów JSON dla każdego wpisu w historii przestrzeni nazw:

`owner` : Hash nazwy użytkownika profilu właściciela.

`version` : Wersja serializacji przestrzeni nazw.

`created` : Sygnatura czasowa systemu UNIX, kiedy obiekt został utworzony.

`modified` : Sygnatura czasowa systemu UNIX, kiedy obiekt został zaktualizowany.

`type` : Typ rejestru - OBJECT | READONLY | RAW.

`name` : Nazwa identyfikująca rejestr obiektów.

`namespace` : Nazwa przestrzeni nazw lub przestrzeni nazw, w której nazwa została utworzona. W przypadku nazw globalnych zostanie ustawiona wartość ~~GLOBAL~~.

`address` : Adres rejestru obiektu.

---
&nbsp;

## update <a href="#update" id="update"></a>

Ta metoda umożliwia zmianę adresu rejestru w obiekcie nazwy.

```
names/update/noun
```

To polecenie nie obsługuje rzeczowników `name`, `namespace`, `any`.

### Parametry:

`pin` : Wymagany, jeśli **zablokowany**. PIN do autoryzacji transakcji.

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`name` : Wymagane do **zidentyfikowania** nazwy obiektu name. Nazwa powinna być w formacie nazwa (dla nazw globalnych) username:name (dla nazw lokalnych) lub namespace::name (dla nazw w przestrzeni nazw). Jest to opcjonalne, jeśli podano `address`.

`address` : Wymagane do **określenia** zarejestrowanego adresu nazwy. Jest to opcjonalne, jeśli podano `name`.

`register_address` : Nowy adres rejestru, na który powinna wskazywać ta nazwa.

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

`success` : Flaga logiczna wskazująca, że obiekt został pomyślnie zaktualizowany.

`txid` : Identyfikator (hash) transakcji dla zaktualizowanego obiektu.

---
&nbsp;

## transfer <a href="#transfer" id="transfer"></a>

Spowoduje to zainicjowanie przeniesienia własności określonego rzeczownika.

```
names/transfer/noun
```


> **NOTA:** Można przenosić tylko nazwy globalne lub **nazwy** utworzone w przestrzeni nazw (o nazwie w formacie mynamespace::myname).
> {.is-info}


Ta metoda używa rzeczowników `name` i `namespace`.

##### transfer/name

Spowoduje to przeniesienie własności nazw globalnych i nazw utworzonych w przestrzeni nazw (nazwa w formacie mynamespace::myname) na określonego odbiorcę.

##### transfer/namespace

Spowoduje to przeniesienie własności obiektu przestrzeni nazw na określonego odbiorcę.

### Parametry:

`pin`: Wymagany, jeśli jest zablokowany. PIN do autoryzacji transakcji.

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`recipient` : Wymagany do **zidentyfikowania** konta odbiorcy. Może to być nazwa użytkownika profilu lub hash genesis.

`expires` : Opcjonalne pole umożliwia dzwoniącym określenie **wygaśnięcia** transakcji transferu. Wartość wygaśnięcia to liczba sekund od czasu utworzenia transakcji, po której odbiorca nie może już odebrać transakcji. Z drugiej strony, gdy stosujesz wygaśnięcie transakcji, nie możesz anulować transakcji, dopóki nie upłynie czas wygaśnięcia. Jeśli opcja wygasa jest ustawiona na 0, transakcja nigdy nie wygaśnie, przez co nadawca nie będzie mógł nigdy anulować transakcji. W przypadku pominięcia zostanie zastosowany domyślny okres wygaśnięcia wynoszący 7 dni (604800 sekund).

##### transfer/name

`name` : Wymagane do **zidentyfikowania** Nazwy nazwy obiektu. Nazwa powinna mieć format username:name (w przypadku nazw lokalnych) lub namespace::name (w przypadku nazw w przestrzeni nazw). Jest to opcjonalne, jeśli podano nazwę `address`.

`address` : Wymagane do **określenia** adresu rejestru elementu. Jest to opcjonalne, jeśli podano `name`.

##### transfer/namespace

`namespace` : Wymagane do **zidentyfikowania** nazwy obiektu przestrzeni nazw. Jest to opcjonalne, jeśli podano przestrzeń nazw `address`.

`address` : Wymagane do **zidentyfikowania** adresu rejestru przestrzeni nazw. Jest to opcjonalne, jeśli podano `namespace`.

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
{
    "success": true,
    "address": "8LBEGF1Yo3UR2HPtVVokZMpmAespLfDdPdt99cpKiFJ7VSufsJ5",
    "txid": "017c673317370ea713d29d5743e4affc5fc7f9572ebecb8f4aac3a729a139b8b3e0dc7d30868328fb00f29324d365f381a4cb079bf86ef707954a1510a29053a"
}
[Completed in 4999.664459 ms]
```

#### Zwracane wartości:

`txid` : Identyfikator (hash) transakcji, która zawiera przeniesienie nazwy.

`address`: Adres rejestru dla tej nazwy.

---
&nbsp;

## claim <a href="#claim" id="claim"></a>

Ta metoda przejmie własność określonego rzeczownika przez odbiorcę, aby zakończyć odpowiednią transakcję transferu.

```
nazwiska/roszczenie/rzecz
```

Ta metoda używa rzeczowników `nazwa` i `przestrzeń nazw`.

##### roszczenie/nazwa

Nazwiska, które zostały przeniesione, muszą zostać zgłoszone przez odbiorcę. Ta metoda tworzy transakcję roszczenia.

##### roszczenie/przestrzeń nazw

Przestrzenie nazw, które zostały przeniesione, muszą zostać zgłoszone przez odbiorcę. Ta metoda tworzy transakcję roszczenia.

### Parametry:

`pin`: wymagany, jeśli jest zablokowany. PIN do autoryzacji transakcji.

`session` : wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`txid`: Wymagany **identyfikator transakcji** (hash) transakcji przeniesienia nazwy, dla której żądany jest.

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
{
    "przejęte":
    [
        "25428293b6631d2ff55b3a931926fec920e407a56f7759495e36089914718d68",
        "1ff463e036cbde3595fbe2de9dff15721a89e99ef3e2e9bfa7ce48ed825e9ec2"
    ],
    "txid": "27ef3f31499b6f55482088ba38b7ec7cb02bd4383645d3fd43745ef7fa3db3d1"
}
```

#### Rezygnacja







