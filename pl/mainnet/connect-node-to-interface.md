---
title: Połącz Węzeł z Interfejsem
description: Jak uzyskać dostęp do zdalnego rdzenia CLI za pomocą interfejsu
published: true
date: 2022-11-20T23:35:31.455Z
tags: 
editor: markdown
dateCreated: 2022-11-20T23:35:31.455Z
---

# Podłącz Węzeł do Interfejsu

Ten przewodnik pomoże uzyskać dostęp do demona portfela za pomocą interfejsu zdalnego portfela. W tym celu będziesz potrzebować adresu IP swojego węzła, a także interfejsu komputera. W przypadku komputera zdalnego możesz przejść do ustawień, sieci i kliknąć szczegóły, które pokażą adres IP komputera.

Na komputerze, na którym będzie uruchomiony interfejs, przejdź do [https://](https://crypto.nexus.io/wallet)[nexus.io/wallets](https://nexus.io/wallets) i pobierz portfel dla twojego systemu operacyjnego.


> Zawsze sprawdzaj integralność portfela. Postępuj zgodnie z instrukcjami w linku poniżej.
{.is-info}

https://nexus.io/ResourceHub/wallet-guide#download-verify-install

Zainstaluj i uruchom portfel. Po załadowaniu portfela natychmiast przejdź do _'Ustawienia'_, kliknij _'Core'_, przewiń w dół i włącz ręczny tryb rdzenia za pomocą suwaka.

![](https://thedigitalfuture.net/wp-content/uploads/2020/12/RPI-Interface1.png)

SSH do węzła.

```
ssh ubuntu@192.168.3.144
```

Otwórz plik konfiguracyjny nexusa.

```
nano ~/.Nexus/nexus.conf
```

Ustaw nexus.conf i interfejs obok siebie.

W pliku konfiguracyjnym wprowadź unikalną apiusername i apipassword, które będą używane w polu nazwy użytkownika i hasła w ustawieniach interfejsu tritium core, adres IP zastąp domyślny adres 127.0.0.1 adresem IP węzła demona. Pozostaw domyślny port i kliknij zapisz ustawienia.

W interfejsie przejdź do menu '_File_' i kliknij '_Switch to Legacy Mode_', a teraz znajdziesz się w starszym trybie z ręcznymi ustawieniami rdzenia.

![](https://thedigitalfuture.net/wp-content/uploads/2020/12/RPI-Interface2.png)

Użyj unikalnej nazwy rpcusername i rpcpassword, a te same zostaną użyte w polu nazwy użytkownika i hasła w starszych podstawowych ustawieniach interfejsu. Adres IP zastąp domyślny adres 127.0.0.1 adresem IP węzła. Pozostaw domyślny port i kliknij zapisz ustawienia.


> W pliku konfiguracyjnym, adres IP 'llpallowIp' powinien odnosić się do interfejsu komputera.
{.is-info}



Użyj Ctrl+S i Ctrl+X, aby zapisać i wyjść z pliku konfiguracyjnego.

Zmień katalog na plik wykonywalny Nexusa.

```
cd LLL-TAO
```

Uruchom demona portfela Nexus.

```
./nexus
```

Powinieneś zobaczyć swój interfejs portfela połączony z demonem i przegląd pokazujący informacje o węźle. Jeśli interfejs nie jest podłączony, musisz zatrzymać portfel i otworzyć porty 8080 i 9336 na zaporze.

W węźle zatrzymaj demona portfela.

```
./nexus system/stop
```

Na zaporze ufw zezwól na port 8080 dla interfejsu API.

```
sudo ufw allow 8080/tcp
```

Zezwalaj na port 9336 dla RPC.

```
sudo ufw allow 9336/tcp
```

Sprawdź stan zapory ufw.

```
sudo ufw status
```

ufw status – Dane wyjściowe powinny wyglądać jak poniżej.

![](https://thedigitalfuture.net/wp-content/uploads/2020/12/RPI-ufw.png)

Następnie uruchom demona.

```
./nexus
```

Odczekaj kilka sekund i

![](https://thedigitalfuture.net/wp-content/uploads/2020/12/RPI-Sync.png)

Interfejs zostanie połączony z węzłem, a informacje pojawią się na stronie przeglądu.

Teraz zaloguj się i przeprowadzaj transakcje normalnie za pomocą interfejsu.


> W przypadku stakowania w węźle CLI. Nie wylogowuj się z interfejsu, tylko zamknij interfejs.
{.is-warning}



Aby wyjść z SSH lub putty, użyj poniższego polecenia. Spowoduje to zamknięcie tylko terminala SSH lub putty, a węzeł będzie działał, co można potwierdzić za pomocą interfejsu.

```
exit
```


> Gdy węzeł CLI jest podłączony do interfejsu, nie wyłączaj ani nie włączaj „Ręcznego trybu podstawowego”. Spowoduje to wysłanie sygnału wyłączenia do rdzenia. Ten problem zostanie naprawiony w następnej wersji.
{.is-warning}