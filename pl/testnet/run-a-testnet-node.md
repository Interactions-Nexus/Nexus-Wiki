---
title: Uruchom Węzeł Sieci Testowej
description: Uruchom węzeł w sieci testowej, aby przetestować interfejsy API lub aplikacje
published: true
date: 2022-11-24T23:36:40.524Z
tags: 
editor: markdown
dateCreated: 2022-11-24T23:01:38.536Z
---

# Uruchom Węzeł Sieci Testowej

Ten przewodnik pomoże skonfigurować węzeł w sieci testowej nexusa. Dołączenie do sieci testowej nie wymaga żadnych uprawnień, a użytkownicy mają pełną kontrolę nad dedykowanym węzłem.

Konfiguracja węzła będzie się różnić w zależności od indywidualnych wymagań aplikacji lub ilości generowanych transakcji.

> Jeśli potrzebujesz pomocy w zakresie specyfikacji węzła dla konkretnej aplikacji, skontaktuj się z pomocą techniczną dla programistów [tutaj](https://t.me/NexusDevelopers).
{.is-info}

## 1. Zanim zaczniesz:

* Komputer z minimum 1 CPU, 1 GB RAM, 20 GB miejsca na dysku, Raspberry Pi 4 z 2 GB RAM.
* VPS z 1 GB RAM jest wystarczający do normalnego użytkowania.
* [`Ubuntu server 20.04 LTS`](https://ubuntu.com/download/server#downloads) lub [`Debian 11`](https://www.debian.org/download) dla AMD/IA64 lub [ `Ubuntu IOT`](https://ubuntu.com/download/raspberry-pi/thank-you?version=20.04.3\&architecture=server-arm64+raspi) / [`Raspberry Pi OS 64 bit`](https://www.raspberrypi.com/software/operating-systems/) dla Raspberry Pi (Użyj dowolnej wybranej dystrybucji Linuksa, ale ten przewodnik jest dostosowany do Debiana / Ubuntu).
* Dysk USB lub karta SD do instalacji ubuntu.
* Etcher – Aby nagrać plik obrazu systemu operacyjnego na kartę USB/SD.
* Putty, jeśli używasz ssh przez Windows.

> Nie używaj Ubuntu 22.04, ponieważ ma nową wersję openssl, która łamie kompatybilność z rdzeniem.
{.is-info}

## 2. Linki do węzłów Testnet Mining:

Poniżej wymieniono węzły górnicze sieci testowej.

- http://testnet1.interactions-nexus.io
- http://testnet2.interactions-nexus.io
- http://testnet3.interactions-nexus.io

## 3. Porty sieci testowej:

Sieć testowa używa innego zestawu portów niż sieć główna. Jeśli używasz zapory, upewnij się, że zezwoliłeś na następujące porty. Wersja Legacy jest wyłączona, dlatego port RPC 8336 jest niedozwolony.

* 7080 - API port
* 8325 - Port górniczy, włączony tylko w przypadku wydobycia w sieci testowej
* 8888 - Wychodzące połączenia węzłowe

## **4. Przygotuj węzeł:**

[Zainstaluj serwer ubuntu 20.04 LTS](https://ubuntu.com/tutorials/install-ubuntu-server#1-overview) lub wybraną dystrybucję, zainstaluj serwer open-ssh podczas instalacji, a po zakończeniu instalacji uruchom ponownie węzeł. SSH w swoim węźle i postępuj zgodnie z poniższymi poleceniami. Możesz skopiować polecenia i wkleić je w terminalu za pomocą klawiszy CTRL+SHIFT+v

Zaktualizuj swój węzeł:

```
sudo apt update
```

Zaktualizuj swój węzeł:

```
sudo apt upgrade -y
```

Otwórz port SSH przed włączeniem zapory:

```
sudo ufw allow ssh
```

Zezwól na port API 7080

```
sudo ufw allow 7080/tcp
```

Zezwól na połączenia wychodzące na porcie 8888

```
sudo ufw allow 8888/tcp
```

Zezwalaj na port wydobywczy 8325, tylko w przypadku wydobycia

```
sudo ufw allow 8325/tcp
```

Włącz Firewall:

```
sudo ufw enable
```

Sprawdź stan zapory:

```
sudo ufw status
```

Ustaw swoją strefę czasową:

```
sudo dpkg-reconfigure tzdata
```

Jeśli musisz zmienić nazwę hosta – nieobowiązkowa, jeśli już ją ustawiłeś podczas instalacji

```
sudo hostnamectl set-hostname <newhostname>
```

Uruchom ponownie węzeł:

```
sudo reboot
```

mamy nasz komputer gotowy do zainstalowania rdzenia nexusa