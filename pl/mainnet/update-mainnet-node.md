---
title: Aktualizacja Węzła Sieci Głównej
description: Jak zaktualizować węzeł sieci głównej
published: true
date: 2022-11-21T22:33:17.734Z
tags: 
editor: markdown
dateCreated: 2022-11-21T22:14:45.405Z
---

# Aktualizacja Węzła Sieci Głównej

Gdy pojawia się nowa wersja rdzenia, należy ją zaktualizować.


>Ten przewodnik jest dostosowany do dystrybucji ubuntu/raspian.
{.is-info}


>Obowiązkowe lub przyrostowe aktualizacje portfela można zrozumieć, patrząc na numer wersji nowego i starego portfela. Jeśli pierwsza cyfra nowej wersji podstawowej zostanie zwiększona, jest to obowiązkowa aktualizacja, która może być hard forkiem lub poważnymi zmianami w protokole. Jeśli druga lub trzecia cyfra zostanie zwiększona, jest to aktualizacja przyrostowa. Aktualizacje przyrostowe mogą zostać pominięte, ale zalecamy aktualizację.
{.is-info}

Aby zaktualizować węzeł, zmień na folder LLL-TAO.

```
cd LLL-TAO
```

Zatrzymaj rdzeń.

```
./nexus system/stop
```

Przejdź do katalogu domowego.

```
cd
```

Zaleca się aktualizację systemu operacyjnego węzła. To polecenie może zająć trochę czasu.

```
sudo apt update; sudo apt upgrade -y
```

Uruchom ponownie węzeł. To polecenie zrestartuje węzeł, a także zamknie połączenie SSH lub putty.

```
sudo reboot
```

Daj dwie minuty na ponowne uruchomienie węzła, a następnie zaloguj się przez SSH lub putty.

```
ssh ubuntu@<IPaddress>
```

Zmień nazwę istniejącego folderu 'LLL-TAO' na 'old-LLL'.

```
mv LLL-TAO old-LLL
```

Następnie pobierz najnowszy kod źródłowy portfela Nexus z github. Główna gałąź LLL-TAO jest połączona z gałęzią łączącą.

W przypadku podstawowej wersji 5.0.5 użyj poniższego łącza.

```
git clone -b 5.0.5 https://github.com/Nexusoft/LLL-TAO
```

W przypadku gałęzi głównej, która z kolei będzie odnosić się do łączenia, użyj poniższego łącza, jest to rdzeń 5.1, który nie jest kompatybilny z wersją stabilną.

```
git clone --depth 1 https://github.com/Nexusoft/LLL-TAO
```

Przejdź do katalogu kodu źródłowego.

```
cd LLL-TAO
```

Uruchom `make`, aby skompilować ze źródła. 4 w 'j4' odnosi się do nr. liczby rdzeni/wątków dostępnych w CPU (RPI-4B ma 4 rdzenie). Więcej wątków kompilacji zużywa pamięć, jeśli masz 1 GB pamięci, zalecamy użycie j1, aby uniknąć błędu 'brak pamięci'.

>Aby zbudować na Raspberry Pi 3 lub 4 z 1 GB RAM, włącz pamięć wymiany, postępując zgodnie z instrukcjami z linku poniżej. Kontynuuj po skonfigurowaniu wymiany.
{.is-warning}

https://rayanfer32.medium.com/enable-swap-memory-on-ubuntu-on-raspberry-pi-a0f873a65e74

Rozpoczyna się kompilacja portfela, prosimy o cierpliwość, ponieważ ten krok może zająć bardzo dużo czasu w zależności od procesora.

W przypadku komputerów opartych na X86/IA64 użyj poniższego polecenia.

```
make -f makefile.cli -j1 AMD64=1
```

W przypadku Raspberry Pi użyj poniższego polecenia.

```
make -f makefile.cli -j1 ARM64=1
```

Po udanej kompilacji pokaże komunikat “Finished building nexus”.

Aby uruchomić rdzeń.

```
./nexus
```

Aby sprawdzić informacje o węźle.

```
./nexus system/get/info
```

Sprawdź, czy wersja podstawowa pokazuje nową wersję.

>Jeśli używasz interfejsu nexus do zdalnego dostępu do węzła, zaktualizuj do najnowszej wersji, brak aktualizacji może spowodować problemy z użytecznością lub funkcjonalnością. Przejdź do [https://nexus.io/wallets](https://nexus.io/wallets), aby pobrać najnowszy interfejs.
{.is-warning}

Mam nadzieję, że ten przewodnik był pomocny !!