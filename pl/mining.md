---
title: Górnictwo
description: 
published: true
date: 2022-10-27T21:55:16.040Z
tags: 
editor: markdown
dateCreated: 2022-10-20T21:21:43.179Z
---

# Górnictwo

Nexus ma trzy kanały konsensusu, dwa górnicze `hash` , `prime`, a trzeci to `stake`. Każdy może kopać na Nexusie i nie potrzebuje pozwolenia. Zespół programistów Nexusa ma dedykowany zespół programistów ds. górnictwa, który zajmuje się obsługą górników i puli.

## Wsparcie górnicze:

Aby uzyskać pomoc lub wsparcie związane z wydobywaniem, dołącz do naszego kanału Telegram, do którego link znajduje się poniżej:

[NexusMiners](/https://t.me/NexusMiners)

## Kanały górnicze:

* **Prime Mining:** GPU - Obsługuje zarówno Solo & Pool.
* **Hash Mining:** GPU lub FPGA’s - Obsługuje zarówno Solo & Pool.

> **Dobrze wiedzieć:** Nie zalecamy kopania CPU prime lub hash mining, ponieważ nie jest to opłacalne i służy tylko do kopania sieci testowej.
{.is-info}

### Solo Mining:

Solo oznacza pojedyncze lub indywidualne wydobycie. Wymaga połączenia górnika z portfelem Nexusa. Portfel i koparka mogą być uruchomione na tym samym lub oddzielnym komputerze, szczególnie podczas kopania za pomocą FPGA.&#x20;

> **Dobrze wiedzieć:** Wydobycie solo nie jest opłacalne dla prime i hash, chyba że masz bardzo dużą konfigurację wydobywczą.
{.is-info}

### Pool Mining

Wydobycie puli jest podobne do wydobycia grupowego, a górnik musi być podłączony do puli wydobywczej. Górnik jest bezpośrednio połączony z pulą, a nagrody za wydobycie są wypłacane górnikom w zależności od procentu indywidualnej stawki haszowania. Za wydobycie w puli pobierane są opłaty, które są odliczane od wypłat za wydobycie.&#x20;

## Mining Pools dla Nexus:

Zespół wydobywczy utrzymuje otwarte pule górnicze dla górników:

## Prime Pool:

Link do strony głównej puli:

[primepool.nexus.io](https://primepool.nexus.io)

Zespół wydobywczy Nexusa udostępnił otwartą pule prime. Aby użyć tej puli, skopiuj poniższe wiersze w konfiguracji górnika.

```
    "wallet_ip" : "primepool.nexus.io", 
    "port" : 50000,
```

## Hash Pool:

Zespół wydobywczy Nexusa udostępnił otwartą pulę hash. Aby dołączyć do puli, użyj poniższych linii w konfiguracji górnika.

```
    "wallet_ip" : "hashpool.nexus.io", 
    "port" : 50000,
```

Link do strony internetowej puli hash:

[hashpool.nexus.io](https://hashpool.nexus.io)


## Kompatybilny sprzęt górniczy

NexusMiner może korzystać z CPU, GPU dla Prime i FPGA dla Hash mining. Kopanie procesora nie jest zalecane, ponieważ nie jest wydajne.

### GPU:

Jeśli korzystasz z kopania GPU, NexusMIner V1.5 obsługuje zarówno procesory graficzne Nvidia, jak i AMD. Rdzenie CUDA firmy Nvidia są w pełni obsługiwane i działają wydajnie. Wsparcie AMD zostało niedawno włączone tylko dla wersji prime tylko na linuksie i zajmie trochę czasu, zanim będzie w pełni wydajna.&#x20;

> **Dobrze wiedzieć:** Obsługa procesorów graficznych AMD jest wciąż na wczesnym etapie i zostanie ulepszona w przyszłości
{.is-info}

Aby w pełni wykorzystać możliwości kart graficznych NVIDIA, zalecamy korzystanie z najnowszych sterowników graficznych i [MSI Afterburner](https://www.msi.com/Landing/afterburner/vga).


> Nie instaluj sterowników kreatora treści Nvidia, ponieważ koparka nie będzie działać poprawnie.
{.is-warning}

## FPGA:

Koparki FPGA dla Nexusa są dostępne tylko od [Blackminer](https://www.hashaltcoin.com/en/miners). Tych koparek można używać tylko na kanale Hash.

### Kalkulator górniczy:

Aby lepiej zrozumieć wydajność wydobycia różnych urządzeń, skorzystaj z kalkulatora wydobycia, do którego link znajduje się poniżej:

[Link do kalkulatora górniczego](https://primepool.nexus.io/mining\_calc/)

## Chapters
- [Kopanie w Windows *Jak kopać w systemie Windows*](/pl/mining/mining-on-windows)
- [Kopanie na Linuksie *Jak kopać na Linuksie*](/pl/mining/mining-on-linux)
- [Konfiguracja górnika *Jak skonfigurować górnika*](/pl/mining/miner-config)
- [Tabela Hash-Rate *To jest tabela Hash-Rate wydobycia Nexusa*](/pl/mining/hash-rate-table)
{.links-list}