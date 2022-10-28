---
title: Konfiguracja górnika
description: 
published: true
date: 2022-10-28T21:47:01.112Z
tags: 
editor: markdown
dateCreated: 2022-10-27T22:28:31.131Z
---

# Konfiguracja górnika

Konfiguracja górnika jest najbardziej krytyczną częścią i używa formatu JSON. Ta konfiguracja jest taka sama dla systemu Windows lub Linux.


> **UWAGA:** Upewnij się, że plik wykonywalny NexusMiner i konfiguracja minera znajdują się w tym samym folderze
{.is-info}


Konfiguracja górnika jest przechowywana w pliku **`miner.conf`**, powinien znajdować się w tym samym folderze co plik wykonywalny `NexusMiner`. W systemie Windows lub Linux z interfejsem użytkownika można utworzyć plik tekstowy i zapisać konfigurację oraz zapisać plik jako miner.conf.

W przypadku linux CLI użyj poniższych poleceń:

Aby przejść do folderu Miner, w którym dostępny jest plik wykonywalny NexusMIner, jeśli jest to inny folder, zmień odpowiednio.

````
cd Miner
````

Utwórz plik miner.conf.

````
nano miner.conf
````

Znajdź poniżej pliki konfiguracyjne JSON dla koparek prime i hash. Skopiuj wklej i zmień ustawienia zgodnie z konfiguracją. Pamiętaj, że każdy GPU lub FPGA musi być skonfigurowany jako unikalny górnik. Upewnij się również, że dane "wallet\_ip" "port", "local\_ip", "mining\_mode" i "pool" są poprawne.

W przypadku puli Nexus prime i hash adres wypłaty będzie identyfikatorem puli, a wypłata nagrody zostanie dokonana na ten sam adres. Większość puli ma minimalną kwotę nagrody, którą należy zebrać przed wypłatą.

&nbsp;

### Prime Pool

````
{
    "wersja 1,
    "wallet_ip" : "primepool.nexus.io",
    "port" : 50000,
    "local_ip" : "auto",
    "mining_mode" : "PRIME",
    "basen" :
    {
        "nazwa użytkownika" : "<INSERT_HERE NXS ADDRESS>",
        "display_name" : "<WSTAW TUTAJ>"
    },
    "stats_printers" :
    [
        {
            "stats_printer" :
            {
                „tryb” : „konsola”
            }
        }
    ],
    "pracownicy" :
    [
        {
            "pracownik" :
            {
                "id" : "myWorker0",
                "tryb" :
                {
                    „sprzęt” : „gpu”,
"urządzenie" : 0
                }
            }
        }
    ]
}
````

&nbsp;

### Hash Solo
````
{
    "wersja 1,
    "ip_portfela" : "127.0.0.1",
    "port" : 9325,
    "local_ip" : "127.0.0.1",
    "mining_mode" : "HASH",
    "interwał_ponawiania_ponownych_połączeń" : 5,
    "get_height_interval" : 2,
    "interwał_pingu" : 10,
    "poziom_logowania" : 2,
    "logfile" : "miner.log",
    "stats_printers" :
    [
        {
            "stats_printer" :
            {
                „tryb” : „konsola”
            }
        },
        {
            "stats_printer" :
            {
                "tryb" : "plik",
                "nazwa pliku" : "stats.log"
            }
        }
    ],
    "interwał_statystycznych_druku" : 10,
    "pracownicy" :
    [
        {
            "pracownik" :
            {
                "id" : "myWorker0",
                "tryb" :
                {
                    „sprzęt” : „gpu”,
                    "urządzenie" : 0
                }
            }
        },
        {
            "pracownik" :
            {
                "id" : "myWorker1",
                "tryb" :
                {
                    „sprzęt” : „gpu”,
                    "urządzenie" : 1
                }
            }
        },
        {
            "pracownik" :
            {
                "id" : "myWorker2",
                "tryb" :
                {
                    „sprzęt” : „gpu”,
                    „urządzenie” : 2
                }
            }
        }
    ]
}cii
````
&nbsp;

### Hash Pool
````
{
    "wersja 1,
    "wallet_ip" : "hashpool.nexus.io",
    "port" : 50000,
    "local_ip" : "auto",
    "mining_mode" : "HASH",
    "basen" :
    {
        "nazwa użytkownika" : "<INSERT_HERE NXS ADDRESS>",
        "display_name" : "<WSTAW TUTAJ>"
    },
    "stats_printers" :
    [
        {
            "stats_printer" :
            {
                „tryb” : „konsola”
            }
        }
    ],
    "pracownicy" :
    [
        {
            "pracownik" :
            {
                "id" : "myWorker0",
                "tryb" :
                {
                    „sprzęt” : „fpga”,
"serial_port" : "<WSTAW TUTAJ>"
                }
            }
        }
    ]
}
````

Aby zapisać plik konfiguracyjny Ctrl+s i Ctrl+x

&nbsp;

#### Bezpośrednie łącze do konfiguracji Minera:

Zapewniamy kilka standardowych konfiguracji kopania, które można pobrać i skonfigurować, aby dopasować je do konfiguracji. Każdy GPU lub FPGA zostanie skonfigurowany jako oddzielny górnik. (Każdy rdzeń na procesorze zostanie skonfigurowany jako górnik — używany do samodzielnego wydobywania w sieci testnet).&#x20;

Pobierz pliki konfiguracyjne z poniższego linku:


- [Przykładowe konfiguracje](https://github.com/Nexusoft/NexusMiner/tree/master/example_configs)
{.lista-linków}