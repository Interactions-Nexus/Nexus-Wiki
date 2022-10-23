---
title: Węzły i rdzeń
description: Czym są węzły i rdzeń?
published: true
date: 2022-10-23T20:50:25.210Z
tags: 
editor: markdown
dateCreated: 2022-10-21T21:56:44.831Z
---

# Węzły i rdzeń
## WĘZEŁ

Nexus to rozproszona sieć komputerów z oprogramowaniem (znanych jako węzły), które mogą weryfikować bloki i dane transakcji. Aby „uruchomić” węzeł, uczestnicy potrzebują na komputerze aplikacji zwanej rdzeniem.

### TYPY WĘZŁÓW

Rdzeń Nexusa można skonfigurować tak, aby działał jako różne typy węzłów, które w różny sposób zużywają dane. Rdzeń Nexusa może obsługiwać dwa różne typy węzłów — pełny i lekki.&#x20;

### Pełny węzeł

* Przechowuje pełne dane łańcucha bloków.
* Uczestniczy w walidacji bloków, weryfikuje wszystkie bloki i stany.
* Wszystkie stany mogą pochodzić z pełnego węzła.
* Obsługuje sieć i udostępnia dane na żądanie.

### Węzeł Lite

* Przechowuje nagłówki bloków i dane łańcucha sygnatur i żąda wszystkiego innego.
* Potrafi zweryfikować ważność danych w stosunku do korzeni stanu w nagłówkach bloków.
* Przydatne w przypadku urządzeń o małej pojemności, takich jak urządzenia wbudowane, IoT i telefony komórkowe, których nie stać na przechowywanie gigabajtów danych blockchain.

## CORE <a href="#evm" id="evm"></a>

Core to programowa implementacja protokołów, które zasilają sieć Nexusa. Uczestnicy sieci uruchamiają rdzeń na komputerze, który łączy się i komunikuje z innymi komputerami obsługującymi rdzeń za pośrednictwem Internetu, tworząc jedną całość, którą jest sieć Nexus.

#### Rdzeń zawiera:&#x20;

Biblioteka niższego poziomu (LLL), która jest serią szablonów dla krypto, bazy danych i protokołu. Podstawowe szablony dla frameworka TAO, które dziedziczą te szablony i tworzą wyższy poziom funkcjonalności.

Tritium Amine Obsidian (TAO) — protokoły, które zarządzają siecią Nexus, wykorzystujące LLL jako podstawowe szablony dla zestawów funkcji Tritium, Amine i Obsidian.