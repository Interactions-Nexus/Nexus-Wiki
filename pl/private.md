---
title: Prywatna Sieć Testowa
description: 
published: true
date: 2022-11-25T21:57:41.066Z
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

* Dowolny komputer z minimum 1 CPU, 2 GB RAM i 20 GB miejsca na dysku twardym, Raspberry Pi 4 z 2 GB RAM
* Serwer Ubuntu 20.04 LTS dla AMD/IA64 lub Ubuntu IOT dla Raspberry Pi. (Użyj dowolnej dystrybucji Linuksa, ale ten przewodnik jest dostosowany do Ubuntu)
* Dysk USB lub karta SD do instalacji ubuntu
* Etcher – Aby nagrać plik obrazu systemu operacyjnego na kartę USB/SD
* Putty, jeśli używasz ssh przez Windows.

## 1. Przygotuj węzeł

[Zainstaluj serwer ubuntu 20.04 LTS](https://ubuntu.com/tutorials/install-ubuntu-server#1-overview) lub wybraną dystrybucję, zainstaluj serwer open-ssh podczas instalacji, a po zakończeniu instalacji uruchom ponownie węzeł. SSH do węzła i postępuj zgodnie z poniższymi poleceniami. Skopiuj polecenia i wklej je w terminalu za pomocą klawiszy CTRL+SHIFT+v

Zaktualizuj i ulepsz węzeł:

```
sudo apt update; sudo apt upgrade -y
```

Otwórz port SSH przed włączeniem zapory:

```
sudo ufw allow ssh
```

Włącz Firewall:

```
sudo ufw enable
```

Sprawdź stan zapory:

```
sudo ufw status
```

Ustaw strefę czasową:

```
sudo dpkg-reconfigure tzdata
```

Aby zmienić nazwę hosta, jest to opcjonalne:

```
sudo hostnamectl set-hostname <newhostname>
```

Uruchom ponownie węzeł:

```
sudo reboot
```

Komputer jest gotowy do zainstalowania rdzenia nexusa.

## 2. Kompilowanie rdzenia Nexusa:

Zainstaluj zależności wymagane do skompilowania rdzenia nexusa. Zajmie to trochę czasu w zależności od szybkości Internetu:

```
sudo apt-get install -y build-essential libssl-dev libminiupnpc-dev git
```

Pobierz najnowszy kod źródłowy Tritium++ core (5.1), jego ukończenie powinno zająć tylko kilka sekund:

```
git clone -b merging https://github.com/Nexusoft/LLL-TAO
```

> Tritium++ jest w fazie łączenia w momencie pisania tego przewodnika
{.is-info}


Aby zainstalować Tritium / 5.0.5, użyj następującego polecenia:

```
git clone --depth 1 https://github.com/Nexusoft/LLL-TAO
```

Przejdź do katalogu kodu źródłowego:

```
cd LLL-TAO
```

Uruchom polecenie, aby skompilować ze źródła, bądź cierpliwy, ponieważ może to zająć bardzo dużo czasu w zależności od procesora. Zamień 1 w 'j1' na liczbę rdzeni / wątków, aby kompilować szybciej:

```
make -f makefile.cli clean
```

W przypadku komputerów x86/IA64 użyj:

```
make -f makefile.cli -j1 AMD64=1 NO_WALLET=1
```

Do kompilacji na Raspberry Pi użyj:

```
make -f makefile.cli -j1 ARM64=1 NO_WALLET=1
```

Po udanej kompilacji pokaże komunikat “Finished building nexus”.

Komenda make tworzy nowy plik wykonywalny o nazwie 'nexus'. Aby to sprawdzić, użyj polecenia list:

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

Utwórz główny katalog Nexusa (Jest to ukryty katalog. Demon Nexusa tworzy go automatycznie przy pierwszym uruchomieniu. Tworzymy go ręcznie, aby utworzyć plik konfiguracyjny. Jeśli katalog jest dostępny, pomiń ten krok).

```
mkdir ~/.Nexus
```

Konfiguracja portfela jest przechowywana w pliku nexus.conf. Utwórz plik nexus.conf:

```
nano ~/.Nexus/nexus.conf
```

Skopiuj poniższą konfigurację do pliku nexus.conf za pomocą klawiszy ctrl+shift+v i edytuj lub wyłącz parametry według potrzeb:

```
#Nexus private standalone node config- Only for 5.1 rc1 & above
#Default API user/pass to blank for private network 
#apiuser=<username>
#apipassword=<password>
#Disable authentication of API requests
apiauth=0
#To remotely access the node API's
apiremote=1
#To remotely access API's use the llpallowip flag. The <ipaddress> can use wildcards; (llpallowip=192.168.*.*:7080)
llpallowip=*.*.*.*:7080
#Run wallet as a daemon
daemon=1
#Run node in private mode (defaults to testnet in 5.1)
private=1
#Run as a standalone node. (Disable this on additional nodes) 
manager=0
#Run as a local node, disable for public node
nodns=1
#Enables multiple users to be logged in concurrently    
multiuser=1
#Latency is in ms, this is the min time between blocks
latency=500
#Enables creation of blocks in private mode.( Use only on one node) (Use a secure password)
generate=<password>
#To connect additional nodes use addnode flag, the ipaddress will be of the first node with the ‘generate’ flag)
addnode=<ipaddress>
#To avoid accidental node shutdown with the stop command
system/stop=<password>
```

Ctrl+s i Ctrl+x, aby zapisać i wyjść z edytora.

>
> Aby dodać dodatkowy węzeł do sieci prywatnej, wyłącz flagi ‘manager’ i ‘generate’ w konfiguracji dodatkowego węzła. Dodaj flagę ‘addnode’ z ipaddress odnoszącą się do pierwszego węzła lub z flagą ‘generate’ i dodatkową linię dla dowolnego innego węzła w sieci.
{.is-info}

## 4. Polecenia API Tritium

Aby wchodzić w interakcje z rdzeniem nexusa, użyj poleceń API za pośrednictwem terminala lub zdalnie. Jeśli masz jakiekolwiek wątpliwości, możesz zapoznać się z [dokumentacją API](/en/tritium).

Otwórz porty 7080 i 8336 w zaporze:

```
sudo ufw allow 7080/tcp
```

```
sudo ufw allow 8336/tcp
```

Jeśli plik wykonywalny znajduje się w katalogu LLL-TAO, aby uruchomić nexus core, przejdź do folderu LLL-TAO, aby uruchomić wszystkie następujące polecenia:

```
cd LLL-TAO
```

Aby uruchomić demona, użyj ścieżki i nazwy pliku wykonywalnego:

```
./nexus
```

Jeśli przeniosłeś plik wykonywalny nexusa do /user/bin, użyj następującego polecenia z dowolnego nexusa lokalizacji i bez ścieżki (./).

Aby zatrzymać demona bez ochrony hasłem w konfiguracji:

```
nexus system/stop
```

Aby zatrzymać demona z ochroną hasłem w konfiguracji:

```
nexus system/stop password=<password>
```

Aby uzyskać informacje o węźle:

```
./nexus system/get/info
```

Aby monitorować dzienniki:

```
tail -f ~/.Nexus/testnet1/log/0.log
```

Aby utworzyć konto użytkownika (łańcuch podpisów). Nazwa użytkownika musi składać się z co najmniej 2 znaków, hasło musi mieć 8 znaków, a kod PIN 4 znaki. PIN może być kombinacją liter/cyfr/symboli:

```
nexus users/create/user username=<username> password=<password> pin=<pin> 
```


> Tryb wielu użytkowników tworzy nową sesję dla każdego zalogowanego użytkownika, a użytkownik musi używać tego konkretnego identyfikatora sesji przy każdym żądaniu API dla konkretnego użytkownika. Zapisz identyfikator sesji.
{.is-info}


Aby zalogować użytkownika:

```
nexus users/login/user username=<username> password=<password> pin=<pin>
```

Aby odblokować konto, ustaw automatyczne uznawanie transakcji przychodzących (notifications=1). Jeśli nie jest ustawiona, będziesz musiał ręcznie zaksięgować transakcje przychodzące, w przeciwnym razie zostanie ona zwrócona na konto nadawcy po 24 godzinach. Jest to odwracalna funkcja transakcji działająca zgodnie z założeniami:

```
nexus users/unlock/user pin=<pin> notifications=1 session=<sessionid> 
```

Aby sprawdzić pełne metryki węzła:

```
./nexus system/get/metrics 
```

Polecenia API mogą być używane z poziomu przeglądarki, a dane wyjściowe są wyświetlane w formacie JSON (Zalecane jest rozszerzenie `JSON formatter` do analizowania danych wyjściowych JSON dla chrome i wariantów, które firfox ma wbudowany parser).

&nbsp;

## 5. Polecenia API Tritium++ (5.1)

Aby wchodzić w interakcje z rdzeniem tritium++, użyj poleceń interfejsu API tritium++ za pośrednictwem terminala lub zdalnie. Jeśli masz jakiekolwiek wątpliwości, możesz zapoznać się z [dokumentacją API Tritum++](/pl/tritium++). Dokumentacja dla 5.1 jest prawie kompletna i być może pojawią się pewne zmiany w miarę rozwoju.

Otwórz porty 7080 i 8336 w zaporze:

```
sudo ufw allow 7080/tcp
```

```
sudo ufw allow 8336/tcp
```

Jeśli plik wykonywalny znajduje się w katalogu LLL-TAO, aby uruchomić nexus core, przejdź do folderu LLL-TAO, aby uruchomić następujące polecenia:

```
cd LLL-TAO
```

Aby uruchomić demona, użyj ścieżki i nazwy pliku wykonywalnego:

```
./nexus 
```

Jeśli przeniosłeś plik wykonywalny nexusa do /user/bin, użyj następującego polecenia z dowolnego nexusa lokalizacji i bez ścieżki (./).

Aby zatrzymać demona bez ochrony hasłem w konfiguracji:

```
nexus system/stop
```

Aby zatrzymać demona z ochroną hasłem w konfiguracji:

```
nexus system/stop password=<password>
```

Aby uzyskać informacje o węźle:

```
./nexus system/get/info
```

Aby monitorować dzienniki:

```
tail -f ~/.Nexus/testnet1/log/0.log
```

Aby utworzyć profil użytkownika (łańcuch podpisów). Nazwa użytkownika musi składać się z co najmniej 2 znaków, hasło musi mieć 8 znaków, a kod PIN 4 znaki. PIN może być kombinacją liter/cyfr/symboli:

```
nexus profiles/create/master username=<username> password=<password> pin=<pin> 
```

Użytkownik musi utworzyć sesję, aby uzyskać dostęp do profilu użytkownika:

```
nexus sessions/create/local username=<username> password=<password> pin=<pin>
```

> Podczas tworzenia sesji profilu w trybie wielu użytkowników, zwraca unikalny identyfikator sesji dla każdego zalogowanego użytkownika, a użytkownik musi użyć tego konkretnego identyfikatora sesji przy każdym żądaniu API dla każdej transakcji dla tego konkretnego użytkownika. Pamiętaj o zapisaniu identyfikatora sesji.
{.is-info}


Aby odblokować konto, ustaw automatyczne uznawanie transakcji przychodzących (notifications=1). Jeśli nie jest ustawiona, będziesz musiał ręcznie zaksięgować transakcje przychodzące, w przeciwnym razie zostanie ona zwrócona na konto nadawcy po 7 dniach lub po upływie ustawionego terminu wygaśnięcia. Jest to odwracalna funkcja transakcji działająca zgodnie z założeniami:

```
nexus sessions/unlock/local pin=<pin> notifications=1 session=<sessionid> 
```

Aby sprawdzić pełne metryki węzła:

```
./nexus system/get/metrics 
```

Polecenia API mogą być używane z poziomu przeglądarki, a dane wyjściowe są wyświetlane w formacie JSON (Zalecane jest rozszerzenie `JSON formatter` do analizowania danych wyjściowych JSON dla chrome i wariantów, które firfox ma wbudowany parser).

Mam nadzieję, że ten przewodnik był pomocny !!
