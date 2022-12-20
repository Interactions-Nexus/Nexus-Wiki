---
title: Konfiguracja górnika
description: 
published: true
date: 2022-12-20T22:59:58.357Z
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

```
{
    "version" : 1,
    "wallet_ip" : "primepool.nexus.io",
    "port" : 50000,
    "local_ip" : "auto",
    "mining_mode" : "PRIME",
    "pool" :
    {
        "username" : "<INSERT_HERE NXS ADDRESS>",
        "display_name" : "<INSERT HERE>"
    },
    "stats_printers" :
    [
        {
            "stats_printer" :
            {
                "mode" : "console"
            }
        }
    ],
    "workers" : 
    [
        {
            "worker" :
            {
                "id" : "myWorker0",
                "mode" : 
                {
                    "hardware" : "gpu",
					"device" : 0
                }
            }
        }
    ]
}
```

&nbsp;

### Hash Solo
```
{
    "version" : 1,
    "wallet_ip" : "127.0.0.1",
    "port" : 9325,
    "local_ip" : "127.0.0.1",
    "mining_mode" : "HASH",
    "connection_retry_interval" : 5,
    "get_height_interval" : 2,
    "ping_interval" : 10,
    "log_level" : 2,
    "logfile" : "miner.log",
    "stats_printers" :
    [
        {
            "stats_printer" :
            {
                "mode" : "console"
            }
        },
        {
            "stats_printer" :
            {
                "mode" : "file",
                "filename" : "stats.log"
            }
        }
    ],
    "print_statistics_interval" : 10,
    "workers" : 
    [
        {
            "worker" :
            {
                "id" : "myWorker0",
                "mode" : 
                {
                    "hardware" : "gpu",
                    "device" : 0
                }
            }
        },
        {
            "worker" :
            {
                "id" : "myWorker1",
                "mode" : 
                {
                    "hardware" : "gpu",
                    "device" : 1
                }
            }
        },
        {
            "worker" :
            {
                "id" : "myWorker2",
                "mode" : 
                {
                    "hardware" : "gpu",
                    "device" : 2
                }
            }
        } 
    ]
}sh
```
&nbsp;

### Hash Pool
```
{
    "version" : 1,
    "wallet_ip" : "hashpool.nexus.io",
    "port" : 50000,
    "local_ip" : "auto",
    "mining_mode" : "HASH",
    "pool" :
    {
        "username" : "<INSERT_HERE NXS ADDRESS>",
        "display_name" : "<INSERT HERE>"
    },
    "stats_printers" :
    [
        {
            "stats_printer" :
            {
                "mode" : "console"
            }
        }
    ],
    "workers" : 
    [
        {
            "worker" :
            {
                "id" : "myWorker0",
                "mode" : 
                {
                    "hardware" : "fpga",
					"serial_port" : "<INSERT HERE>"
                }
            }
        }
    ]
}
```

Aby zapisać plik konfiguracyjny Ctrl+s i Ctrl+x

&nbsp;

#### Bezpośrednie łącze do konfiguracji Minera:

Zapewniamy kilka standardowych konfiguracji kopania, które można pobrać i skonfigurować, aby dopasować je do konfiguracji. Każdy GPU lub FPGA zostanie skonfigurowany jako oddzielny górnik. (Każdy rdzeń na procesorze zostanie skonfigurowany jako górnik — używany do samodzielnego wydobywania w sieci testnet).&#x20;

Pobierz pliki konfiguracyjne z poniższego linku:


- [Przykładowe konfiguracje](https://github.com/Nexusoft/NexusMiner/tree/master/example_configs)
{.links-list}