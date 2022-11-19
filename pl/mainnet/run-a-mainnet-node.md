---
title: Uruchom Węzeł Sieci Głównej
description: Jak uruchomić węzeł CLI w sieci głównej — Stabilny i Testowy
published: true
date: 2022-11-19T22:10:31.571Z
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

Jeśli działa jako węzeł inicjujący, zezwól na port UTS (ujednolicona synchronizacja czasu) 9324, tylko w przypadku podłączenia górnika:

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

Instaluje zależności wymagane do kompilacji nexus core CLI. Ukończenie zajmie trochę czasu w zależności od szybkości Internetu

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
make -f makefile.cli czyste
```

Na koniec uruchom to polecenie, aby skompilować ze źródła. Spowoduje to rozpoczęcie kompilacji rdzenia nexusa. Prosimy o cierpliwość, ponieważ w zależności od procesora może to zająć bardzo dużo czasu. Zamień 1 w „j1” na liczbę rdzeni / wątków, aby kompilować szybciej.

```
make -f makefile.cli -j1 AMD64=1
```

Do kompilacji na Raspberry Pi użyj:

```
make -f makefile.cli -j1 ARM64=1
```

Po udanej kompilacji pokaże komunikat „Ukończono budowanie nexusa”.

&nbsp;

## 4. Skonfiguruj portfel (nexus.conf):

Utwórz główny katalog danych Nexusa (jest to ukryty katalog, demon Nexusa tworzy go automatycznie przy pierwszym uruchomieniu. Tworzymy go ręcznie, aby utworzyć plik konfiguracyjny. Jeśli katalog jest już dostępny, pomiń ten krok).

```
mkdir ~/.Nexus
```
 
> Konfiguracja portfela jest przechowywana w pliku nexus.conf, znajdującym się w głównym katalogu danych
{.to-informacja}


Utwórz plik nexus.conf:

```
nano ~/.Nexus/nexus.conf
```

Skopiuj poniższy kod do pliku. Podaj użytkownika i hasło do RPC i API oraz usuń `#` w `#stake=1`, jeśli zamierzasz stawiać.

```
# To jest przykład nexus.conf. Dostosuj go do swojego wdrożenia.
Poświadczenia #RPC, zmień w razie potrzeby
rpcuser=<użytkownik dla RPC>
rpcpassword=<pw dla RPC>
Poświadczenia uwierzytelniania #API http. Zmień w razie potrzeby
apiuser=<użytkownik API>
apipassword=<pw dla API>
#Aby uruchomić rdzeń nexusa jako demon
demon=1
#Aby włączyć eksplorację za pomocą węzła,
#wydobycie=1
#Aby włączyć tyczenie
#stawka=1
```

Aby uzyskać zdalny dostęp do portfela (z interfejsu portfela na innym komputerze), dodaj następujące wiersze w pliku konfiguracyjnym.

`<ipaddress>` to adres IP maszyny łączącej się zdalnie z twoim węzłem, może to być adres IP interfejsu lub serwera dapp