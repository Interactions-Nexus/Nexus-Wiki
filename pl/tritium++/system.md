---
title: SYSTEM
description: System API
published: true
date: 2022-11-04T23:08:42.641Z
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

`registers` : Statystyki w bazie danych rejestrów.

`names` : Całkowita liczba rejestrów nazw, w tym użytkowników lokalnych, globalnych i przestrzeni nazw.

`global` : Liczba nazw, które zostały utworzone w globalnej przestrzeni nazw.

`local` : Liczba nazw, które zostały utworzone w lokalnej przestrzeni nazw.

`namespaced` : Liczba nazw, które zostały utworzone w przestrzeni nazw.


`namespaces` : Liczba przestrzeni nazw, które zostały utworzone.

`objects` : Statystyka niestandardowych rejestrów obiektów. Należą do nich konta, tokeny, krypto, aktywa, przedmioty i wszelkie inne pochodne rejestry obiektów.

`accounts`: Liczba rejestrów kont. Obejmuje to zarówno konta NXS, jak i inne konta tokenowe.

`assets` : Liczba rejestrów aktywów.

`crypto` : Liczba rejestrów kryptograficznych.

`tokenized` : Liczba rejestrów obiektów, które zostały poddane tokenizacji (gdzie właściciel obiektu jest tokenem, a nie profilem).

`tokens` : Liczba rejestrów tokenów.


`state` : Statystyka rejestrów surowych i tylko do odczytu.

`raw` : Liczba rejestrów surowych.

`readonly` : Liczba rejestrów tylko do odczytu.



`sig_chains` : Całkowita liczba łańcuchów podpisów w księdze.

`trust` : Statystyki dotyczące aktywnych kont trust.

`total` : Całkowita liczba kont trust, które są aktywne (mają niezerowe saldo stawek).

`stake` : Całkowita ilość NXS aktualnie stakowana w całej sieci.

`trust`: Całkowity wynik zaufania wszystkich stakowanych kont trust.


`reserves` : Statystyki dotyczące ilości NXS aktualnie w różnych rezerwach.

`ambasador` : Ilość NXS w rezerwach ambasadora, oczekująca na zapłatę w łańcuchach ambasadorów.

`developer` : Ilość NXS w rezerwach deweloperów, czekająca na zapłatę w sieciach podpisów deweloperów.

`fee` : Kwota NXS w rezerwie opłat.

`hash` : Ilość NXS w rezerwach kanału hash.

`prime` : Ilość NXS w rezerwach kanału prime.


---
&nbsp;

## list/peers <a href="#list/peers" id="list/peers"></a>

Zwraca podsumowanie informacji o peerach aktualnie połączonych z tym węzłem. Zwracana tablica jest sortowana według wartości wyniku równorzędnego.

```
system/list/peers
```

### Parametry:

[`Sorting`](/en/tritium++/sorting).

[`Filtering`](/en/tritium++/filtering)

[`Operators`](/en/tritium++/operators)

### Wyniki:

#### Zwracana wartość obiektu JSON:

```
[
    {
        "address": "45.180.14.231:9888",
        "type": "5.0.5 Tritium CLI [LLD][x64]",
        "version": 30000,
        "session": 8412734217501590516,
        "outgoing": true,
        "height": 0,
        "best": "00000000000000000000",
        "latency": 4294967295,
        "lastseen": 1658762086,
        "connects": 3,
        "drops": 0,
        "fails": 0,
        "score": 8850.0
    },
    {
        "address": "29.19.192.168:9888",
        "type": "5.1.0-rc2 Tritium++ CLI [LLD][x64]",
        "version": 3010000,
        "session": 10774729209155580028,
        "outgoing": true,
        "height": 0,
        "best": "00000000000000000000",
        "latency": 4294967295,
        "lastseen": 1658762098,
        "connects": 3,
        "drops": 1,
        "fails": 0,
        "score": 10195.0
    }
]
[Completed in 0.409770 ms]
```

#### Zwracane wartości:

`address` : Adres IP i port peera. Może to być LISP EID używający nakładki LISP lub adres IP używający natywnego podkładu.

`type` : Łańcuch wersji oprogramowania demona podłączonego peera.

`version` : Wersja protokołu używanego do komunikacji.

`session` : Identyfikator sesji dla bieżącego połączenia.

`outgoing` : Flaga wskazująca, czy było to połączenie wychodzące czy przychodzące.

`height` : Aktualna wysokość peera.

`best` : Blok hash najlepszego łańcucha peera.

`latency` : Obliczone opóźnienie sieci między tym węzłem, a równorzędnym.

`lastseen` : Sygnatura czasowa UNIX ostatniej komunikacji tego węzła z peerem.

`connects` : Liczba połączeń pomyślnie nawiązanych z tym peerem od momentu uruchomienia tego węzła.

`drops` : Liczba połączeń zerwanych z tym peerem od momentu uruchomienia tego węzła.

`fails` : Liczba nieudanych prób połączenia z tym peerem od momentu uruchomienia tego węzła.

`score` : Wartość wyniku przypisana do tego peera na podstawie czasu oczekiwania i innych statystyk połączenia.

---
&nbsp;

## list/lisp-eids <a href="#list/lisp-eids" id="list/lisp-eids"></a>

Zwróci to LISP Endpoint Identifiers (EID) aktualnie skonfigurowane dla tego węzła. Jeśli API lispers.net nie działa / nie jest dostępne, zwróci pustą tablicę.

```
system/list/lisp-eids
```

### Parametry:

-none-

### Wyniki:

#### Zwracana wartość obiektu JSON:

```
[
    {
        "instance-id": "200",
        "eid": "240.139.76.244",
        "rlocs": [
            {
                "interface": "wlp59s0",
                "rloc-name": "mymachine",
                "rloc": "102.162.64.46"
            }
        ]
    },
    {
        "instance-id": "200",
        "eid": "fe::139:76:244",
        "rlocs": [
            {
                "interface": "wlp59s0",
                "rloc-name": "mymachine",
                "rloc": "102.162.64.46"
            }
        ]
    }
]
[Completed in 1004.256167 ms]
```

#### Zwracane wartości:

`instance-id` : Grupa instancji LISP, do której należy ten EID.

`eid` : Identyfikator punktu końcowego. Może to być format IPv4 lub IPv6.

`rlocs` : Tablica RLOC (lokatorów routingu) skojarzona z EID.

`interface` : Nazwa urządzenia dla RLOC.

`rloc-name` : Nazwa hosta powiązana z urządzeniem.

`rloc` : Adres IP powiązany z urządzeniem.

---
&nbsp;

## validate/address <a href="#validate/address" id="validate/address"></a>

Weryfikuje rejestr/adres dotychczasowy.

```
system/validate/address
```

### Parametry:

`address` : Wymagany do **weryfikacji** rejestru zakodowanego w standardzie Base58 lub starszego adresu do sprawdzenia.

### Wyniki:

#### Zwracana wartość obiektu JSON:

```
{
    "address": "8BuhE1y5oard3cEWqCSYK35bC6LdPRvcPR8N7GXYNatTw6De8eK",
    "is_valid": true,
    "type": "OBJECT",
    "object_type": "ACCOUNT"
}
```

#### Zwracane wartości:

`address` : Adres, który został zweryfikowany.

`is_valid` : Flaga logiczna wskazująca, czy adres jest prawidłowy, czy nie. W przypadku adresów Legacy oznacza to, że adres jest po prostu poprawnie sformatowany. W przypadku adresów rejestrów ta flaga sprawdza, czy pod określonym adresem istnieje rejestr w łańcuchu bloków.

`type` : W przypadku adresów rejestrów, typ rejestru pod adresem. Wartości mogą być APPEND, LEGACY, OBJECT, RAW, READONLY, RESERVED, SYSTEM, UNKNOWN.

`object_type` : Jeśli typem jest OBJECT, to pole zawiera standardowy typ obiektu rejestru obiektów. Możliwe wartości to ACCOUNT, CRYPTO, NAME, NAMESPACE, REGISTER, TOKEN, TRUST, UNKNOWN.

`is_mine` : Jeśli typ to LEGACY, ta flaga logiczna wskazuje, czy klucz prywatny adresu jest przechowywany w portfelu lokalnym.



