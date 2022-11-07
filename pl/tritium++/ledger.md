---
title: KSIĘGA GŁÓWNA
description: API księgi głównej
published: true
date: 2022-11-07T23:23:59.361Z
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

`proofhash` : Hash dowodowy bloku.

`size` : Rozmiar bloku w bajtach.

`height` : Wysokość bloku.

`channel` : Kanał blokowy (0=Stake, 1=Prime, 2=Hash).

`version` : Wersja serializacji tego bloku.

`merkleroot` : Hash merkle root transakcji blokowych.

`time` : Ujednolicony czas utworzenia bloku.

`nonce`: Rozwiązanie nonce.

`bits` : Kompaktowa reprezentacja trudności bloku.

`difficulty` : Trudność specyficzna dla kanału.

`mint` : Wartość wybita w tym bloku.

`previousblockhash` : Hash poprzedniego bloku w łańcuchu.

`nextblockhash` : Hash następnego bloku w łańcuchu, chyba że jest to ostatni blok w łańcuchu.

`tx` : Tablica transakcji zawartych w tym bloku.

`type` : Opis transakcji (legacy | tritium base | trust | genesis | user).

`version` : Wersja serializacji transakcji.

`sequence` : Numer kolejny tej transakcji w łańcuchu podpisów.

`timestamp` : Uniksowy znacznik czasu utworzenia transakcji.

`blockhash` : Hash bloku, w którym zawarta jest ta transakcja. Pusty, jeśli nie został jeszcze uwzględniony w bloku.

`confirmations` : Liczba potwierdzeń uzyskanych przez tę transakcję przez sieć.

`genesis` : To jest hash nazwy użytkownika profilu, znany również jako hash właściciela.

`nexthash` : Hash następnej transakcji w sekwencji.

`prevhash` : Hash poprzedniej transakcji w sekwencji.

`pubkey` : Klucz publiczny.

`signature` : Hash podpisu.

`hash` : Hash transakcji.

`contracts` : Tablica kontraktów powiązanych z tą transakcją oraz ich szczegóły z kodami operacyjnymi.

`idcontractid` : Identyfikator sekwencyjny tego kontraktu w ramach transakcji.

`OP` : Operacja kontraktu. Może być APPEND, CLAIM, COINBASE, CREATE, CREDIT, DEBIT, FEE, GENESIS, LEGACY, TRANSFER, TRUST, STAKE, UNSTAKE, WRITE.

`for` : Dla transakcji CREDIT, kontrakt, dla którego utworzono ten kredyt . Może być COINBASE, DEBIT lub LEGACY.

`txid` : Transakcja, która została uznana / zgłoszona.

`contract` : Identyfikator kontraktu w ramach transakcji, która została uznana / zgłoszona.

`proof`: Adres rejestru potwierdzający kredyt.

`from` : Dla transakcji DEBIT, CREDIT, FEE adres rejestrowy konta, z którego dokonywany jest debet.

`from_name` : W przypadku transakcji DEBIT, CREDIT, FEE nazwa rachunku, z którego dokonywany jest debet. Uwzględniane tylko wtedy, gdy nazwa może zostać rozwiązana.

`to` : W przypadku transakcji DEBIT i CREDIT adres rejestru konta odbiorcy.

`to_name` : W przypadku transakcji DEBIT i CREDIT nazwa konta odbiorcy. Uwzględniane tylko wtedy, gdy nazwa może zostać rozwiązana.

`amount` : Kwota tokena transakcji.

`token` : Adres rejestru tokena, którego dotyczy transakcja. Ustaw na 0 dla transakcji NXS.

`ticker` : Nazwa tokena, którego dotyczy transakcja.

`reference` : W przypadku transakcji DEBIT i CREDIT jest to referencja podana przez użytkownika, używana przez odbiorcę do powiązania transakcji z numerem zamówienia lub faktury.

---
&nbsp;

## list/blocks <a href="#list/blocks" id="list/blocks"></a>

Pobiera tablicę danych bloku dla sekwencyjnego zakresu bloków z danego hash lub wysokości.

````
ledger/list/blocks
````

> **NOTA:**
> Pobieranie danych bloku według wysokości jest możliwe tylko wtedy, gdy rdzeń został skonfigurowany z flagą --indexheight.
> {.is-info}


### Parametry:

`hash` : Wymagany do **identyfikacji** bloku, dla którego ma zostać pobrane dane bloku. Jest to opcjonalne, jeśli podano `height`.

`height` : Wymagany do **identyfikacji** bloku, dla którego ma zostać pobrane dane bloku. Jest to opcjonalne, jeśli podano `hash`.

`verbose` : Jest to opcja opcjonalna, określa, ile **danych transakcyjnych** należy uwzględnić w odpowiedzi. Obsługiwane wartości to:

* `summary` : type, version, sequence, timestamp, and operation
* `detail` : genesis, nexthash, prevhash, pubkey and signature

`where` : Tablica klauzul do **filtrowania** wyników JSON. Więcej informacji na temat filtrowania wyników z metod API /list/xxx można znaleźć pod adresem [`Queries`](/pl/tritium++/queries).

[`Sorting`](/pl/tritium++/sorting)

[`Filtering`](/pl/tritium++/filtering)

[`Operators`](/pl/tritium++/operators).

> **NOTA:**
> Należy podać hash lub height, ale nie oba.
> Pobieranie danych bloku według wysokości jest dozwolone tylko wtedy, gdy demon został skonfigurowany z indexheight=1.
{.is-info}


### Zwroty:

#### Zwracana wartość obiektu JSON:

```
[
    {
        "hash": "5c985f5402f0bcb339ebef0e2edcad30427bf79803994772cd3a1458012748cd1d9d2ee8d6f1466f0c8ca867e1d8a2d9cfe6bc8cfdd885421fb56c55bfc11328f19c61bdc87193831851526a835e457fb46fcd0088879d564e88bb39524aa40489329ecc2cbc6a0453b8dd69a90b82232df6ee6d39ddec80e16149c99b1ddeab",
        "proofhash": "3f10d762af5952f7fdda2f84a27f9afe121e54be25eb0a41ee5074219919b9a2832d535d2c7c995a91e21ee6000017b2e7cc2099537cda035c09ebcaa94112384e88cdeec9d1ba6eb662b1acdf4f41d9b964f3da5a578d757bd2653acd8ed7364e8bd807777fbaabb4cda19cad6506b84431940e6a1e43a32d92eff9d9ace635",
        "size": 807,
        "height": 4555101,
        "channel": 1,
        "version": 8,
        "merkleroot": "0161d4629a2f385be81bda414359aaafb6baec7522f017c6fd06183c975c6c4a9baf4b89e5890327ddd79853eb415bfb054f84da719ac653520097bbc01b6e6c",
        "timestamp": 1658817563,
        "date": "2022-07-26 06:39:23 UTC",
        "nonce": 15731843013639865474,
        "bits": "04c23531",
        "difficulty": 7.9836465,
        "mint": 1.92113,
        "previousblockhash": "69336bc69ac2b9d06d7b9f9ede253cbeadba227751125cbb220654499c59a7b5138ea06ff62670fae614e5fed26aec8d3a0f346e03f10ea6c83dcb20ba8d93d17d92fffd6604666034e7002f421e39e64cef43325dfdf2c0334e51e018a31710c8fac17214d96d309b8dddb8f9bf9b3a27d28c71016b93a0e89f588c3604420a",
        "nextblockhash": "6e4b01acefa38b2f591ba7060c165daafe4cdaac8f147f7b8a02986b8f8b3c82d051601746ac53ff57167a650d75d501eab859b4a52d48444f036b9df1571648a22d777dd71896860b6faa7236bcd54d2f2de2445dcdf2e5a34f64b5c8918d3a8a8fce357024d74ca3c8b76c5a1457d4182ce18e015a782316390fc0dfb8eb34",
        "tx": [
            {
                "txid": "0161d4629a2f385be81bda414359aaafb6baec7522f017c6fd06183c975c6c4a9baf4b89e5890327ddd79853eb415bfb054f84da719ac653520097bbc01b6e6c",
                "type": "tritium base",
                "version": 4,
                "sequence": 176177,
                "timestamp": 1658817543,
                "blockhash": "5c985f5402f0bcb339ebef0e2edcad30427bf79803994772cd3a1458012748cd1d9d2ee8d6f1466f0c8ca867e1d8a2d9cfe6bc8cfdd885421fb56c55bfc11328f19c61bdc87193831851526a835e457fb46fcd0088879d564e88bb39524aa40489329ecc2cbc6a0453b8dd69a90b82232df6ee6d39ddec80e16149c99b1ddeab",
                "confirmations": 249,
                "contracts": [
                    {
                        "id": 0,
                        "OP": "COINBASE",
                        "genesis": "a165c6bc1b1e0dd9444f3ec01f07686991a8b4bdc1ceb4143dbb3eed16339a74",
                        "nonce": 308,
                        "amount": 1.92113,
                        "token": "0000000000000000000000000000000000000000000000000000000000000000",
                        "ticker": "NXS"
                    }
                ]
            }
        ]
    }
]
[Completed in 8.883924 ms]
```

#### Zwracane wartości:

`hash` : Hash bloku.

`proofhash` : Hash dowodowy bloku.

`size` : Rozmiar bloku w bajtach.

`height` : Wysokość bloku.

`channel` : Kanał blokowy (0=Stake, 1=Prime, 2=Hash).

`version` : Wersja serializacji tego bloku.

`merkleroot` : Hash merkle root transakcji blokowych.

`time` : Ujednolicony czas utworzenia bloku.

`nonce`: Rozwiązanie nonce.

`bits` : Kompaktowa reprezentacja trudności bloku.

`difficulty` : Trudność specyficzna dla kanału.

`mint` : Wartość wybita w tym bloku.

`previousblockhash` : Hash poprzedniego bloku w łańcuchu.

`nextblockhash` : Hash następnego bloku w łańcuchu, chyba że jest to ostatni blok w łańcuchu.

`tx` : Tablica transakcji zawartych w tym bloku.

`type` : Opis transakcji (legacy | tritium base | trust | genesis | user).

`version` : Wersja serializacji transakcji.

`sequence` : Numer kolejny tej transakcji w łańcuchu podpisów.

`timestamp` : Uniksowy znacznik czasu utworzenia transakcji.

`blockhash` : Hash bloku, w którym zawarta jest ta transakcja. Pusty, jeśli nie został jeszcze uwzględniony w bloku.

`confirmations` : Liczba potwierdzeń uzyskanych przez tę transakcję przez sieć.

`genesis` : To jest hash nazwy użytkownika profilu, znany również jako hash właściciela.

`nexthash` : Hash następnej transakcji w sekwencji.

`prevhash` : Hash poprzedniej transakcji w sekwencji.

`pubkey` : Klucz publiczny.

`signature` : Hash podpisu.

`hash` : Hash transakcji.

`contracts` : Tablica kontraktów powiązanych z tą transakcją oraz ich szczegóły z kodami operacyjnymi.

`idcontractid` : Identyfikator sekwencyjny tego kontraktu w ramach transakcji.

`OP` : Operacja kontraktu. Może być APPEND, CLAIM, COINBASE, CREATE, CREDIT, DEBIT, FEE, GENESIS, LEGACY, TRANSFER, TRUST, STAKE, UNSTAKE, WRITE.

`for` : Dla transakcji CREDIT, kontrakt, dla którego utworzono ten kredyt . Może być COINBASE, DEBIT lub LEGACY.

`txid` : Transakcja, która została uznana / zgłoszona.

`contract` : Identyfikator kontraktu w ramach transakcji, która została uznana / zgłoszona.

`proof`: Adres rejestru potwierdzający kredyt.

`from` : Dla transakcji DEBIT, CREDIT, FEE adres rejestrowy konta, z którego dokonywany jest debet.

`from_name` : W przypadku transakcji DEBIT, CREDIT, FEE nazwa rachunku, z którego dokonywany jest debet. Uwzględniane tylko wtedy, gdy nazwa może zostać rozwiązana.

`to` : W przypadku transakcji DEBIT i CREDIT adres rejestru konta odbiorcy.

`to_name` : W przypadku transakcji DEBIT i CREDIT nazwa konta odbiorcy. Uwzględniane tylko wtedy, gdy nazwa może zostać rozwiązana.

`amount` : Kwota tokena transakcji.

`token` : Adres rejestru tokena, którego dotyczy transakcja. Ustaw na 0 dla transakcji NXS.

`ticker` : Nazwa tokena, którego dotyczy transakcja.

`reference` : W przypadku transakcji DEBIT i CREDIT jest to referencja podana przez użytkownika, używana przez odbiorcę do powiązania transakcji z numerem zamówienia lub faktury.

---
&nbsp;

## get/transaction <a href="#get/transaction" id="get/transaction"></a>

Pobiera dane transakcji dla danego hash transakcji.

````
ledger/get/transaction
````

### Parametry:

`format` : Określa **format** zwracanej wartości. Wartością parametru może być JSON (domyślna) lub surowa. Jeśli określono wartość raw, metoda zwraca zserializowaną transakcję zakodowaną szesnastkowo, która może być następnie rozgłaszana do sieci za pośrednictwem /ledger/submit/transaction.

`txid` : Wymagany do **identyfikacji** txid, dla którego mają zostać pobrane dane transakcji.

`verbose` : Opcjonalny, określa, ile **danych transakcji** należy uwzględnić w odpowiedzi. Jest to ignorowane, jeśli wymagany jest format surowy. Obsługiwane wartości to:

* summary : hash, type, version, sequence, timestamp, and contracts
* detail : genesis, nexthash, prevhash, pubkey and signature

[`Sorting`](/pl/tritium++/sorting)

[`Filtering`](/pl/tritium++/filtering)

### Zwroty:

#### Zwracana wartość obiektu JSON:

```
{
    "txid": "017ff70158049886f8bad93cfe15285bae34d0e643991088e00769228161868a60230551724ac0ad5c7a98fabfdbebca88dffedf1a9e5ff095524b7565bccee1",
    "type": "tritium base",
    "version": 4,
    "sequence": 11340,
    "timestamp": 1658817487,
    "blockhash": "69336bc69ac2b9d06d7b9f9ede253cbeadba227751125cbb220654499c59a7b5138ea06ff62670fae614e5fed26aec8d3a0f346e03f10ea6c83dcb20ba8d93d17d92fffd6604666034e7002f421e39e64cef43325dfdf2c0334e51e018a31710c8fac17214d96d309b8dddb8f9bf9b3a27d28c71016b93a0e89f588c3604420a",
    "confirmations": 267,
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
[Completed in 0.290130 ms]
```

#### Zwracane wartości:

`txid` : Hash transakcji.

`type` : Opis transakcji (legacy | tritium base | trust | genesis | user).

`version` : Wersja serializacji transakcji.

`sequence` : Numer kolejny tej transakcji w łańcuchu podpisów.

`timestamp` : Uniksowy znacznik czasu utworzenia transakcji.

`blockhash` : Hash bloku, w którym zawarta jest ta transakcja. Pusty, jeśli nie został jeszcze uwzględniony w bloku.

`confirmations` : Liczba potwierdzeń uzyskanych przez tę transakcję przez sieć.

`genesis` : To jest hash nazwy użytkownika profilu, znany również jako hash właściciela.

`nexthash` : Hash następnej transakcji w sekwencji.

`prevhash` : Hash poprzedniej transakcji w sekwencji.

`pubkey` : Klucz publiczny.

`signature` : Hash podpisu.

`contracts` : Tablica kontraktów powiązanych z tą transakcją oraz ich szczegóły z kodami operacyjnymi.

`id` : Identyfikator sekwencyjny tego kontraktu w ramach transakcji.

`OP` : Operacja kontraktu. Może być APPEND, CLAIM, COINBASE, CREATE, CREDIT, DEBIT, FEE, GENESIS, LEGACY, TRANSFER, TRUST, STAKE, UNSTAKE, WRITE.

`for` : Dla transakcji CREDIT, kontrakt, dla którego utworzono ten kredyt . Może być COINBASE, DEBIT lub LEGACY.

`txid` : Transakcja, która została uznana / zgłoszona.

`contract` : Identyfikator kontraktu w ramach transakcji, która została uznana / zgłoszona.

`proof`: Adres rejestru potwierdzający kredyt.

`from` : Dla transakcji DEBIT, CREDIT, FEE adres rejestrowy konta, z którego dokonywany jest debet.

`from_name` : W przypadku transakcji DEBIT, CREDIT, FEE nazwa rachunku, z którego dokonywany jest debet. Uwzględniane tylko wtedy, gdy nazwa może zostać rozwiązana.

`to` : W przypadku transakcji DEBIT i CREDIT adres rejestru konta odbiorcy.

`to_name` : W przypadku transakcji DEBIT i CREDIT nazwa konta odbiorcy. Uwzględniane tylko wtedy, gdy nazwa może zostać rozwiązana.

`amount` : Kwota tokena transakcji.

`token` : Adres rejestru tokena, którego dotyczy transakcja. Ustaw na 0 dla transakcji NXS.

`ticker` : Nazwa tokena, którego dotyczy transakcja.

`reference` : W przypadku transakcji DEBIT i CREDIT jest to referencja podana przez użytkownika, używana przez odbiorcę do powiązania transakcji z numerem zamówienia lub faktury.

---
&nbsp;

## list/transactions <a href="#list/transactions" id="list/transactions"></a>

Pobiera dane transakcji dla danego hash transakcji.

````
ledger/list/transactions
````

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika nie należy podawać sesji.

`verbose` : Opcjonalny, określa, ile **danych transakcji** należy uwzględnić w odpowiedzi. Obsługiwane wartości to:

* summary : hash, type, version, sequence, timestamp, contracts
* detail : genesis, nexthash, prevhash, pubkey, signature

`where` : Tablica klauzul do **filtrowania** wyników JSON. Więcej informacji na temat filtrowania wyników z metod API /list/xxx można znaleźć pod adresem [`Queries`](/pl/tritium++/queries).

[`Sorting`](/pl/tritium++/sorting)

[`Filtering`](/pl/tritium++/filtering)

[`Operators`](/pl/tritium++/operators)

### Zwroty:

#### Zwracana wartość obiektu JSON:

```
{
    "txid": "017ff70158049886f8bad93cfe15285bae34d0e643991088e00769228161868a60230551724ac0ad5c7a98fabfdbebca88dffedf1a9e5ff095524b7565bccee1",
    "type": "tritium base",
    "version": 4,
    "sequence": 11340,
    "timestamp": 1658817487,
    "blockhash": "69336bc69ac2b9d06d7b9f9ede253cbeadba227751125cbb220654499c59a7b5138ea06ff62670fae614e5fed26aec8d3a0f346e03f10ea6c83dcb20ba8d93d17d92fffd6604666034e7002f421e39e64cef43325dfdf2c0334e51e018a31710c8fac17214d96d309b8dddb8f9bf9b3a27d28c71016b93a0e89f588c3604420a",
    "confirmations": 267,
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
[Completed in 0.290130 ms]
```

#### Zwracane wartości:

`txid` : Hash transakcji.

`type` : Opis transakcji (legacy | tritium base | trust | genesis | user).

`version` : Wersja serializacji transakcji.

`sequence` : Numer kolejny tej transakcji w łańcuchu podpisów.

`timestamp` : Uniksowy znacznik czasu utworzenia transakcji.

`blockhash` : Hash bloku, w którym zawarta jest ta transakcja. Pusty, jeśli nie został jeszcze uwzględniony w bloku.

`confirmations` : Liczba potwierdzeń uzyskanych przez tę transakcję przez sieć.

`genesis` : To jest hash nazwy użytkownika profilu, znany również jako hash właściciela.

`nexthash` : Hash następnej transakcji w sekwencji.

`prevhash` : Hash poprzedniej transakcji w sekwencji.

`pubkey` : Klucz publiczny.

`signature` : Hash podpisu.

`contracts` : Tablica kontraktów powiązanych z tą transakcją oraz ich szczegóły z kodami operacyjnymi.

`id` : Identyfikator sekwencyjny tego kontraktu w ramach transakcji.

`OP` : Operacja kontraktu. Może być APPEND, CLAIM, COINBASE, CREATE, CREDIT, DEBIT, FEE, GENESIS, LEGACY, TRANSFER, TRUST, STAKE, UNSTAKE, WRITE.

`for` : Dla transakcji CREDIT, kontrakt, dla którego utworzono ten kredyt . Może być COINBASE, DEBIT lub LEGACY.

`txid` : Transakcja, która została uznana / zgłoszona.

`contract` : Identyfikator kontraktu w ramach transakcji, która została uznana / zgłoszona.

`proof`: Adres rejestru potwierdzający kredyt.

`from` : Dla transakcji DEBIT, CREDIT, FEE adres rejestrowy konta, z którego dokonywany jest debet.

`from_name` : W przypadku transakcji DEBIT, CREDIT, FEE nazwa rachunku, z którego dokonywany jest debet. Uwzględniane tylko wtedy, gdy nazwa może zostać rozwiązana.

`to` : W przypadku transakcji DEBIT i CREDIT adres rejestru konta odbiorcy.

`to_name` : W przypadku transakcji DEBIT i CREDIT nazwa konta odbiorcy. Uwzględniane tylko wtedy, gdy nazwa może zostać rozwiązana.

`amount` : Kwota tokena transakcji.

`token` : Adres rejestru tokena, którego dotyczy transakcja. Ustaw na 0 dla transakcji NXS.

`ticker` : Nazwa tokena, którego dotyczy transakcja.

`reference` : W przypadku transakcji DEBIT i CREDIT jest to referencja podana przez użytkownika, używana przez odbiorcę do powiązania transakcji z numerem zamówienia lub faktury.

---
&nbsp;

## submit/transaction <a href="#submit/transaction" id="submit/transaction"></a>

Przesyła transakcję, która ma zostać uwzględniona w pamięci i rozesłana do sieci.

````
ledger/submit/transaction
````

### Parametry:

`data` : Serializowane, zakodowane szesnastkowo dane transakcji do przesłania.

### Wyniki:

#### Zwracana wartość obiektu JSON:

````
{ "hash": "47959e245f45aab773c0ce5320a5454f49ac15f63e15acb36855ac654d54d6314fe36b61dd64ec7a9a546bcc439a628e9badcdccb6e5f8072d04a0a3b67f8679" }
````

#### Zwracane wartości:

`hash` : Hash transakcji, jeśli pomyślnie zatwierdzono do pamięci / rozgłoszenia.

---
&nbsp;

## get/info <a href="#get/info" id="get/info"></a>

Pobiera dane związane z wydobywaniem i podażą NXS dla księgi.

````
ledger/get/info
````

#### Parametry:

[`Filtering`](/pl/tritium++/filtering)

#### Zwroty:

#### Zwracana wartość obiektu JSON:

```
{
    "stake": {
        "height": 1478452,
        "weight": "0000000000000000000136d9ce5eff4a",
        "timespan": 163,
        "fees": 17789.398,
        "difficulty": 528.770417
    },
    "prime": {
        "height": 1607544,
        "weight": "0000000000000000000acf8296a5dace",
        "timespan": 152,
        "fees": 40208.42,
        "difficulty": 7.5050107,
        "reserve": 275.540352,
        "reward": 1.89596,
        "primes": 721104210
    },
    "hash": {
        "height": 1508658,
        "weight": "00000000000000000153053d8ed4b372",
        "timespan": 162,
        "fees": 50891.389,
        "difficulty": 995.146668,
        "reserve": 390.83726,
        "reward": 1.895962,
        "hashes": 1700092903007
    },
    "supply": {
        "total": 74104442.485668,
        "target": 71313176.905702,
        "inflation": 0.4766,
        "minute": 3.651488,
        "hour": 219.087198,
        "day": 5256.922284,
        "week": 36747.303,
        "month": 146280.58871
    },
    "height": 4594651,
    "timestamp": 1660902585,
    "checkpoint": "20b50d243a585a6c9a3d420ebfa61aee8ac0a68c1d8c71ef415247fc3d677c44b6f0a2b497c72ca4d9f2271cfbe1090042522740e7671781c7548b275f84eebce7d4340b703abfe8544a3fd0ff1cd6132f6acb1b04948da81ae965a1828e307d1ab47b731d9cca7f28be830082b81c2a3d0b1fadd3e9fcc2ec9203d22a61ab12"
}
[Completed in 3827.013421 ms]
```













