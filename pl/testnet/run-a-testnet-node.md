---
title: Uruchom Węzeł Sieci Testowej
description: Uruchom węzeł w sieci testowej, aby przetestować interfejsy API lub aplikacje
published: true
date: 2022-11-24T23:41:42.990Z
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

Ulepsz swój węzeł:

```
sudo apt upgrade -y
```

Otwórz port SSH przed włączeniem zapory:

```
sudo ufw allow ssh
```

Zezwól na port API 7080:

```
sudo ufw allow 7080/tcp
```

Zezwól na połączenia wychodzące na porcie 8888:

```
sudo ufw allow 8888/tcp
```

Zezwalaj na port górniczy 8325, tylko w przypadku wydobycia:

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

Jeśli musisz zmienić nazwę hosta – nieobowiązkowa, jeśli już ją ustawiłeś podczas instalacji:

```
sudo hostnamectl set-hostname <newhostname>
```

Uruchom ponownie węzeł:

```
sudo reboot
```

Mamy nasz komputer gotowy do zainstalowania rdzenia nexusa.

## **5. Kompilowanie rdzenia Nexusa:**

Instaluje zależności wymagane do kompilacji nexus core CLI. Ukończenie zajmie trochę czasu w zależności od szybkości Internetu

```
sudo apt-get install -y build-essential libssl-dev libdb-dev libdb++-dev libminiupnpc-dev git
```

Pobierz najnowszy kod źródłowy rdzenia nexusa, a jego ukończenie powinno zająć tylko kilka sekund,

```
git clone -- scalanie gałęzi https://github.com/Nexusoft/LLL-TAO
```

Przejdź do katalogu kodu źródłowego

```
cd LLL-TAO
```

Na koniec uruchom to polecenie, aby skompilować ze źródła. Spowoduje to rozpoczęcie kompilacji rdzenia nexusa. Prosimy o cierpliwość, ponieważ w zależności od procesora może to zająć bardzo dużo czasu. Zamień 1 w „j1” na liczbę rdzeni / wątków, aby kompilować szybciej.


> Aby zbudować na Raspberry Pi z 1 GB pamięci RAM, musisz włączyć pamięć wymiany.
Kontynuuj po skonfigurowaniu wymiany.
{.to-informacja}

https://rayanfer32.medium.com/enable-swap-memory-on-ubuntu-on-raspberry-pi-a0f873a65e74

```
make -f makefile.cli czyste
```

W przypadku komputerów x86/IA64 użyj:

```
make -f makefile.cli -j1 AMD64=1 NO_WALLET=1
```

Do użycia Raspberry Pi:

```
make -f makefile.cli -j4 ARM64=1 NO_WALLET=1
```

Po udanej kompilacji pokaże komunikat „Ukończono budowanie nexusa”.

## **6.** Konfiguracja węzła sieci testowej:

Konfiguracja portfela nexus jest przechowywana w pliku nexus.conf w `~/.Nexus`, który jest głównym katalogiem nexusa

Utwórz główny katalog Nexusa (jest to ukryty katalog, jeśli masz katalog, możesz pominąć ten krok).

```
mkdir ~/.Nexus
```

Utwórz plik nexus.conf

```
nano ~/.Nexus/nexus.conf
```

Skopiuj poniższą konfigurację do pliku nexus.conf i zmień wartości oznaczone „< >”, aby pasowały do ​​Twojej konfiguracji

```
#Nexus testnet config - ZMIEŃ NA ODPOWIEDNIE WARTOŚCI
#Ustaw poświadczenia API
apiuser=<nazwa użytkownika>
apipassword=<hasło>
#Aby włączyć uwierzytelnianie API na potrzeby testowania
apiauth=1
#Aby włączyć zdalny dostęp API
apiremote=1
#Do białej listy adresów IP dla dostępu API
llpallowip=<adres IP>:7080
#Aby włączyć tryb wielu użytkowników: umożliwia zalogowanie się więcej niż jednego użytkownika do węzła
wielu użytkowników=1
#Aby włączyć tryb debugowania
#debugowanie=1
#Aby włączyć tryb demona
demon=1
#Aby zaakceptować przychodzące polecenia JSON-RPC
serwer=1
#Włącz wydobycie
#wydobycie=1
#Włącz tyczenie
#stawka=1
# Flaga testnet domyślnie ustawia port API na 7080, RPC na 8336 i port górniczy na 8325
sieć testowa=1
#Aby połączyć się z publiczną siecią testową Nexusa.
connect=testnet1.nexus-interactions.io
connect=testnet2.nexus-interactions.io
connect=testnet3.nexus-interactions.io
# Aby wyłączyć główne węzły DNS
kiwa głową=1
#przetwarzaj powiadomienia (transakcje przychodzące) automatycznie w tle
powiadomienia procesowe=1
#Aby dodać hasło zatrzymania w celu ochrony przed przypadkowym wyjściem z portfela
system/stop=<hasło>
```

ctrl+s & ctrl+x, aby zapisać i wyjść z edytora tekstu nano

Konfiguracja portfela została zakończona.

## 7. API do sterowania Node

Aby rozpocząć, zatrzymać i sprawdzić informacje o węźle, musisz użyć interfejsów API z terminala

Przejdź do katalogu LLL-TAO, aby uruchomić rdzeń nexusa (musisz znajdować się w folderze LLL-TAO, aby uruchomić wszystkie poniższe polecenia)

```
cd LLL-TAO
```

### Aby uruchomić demona:

```
./ogniwo
```

Nexus core będzie działał w tle jako demon. Połączy się z węzłami wydobywczymi określonymi w konfiguracji i zsynchronizuje blockchain. Znalezienie peerów i zsynchronizowanie łańcucha zajmie kilka minut.

### Aby zatrzymać demona:

```
./system nexus/stop
```

```
./nexus system/stop hasło=<hasło>
```

### Aby uzyskać informacje o węźle:

```
./nexus system/get/info
```

Teraz węzeł testnet jest gotowy do użycia w Twojej aplikacji.

Mam nadzieję, że ten przewodnik był pomocny !!