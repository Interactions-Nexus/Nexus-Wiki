---
title: Sklep Budowlany
description: Przypadki użycia w świecie rzeczywistym dla sklepów stacjonarnych
published: true
date: 2022-10-29T22:08:11.079Z
tags: 
editor: markdown
dateCreated: 2022-10-23T12:12:01.736Z
---

# 🏪 Sklep Budowlany
Nexus został zaprojektowany z myślą o prawdziwym świecie, do codziennego użytku przez przeciętnego użytkownika i może być zrozumiały w tym przypadku użycia. Można to łatwo wdrożyć w dowolnym sklepie stacjonarnym i samochodowym, aby zarządzać sklepem poprzez integrację Nexusa.

Nexus może być używany do płatności, faktur, logistyki i śledzenia, internetowego rynku. Aby to ułatwić, musimy zrozumieć, jak te rzeczy można wdrożyć.


> W zależności od lokalizacji i lokalnych przepisów płatności kryptograficzne mogą nie być możliwe. System może wymagać dostosowania do lokalnych przepisów.
> {.is-warning}


## Jak można to zaimplementować

Sklepy stacjonarne będą korzystać z funkcji sieci hybrydowej, w której będą mogły przyjmować płatności od klientów i wykorzystywać faktury do przyjmowania płatności i płacenia dystrybutorom w sieci publicznej. Podczas gdy mogą zarządzać zapasami i dbać o logistykę w prywatnym łańcuchu. Ułatwia to, ponieważ w łańcuchu prywatnym nie ma żadnych opłat, a dane są prywatne.

Sklep może nawet mieć sklep internetowy obsługiwany przez API P2P, który jest siecią wymiany ksiąg zamówień.

Sklep musi zintegrować Nexus API z zupełnie nowym systemem Point of Sale (POS) lub zintegrować się z istniejącymi systemami.

## Koszty ogólne dla sklepu

Właściciel sklepu będzie musiał uruchomić węzły, aby utrzymać sieć hybrydową. Liczba węzłów będzie zależeć od nadmiarowości wymaganej przez bazę danych. W porównaniu z istniejącymi systemami koszty ogólne są bardzo niskie. Jeśli właściciel sklepu potrzebuje 3x nadmiar, musi uruchomić 3 węzły, które będą hostowane na VPS lub posiadanym sprzęcie lub mieszankę obu.

Nowy POS lub integracja z systemem może być dodatkowym kosztem, ale jeśli uda nam się stworzyć kod open source, który może być używany przez każdy sklep, który może zaoszczędzić na tych kosztach.

## Jakie rzeczy mogą wdrożyć Sklepy

Sklepy budowlane mogą korzystać z jednej lub wszystkich opcji wymienionych poniżej:

### Płatności:

Interfejs Nexusa będzie miał moduł płatności w punkcie sprzedaży. Ułatwi to klientom płacenie za pomocą portfela mobilnego. Będzie to podobne do Apple Pay lub Google Pay, gdzie użytkownik skanuje kod QR, aby wysłać płatność. Sklep może nawet zintegrować interfejs API Nexusa z istniejącym systemem. Dzięki Query DSL bardzo łatwo jest śledzić wszystkie płatności i generować raporty.

### Faktury:

Sklep może wystawiać faktury lub akceptować faktury od dystrybutorów, które będą na bieżąco śledzić wszystkie dokonane płatności. Dostęp do tego można uzyskać za pomocą modułu fakturowania interfejsu lub integrując API faktury z istniejącym systemem. Raporty są wbudowane w interfejs API faktur i można je dodatkowo zawęzić za pomocą wyszukiwania w łańcuchu obsługiwanego przez Query DSL.

### Śledzenie zapasów:

Nexus ma interfejs API dostaw, którego można używać do śledzenia zapasów. Dane te będą przechowywane po prywatnej stronie sieci hybrydowej, która nie wiąże się z żadnymi opłatami, jest bardzo szybka i bezpłatna. Każda pozycja będzie miała swój własny kod QR generowany podczas wybijania jako pozycja, a istniejące kody kreskowe produktów można zintegrować z pozycjami zaopatrzenia jako unikalny identyfikator lub nazwę.

### Rynek internetowy:

Sklepy budowlane również mogą być obecne na rynku online z nadchodzącym rynkiem P2P, który może być używany do wymiany tokenów i aktywów. Właściciele sklepów muszą tworzyć swoje dobra fizyczne jako aktywa w łańcuchu publicznym, wystawiać je na sprzedaż z lokalizacją i nazwą sklepu. Użytkownicy mogą wyszukiwać zasoby dostępne w ich okolicy za pomocą lokalizacji i kupować je online, a właściciel sklepu może korzystać z API łańcucha dostaw publicznych do śledzenia towarów wysyłanych kurierem.