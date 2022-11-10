---
title: RYNEK
description: API rynku
published: true
date: 2022-11-10T00:04:00.165Z
tags: 
editor: markdown
dateCreated: 2022-10-24T22:30:41.330Z
---

# RYNEK

Market API to oparty na księdze zleceń rynek P2P do handlu tokenami i aktywami. Aktywa mogą obejmować zarówno towary cyfrowe, jak i fizyczne. Użytkownicy zaczynają od stworzenia nowego rynku z parą tokenów (NXS/XYZ), a inni użytkownicy mogą uczestniczyć w tym konkretnym rynku, wykonać określone zlecenie lub anulować złożone zlecenie.

## Jak kwotowane są ceny rynkowe

Każda para rynkowa reprezentuje aktualny kurs wymiany dla dwóch tokenów. Oto jak zinterpretować te informacje, używając jako przykładu market=NXS/XYZ lub kursu wymiany Nexus na XYZ:

> Aktualna cena to ostatnia cena handlowa i nie ma nic wspólnego z ceną kupna lub sprzedaży.
{.is-info}


* Token po lewej stronie (NXS) to token bazowy.
* Token po prawej (XYZ) to token notowany.
* Podana cena oznacza, jaka część tokenu notowanego jest potrzebna do zakupu 1 jednostki tokenu bazowego. W rezultacie token bazowy jest zawsze wyrażany jako 1 jednostka, podczas gdy waluta notowana różni się w zależności od aktualnego rynku i tego, ile jest potrzebne do zakupu 1 jednostki waluty bazowej.
* Jeśli kurs wymiany NXS/XYZ wynosi 1.2, oznacza to, że 1 NXS kupi 1.20 XYZ (lub, mówiąc inaczej, zakup 1 NXS będzie kosztował 1.20 XYZ).
* Gdy kurs rynkowy rośnie, oznacza to, że wartość tokena bazowego wzrosła w stosunku do tokena notowanego (ponieważ 1 NXS kupi więcej tokenów XYZ) i odwrotnie, jeśli kurs rynkowy spadnie, oznacza to, że wartość tokena bazowego spadła.


> **Nota:** Pary rynkowe są zazwyczaj prezentowane jako pierwszy token bazowy, a jako drugi token notowany. API rynku pozwala na użycie rynku odwrotnego=XYZ/NXS i traktowanie go jako bid/ask w zależności od rzeczownika.
{.is-info}

![market-quote-nxs-token.png](/market-quote-nxs-token.png)<p align=center>*Wycena Rynkowa: NXS-token*</p>

![market-quote-token1-token2.png](/market-quote-token1-token2.png)<p align=center>*Wycena Rynkowa: token1-token2*</p>

W pełni obsługiwany punkt końcowy rynku URI jest następujący:

````
market/verb/noun/filter/operator
````

Minimalne wymagane składniki identyfikatora URI to:

````
market/verb/noun
````
---
&nbsp;

## Obsługiwane czasowniki (verbs)

Następujące czasowniki są obecnie obsługiwane przez ten zestaw poleceń interfejsu API:

[`create`](#create) - Tworzy nowy rynek lub staje się częścią już istniejącego.
[`list`](#list) — Lista wszystkich zamówień dla określonego rynku.
[`execute`](#execute) — Pełne wypełnienie określonego zlecenia rynkowego.
[`cancel`](#cancel) - Aby anulować określone zlecenie rynkowe.
[`user`](#user) — Pobiera wszystkie zlecenia rynkowe dla profilu.

---
&nbsp;

## Obsługiwane rzeczowniki (nouns)

W tym zestawie poleceń interfejsu API obsługiwane są następujące rzeczowniki:

[`bid`] - Zlecenie rynkowe złożone, aby kupić token lub aktywa.
[`ask`] - Zlecenie rynkowe złożone w celu sprzedaży tokena lub aktywów.
[`order`] - Zlecenie rynkowe, które może być kupnem lub zapytaniem.
[`executed`] - Zlecenie rynkowe, które zostało wypełnione.

---
&nbsp;

## create <a href="#create" id="create"></a>

Ta metoda tworzy nową parę rynków lub staje się częścią istniejącego rynku reprezentowanego przez token lub parę aktywów token1/token2. Para rynkowa token2/token1 jest również częścią tego samego rynku.

````
market/create/noun
````

To polecenie obsługuje rzeczowniki `bid` i `ask`.

##### create/bid

Tworzy to zlecenie rynkowe **bid** dla market=token1/token2, **ask** dla market=token2/token1

##### create/ask

Aby utworzyć zlecenie rynkowe **ask** dla market=token1/token2, **bid** dla market=token2/token1

> Gdy rynek=token1/token2 zostanie odwrócony na rynek=token2/token1 cena musi zostać odpowiednio zmieniona. Para rynkowa jest określona przez pierwsze zlecenie, które tworzy rynek.
{.is-info}


### Parametry:

`pin` : Wymagany, jeśli **zablokowane**. Kod PIN do autoryzacji transakcji.

`session` : Wymagane przez **argument** `-multiuser=1` do identyfikacji sesji. W trybie API pojedynczego użytkownika nie należy podawać `session`.&#x20;

`market` : token1/token2 - Para tokenów, dla której tworzone jest zlecenie.

`amount` : Kwota tokena2 do wymiany.

`price` : Cena tokena2 w stosunku do tokena1.

`to` : To jest nazwa konta odbiorczego lub adres rejestracyjny do tokena1.

`from` : Jest to nazwa konta wysyłającego lub adres rejestru do obciążenia tokena2.

### Wyniki:

#### Zwracana wartość obiektu JSON:

```
{
    "success": true,
    "address": "8CupQ2dym1CZGZZ7U3F8UQ2xR2fr2PZmtEqB5Ds2EJsG1jA3JZw",
    "txid": "012bc5f80460a9605706e643f9364722e97ffe3dd4e94bce8e41ea6ae70b3336fe6274cfe74583bf72cf77d8bbdc951ae1b25c706253590e0c6d74fa4f78f4df"
}
[Completed in 4991.918611 ms]
```

#### Zwracane wartości:

`txid` : Hash transakcji, który został wygenerowany dla tego TX. Jeśli używasz `-autotx` to pole zostanie pominięte.

`address` : Adres rejestracyjny dla tego konta. Adres (lub nazwa, które haszuje na ten adres) jest potrzebny podczas tworzenia uznania lub obciążenia konta.

---
&nbsp;

## list <a href="#list" id="list"></a>

Utwórz nowy rejestr obiektów określony przez podany rzeczownik.

````
market/list/noun
````

To polecenie obsługuje wszystkie rzeczowniki.

### Parametry:

`pin` : Wymagany, jeśli **zablokowane**. Kod PIN do autoryzacji transakcji.

`session` : Wymagane przez **argument** `-multiuser=1` do identyfikacji sesji. W trybie API pojedynczego użytkownika nie należy podawać `session`.&#x20;

`market` : Wymagany do **identyfikacji** pary tokenów rynkowych.

### Wyniki:

#### Zwracana wartość obiektu JSON:

```
{
    "bids": [
        {
            "txid": "012bc5f80460a9605706e643f9364722e97ffe3dd4e94bce8e41ea6ae70b3336fe6274cfe74583bf72cf77d8bbdc951ae1b25c706253590e0c6d74fa4f78f4df",
            "timestamp": 1655815697,
            "owner": "b7392196b83aca438567558462cd0c5d982569c7cefa668500c4bf3e61a03b7a",
            "market": "XYZ/BIT",
            "price": 1.0,
            "type": "bid",
            "contract": {
                "OP": "DEBIT",
                "from": "8CupQ2dym1CZGZZ7U3F8UQ2xR2fr2PZmtEqB5Ds2EJsG1jA3JZw",
                "amount": 10.0,
                "token": "8EdBM41i1MAgb7w2tjEsdd7DeKntUcsw4JWK1LswW457e2jDa8a",
                "ticker": "BIT"
            },
            "order": {
                "OP": "DEBIT",
                "to": "8Cu9QHELK6ofHzbAwtWGnUcfkDz3zvGoSf7eDGZfh81AeMuqcYY",
                "amount": 10.0,
                "token": "8DXmAmkTtysSZUxM3ePA8wRmbSUofuHKSoCyDpN28aLuSrm1nDG",
                "ticker": "XYZ"
            }
        }
    ],
    "asks": [
        {
            "txid": "016d62c69f05a82eefb463604325dd0331aeee787748a06619d6ca665c5a0576705c62de29f20c3eccfb8cbb25c4df169a53baa1e55493f5293fbbf864af7389",
            "timestamp": 1655817006,
            "owner": "b7a57ddfb001d5d83ab5b25c0eaa0521e6b367784a30025114d07c444aa455c0",
            "market": "XYZ/BIT",
            "price": 1.0,
            "type": "ask",
            "contract": {
                "OP": "DEBIT",
                "from": "8B9adrgaFX8hZvH1vQGjibHVYhsLuDTDu2Kn1FM25RZQtuUFyiE",
                "amount": 10.0,
                "token": "8DXmAmkTtysSZUxM3ePA8wRmbSUofuHKSoCyDpN28aLuSrm1nDG",
                "ticker": "XYZ"
            },
            "order": {
                "OP": "DEBIT",
                "to": "8C3AiDrbDmbkeza1eBeeEJ2r5wqrnWGr9D1kewKqHfPzdY7jRkF",
                "amount": 10.0,
                "token": "8EdBM41i1MAgb7w2tjEsdd7DeKntUcsw4JWK1LswW457e2jDa8a",
                "ticker": "BIT"
            }
        }
    ]
}
```

#### Zwracane wartości:

`order` : Tablica dla różnych typów zamówień `bid` lub `ask`.

`txid` : Hash transakcji, który został wygenerowany dla tego TX. Jeśli używasz `-autotx` to pole zostanie pominięte.

`timestamp` : Uniksowy znacznik czasu utworzenia transakcji.

`owner` : Hash nazwy użytkownika profilu, do którego należy to konto.

`market` : Rynek, dla którego są wystawiane zlecenia.

`price` : Cena za to konkretne zamówienie.

`type` : Typ zamówienia `bid` lub `ask`.

`contracts` : Tablica kontraktów powiązanych z tą transakcją oraz ich szczegóły z kodami operacyjnymi.

`OP` : Operacja kontraktu. Może to być `APPEND`, `CLAIM`, `COINBASE`, `CREATE`, `CREDIT`, `DEBIT`, `FEE`, `GENESIS`, `LEGACY`, `TRANSFER`, `TRUST`, `STAKE`, `UNSTAKE`, `WRITE`.

`from` : W przypadku transakcji `DEBIT` i `CREDIT`, adres rejestru konta nadawcy.

`to` : W przypadku transakcji `DEBIT` i `CREDIT`, adres rejestru konta odbiorcy.

`amount` : Kwota tokena transakcji.

`token` : Adres rejestru tokena, którego dotyczy transakcja. Ustaw na 0 dla transakcji NXS.

`ticker` : Globalna nazwa przypisana do tokena.

`address` : Adres rejestracyjny dla tego konta. Adres (lub nazwa, które haszuje na ten adres) jest potrzebny podczas tworzenia uznania lub obciążenia konta.

---
&nbsp;

## wykonaj <a href="#execute" id="execute"></a>

Utwórz nowy rejestr obiektów określony przez podany rzeczownik.

````
rynek/lista/rzeczownik
````

To polecenie obsługuje rzeczowniki `bid` i `ask`.

### Parametry:

`pin` : Wymagane, jeśli **zablokowane**. Kod PIN do autoryzacji transakcji.

`session` : Wymagane przez **argument** `-multiuser=1` do identyfikacji sesji. W trybie API pojedynczego użytkownika nie należy podawać `sesji`.&#x20;

`txid`: identyfikator transakcji realizowanej oferty /ask.

`to` : To jest nazwa konta odbiorczego lub adres rejestracyjny do tokena1.

`from` : To jest nazwa konta wysyłającego lub adres rejestru do obciążenia tokena2

### Wyniki:

#### Zwracana wartość obiektu JSON:

````
{
    "sukces": prawda,
    "adres": "8CupQ2dym1CZGZZ7U3F8UQ2xR2fr2PZmtEqB5Ds2EJsG1jA3JZw",
    "txid": "012bc5f80460a9605706e643f9364722e97ffe3dd4e94bce8e41ea6ae70b3336fe6274cfe74583bf72cf77d8bbdc951ae1b25c706253590e0c6d74fa4f78f4df"
}
[Ukończono w 4991.918611 ms]
````

#### Zwracane wartości:

`success` : flaga logiczna wskazująca, że ​​zamówienie zostało wykonane pomyślnie.

`txid` : Hash transakcji, który został wygenerowany dla tego TX. Jeśli używasz `-autotx` to pole zostanie pominięte.

`address` : adres rejestracyjny dla tego konta. Adres (lub imię i nazwisko, które haszuje na ten adres) jest potrzebny podczas tworzenia uznania lub obciążenia konta.

---
&nbsp;

## cancel <a href="#cancel" id="cancel"></a>

Utwórz nowy rejestr obiektów określony przez podany rzeczownik.

````
rynek/lista/rzeczownik
````

To polecenie obsługuje rzeczowniki `bid i` `ask`.

### Parametry:

`pin` : Wymagane, jeśli **zablokowane**. Kod PIN do autoryzacji transakcji.

`session` : Wymagane przez **argument** `-multiuser=1` do identyfikacji sesji. W trybie API pojedynczego użytkownika nie należy podawać `sesji`.&#x20;

`txid` : Hash transakcji dla zamówienia, które ma zostać anulowane.

### Wyniki:

#### Zwracana wartość obiektu JSON:

````
{
    "sukces": prawda,
    "txid": "010b0dbb226835c59b62d0761feac027cceb75ceb7d8d52abbd8072158415cf8c210af810f4d41ee6ad86dc6d754a17a0269db9025ba47becdb87a19ee71e99f"
}
[Ukończono w 4976,551936 ms]
````

#### Zwracane wartości:

`success` : flaga logiczna wskazująca, że ​​anulowanie zamówienia powiodło się.

`txid` : skrót transakcji wygenerowany w celu anulowania zamówienia. Jeśli używasz `-autotx` to pole zostanie pominięte.

---
&nbsp;

## użytkownik <a href="#user" id="user"></a>

Pobiera zamówienia rynkowe użytkowników na podstawie rzeczownika.

````
rynek/lista/rzeczownik
````

To polecenie obsługuje rzeczowniki `order` i `executed`.

### Parametry:

`pin` : Wymagane, jeśli **zablokowane**. PIN do autoryzacji transakcji.

`session` : Wymagane przez **argument** `-multiuser=1` w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika nie należy podawać sesji.

`token` : Wymagany do **identyfikacji** tokena, dla którego żądane są dane.

[`Sortowanie`](/pl/tryt++/sortowanie)

[`Filtrowanie`](/pl/tryt++/filtrowanie)

[`Operatorzy`](/pl/tryt++/operatorzy)

### Wyniki:

#### Zwracana wartość obiektu JSON:

````
{
    "sukces": prawda,
    "adres": "8CupQ2dym1CZGZZ7U3F8UQ2xR2fr2PZmtEqB5Ds2EJsG1jA3JZw",
    "txid": "012bc5f80460a9605706e643f9364722e97ffe3dd4e94bce8e41ea6ae70b3336fe6274cfe74583bf72cf77d8bbdc951ae1b25c706253590e0c6d74fa4f78f4df"
}
[Ukończono w 4991.918611 ms]
````

#### Zwracane wartości:

`txid` : Hash transakcji, który został wygenerowany dla tego TX. Jeśli używasz `-autotx` to pole zostanie pominięte.

`address` : adres rejestracyjny dla tego konta. Adres (lub imię i nazwisko, które haszuje na ten adres) jest potrzebny podczas tworzenia uznania lub obciążenia konta.

