---
title: FAKTURY
description: API faktur
published: true
date: 2023-01-05T23:39:58.541Z
tags: 
editor: markdown
dateCreated: 2023-01-05T23:00:33.647Z
---

# API faktur
--------------------------------------------------
Interfejs API faktur zapewnia użytkownikom i twórcom aplikacji możliwość wystawiania i opłacania faktur w łańcuchu blokowym Nexus. W pełni obsługiwany punkt końcowy identyfikatora URI faktury jest następujący:

```
invoices/verb/noun/filter/operator
```

Minimalne wymagane elementy identyfikatora URI to:

```
invoices/verb/noun
```

## Obsługiwane czasowniki (verbs)

Poniższe czasowniki są obecnie obsługiwane przez ten zestaw poleceń interfejsu API:

[`create`](#create) - Generuje nowy obiekt obsługiwanego typu.
[`get`](#get) - Pobierz obiekt obsługiwanego typu.
[`list`](#list) - Lista wszystkich obiektów posiadanych przez danego użytkownika.
[`pay`](#pay) - Wydawaj środki z obsługiwanego typu.
[`cancel`](#cancel) - Aby anulować utworzoną fakturę.
[`history`](#history) - Wygeneruj historię wszystkich ostatnich stanów.
[`transactions`](#transactions) - Lista wszystkich transakcji, które zmodyfikowały określony obiekt.


## Obsługiwane rzeczowniki (nouns)

Ten zestaw poleceń interfejsu API obsługuje następujące rzeczowniki:

[`invoice`] - Rejestr obiektów zawierający token-id i saldo.
[`outstanding`] - Wygeneruj historię wszystkich ostatnich stanów.
[`paid`] - Zgłoś żądanie określonego rejestru obiektów.
[`cancelled`] - Przejmij określony rejestr obiektów.



## <a name="create"></a> create

Utwórz nowy obiekt faktury.

```
invoices/create/noun
```

To polecenie obsługuje tylko rzeczownik faktury.

### Parametry:

`pin` : Wymagany, jeśli **zablokowany**. PIN do autoryzacji transakcji.

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`name` : Opcjonalne do **identyfikacji** faktury. Jeśli zostanie podana, obiekt Nazwa zostanie również utworzony w lokalnej przestrzeni nazw użytkownika, umożliwiając dostęp do faktury/pobieranie jej według nazwy. Jeśli nazwa nie zostanie podana, konto będzie wymagało dostępu/pobrania za pomocą jego 256-bitowego adresu w rejestrze.

`account` : Wymagane do **zidentyfikowania** konta, na które ma zostać opłacona faktura. Konto powinno mieć format username:name (dla nazw lokalnych) lub namespace::name.

`account` : Wymagane do **zidentyfikowania** 256-bitowego adresu w rejestrze konta, na które należy zapłacić fakturę. Jest to opcjonalne, jeśli podano „nazwa”.

`recipient` : Wymagany do **identyfikacji** odbiorcy faktury. Może to być nazwa użytkownika identyfikująca konto użytkownika (sig-chain) lub skrót genezy łańcucha podpisów, na który ma zostać wystawiona faktura.

`items` : Tablica pozycji składających się na tę fakturę. Należy uwzględnić co najmniej jeden element w tablicy items. Całkowita kwota faktury jest obliczana jako suma wszystkich kwot pozycji, a kwota każdej pozycji jest obliczana jako kwota jednostki pomnożona przez jednostki.

`description` : Opis elementu zamówienia.

`amount` : Kwota jednostkowa do zafakturowania dla tej pozycji. Kwotę tę należy podać w walucie rachunku płatniczego.

`units` : Liczba jednostek do zafakturowania według kwoty jednostkowej.


### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
"result": {
		"success": true,
		"address": "81N7yg7NJa66v8Nmh4eSeYk7QTbxjxgnLF6CLQQrH5zoHmfY6br",
		"txid": "011a2561abc7ec305e288ea73b6346f92ac63a6cca17d931fd47fddc2beb8ee19cd2c73a1ae4e1ead36487b6b672dc2c8f781cbf0339fbd6b8a7869fcbff410c"
	}
```

#### Zwracane wartości:

`success`: Flaga logiczna wskazująca, że faktura została utworzona pomyślnie.

`address` : Adres rejestracyjny dla faktury. Adres jest potrzebny przy pobieraniu lub opłaceniu faktury.

`txid` : Identyfikator (hash) transakcji, która obejmuje utworzenie faktury.

--------------------------------------------------

## <a name="get"></a> get

Pobiera informacje o fakturze.

```
invoices/get/noun
```

To polecenie obsługuje tylko rzeczownik faktury.

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`name` : Wymagane do **określenia** nazwy faktury. Nazwa powinna mieć format username:name (dla nazw lokalnych). Jest to opcjonalne, jeśli podano `address`.

`address` : Wymagany do **określenia** adresu rejestracji faktury. Jest to opcjonalne, jeśli podano `name`.


### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
[
    {
        "address": "822G7ZSsHh1ncTj4AJt6FnZ6MTWG3Q9NNTZ9KvG3CWA1SP3aq97",
        "created": 1581389015,
        "modified": 1581389107,
        "owner": "a2056d518d6e6d65c6c2e05af7fe2d3182a93def20e960fcfa0d35777a082440",
        "account": "8Bx6ZmCev3DsGjoWuhfQSNmycdZT4cyKKJNc36NWTMik6Zkqh7N",
        "recipient": "a2056d518d6e6d65c6c2e05af7fe2d3182a93def20e960fcfa0d35777a082440",
        "number": "0004",
        "PO": "Purch1234",
        "contact": "accounts@mycompany.com",
        "sender_detail": "My Company, 32 Some Street, Some Place",
        "recipient_detail": "Some recipient details such as address or email",
        "items": [
            {
                "description": "First item description",
                "base_price": 1.0,
                "tax": 0.1,
                "unit_amount": "1.1",
                "units": 3
            },
            {
                "description": "Second item description",
                "base_price": 5.0,
                "tax": 0.5,
                "unit_amount": "5.5",
                "units": 1
            }
        ],
        "amount": 8.8,
        "token": "0",
        "status": "PAID"
    }
]
```

#### Zwracane wartości:

`owner` : Hash nazwy użytkownika profilu właściciela.

`created` : Sygnatura czasowa systemu UNIX podczas tworzenia faktury.

`modified` : Sygnatura czasowa systemu UNIX, kiedy faktura była ostatnio modyfikowana.

`name` : Nazwa identyfikująca fakturę. Ze względu na prywatność jest to uwzględniane w odpowiedzi tylko wtedy, gdy osoba wywołująca jest właścicielem faktury.

`address` : Adres rejestracji faktury.

`recipient` : Hash genezy łańcucha podpisów, dla którego ma zostać wystawiona faktura.

`account` : Rejestrowy adres konta, na które ma zostać opłacona faktura.

`items` : Tablica pozycji składających się na tę fakturę.

`amount` : Kwota jednostkowa do zafakturowania dla tej pozycji.

`units` : Liczba jednostek do zafakturowania według kwoty jednostkowej.

`description` : Opis elementu zamówienia.

`amount` : Całkowita kwota faktury. Jest to suma łącznych kwot wszystkich pozycji (unit_amount x units).

`token` : Adres rejestru tokena, którym ta faktura powinna być opłacona. Ustaw na 0 dla transakcji NXS.

`status` : Bieżący status tej faktury. Wartości mogą być OUTSTANDING (faktura została wystawiona, ale niezapłacona), PAID (faktura została zapłacona przez odbiorcę) lub CANCELLED (faktura została anulowana przez wystawcę przed dokonaniem płatności).

--------------------------------------------------

## <a name="list"></a> list

Spowoduje to wyświetlenie wszystkich faktur wystawionych lub otrzymanych przez łańcuch podpisów.

```
nvoices/list/noun
```

To polecenie obsługuje wszystkie rzeczowniki.

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`genesis` : Hash genezy identyfikujący łańcuch sygnatur (opcjonalnie, jeśli podano nazwę użytkownika).

`username`: Nazwa użytkownika identyfikująca łańcuch sygnatur (opcjonalna, jeśli podano genezę).

`status` : Opcjonalne filtrowanie według statusu faktury. Wartości mogą być OUTSTANDING (faktura została wystawiona, ale nie zapłacona), PAID (faktura została zapłacona przez odbiorcę) lub CANCELLED (faktura została anulowana przez wystawcę przed dokonaniem płatności).

`limit` : Liczba rekordów do zwrócenia dla bieżącej strony. Wartość domyślna to 100.

`page` : Umożliwia zwracanie wyników według stron (liczonych od zera). Np. przekazanie page=1 zwróci drugi zestaw rekordów (limit). Wartość domyślna to 0, jeśli nie została podana.

`offset`: Alternatywa dla strony, przesunięcie może być użyte do zwrócenia zestawu (limitów) wyników z określonego indeksu.

`where` : Tablica klauzul do filtrowania wyników JSON. Więcej informacji na temat filtrowania wyników z metod API /list/xxx można znaleźć tutaj [Filtrowanie](https://wiki.nexus.io/pl/tritium++/filtering).

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
[
    {
        "address": "822G7ZSsHh1ncTj4AJt6FnZ6MTWG3Q9NNTZ9KvG3CWA1SP3aq97",
        "created": 1581389015,
        "modified": 1581389107,
        "owner": "a2056d518d6e6d65c6c2e05af7fe2d3182a93def20e960fcfa0d35777a082440",
        "account": "8Bx6ZmCev3DsGjoWuhfQSNmycdZT4cyKKJNc36NWTMik6Zkqh7N",
        "recipient": "a2056d518d6e6d65c6c2e05af7fe2d3182a93def20e960fcfa0d35777a082440",
        "number": "0004",
        "PO": "Purch1234",
        "contact": "accounts@mycompany.com",
        "sender_detail": "My Company, 32 Some Street, Some Place",
        "recipient_detail": "Some recipient details such as address or email",
        "items": [
            {
                "description": "First item description",
                "base_price": 1.0,
                "tax": 0.1,
                "unit_amount": "1.1",
                "units": 3
            },
            {
                "description": "Second item description",
                "base_price": 5.0,
                "tax": 0.5,
                "unit_amount": "5.5",
                "units": 1
            }
        ],
        "amount": 8.8,
        "token": "0",
        "status": "PAID"
    }
]
```

#### Zwracane wartości:

`owner` : Hash nazwy użytkownika profilu właściciela.

`created` : Sygnatura czasowa systemu UNIX podczas tworzenia faktury.

`modified` : Sygnatura czasowa systemu UNIX, kiedy faktura była ostatnio modyfikowana.

`name` : Nazwa identyfikująca fakturę. Ze względu na prywatność jest to uwzględniane w odpowiedzi tylko wtedy, gdy osoba dzwoniąca jest właścicielem faktury.

`address` : Adres rejestracji faktury.

`recipient` : Hash genezy łańcucha podpisów, dla którego ma zostać wystawiona faktura.

`account` : Rejestrowy adres konta, na które ma zostać opłacona faktura.

`items` : Tablica pozycji składających się na tę fakturę.

`amount` : Kwota jednostkowa do zafakturowania dla tej pozycji.

`unit` : Liczba jednostek do zafakturowania według kwoty jednostkowej.

`description` : Opis elementu zamówienia.

`amount` : Całkowita kwota faktury. Jest to suma łącznych kwot wszystkich pozycji (unit_amount x units).

`token` : Adres rejestru tokena, którym ta faktura powinna być opłacona. Ustaw na 0 dla transakcji NXS.

`status` : Bieżący status tej faktury. Wartości mogą być OUTSTANDING (faktura została wystawiona, ale niezapłacona), PAID (faktura została zapłacona przez odbiorcę) lub CANCELLED (faktura została anulowana przez wystawcę przed dokonaniem płatności).

--------------------------------------------------

## <a name="pay"></a> pay

Dokonaj płatności (obciążenia) w celu uregulowania faktury.

```
invoices/pay/noun
```

To polecenie obsługuje tylko rzeczownik faktury.

### Parametry:

`pin` : Wymagany, jeśli **zablokowany**. PIN do autoryzacji transakcji.

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`name` : Wymagane do **określenia** nazwy faktury. Nazwa powinna mieć format username:name (dla nazw lokalnych). Jest to opcjonalne, jeśli podano `address`.

`address` : Wymagany do **określenia** adresu rejestracji faktury. Jest to opcjonalne, jeśli podano `name`.

`from` : Wymagane do **zidentyfikowania** konta do obciążenia (zapłać fakturę z). Powinien mieć format username:name (w przypadku nazw lokalnych) lub namespace::name (w przypadku nazw w przestrzeni nazw) lub adres rejestru konta do obciążenia (zapłać fakturę z).

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
{
    "txid": "318b86d2c208618aaa13946a3b75f14472ebc0cce9e659f2830b17e854984b55606738f689d886800f21ffee68a3e5fd5a29818e88f8c5b13b9f8ae67739903d"
}
```

#### Zwracane wartości:

`txid` : Identyfikator (hash) transakcji, która obejmuje DEBIT do zapłaty za fakturę i CLAIM do żądania własności faktury.

--------------------------------------------------

## <a name="cancel"></a> cancel

Anuluje niezapłaconą fakturę, aby własność powróciła do łańcucha podpisów wystawców.

```
invoices/cancel/noun
```

To polecenie obsługuje tylko rzeczowniki „faktura” i „zaległe”.

### Parametry:

`pin` : Wymagany, jeśli **zablokowany**. PIN do autoryzacji transakcji.

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`name` : Wymagane do **określenia** nazwy faktury. Nazwa powinna mieć format username:name (dla nazw lokalnych). Jest to opcjonalne, jeśli podano `address`.

`address` : Wymagany do **określenia** adresu rejestracji faktury. Jest to opcjonalne, jeśli podano `name`.

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
{
    "txid": "318b86d2c208618aaa13946a3b75f14472ebc0cce9e659f2830b17e854984b55606738f689d886800f21ffee68a3e5fd5a29818e88f8c5b13b9f8ae67739903d"
}
```

#### Zwracane wartości:

`txid` : Identyfikator (hash) transakcji, która obejmuje DEBIT do zapłaty za fakturę i CLAIM do żądania własności faktury.

--------------------------------------------------

## <a name="history"></a> history

Spowoduje to uzyskanie historii transakcji dla faktury pokazującej, kiedy została utworzona i przeniesiona (dwie umowy, które mają miejsce w tym samym momencie, gdy tworzona jest faktura) i zażądana (zapłacona lub anulowana).

```
invoices/history/noun
```

To polecenie obsługuje wszystkie rzeczowniki.

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`name` : Wymagane do **określenia** nazwy faktury. Nazwa powinna mieć format username:name (dla nazw lokalnych). Jest to opcjonalne, jeśli podano `address`.

`address` : Wymagany do **określenia** adresu rejestracji faktury. Jest to opcjonalne, jeśli podano `name`.

### Wyniki:

#### Wartość zwracana Obiekt JSON:

```
[
    {
        "owner": "b7a57ddfb001d5d83ab5b25c0eaa0521e6b367784a30025114d07c444aa455c0",
        "version": 1,
        "created": 1658006314,
        "modified": 1658006314,
        "type": "READONLY",
        "json": {
            "account": "8CAJbt8MJUXsUzd5J4VVnhtcHuLqeV27Tixs3arGewAic7ZZQmE",
            "recipient": "b7fa11647c02a3a65a72970d8e703d8804eb127c7e7c41d565c3514a4d3fdf13",
            "items": [
                {
                    "amount": 2.0,
                    "units": 1
                },
                {
                    "amount": 0.24,
                    "units": 3
                }
            ],
            "address": "8CAJbt8MJUXsUzd5J4VVnhtcHuLqeV27Tixs3arGewAic7ZZQmE",
            "reference": "Rado ",
            "description": "rado Aviator 2",
            "number": "2",
            "sender_detail": "Alice",
            "amount": 2.72,
            "token": "8DS2qGLhuEC2reKrzxyWaXXwtVq2KmGWGQCWKBQwrCQc4XS2b8V"
        },
        "address": "82UKk7weRui3d8HuZrMuoD5h49anQgpKUJm8CPkbsGNHwuu3FVv",
        "action": "CREATE"
    },
    {
        "owner": "00a57ddfb001d5d83ab5b25c0eaa0521e6b367784a30025114d07c444aa455c0",
        "version": 1,
        "created": 1658006314,
        "modified": 1658006314,
        "type": "READONLY",
        "json": {
            "account": "8CAJbt8MJUXsUzd5J4VVnhtcHuLqeV27Tixs3arGewAic7ZZQmE",
            "recipient": "b7fa11647c02a3a65a72970d8e703d8804eb127c7e7c41d565c3514a4d3fdf13",
            "items": [
                {
                    "amount": 2.0,
                    "units": 1
                },
                {
                    "amount": 0.24,
                    "units": 3
                }
            ],
            "address": "8CAJbt8MJUXsUzd5J4VVnhtcHuLqeV27Tixs3arGewAic7ZZQmE",
            "reference": "Rado ",
            "description": "rado Aviator 2",
            "number": "2",
            "sender_detail": "Alice",
            "amount": 2.72,
            "token": "8DS2qGLhuEC2reKrzxyWaXXwtVq2KmGWGQCWKBQwrCQc4XS2b8V"
        },
        "address": "82UKk7weRui3d8HuZrMuoD5h49anQgpKUJm8CPkbsGNHwuu3FVv",
        "action": "TRANSFER"
    }
]
[Completed in 1.392150 ms]
```

#### Zwracane wartości:

Zwracana wartość to tablica obiektów JSON dla każdego wpisu w historii faktury:

`type`: Akcja, która miała miejsce. - CREATE | TRANSFER | CLAIM

`owner` : Hash nazwy użytkownika profilu właściciela.

`modified` : Uniksowy znacznik czasu aktualizacji faktury.

`checksum` : Suma kontrolna rejestru stanu używana do czyszczenia.

`address` : Adres rejestracji faktury.

`name` : Nazwa faktury.

`data` : Dane faktury JSON.

--------------------------------------------------

## <a name="transactions"></a> transactions

Spowoduje to wyświetlenie wszystkich transakcji dla określonego rzeczownika.

```
faktury/transakcje/rzecz
```

To polecenie obsługuje rzeczowniki konta, zaufania i tokena.

### Parametry:

`session` : wymagane przez **argument** `-multiuser=1` do podania w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika sesja nie powinna być dostarczana.

`verbose` : opcjonalne, określa, ile danych transakcji ma zostać uwzględnionych w odpowiedzi. Obsługiwane wartości to:

- domyślnie: hasz

- podsumowanie: typ, wersja, sekwencja, znacznik czasu, operacja i potwierdzenia.

- szczegóły: genesis, nexthash, prevhash, klucz pubowy i podpis.

Ta metoda obsługuje parametry Sortowanie / Filtrowanie.

### Wyniki:

#### Wartość zwracana Obiekt JSON:









