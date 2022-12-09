---
title: Stakowanie - Wymagania
description: Wymagania sprzętowe do stakowania
published: true
date: 2022-12-09T00:05:11.175Z
tags: 
editor: markdown
dateCreated: 2022-12-08T23:57:10.780Z
---

# Stakowanie - Wymagania

## **System operacyjny:**

Obsługiwane są wszystkie główne systemy operacyjne (OS), ale zalecanym przez społeczność systemem operacyjnym jest Ubuntu LTS lub pochodne. Można użyć dowolnej dystrybucji Linuksa, jednak przewodniki zostały dostosowane do Ubuntu.

## **Wymagania dotyczące komputera:**

Demon został przetestowany i działa bezbłędnie na Raspberry Pi 3B+ z 1 GB RAM, ale minimalne zalecenia są następujące, aby uwzględnić wzrost:

### **ARM:**

Raspberry Pi 4B z 2 GB RAM lub równoważnym SBC z 2 GB i kartą SD o pojemności co najmniej 64 GB (tylko w przypadku systemu Linux/Daemon/CLI).

### **x64:**

Dowolny procesor z 4 GB RAM. Przed zainstalowaniem portfela upewnij się, że masz co najmniej 30 GB wolnego miejsca na dysku twardym.


> **Nota:** Pełny węzeł pobierze kompletną kopię bazy danych łańcucha bloków i na dzień dzisiejszy wyodrębniona baza danych ma rozmiar około 16 GB i rośnie z czasem. Węzły Lite będą przechowywać tylko nagłówki bloków i dane łańcucha sygnatur, radykalnie minimalizując wpływ na pamięć masową, około 250 MB.
{.is-info}

## **Modułowa konstrukcja portfela:**

Portfel Nexus zawiera modułową funkcjonalność składającą się z interfejsu, szkieletu modułu i rdzenia. Intuicyjny interfejs zapewnia użytkownikom i firmom łatwą i bezproblemową obsługę. Węzeł może również działać jako demon wyłącznie z zarządzaniem dostępnym przez API lub zdalny interfejs. Jest to korzystne w przypadku uruchamiania węzła stakingowego w systemie bezgłowym, takim jak Raspberry Pi lub NUC.

## **Ekonomiczne wdrożenia i IoT:**

Podstawową zasadą PoS jest zabezpieczanie sieci i zapewnia to zachętę. Operatorzy węzłów ponoszą wydatki na sprzęt, zarządzanie, przepustowość i energię elektryczną. Instrukcje w tej sekcji zapewniają optymalną konfigurację dla ścisłych budżetów i branży IoT.

### **Zwykli użytkownicy (portfel GUI):**&#x20;

Dowolny komputer spełniający minimalne wymagania. Jeśli staking jest jedyną planowaną usługą, zalecany jest Intel NUC core i3 / Ryzen 3 lub odpowiednik z 4 GB RAM i 120 GB SSD. Jeśli komputer stakingowy będzie używany do innych celów, należy odpowiednio zwiększyć pamięć i miejsce na dysku.


> Intel NUC lub odpowiednik będzie dobrym wyborem, jeśli szukasz samodzielnego węzła do stakingu.
{.is-info}



### **Użytkownicy zaawansowani (portfel CLI):**&#x20;

Raspberry Pi (RPI) 4 z 2/4 GB, NUC lub odpowiednikiem będzie obsługiwał bezgłowy rdzeń, a użytkownicy mogą sterować nim za pośrednictwem interfejsu z innego komputera. (RPI może uruchamiać tylko demona CLI, więc konieczna jest interakcja z wiersza poleceń. Nexus ma świetne przewodniki krok po kroku, które pomogą tym, którzy nie są zaznajomieni).

![Daemon portfela Nexusa staking na Raspberry Pi 4 zajmuje tylko 243 MB pamięci RAM i jest ogólnie bardzo oszczędny pod względem zasobów.](https://nexus.io/ResourceHub/images/guide/stake-guide1.png#)Rdzeń wymaga bardzo mało zasobów, nawet na Raspberry Pi.