---
title: KSIĘGA GŁÓWNA
description: API księgi głównej
published: true
date: 2022-11-07T22:48:47.897Z
tags: 
editor: markdown
dateCreated: 2022-10-24T22:26:47.955Z
---

# KSIĘGA GŁÓWNA

Ledger API zapewnia użytkownikom dostęp do danych przechowywanych w księdze, takich jak bloki, transakcje oraz informacje dotyczące stakowania i wydobywania w całej sieci.

## Bezpośrednie punkty końcowe

Poniższe polecenia są bezpośrednimi punktami końcowymi i dlatego nie obsługują powyższej struktury czasowników i rzeczowników dostępnych powyżej.

[`get/blockhash`](#get/blockhash)
[`get/block`](#get/block)
[`list/blocks`](#list/blocks)
[`get/transaction`](#get/transaction)
[`list/transactions`](#list/transactions)
[`submit/transaction`](#submit/transaction)
[`get/info`](#get/info)
[`get/metrics`](#get/metrics)

Bezpośrednie punkty końcowe obsługują `filters` i `operators`.

---
&nbsp;

## get/blockhash <a href="#get/blockhash" id="get/blockhash"></a>

Pobiera skrót bloku dla danej wysokości.

````
ledger/get/blockhash
````

### Parametry:

`height` : **Wysokość bloku**, dla którego ma zostać pobrany hash.

### Wyniki:

#### Zwracana wartość obiektu JSON:

```
{
    "hash": "289b76fbe40ca5e0d0df68016677a8c9be6389f3225cc9faf65cb92bbc98a3580b57cb7ba3d7f7ab36ce890d47a4be90254d407270ad4c2e69c99c998ef8547ca45f054b081959d4d59feb871360bce888f82b4cdc1476502bd1b8e95dffe811e55592d3d4768b56e0510e02b5e32171858de097cd811e7c8d09920c24960ae8"
}
[Completed in 0.083791 ms]  
```

#### Zwracane wartości:

`hash` : Hash bloku.

---
&nbsp;

## get/block <a href="#get/block" id="get/block"></a>

Pobiera dane bloku dla danego hash bloku lub wysokości.

````
ledger/get/block
````

> **NOTA:**
> Pobieranie danych bloku według wysokości jest możliwe tylko wtedy, gdy rdzeń został skonfigurowany z flagą --indexheight.
{.is-info}


### Parametry:

`hash` : Wymagany do **identyfikacji** bloku, dla którego mają zostać pobrane dane bloku. Jest to opcjonalne, jeśli podano wysokość.

`height` : Wymagany do **identyfikacji** bloku, dla którego mają zostać pobrane dane bloku. Jest to opcjonalne, jeśli podano hash.

`verbose` : Opcjonalny, określa, ile **danych transakcji** należy uwzględnić w odpowiedzi. Obsługiwane wartości to:

* `default` : hash
* `summary` : type, version, sequence, timestamp, contracts
* `detail` : genesis, nexthash, prevhash, pubkey, signature

[`Sorting`](/pl/tritium++/sorting)

[`Filtering`](/pl/tritium++/filtering)

### Wyniki:

#### Zwracana wartość obiektu JSON:

```
{
    "hash": "69336bc69ac2b9d06d7b9f9ede253cbeadba227751125cbb220654499c59a7b5138ea06ff62670fae614e5fed26aec8d3a0f346e03f10ea6c83dcb20ba8d93d17d92fffd6604666034e7002f421e39e64cef43325dfdf2c0334e51e018a31710c8fac17214d96d309b8dddb8f9bf9b3a27d28c71016b93a0e89f588c3604420a",
    "proofhash": "0000000000036b5c62766b5781f78734cf336f6fc6bce0363b93092551390fa7bd4d942d20316758def777b770db0500c3910f43b147c006ad11246ae62ed28284a4af309aebdc31ed6df23ebc7218b5a638b4da42cb496661fb12cace6890b920233e7db70a3daa8b439e0973a0dd01be67db652eaf8e7281027228f47a89cf",
    "size": 797,
    "height": 4555100,
    "channel": 2,
    "version": 8,
    "merkleroot": "017ff70158049886f8bad93cfe15285bae34d0e643991088e00769228161868a60230551724ac0ad5c7a98fabfdbebca88dffedf1a9e5ff095524b7565bccee1",
    "timestamp": 1658817542,
    "date": "2022-07-26 06:39:02 UTC",
    "nonce": 396216179366,
    "bits": "7b06e198",
    "difficulty": 2380.934877,
    "mint": 1.921131,
    "previousblockhash": "7dff690671fb7af3413f59315757a2fad8fb8acb7ea323269cc94152e9cbc696ed5064ec581c0709972a584f159ec75f8597559f93ec5f13d1bc608c0e7799ec891a5f26b455c97f0ac9dd1d826cb396aae1bcef8c0b74639e034161bb1d22a7cd4b29580d73ecba882a91273cc10121233096a5bb12c45ad774975c1bef925e",
    "nextblockhash": "5c985f5402f0bcb339ebef0e2edcad30427bf79803994772cd3a1458012748cd1d9d2ee8d6f1466f0c8ca867e1d8a2d9cfe6bc8cfdd885421fb56c55bfc11328f19c61bdc87193831851526a835e457fb46fcd0088879d564e88bb39524aa40489329ecc2cbc6a0453b8dd69a90b82232df6ee6d39ddec80e16149c99b1ddeab",
    "tx": [
        {
            "txid": "017ff70158049886f8bad93cfe15285bae34d0e643991088e00769228161868a60230551724ac0ad5c7a98fabfdbebca88dffedf1a9e5ff095524b7565bccee1",
            "type": "tritium base",
            "version": 4,
            "sequence": 11340,
            "timestamp": 1658817487,
            "blockhash": "69336bc69ac2b9d06d7b9f9ede253cbeadba227751125cbb220654499c59a7b5138ea06ff62670fae614e5fed26aec8d3a0f346e03f10ea6c83dcb20ba8d93d17d92fffd6604666034e7002f421e39e64cef43325dfdf2c0334e51e018a31710c8fac17214d96d309b8dddb8f9bf9b3a27d28c71016b93a0e89f588c3604420a",
            "confirmations": 262,
            "genesis": "a1e91c3b5d2856427508823fea815a37a11f5745d78e79091022d55e5bdb224d",
            "nexthash": "6adfd58123aa4ea622d808bbcf5b11d80d41921358c50dea71d25cf5791df106",
            "prevhash": "018f90d5ed4c2744e1d319c3b77e16f3a06187ee79e4a2bc982bc53dedfb2298aa0df30622df9cf080324aa103623db21648043cb1bb8f5a186764151fa9b242",
            "pubkey": "025d8d82339653aa9256bec27119cee55a9535e07b55aedcf7ed44a1f775a6afde6db2f76df2f337dd941ec337a98ad196c6840c040130ddc033cf779680735cd4",
            "signature": "30818402404da5e71d74b981fc7027cf30d0e7e56ea79367e6f97c76d3380bd3b56ea6aa608f6c370553c17c66fa022571412ab6cf2ebd41d9cc80295e37d6b59ed3a82fe602407a09ed3861823b1ec0ddd0d45a327b7615408b7d116032f6a806d2f286a420ac52275b1540085048491667173429c72113654255da72b12189a22eea89b8fa90",
            "contracts": [
                {
                    "id": 0,
                    "OP": "COINBASE",
                    "genesis": "a1e91c3b5d2856427508823fea815a37a11f5745d78e79091022d55e5bdb224d",
                    "nonce": 180,
                    "amount": 1.921131,
                    "token": "0000000000000000000000000000000000000000000000000000000000000000",
                    "ticker": "NXS"
                }
            ]
        }
    ]
}
[Completed in 0.422600 ms]
```

#### Zwracane wartości:

`hash` : Hash bloku.

`proofhash` : skrót dowodowy bloku.

`size` : Rozmiar bloku w bajtach.

`height` : wysokość bloku.

`channel` : Kanał blokowy (0=Stawka, 1=Prime, 2=Hash).

`version` : Wersja serializacji tego bloku.

`merkleroot` : hash merkle root transakcji blokowych.

`time` : ujednolicony czas utworzenia bloku.

`nonce`: rozwiązanie nonce.

`bits` : Kompaktowa reprezentacja trudności bloku.

`difficulty` : Trudność specyficzna dla kanału.

`mint` : Wartość wybita w tym bloku.

`previousblockhash` : skrót poprzedniego bloku w łańcuchu.

`nextblockhash` : skrót następnego bloku w łańcuchu, chyba że jest to ostatni blok w łańcuchu.

`tx` : Tablica transakcji zawartych w tym bloku.

`type` : Opis transakcji (starsza | baza trytu | zaufanie | geneza | użytkownik).

`version` : wersja serializacji transakcji.

`sequence` : Numer kolejny tej transakcji w łańcuchu podpisów.

`timestamp` : Uniksowy znacznik czasu utworzenia transakcji.

`blockhash` : Hash bloku, w którym zawarta jest ta transakcja. Pusty, jeśli nie został jeszcze uwzględniony w bloku.

`confirmations` : Liczba potwierdzeń uzyskanych przez tę transakcję przez sieć.

`genesis` : To jest skrót nazwy użytkownika profilu, znany również jako skrót właściciela.

`nexthash` : Hash następnej transakcji w sekwencji.

`prevhash` : Hash poprzedniej transakcji w sekwencji.

`pubkey` : klucz publiczny.

`signature` : skrót podpisu.

`hash` : hash transakcji.

`contracts` : Tablica kontraktów powiązanych z tą transakcją oraz ich szczegóły z kodami operacyjnymi.
{
`idcontractid` : Identyfikator sekwencyjny tego kontraktu w ramach transakcji.

`OP` : Operacja kontraktu. Może być DODATEK, ROSZCZENIE, COINBASE, UTWÓRZ, KREDYT, DEBET, OPŁATA, GENESIS, DZIEDZICTWO, PRZELEW, ZAUFANIE, STAWKA, ODSTAWIANIE, NAPISZ.

`for` : dla transakcji KREDYTOWYCH, kontrakt, dla którego utworzono ten kredyt . Może być COINBASE, DEBIT lub LEGACY.

`txid` : Transakcja, która została uznana / zgłoszona.

`contract` : Identyfikator kontraktu w ramach transakcji, która została uznana / zgłoszona.

`proof`: adres rejestru potwierdzający kredyt.

`from` : Dla transakcji DEBIT, KREDYT, OPŁATY adres rejestrowy konta, z którego dokonywany jest debet.

`from_name` : W przypadku transakcji DEBIT, KREDYT, OPŁATY nazwa rachunku, z którego dokonywany jest debet. Uwzględniane tylko wtedy, gdy nazwa może zostać rozwiązana.

`to` : W przypadku transakcji DEBIT i KREDYT adres rejestru konta odbiorcy.

`to_name` : W przypadku transakcji DEBIT i KREDYT nazwa konta odbiorcy. Uwzględniane tylko wtedy, gdy nazwa może zostać rozwiązana.

`amount` : kwota tokena transakcji.

`token` : adres rejestru tokena, którego dotyczy transakcja. Ustaw na 0 dla transakcji NXS.

`ticker` : nazwa tokena, którego dotyczy transakcja.

`reference` : W przypadku transakcji DEBIT i KREDYT jest to referencja podana przez użytkownika, używana przez odbiorcę do powiązania transakcji z numerem zamówienia lub faktury.
}

---
&nbsp;

## list/blocks <a href="#list/blocks" id="list/blocks"></a>

Pobiera tablicę danych bloku dla sekwencyjnego zakresu bloków z danego skrótu lub wysokości.

````
ledger/get/transaction
````

> **UWAGA:**
> Pobieranie danych bloku według wysokości jest możliwe tylko wtedy, gdy rdzeń został skonfigurowany z flagą --indexheight.
> {.is-info}


### Parametry:

`hash` : Wymagany do **identyfikacji** bloku, dla którego ma zostać pobrane dane bloku. Jest to opcjonalne, jeśli podano `wysokość`

`height` : Wymagany do **identyfikacji** bloku, dla którego ma zostać pobrane dane bloku. Jest to opcjonalne, jeśli podano `hash`

`verbose` : Jest to opcja opcjonalna, określa, ile **danych transakcyjnych** należy uwzględnić w odpowiedzi. Obsługiwane wartości to:

* `podsumowanie` : typ, wersja, kolejność, znacznik czasu i operacja.
* `detail` : geneza, nexthash, prevhash, pubkey i sygnatura.

`where` : tablica klauzul do **filtrowania** wyników JSON. Więcej informacji na temat filtrowania wyników z metod API /list/xxx można znaleźć pod adresem [`Queries`](/en/tritium++/queries).

[`Sortowanie`](/pl/tryt++/sortowanie)

[`Filtrowanie`](/pl/tryt++/filtrowanie)

[`Operatorzy`](/pl/tryt++/operatorzy).

> **UWAGA :**
> Należy podać hasz lub wysokość, ale nie oba.
> Pobieranie danych bloku według wysokości jest dozwolone tylko wtedy, gdy demon został skonfigurowany z indexheight=1.
{.is-info}


### Zwroty:

#### Zwracana wartość obiektu JSON:

