---
title: Prywatna Sieć Testowa
description: 
published: true
date: 2022-11-25T21:12:47.460Z
tags: 
editor: markdown
dateCreated: 2022-11-25T21:04:58.085Z
---

# Prywatna Sieć Testowa Tritium++

Ten przewodnik ma na celu uruchomienie pojedynczego lub wyspowego węzła do testowania. Nie wymaga kopania ani stakowania do produkcji bloków.

## Wstęp:

Ten przewodnik pomoże skonfigurować prywatną sieć testową do programowania. Węzeł prywatny nie ma konsensusu i jest prywatną bazą danych. Ten węzeł może być używany do testowania wywołań API, bez wydawania pieniędzy na kopanie lub używanie monet.

## Zrozumienie Publiczny, Prywatny i Hybrydowy

Portfel Nexus może być używany do obsługi sieci publicznych, prywatnych i hybrydowych, a konfiguracja jest tym, co je wyróżnia. Sieci prywatne i hybrydowe nie będą kompatybilne z legacy.

Sieć publiczna to sieć główna, która jest otwartą siecią publiczną. Tryb prywatny to sieć z uprawnieniami, nie jest połączona z siecią główną i jest siecią samodzielną. Sieć hybrydowa to połączenie sieci prywatnej i publicznej. Tryb hybrydowy pomaga organizacjom zachować bezpieczeństwo, prywatność i kontrolę poufnych danych, jednocześnie korzystając z bezpieczeństwa sieci publicznej i przekazując wartość między nimi.

W sieci prywatnej przepustowość można zwiększyć, dodając dodatkowe węzły. W sieci prywatnej nie ma potrzeby kopania ani stakingu w celu zabezpieczenia sieci.

## Przed rozpoczęciem tego przewodnika:

* Dowolny komputer z minimum 1 procesorem, 2 GB RAM i 20 GB miejsca na dysku twardym, Raspberry Pi 4 z 2 GB RAM
* Serwer Ubuntu 20.04 LTS dla AMD/IA64 lub Ubuntu IOT dla Raspberry Pi. (Użyj dowolnej dystrybucji Linuksa, ale ten przewodnik jest dostosowany do Ubuntu)
* Dysk USB lub karta SD do instalacji ubuntu
* Etcher – Aby nagrać plik obrazu systemu operacyjnego na kartę USB/SD
* Putty, jeśli używasz ssh przez Windows.

## 1. Przygotuj węzeł

[Zainstaluj serwer ubuntu 20.04 LTS](https://ubuntu.com/tutorials/install-ubuntu-server#1-overview) lub wybraną dystrybucję, zainstaluj serwer open-ssh podczas instalacji, a po zakończeniu instalacji uruchom ponownie węzeł. SSH do węzła i postępuj zgodnie z poniższymi poleceniami. Skopiuj polecenia i wklej je w terminalu za pomocą klawiszy CTRL+SHIFT+v

Zaktualizuj i zaktualizuj węzeł:

```
Sudo trafna aktualizacja; sudo apt upgrade -y
```

Otwórz port SSH przed włączeniem zapory:

```
sudo ufw zezwól na ssh
```

Włącz Firewall:

```
sudo ufw włącz
```

Sprawdź stan zapory:

```
Sudo ufw stan
```

Ustaw strefę czasową:

```
sudo dpkg-ponownie skonfiguruj tzdata
```

Aby zmienić nazwę hosta, jest to opcjonalne

```
sudo hostnamectl set-hostname <nowa nazwa_hosta>
```

Uruchom ponownie węzeł:

```
Sudo restart
```

Komputer jest gotowy do zainstalowania rdzenia nexusa

## 2. Kompilowanie rdzenia Nexusa:

Zainstaluj zależności wymagane do skompilowania rdzenia nexusa. Zajmie to trochę czasu w zależności od szybkości Internetu

```
sudo apt-get install -y build-essential libssl-dev libminiupnpc-dev git
```

Pobierz najnowszy kod źródłowy Tritium++ core (5.1), jego ukończenie powinno zająć tylko kilka sekund

```
git clone -b scalanie https://github.com/Nexusoft/LLL-TAO
```

> Tritium++ jest w fazie łączenia w momencie pisania tego przewodnika
{.to-informacja}


Aby zainstalować Tritium / 5.0.5, użyj następującego polecenia

```
git klon --głębokość 1 https://github.com/Nexusoft/LLL-TAO
```

Przejdź do katalogu kodu źródłowego

```
cd LLL-TAO
```

Uruchom polecenie, aby skompilować ze źródła, bądź cierpliwy, ponieważ może to zająć bardzo dużo czasu w zależności od procesora. Zamień 1 w „j1” na liczbę rdzeni / wątków, aby kompilować szybciej.

```
make -f makefile.cli czyste
```

W przypadku komputerów x86/IA64 użyj:

```
make -f makefile.cli -j1 AMD64=1 NO_WALLET=1
```

Do kompilacji na Raspberry Pi użyj:

```
make -f makefile.cli -j1 ARM64=1 NO_WALLET=1
```

Po udanej kompilacji pokaże komunikat „Ukończono budowanie nexusa”.

Komenda make tworzy nowy plik wykonywalny o nazwie „nexus”. Aby to sprawdzić, użyj polecenia list

```
ls
```

Polecenie `ls` wyświetla zawartość folderu. Wyświetlany jest plik wykonywalny „nexus”.

![](https://nexus.io/ResourceHub/images/5.1\_testnet/testnet1.png)

Dostęp do portfela można uzyskać na dwa sposoby; z folderu LLL-TAO dostęp do API można uzyskać z tej lokalizacji tylko przez terminal i dla każdego polecenia należy podać ścieżkę (./) przed nazwą pliku wykonywalnego (./nexus) lub jeśli plik wykonywalny jest przenoszony do / usr/bin, można uzyskać do niego uniwersalny dostęp z dowolnej lokalizacji bez ścieżki (nexus). W tym przewodniku nie użyjemy ścieżki.

Aby przenieść plik wykonywalny nexus do folderu /usr/bin:

```
sudo mv ~/LLL-TAO/nexus /usr/bin
```

## 3. Konfigurowanie Portfela (nexus.conf)

Utwórz główny katalog Nexusa (jest to ukryty katalog, demon Nexusa tworzy go automatycznie przy pierwszym uruchomieniu. Tworzymy go ręcznie, aby utworzyć plik konfiguracyjny. Jeśli katalog jest dostępny, pomiń ten krok).

```
mkdir ~/.Nexus
```

Konfiguracja portfela jest przechowywana w pliku nexus.conf. Utwórz plik nexus.conf

```
nano ~/.Nexus/nexus.conf
```

Skopiuj poniższą konfigurację do pliku nexus.conf za pomocą klawiszy ctrl+shift+v i edytuj lub wyłącz parametry według potrzeb.