---
title: Kopanie w Linux
description: Kopanie na komputerze z systemem Linux.
published: true
date: 2022-10-27T22:58:56.365Z
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