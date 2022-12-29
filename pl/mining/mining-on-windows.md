---
title: Kopanie w Windows
description: 
published: true
date: 2022-12-29T23:07:09.011Z
tags: 
editor: markdown
dateCreated: 2022-10-27T21:56:39.030Z
---

# Kopanie w Windows

Ten przewodnik pomoże skonfigurować kopanie w systemie Windows. Nowy NexusMiner bardzo ułatwia kopanie w systemie Windows. Nexus ma własną otwartą prime pulę wydobywczą, a deweloperzy pracują nad dalszą decentralizacją wydobycia.

## Pobierz Górnika:

Pobierz plik wykonywalny Windows Miner z poniższego linku (nie jest to instalator)


> Górnik nie może jednocześnie uruchamiać trybu prime i hash na jednym komputerze.
{.is-warning}

[NexusMiner](https://github.com/Nexusoft/NexusMiner)

## Konfiguracja górnika:&#x20;

Aby skonfigurować górnika, sprawdź poniższy link:&#x20;

- [Konfiguracja górnika *Jak skonfigurować górnika*](/pl/mining/miner-config)
{.links-list}

## Portfel na komputer Nexus:


> To jest tylko dla górników solo. Górnicy w puli mogą pominąć ten krok.
{.is-info}

### Interfejs Nexusa:

Pobierz i zainstaluj interfejs Nexusa lub skonfiguruj rdzeń CLI.&#x20;

Uruchom portfel, utwórz użytkownika, zaloguj się i odblokuj portfel do wydobywania i powiadomień.

&nbsp;

#### Ustawienia kopania w interfejsie:

1. Przejdź do ustawień> Rdzeń> Włącz wydobywanie, klikając przycisk przełączania obok niego.&#x20;
2. Poniżej pojawi się nowe pole: Mining IP Whitelist. wpisz `<ipaddress:port>` górnika. Jeśli wydobywasz na tym samym komputerze, wpisz `127.0.0.1:9325`, jeśli górnik działa na innym komputerze lub FPGA, wpisz konkretny `ipaddress:9325`. Jeśli jest więcej niż jeden górnik, użyj '; ', aby oddzielić adresy IP. Symbole wieloznaczne `*` są obsługiwane tylko dla adresów IP, np.: 192.168.10.*:9325.

&nbsp;

## Rdzeń Nexusa

Jeśli używasz rdzenia Nexusa, dodaj linię `llpallowip=<ipaddress:port>` w nexus.config dla każdego górnika. Użyj 127.0.0.1:9325 do kopania na tym samym komputerze lub adresu ipaddress:9325 dla oddzielnego górnika.

Uruchom ponownie rdzeń, aby zmiany zaczęły obowiązywać


> **Warto wiedzieć:** Aby wydobycie solo mogło działać, użytkownik musi być zalogowany i odblokowany dla wydobycia i powiadomień.
{.is-info}


## Uruchom górnika

Przejdź do folderu, w którym znajduje się plik wykonywalny NexusMiner i miner.conf, kliknij dwukrotnie plik wykonywalny NexusMiner. Pojawi się okno z ostrzeżeniem o bezpieczeństwie (pokazane na obrazku poniżej), kliknij uruchom, a górnik uruchomi się w terminalu. Górnik uruchomi się i rozpocznie wydobycie, co można zobaczyć w komunikatach w oknie terminala górnika. Nie jest wymagana interakcja użytkownika.&#x20;

![securitywarning.png](/securitywarning.png)<p align="center"  style="color:dodgerblue;">*Windows — ostrzeżeniem o bezpieczeństwie*</p>

Aby sprawdzić, czy wszystko działa, przejdź do poniższego linku do strony puli wydobycia, w prawym nagłówku wklej adres Nexusa wpisany w pliku miner.conf w polu wyszukiwania i kliknij szukaj. Otworzy się strona taka jak poniżej, na której możesz zobaczyć szczegóły swojego górnika.&#x20;

- [**Strona internetowa Prime Pool Miner**](https://primepool.nexus.io/)

![miningdetails.png](/miningdetails.png)<p align="center"  style="color:dodgerblue;">*Prime Pool Account Overview*</p>

## Zatrzymaj górnika

Aby zatrzymać górnika, zamknij okno terminala NexusMiner.

## Zrzuty ekranu

![minerconfig.png](/minerconfig.png)<p align="center"  style="color:dodgerblue;">*miner.conf dla  prime pool z 1 GPU*</p>

![minerwindows.png](/minerwindows.png)<p align="center"  style="color:dodgerblue;">*NexusMiner v1.4 Prime Pool kopanie z jednym GPU*</p>

![minerwindowsshare.png](/minerwindowsshare.png)<p align="center"  style="color:dodgerblue;">*NexusMiner v1.4 Prime Pool - przesłany blok*</p>

![minerconf1.png](/minerconf1.png)<p align="center"  style="color:dodgerblue;">*miner.conf dla prime pool z 1 GPU & 2 rdzeniami CPU*</p>

![minerwindows2.png](/minerwindows2.png)<p align="center"  style="color:dodgerblue;">*NexusMiner v1.4 Prime Pool kopanie z jednym GPU i dwoma rdzeniami CPU*</p>