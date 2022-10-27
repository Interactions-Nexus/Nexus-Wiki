---
title: Kopanie w Linux
description: Kopanie na komputerze z systemem Linux.
published: true
date: 2022-10-27T23:05:53.150Z
tags: 
editor: markdown
dateCreated: 2022-10-27T22:49:58.360Z
---

# Kopanie na Linux

Kopanie w systemie Linux nie jest tak proste jak Windows, a użytkownik musi skompilować NexusMiner ze źródeł. Ten przewodnik pomoże Ci skonfigurować kopanie w systemie Linux. Ten przewodnik jest dostosowany do dystrybucji opartych na Ubuntu i Debianie.

>Upewnij się, że zainstalowałeś najnowsze sterowniki GPU od producenta. Instalacja sterowników wykracza poza zakres tego przewodnika.
{.is-info}

## Przygotuj Ubuntu dla Minera:&#x20;

Zainstaluj zależności.

````
sudo apt install build-essential libboost-all-dev libdb-dev libdb++-dev libssl-dev libminiupnpc-dev libgmp-dev -y
````

Ubuntu nie ma najnowszej wersji boosta. Instalacja będzie procesem ręcznym opisanym poniżej:

### Zainstaluj Boost

Poniżej znajduje się bezpośredni link do strony boosta:

{% embed url="https://www.boost.org/users/download#live" %}

Pobierz najnowszą wersję boosta. W chwili pisania tego artykułu najnowsza wersja boost to 1.78.0:

````
wget https://boostorg.jfrog.io/artifactory/main/release/1.78.0/source/boost_1_78_0.tar.gz
````

Wypakuj instalator boost do nowego katalogu o nazwie Boost.

````
tar xzvf boost_1_69_0.tar.gz -C ~/Boost
````

Przejdź do folderu Boost.

````
cd Boost
````

Zainstaluj boost.

````
./bootstrap.sh --prefix=/usr/
````

Skompiluj boost ze źródła.

````
./b2
````

Skopiuj skompilowane pliki do lokalizacji określonej w opcji wiersza polecenia „_**–prefix**_”.

````
sudo ./b2 install
````

Aby zweryfikować wersję doładowania:

````
./get_boost_version
````

### Zainstaluj Cmake:

Nexus miner używa najnowszej wersji cmake, a Ubuntu nie jest dostarczane z najnowszą wersją cmake. Jeśli dystrybucja ma wersję cmake niższą niż 3.19, wykonaj poniższe czynności, aby ręcznie zainstalować najnowszą wersję cmake.

Przejdź do strony pobierania cmake (link poniżej) i pobierz pliki skryptów cmake dla systemu Linux z rozszerzeniem .sh

{% embed url="https://cmake.org/download" %}

Przejdź do folderu, do którego pobierany jest plik

````
cd Downloads
````

Uruchom instalator.

![](https://lh6.googleusercontent.com/9FU6gF8E6ij0g0gNkuYbuG-7IG7IaypFe\_oKBTi4DUXocjKkKckEHrQLRDMFXscUVmvDuDmM-kKywvYzqNeb1F6xiBo-48uUPovFe10xyO2V57ctc8vB\_\_r81XApwWsRmpIpBkJ6tG7cqFV5-Q)

![](https://lh4.googleusercontent.com/KeXuGqp8Qe4uSpiQ8MTJFlctZcrVGEHUBQzK90ioKSwwiaV7VLbnnuy0I9-kkMLmZT4xwdhwbwL63J1tqFyYhCMb5E-eVmt2fRQ1qN0PdWNmMKZupIu5xGuAobsmnjYLwoIvrkyqWhD4BWrhuA)

```
./<cmakefilename.sh>
```

Najpierw będzie licencja, użyj „Enter”, aby przewinąć w dół lub „spacji”, aby przewinąć do końca, zaakceptuj licencję, a następnie zaakceptuj lokalizację do wyodrębnienia, co zainstaluje plik binarny cmake. Przejdź do folderu cmake/bin. Zmień odpowiednio nazwę folderu cmak

Cmake jest zainstalowany i gotowy do następnego kroku.

## Pobierz i skompiluj NexusMiner

Sklonuj repozytorium NexusMiner.&#x20;

````
git clone --depth 1 https://github.com/Nexusoft/NexusMiner
````

````
git clone --branch v1.4 https://github.com/Nexusoft/NexusMiner
````

Przejdź do folderu z kodem źródłowym.&#x20;

````
cd NexusMiner
````

Przejdź do folderu cmake/bin zainstalowanego w powyższym kroku. W chwili pisania tego tekstu wersja cmake to 3.21.2, odpowiednio zmień nazwę.&#x20;

````
cd /Downloads/cmake-3.21.2-linux-x86_64/bin/
````

Uruchom cmake, aby zbudować plik wykonywalny NexusMiner. \<pathtosource> to ścieżka do folderu NexusMiner, a \<pathtobuildfolder> to ścieżka do NexusMiner/build. Użyj opcji `"-DWITH_PRIME=On"`, aby uwzględnić obsługę prime mining podczas kompilacji.

```
./cmake -S <pathtosource> -B <pathtobuildfolder> -DCMAKE_BUILD_TYPE=Release -DWITH_PRIME=On
```

```
./cmake -S ~/NexusMiner -B ~/NexusMiner/build -DCMAKE_BUILD_TYPE=Release -DWITH_PRIME=On
```

Cmake zbuduje gotowe pliki binarne make i zachowa je w folderze prekompilowanych plików binarnych "/build". Przejdź do folderu kompilacji.

````
cd ~/NexusMiner/build
````

Aby skompilować użyj:

````
make
````

Spowoduje to skompilowanie i utworzenie pliku wykonywalnego NexusMiner.&#x20;



Utwórz folder dla NexusMiner.&#x20;

````
mkdir ~/Miner
````

Skopiuj NexusMiner do folderu `Miner`.

````
cp NexusMiner ~/Miner
````

## Konfiguracja górnika:&#x20;

Aby skonfigurować górnika, sprawdź poniższy link:&#x20;

{% content-ref url="../../mining/mining-on-nexus/miner-configuration.md" %}
[miner-configuration.md](../../mining/mining-on-nexus/miner-configuration.md)
{% ref. treści końcowej %}

## Uruchom Górnika:

Aby uruchomić górnika przejdź do katalogu górnika.

{% wskazówka style="informacje" %}
W przypadku wydobycia solo uruchom portfel, zaloguj się, a następnie uruchom górnika.
{% podpowiedzi %}

````
cd NexusMiner
````

````
./NexusMiner
````

Mam nadzieję, że podobał Ci się przewodnik!!
