---
title: Zapytania
description: Zapytanie DSL (język właściwy dla domeny)
published: true
date: 2022-10-31T23:03:46.544Z
tags: 
editor: markdown
dateCreated: 2022-10-24T22:16:44.849Z
---

# Zapytania

Query DSL (Domian Specific Language) pozwala na rekurencyjne sortowanie i filtrowanie do dowolnej logicznej głębokości. Ta linia DSL może być używana w połączeniu z operatorami do sortowania, filtrowania i obliczania danych w czasie rzeczywistym.

>Query DSL można zastosować do wszystkich poleceń API `list` i `get` z parametrem **`where`** w wersji 5.1
{.is-info}

### `Klawisze wyboru`

W przypadku tego zestawu poleceń interfejsu API obsługiwane są następujące operatory:

\[`object`] — ten klucz selektora oceni porównanie na surowym obiekcie binarnym.\
\[`results`] — ten klucz selektora oceni porównanie wyników json.

### Obsługiwane obiekty

Obsługiwane są następujące klasy obiektów:

* object - operuje na surowym rejestrze obiektów
* results - operacje i filtry na podstawie wyników JSON. Może to być około 10 razy wolniejsze, więc używaj oszczędnie.

### Korzystanie z symboli wieloznacznych

Jeśli wyszukujesz według parametru ciągu, możesz dołączyć '\*' jako dowolne dopasowanie znaku wieloznacznego, dzięki czemu możesz wyszukiwać wartości na podstawie częściowego dopasowania.

````
register/list/accounts WHERE 'object.name=d*'
````

Powyższe zwróci wszystkie konta, które zaczynają się na literę 'd'.

#### Obserwujesz symbol wieloznaczny

Poniżej pokazano, jak sprawdzić za pomocą symboli wieloznacznych.

````
register/list/accounts WHERE 'object.name=*d'
````

Powyższe zwróci wszystkie konta, których nazwa kończy się na literę 'd'.

### Przykłady

Aby filtrować, możesz użyć where='statements' lub wykonać polecenie z ciągiem WHERE:

#### Filtrowanie obiektów z klauzulą ​​WHERE

Poniższa klauzula przefiltruje wszystkie rejestry obiektów nazw, które są nazwami globalnymi zaczynającymi się na literę 'P' ​​lub dowolnymi obiektami zaczynającymi się na literę 'S'.

````
register/list/names WHERE '(object.namespace=*GLOBAL* AND object.name=P*) OR object.name=S*'
````

Użycie klasy obiektu, tj. 'object.namespace' spowoduje wywołanie filtra na obiekcie binarnym.

#### Filtrowanie obiektów z where=

Poniższa klauzula przefiltruje wszystkie rejestry obiektów nazw, które są nazwami globalnymi zaczynającymi się na literę 'P' ​​lub dowolnymi obiektami zaczynającymi się na literę 'S'.

````
register/list/names where='(object.namespace=*GLOBAL* AND object.name=P*) OR object.name=S*'
````

#### Filtrowanie z wieloma operatorami

Poniżej zostaną zwrócone wszystkie konta NXS, które mają saldo większe niż 10 NXS.

````
register/list/accounts WHERE 'object.token=0 AND object.balance>10'
````

#### Tworzenie logicznego grupowania

Poniżej przedstawiono sposób wykonywania zapytań przy użyciu wielu poziomów rekurencyjnych.

```
register/list/accounts WHERE '(object.token=0 AND object.balance>10) OR (object.token=8Ed7Gzybwy3Zf6X7hzD4imJwmA2v1EYjH2MNGoVRdEVCMTCdhdK AND object.balance>1)'
```

To da wszystkie konta NXS z saldem większym niż 10 lub wszystkie konta dla tokena '8Ed7Gzybwy3Zf6X7hzD4imJwmA2v1EYjH2MNGoVRdEVCMTCdhdK' z saldem większym niż 1.

#### Bardziej złożone zapytania

Obecnie nie ma limitu liczby poziomów rekurencji, takich jak:

````
register/list/names WHERE '((object.name=d* AND object.namespace=~GLOBAL~) OR (object.name=e* AND object.namespace=send.to)) OR object.namespace=*s'
````

Powyższe polecenie zwróci wszystkie obiekty zaczynające się na literę 'd', które są nazwami globalnymi, lub wszystkie obiekty zaczynające się na literę 'e' w przestrzeni nazw 'send.to', lub w końcu wszystkie obiekty, które są w przestrzeni nazw, która kończy się na literę 's'.