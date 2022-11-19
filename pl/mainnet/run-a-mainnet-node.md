---
title: Uruchom Węzeł Sieci Głównej
description: Jak uruchomić węzeł CLI w sieci głównej — Stabilny i Testowy
published: true
date: 2022-11-19T22:26:27.419Z
tags: 
editor: markdown
dateCreated: 2022-11-19T22:10:31.571Z
---

# Uruchom Węzeł Sieci Głównej -CLI

> Ten przewodnik jest dostosowany do dystrybucji systemu operacyjnego Debian / Ubuntu / Raspberry Pi.

## 1. Przed rozpoczęciem tego poradnika:

- Komputer z minimum 1 CPU, 2 GB RAM i 64 GB miejsca na dysku twardym, Raspberry Pi 4 z 2 GB RAM z kartą SD 64 GB.
- W przypadku VPS 1 GB pamięci RAM wystarcza do normalnego użytkowania, w celu konfiguracji zaplecza dapp skontaktuj się [tutaj](https://explorer.nexus.io/).
- [`Ubuntu server 20.04 LTS`](https://ubuntu.com/download/server#downloads) lub [`Debian 11`](https://www.debian.org/download) dla AMD/IA64 lub [ `Ubuntu IOT`](https://ubuntu.com/download/raspberry-pi/thank-you?version=20.04.3&architecture=server-arm64+raspi) / [`Raspberry Pi OS 64 bit`](https://www.raspberrypi.com/software/operating-systems/) dla Raspberry Pi.
- [Etcher](https://www.balena.io/etcher/) – Aby nagrać plik obrazu na kartę SD
- Putty, jeśli używasz SSH przez Windows.

> Aby zainstalować stabilny rdzeń 5.0.5, użyj tylko **Ubuntu 20.04 LTS**. Nowsze wersje Ubuntu, Debian i Raspberry Pi OS (wcześniej Raspbian) mają problemy z kompilacją.
{.is-warning}


> Aby zainstalować gałąź łączącą / 5.1, zaleca się zainstalowanie Debiana 11 lub Ubuntu 20.04. Ubuntu 22.04 będzie wymagać obniżenia wersji openssl do wersji 1.1.1, aby pomyślnie skompilować.
{.is-info}


> Aby zbudować na Raspberry Pi 3 lub 4 z 1 GB pamięci RAM, włącz pamięć wymiany, postępując zgodnie z instrukcjami z łącza poniżej. Kontynuuj po skonfigurowaniu wymiany.
{.is-info}


[Włącz pamięć wymiany na raspberry pi](https://rayanfer32.medium.com/enable-swap-memory-on-ubuntu-on-raspberry-pi-a0f873a65e74)

[Jak uruchomić węzeł — film](https://www.youtube.com/watch?t=942s&v=sA-DUX9KBNU)

&nbsp;

## 2. Przygotuj Węzeł:

[Zainstaluj serwer ubuntu 20.04 LTS](https://ubuntu.com/tutorials/install-ubuntu-server#1-overview) lub wybraną dystrybucję, zainstaluj serwer open-ssh podczas instalacji, a po zakończeniu instalacji zrestartuj węzeł . SSH w węźle i postępuj zgodnie z poniższymi poleceniami. Skopiuj polecenia i wklej je w terminalu za pomocą klawiszy CTRL+SHIFT+v

Zaktualizuj i uaktualnij węzeł:

```
sudo apt update; sudo apt upgrade -y
```

Otwórz port SSH przed włączeniem zapory:

```
sudo ufw allow ssh
```

Zezwól na port API 8080:

```
sudo ufw allow 8080/tcp
```

Zezwól na port RPC 9336:

```
sudo ufw allow 9336/tcp
```

Zezwalaj na port górniczy 9325, tylko w przypadku podłączania górnika:

```
sudo ufw allow 9325/tcp
```

Jeśli działa jako węzeł początkowy, zezwól na port UTS (ujednolicona synchronizacja czasu) 9324, tylko w przypadku podłączenia górnika:

```
sudo ufw allow 9324/tcp
```

Włącz zaporę:

```
sudo ufw enable
```

Sprawdź stan zapory:

```
sudo ufw status
```

Ustaw strefę czasową węzła:

```
sudo dpkg-reconfigure tzdata
```

Aby zmienić nazwę hosta – opcjonalnie:

```
sudo hostnamectl set-hostname <newhostname>
```

Uruchom ponownie węzeł:

```
sudo reboot
```

Komputer jest gotowy do zainstalowania rdzenia Nexusa.

&nbsp;

## 3. Kompilowanie rdzenia Nexusa:

Instaluje zależności wymagane do kompilacji nexus core CLI. Ukończenie zajmie trochę czasu w zależności od szybkości Internetu:

```
sudo apt-get install -y build-essential libssl-dev libdb-dev libdb++-dev libminiupnpc-dev git
```

Pobierz stabilny kod źródłowy rdzenia nexusa, a jego ukończenie powinno zająć tylko kilka sekund:

```
git clone -b 5.0.5 https://github.com/Nexusoft/LLL-TAO
```

Przejdź do katalogu kodu źródłowego:

```
cd LLL-TAO
```

Wyczyść wszystkie poprzednie kompilacje:

```
make -f makefile.cli clean
```

Na koniec uruchom to polecenie, aby skompilować ze źródła. Spowoduje to rozpoczęcie kompilacji rdzenia nexusa. Prosimy o cierpliwość, ponieważ w zależności od procesora może to zająć bardzo dużo czasu. Zamień `1` w `j1` na liczbę rdzeni / wątków, aby kompilować szybciej:

```
make -f makefile.cli -j1 AMD64=1
```

Do kompilacji na Raspberry Pi użyj:

```
make -f makefile.cli -j1 ARM64=1
```

Po udanej kompilacji pokaże komunikat “Finished building nexus”.

&nbsp;

## 4. Skonfiguruj portfel (nexus.conf):

Utwórz główny katalog danych Nexusa (jest to ukryty katalog, demon Nexusa tworzy go automatycznie przy pierwszym uruchomieniu. Tworzymy go ręcznie, aby utworzyć plik konfiguracyjny. Jeśli katalog jest już dostępny, pomiń ten krok).

```
mkdir ~/.Nexus
```
 
> Konfiguracja portfela jest przechowywana w pliku nexus.conf, znajdującym się w głównym katalogu danych.
{.is-info}


Utwórz plik nexus.conf:

```
nano ~/.Nexus/nexus.conf
```

Skopiuj poniższy kod do pliku. Podaj użytkownika i hasło do RPC i API oraz usuń `#` w `#stake=1`, jeśli zamierzasz stakować.

```
# This is an example nexus.conf. Tailor it to your deployment.
#RPC credentials, change as needed
rpcuser=<user for RPC>
rpcpassword=<pw for RPC>
#API http authentication credtnials. Change as needed
apiuser=<user for API>
apipassword=<pw for API>
#To run the nexus core as a daemon
daemon=1
#To enable mining with the node, 
#mining=1
#To enable staking
#stake=1
```

Aby uzyskać zdalny dostęp do portfela (z interfejsu portfela na innym komputerze), dodaj następujące wiersze w pliku konfiguracyjnym.

`<ipaddress>` to adres IP maszyny łączącej się zdalnie z twoim węzłem, może to być adres IP interfejsu lub serwera dapp. Możesz także użyć symbolu wieloznacznego '*' aby zezwolić wszystkim komputerom w określonej podsieci. `llpallowip=192.168.10.*:8080` zezwala wszystkim komputerom w sieci lokalnej 192.168.10

```
#To enable RPC remote access
rpcremote=1
#To enable API authentication 
apiauth=1
#To enable remote API access. Local API access will be revoked
apiremote=1
#Whitelist IP address for API & RPC
llpallowip=<ipaddress>:8080  
llpallowip=<ipaddress>:9336
```

W przypadku testowania łączącej się gałęzi / 5.1 :

```
#To index block data, required to access block data.
indexheight=1
#To index account addresses, required to access the account address.
indexaddress=1
```

Jeśli działa jako węzeł początkowy, dodaj poniższe wiersze do pliku konfiguracyjnego:

> Węzły początkowe (seed nodes) muszą mieć statyczny adres IP i przepustowość łącza internetowego.
{.is-info}


```
#Unified time synchronization
unified=1
llpallowip=*.*.*.*:9324
```

Jeśli działa jako węzeł początkowy lub potrzebujesz więcej połączeń równorzędnych z węzłem, dodaj to do konfiguracji:

> Zwiększenie liczby połączeń równorzędnych zwiększy wymagania dotyczące przepustowości węzła.
{.is-warning}

```
#Configure peer connections to the core
#Maximum connections limit to the node
maxconnections=300
#Maximum incoming to a single node (maxconnections - 16)
maxincoming=284
```
Naciśnij Ctrl-S Ctrl-X, aby zapisać i wyjść z edytora.

&nbsp;

## 5. Uruchamianie bazy danych trytu:

Ten krok spowoduje pobranie bazy danych nexus, a następnie rozpakowanie jej do folderu danych. Alternatywnie możesz pominąć ten krok, jeśli zdecydujesz się zsynchronizować dane z rówieśników, co będzie wolne w zależności od połączenia internetowego.

```
cd ~
```

Spowoduje to pobranie bazy danych do folderu domowego. Plik ma rozmiar około 5 GB.

```
wget -c http://bootstrap.nexus.io/tritium.tar.gz
```

Spowoduje to wyodrębnienie bazy danych do głównego katalogu danych Nexusa

```
tar -xf tryt.tar.gz -C ~/.Nexus
```

&nbsp;

## 6. API do kontrolowania węzła:

Aby wchodzić w interakcje z demonem nexus core, użyj poleceń API za pośrednictwem terminala. Zmień lokalizację na folder ~/LLL-TAO, aby interfejsy API działały. Aby uruchomić węzeł, stawkę i transakcję, będziemy używać tylko systemu, użytkowników i finansowych interfejsów API. W razie wątpliwości zajrzyj do dokumentacji API [tutaj](../../api/api-overview/tritium-api/).

&nbsp;

### **Zanim zaczniemy:**

- Uważaj, ponieważ dane logowania są w terminalu i mogą być widoczne dla każdego w pobliżu.
- Terminal Bash zapisuje historię wszystkich wcześniej użytych poleceń.
- Każda transakcja będzie wymagać kodu PIN, chyba że zostanie odblokowana dla transakcji.
- Każda transakcja na blockchainie Nexusa jest obciążeniem konta wysyłającego i uznaniem konta odbierającego, czyli dwiema transakcjami. (Przyda się to do zrozumienia niektórych poleceń API)

Przejdź do katalogu LLL-TAO, aby uruchomić rdzeń nexusa (Przejdź do folderu LLL-TAO, aby uruchomić następujące polecenia)

```
cd LLL-TAO
```

### Aby uruchomić demona:

```
./ogniwo
```

Nexus core będzie działał w tle jako demon. Wykryje rówieśników i zsynchronizuje łańcuch bloków. Znalezienie rówieśników zajmie kilka minut

### Aby zatrzymać demona:

```
./system nexus/stop
```

### Aby uzyskać informacje o węźle:

```
./nexus system/get/info
```

Dane wyjściowe API są w formacie json. Możesz potwierdzić, czy węzeł jest zsynchronizowany, zaznaczając „synchronising”: false i „synccomplete”: 100. Sprawdź wysokość bloku w eksploratorze [tutaj](http://explorer.nexus.io) lub [tutaj](https ://nxsorbitalscan.com)

Po pełnej synchronizacji łańcucha blokowego utwórz nowe konto użytkownika (łańcuch podpisów).

Nazwa użytkownika musi mieć co najmniej 2 znaki, hasło musi mieć 8 znaków, a PIN 4 znaki. PIN może być kombinacją liter/cyfr/symboli.

```
./nexus users/create/user username= hasło= pin=
```

Aby zalogować się na konto (jeśli konto zostało właśnie utworzone, poczekaj kilka bloków, aby potwierdzić nowe konto)

```
./nexus users/login/user username= hasło= pin=
```

Aby odblokować konto do obstawiania i automatycznego uznania transakcji przychodzących (notifications=1). Jeśli nie jest ustawiona, ręcznie uznaj transakcje przychodzące, w przeciwnym razie zostanie ona zwrócona na konto nadawcy po 24 godzinach. Jest to odwracalna funkcja transakcji działająca zgodnie z założeniami.

```
./nexus users/unlock/user pin= obstawianie=1 powiadomienia=1
```

Aby sprawdzić informacje o stawce (działa tylko po zalogowaniu i odblokowaniu do obstawiania)

```
./nexus finance/get/stakeinfo
```

Aby uzyskać szczegółowe informacje o kontach i adresach zalogowanych użytkowników. (Konta zaufane i domyślne są tworzone automatycznie z nowym kontem)

```
./użytkownicy nexusa/lista/konta
```

Spowoduje to wyświetlenie listy wszystkich kont i jego szczegółów

```
./nexus finance/lista/konta
```

Spowoduje to wyświetlenie wszystkich transakcji wysłanych do określonej genezy lub nazwy użytkownika. Jest to przydatne do identyfikowania transakcji, które należy zaakceptować, takich jak kredyty.

```
./użytkownicy nexusa/lista/powiadomienia
```

Jeśli automatyczny kredyt (`notifications=1`) nie jest określony jako opcja z poleceniem `unlock`, zostanie to odzwierciedlone jako oczekująca transakcja i zostanie