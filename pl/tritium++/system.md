---
title: SYSTEM
description: System API
published: true
date: 2022-11-04T22:45:47.663Z
tags: 
editor: markdown
dateCreated: 2022-10-24T22:24:00.047Z
---

# SYSTEM

Interfejs API systemu zapewnia publiczny dostęp do informacji o tym węźle. Obejmuje to dane, takie jak wersja oprogramowania, na którym działa węzeł, stan księgi i pamięci, adres IP węzła i liczba podłączonych peerów.

## Bezpośrednie punkty końcowe

Poniższe polecenia są bezpośrednimi punktami końcowymi i dlatego nie obsługują powyższej struktury czasowników i rzeczowników dostępnych powyżej.

[`stop`](#stop)
[`get/info`](#get/info)
[`get/metrics`](#get/metrics)
[`list/peers`](#list/peers)
[`list/lisp-eids`](#list/lisp-eids)
[`validate/address`](#vlaidate/address)

Bezpośrednie punkty końcowe obsługują filtry i operatory.

---
&nbsp;

## stop <a href="#stop" id="stop"></a>

Zainicjuj sekwencję wyłączania węzła.

````
system/stop
````

### Parametry:

`password` : Opcjonalne do **uwierzytelnienia** przed zainicjowaniem zamknięcia rdzenia. To hasło jest tym, które jest podane w pliku konfiguracyjnym, co pomoże zapobiec przypadkowemu zdalnemu zamknięciu.

**Uwaga:** Hasło uwierzytelniające zamknięcie musi być dostarczone z flagą `-system/stop=<password>`

### Wyniki:

#### **Zwrócona wartość obiektu JSON:**

```
"Nexus server stopping"
[Completed in 0.039270 ms]
```

---
&nbsp;

## get/info <a href="#get/info" id="get/info"></a>

Zwraca podsumowanie informacji o tym węźle.



```
system/get/info
```

### Parametry:

`Filtering`

### Wyniki:

#### Zwracana wartość obiektu JSON:

```
{
    "version": "5.1.0-rc2 Tritium++ CLI [LLD][x64]",
    "protocolversion": 3010000,
    "walletversion": 10001,
    "timestamp": 1658759654,
    "hostname": "localhost",
    "directory": "/home/nexus/.Nexus/",
    "address": "11.79.25.105",
    "private": false,
    "hybrid": false,
    "multiuser": false,
    "litemode": false,
    "blocks": 4553990,
    "synchronizing": false,
    "synccomplete": 100,
    "syncprogress": 100,
    "txtotal": 0,
    "connections": 41
}
[Completed in 0.070190 ms]
```

#### Zwracane wartości:

`version` : Wersja oprogramowania demona.

`protocolversion` : Wersja protokołu niższego poziomu (LLP).

`walletversion` : Wersja portfela Legacy.

`timestamp` : Bieżący ujednolicony czas zgłoszony przez ten węzeł.

`hostname` : Nazwa hosta komputera lokalnego.

`ipaddress` : Publiczny adres IP komputera lokalnego widziany przez peerów, z którymi jesteś połączony. To pole będzie puste, dopóki nie będziesz mieć co najmniej jednego połączenia równorzędnego.

`testnet` : Jeśli ten węzeł działa w sieci testowej, to pokazuje numer sieci testowej.

`private` : Czy ten węzeł działa w trybie prywatnym.

`multiuser` : Czy ten węzeł działa w trybie wielu użytkowników.

`sessions` : Zwracane tylko w trybie wielu użytkowników. Pokazuje liczbę sesji użytkowników aktualnie zalogowanych w węźle.

`clientmode` : Flaga wskazująca, czy ten węzeł działa w trybie klienta.

`nolegacy` : Flaga wskazująca, czy ten węzeł został skompilowany z obsługą portfela Legacy UTxO. Jeśli nie, wszystkie starsze funkcje portfela (dostępne za pośrednictwem starszego RPC) nie są dostępne. Ta flaga jest obecnie pomijana w odpowiedzi, jeśli została skompilowana ze wsparciem wersji Legacy, dlatego zostanie uwzględniona tylko wtedy, gdy jest prawdziwa.

`blocks` : Bieżąca wysokość bloku tego węzła.

`synchronizing` : Flaga wskazująca, czy ten węzeł jest aktualnie synchronizowany. Nieuwzględnione, jeśli private=true.

`synccomplete` : Procent łącznej liczby pobranych bloków.

`syncprogress` : Procent ukończonej bieżącej synchronizacji w stosunku do momentu uruchomienia węzła.

`txtotal` : Liczba transakcji w pamięci węzła.

`connections` : Liczba połączeń równorzędnych.

`eids` : Tablica identyfikatorów punktów końcowych LISP (EID) dla tego węzła. Nieuwzględnione, chyba że ten węzeł używa LISP.

---
&nbsp;

## get/metrics <a href="#get/metrics" id="get/metrics"></a>

Zwraca metryki i statystyki dla księgi głównej, rejestrów, sigchains, zaufania i rezerw.

```
system/get/metrics
```

### Parametry:

[`Filtering`](/en/tritium++/filtering)

### Wyniki:

#### Zwracana wartość obiektu JSON:

```
{
    "registers": {
        "total": 183908,
        "names": {
            "global": 38,
            "local": 60668,
            "namespaced": 29
        },
        "namespaces": 14,
        "objects": {
            "accounts": 91400,
            "assets": 123,
            "crypto": 30362,
            "tokenized": 51,
            "tokens": 134
        },
        "state": {
            "raw": 0,
            "readonly": 706
        }
    },
    "sigchains": 30351,
    "trust": {
        "total": 501,
        "stake": 30155872.897004,
        "trust": 8360292851
    },
    "reserves": {
        "ambassador": 332.180905,
        "developer": 222.343689,
        "fee": 108889.217,
        "hash": 91.32012,
        "prime": 32.78941
    }
}
[Completed in 1020.804545 ms]
```

#### Zwracane wartości:

`rejestry` : Statystyki w bazie danych rejestrów.
{
`names` : Całkowita liczba rejestrów nazw, w tym użytkowników lokalnych, globalnych i przestrzeni nazw.\
{
`global` : Liczba nazw, które zostały utworzone w globalnej przestrzeni nazw.

`local` : Liczba nazw, które zostały utworzone w lokalnej przestrzeni nazw.

`namespaced` : Liczba nazw, które zostały utworzone w przestrzeni nazw.\
}

`przestrzenie nazw` : Liczba przestrzeni nazw, które zostały utworzone.

`objects` : Statystyka niestandardowych rejestrów obiektów. Należą do nich konta, tokeny, krypto, aktywa, przedmioty i wszelkie inne pochodne rejestry obiektów.
{
`accounts`: Liczba rejestrów kont. Obejmuje to zarówno konta NXS, jak i inne konta tokenowe.

`assets` : Liczba rejestrów aktywów.

`crypto` : Liczba rejestrów kryptograficznych.

`tokenized` : Liczba rejestrów obiektów, które zostały poddane tokenizacji (gdzie właściciel obiektu jest tokenem, a nie profilem).

`tokens` : Liczba rejestrów tokenów.
}

`state` : Statystyka rejestrów surowych i tylko do odczytu.
{
`surowe` : Liczba rejestrów surowych.

`tylko do odczytu` : Liczba rejestrów tylko do odczytu.
}
}

`sig_chains` : Całkowita liczba łańcuchów podpisów w księdze.

`zaufanie` : Statystyki dotyczące aktywnych rachunków powierniczych.
{
„total” : Całkowita liczba kont powierniczych, które są aktywne (mają niezerowe saldo stawek).

`stake` : Całkowita ilość NXS aktualnie postawiona w całej sieci).

`zaufanie`: Całkowity wynik zaufania wszystkich postawionych kont powierniczych.
}

„rezerwy” : Statystyki dotyczące ilości NXS aktualnie w różnych rezerwach.
{
`ambasador` : Ilość NXS w rezerwach ambasadora, oczekująca na zapłatę w łańcuchach ambasadorów.

`developer` : Ilość NXS w rezerwach deweloperów, czekająca na zapłatę w sieciach podpisów deweloperów.

`fee` : Kwota NXS w rezerwie opłat.

`hash` : Ilość NXS w rezerwach kanału mieszającego.

`prim` : Ilość NXS w rezerwach kanału głównego.
}

---
&nbsp;

## list/peers <a href="#list/peers" id="list/peers"></a>

Zwraca podsumowanie informacji o peerach aktualnie połączonych z tym węzłem. Zwracana tablica jest sortowana według wartości wyniku równorzędnego.

````
system/lista/rówieśnicy
````

### Parametry:

[`Sortowanie`](/pl/tryt++/sortowanie).

[`Filtrowanie`](/pl/tryt++/filtrowanie)

[`Operatorzy`](/pl/tryt++/operatorzy)

### Wyniki:

#### Zwracana wartość obiektu JSON: