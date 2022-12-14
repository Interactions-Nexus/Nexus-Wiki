---
title: Biblioteka niższego poziomu
description: LLL
published: true
date: 2022-12-14T22:10:12.584Z
tags: 
editor: markdown
dateCreated: 2022-10-21T22:10:53.117Z
---

# Biblioteka niższego poziomu (LLL)

Biblioteka Niższego Poziomu (LLL) jest podstawą dla Ramy TAO. Jest to podstawowa biblioteka szablonów napisana w C++, minimalizująca abstrakcję sprzętową, maksymalizując w ten sposób wydajność bare metal. Architektonicznie LLL jest wymienną konstrukcją wymagającą logicznego opracowania szablonów i modułów dla określonych funkcji. LLL-TAO lub TAO Framework to seria szablonów i modeli danych LLL, które są dostępne za pośrednictwem prostego interfejsu API opartego na JSON, umożliwiając każdemu programiście poprawę bezpieczeństwa, skalowalności i niezawodności aplikacji.

LLL zawiera trzy główne komponenty: kryptografię (LLC), bazę danych (LLD) i protokół (LLP). W stosie jest kilka reprezentacji LLD; Księga, Rejestr, Operacje i API. LLC stosuje się głównie w warstwie Księgi, chociaż można ją wdrożyć gdzie indziej. Jako składnik warstwy sieciowej, LLP ma być lekkim, szybkim protokołem, który pozwala programiście dostosować projekt pakietu i interpretację wiadomości.

## Kryptografia niższego poziomu (LLC)

#### Zestaw operacji do obsługi Crypto, w tym:

* Podpisy cyfrowe (ECDSA, oparte na hashu)
* Haszowanie (SHA3 / Wybitne bezpieczne algorytmy)
* Szyfrowanie (symetryczne / asymetryczne)
* Kryptografia post-kwantowa (eksperymentalna)

#### Obecnie wdrożone:

* SK Hashing (Skein i Keccak)
* Haszowanie hasła Argon2
* Standard AES (symetryczny)
* FALCON (odporne kwantowo sygnatury kratowe)
* Funkcje zawijania OpenSSL (EC\_KEY, BIGNUM)

## Baza danych niższego poziomu (LLD)

Zestaw szablonów do projektowania wysokowydajnych systemów bazodanowych. Szablony podstawowe można rozszerzyć na typy baz danych wyższego poziomu.

* Baza danych Keychain
* Transakcje ACID
* Baza danych Sector

Uwzględnione łańcuchy kluczy:

* Binarna mapa plików
* Binarna mapa hashów

Z zadowoleniem przyjmujemy wszelkie wkłady nowych łańcuchów kluczy, aby zapewnić różne struktury danych indeksowania danych sektorowych.

## Protokół niższego poziomu (LLP)

Zestaw szablonów Klient/Serwer do wydajnej obsługi danych. Dziedzicz i twórz niestandardowe typy pakietów, aby z łatwością napisać nowy protokół i bez konieczności programowania sieci.

* Serwer danych
* Serwer nasłuchiwania
* Typy połączeń
* Style pakietów
* Wyzwalacze zdarzeń
* DDOS dławienie

Wdrożone protokoły LLP:

* Legacy
* Tritium
* HTTP

## Narzędzia

Zestaw przydatnych narzędzi do tworzenia dowolnego programu, takich jak:

* Serializacja
* Czas pracy
* Debugowanie
* Json
* Argumenty
* Pojemniki
* Konfiguracja
* Sortowanie
* Alokatory
* System plików
