---
title: Argumenty wiersza poleceń
description: 
published: true
date: 2022-10-31T23:37:43.839Z
tags: 
editor: markdown
dateCreated: 2022-10-24T22:17:58.572Z
---

# Argumenty wiersza poleceń
Spowoduje to wyświetlenie listy wszystkich parametrów wiersza poleceń lub podstawowych parametrów konfiguracyjnych.


 | Parametr | Opis | Wartości |
 | --- | --- | --- |
 | -addnode | Dodaj do menedżera adresów i pozwól mu nawiązać połączenia |
 | -api | Uchwyt do API, jeśli wykryto symbol '/' | |
 | -apiuser | Nazwa użytkownika uwierzytelniania API | nazwa użytkownika |
 | -apipassword | Hasło uwierzytelniające API | hasło |
 | -apiauth | Włącz/wyłącz uwierzytelnianie API | 0/1 |
 | -apiconnect | Nawiąż połączenie z serwerem API | |
 | -apiport | Ręcznie przypisz port API | port number |
 | -apisssl | Włącz SSL dla API | 0/1 |
 | -apisslport | Przypisz port dla API SSL | numer portu|
 | -apisslrequired | Wartość logiczna, jeśli API używa SSL | prawda/fałsz |
 | -apithreads | | domyślna = 8 |
 | -apicscore | | domyślna = 5 |
 | -apirscore | | domyślna = 5 |
 | -apitimespan | | domyślna = 60 |
 | -apitimeout |
 | -argon2 | Algorytm generowania skrótu | |
 | -argon2_memory | Przydział pamięci dla argonu2 | |
 | -autotx | Kompiluje tx na podstawie listy kontraktów, do wdrożenia jako pojedynczy tx lub wsadowo | domyślna = fałsz |
 | -avatar |
 | -authattempts | Licznik niepowodzeń uwierzytelniania sesji | domyślnie = 3 |
 | -beta | Flaga wyłączająca sprawdzanie punktów kontrolnych w trybie innym niż starszy | |
 | -blocknotify | Powiadomienie o utworzeniu nowego bloku | |
 | -blockrefresh | Chwyć znacznik czasu wygaśnięcia bloku | domyślna = 60 |
 | -client | Flaga, aby włączyć tryb uproszczony | domyślna = fałsz |
 | -checkpoints | Aby cofnąć się do określonych punktów kontrolnych podczas uruchamiania | domyślna = 100 |
 | -connect |
 | -conf |
 | -contractcache| Utwórz instancję bazy danych kontraktów |
 | -cscore |
 | -datadir | Lokalizacja katalogu danych podstawowych |
 | -dbcache | Rozmiar pamięci podręcznej bazy danych Legacy | domyślnie = 25 |
 | -ddos |
 | -dnsupdate | Sprawdź, czy DNS wymaga aktualizacji | domyślnie = 86400 |
 | -dns | Dostarczono flagę, aby włączyć węzły DNS | domyślna = prawda |
 | -flushwallet | Legacy - Flaga do opróżnienia bazy danych portfela | |
 | -forcereindex | Oznacz, aby w razie potrzeby wymusić ponowną indeksację |
 | -forkblocks | Przewiń łańcuch do określonej liczby bloków | domyślnie = 0 |
 | -gdb | Tryb GDB czeka na wejście z klawiatury, aby zainicjować czyste zamknięcie | |
 | -generate | Blokuj hasło generowania dla sieci prywatnych |
 | -httpheader | Zrzuć nagłówek przy każdym odczycie |
 | -httpresponse | Oznacz, aby zarejestrować odpowiedź http | domyślna = fałsz |
 | -hybrid | Tożsamość sieci hybrydowej | hasło |
 | -inactivetimeout | Limit czasu bezczynności sesji | domyślnie = 3600 |
 | -indexheight | Włącz indeksowanie wysokości bloku| 0/1 |
 | -indexaddress | Włącz indeksowanie adresów | 0/1 |
 | -latency | Opóźnienie tworzenia bloków w trybie prywatnym lub hybrydowym | |
 | -ledgercache | Utwórz instancję bazy danych księgi |
 | -legacycache | Utwórz instancję bazy danych Legacy |
 | -latency | Czas tworzenia bloków w sieciach prywatnych |
 | -llpsleep | zegar uśpienia pamięci podręcznej | domyślnie = 0 |
 | -lldmeters | Flaga do śledzenia wątku miernika LLD | |
 | -legacy | Aby sprawdzić, czy adres jest Legacy |
 | -limitfreerelay | Limit szybkości bezpłatnych transakcji w celu ograniczenia zalania | |
 | -listen |
 | -logfiles | Parametr konfiguracyjny rejestrowania debugowania | domyślna = 20 |
 | -logsizeMB | Parametr konfiguracyjny rejestrowania debugowania | domyślnie = 5 |
 | -keypool | Pożądany rozmiar puli kluczy Legacy |
 | -manager | |
 | -mining | Włącz wydobywanie w węźle|
 | -miningthreads |
 | -miningcscore |
 | -miningrscore |
 | -miningtimespan |
 | -miningtimeout |
 | -miningddos |
 | -miningport | Zmień port wydobywczy |
 | -meters |
 | -maturityrequired | Sprawdzenie dojrzałości łańcucha podpisów w celu utworzenia nowej transakcji |
 | -maxconnections | Ustaw maksymalną liczbę połączeń równorzędnych z węzłem | domyślna = 100 |
 | -maxincoming | Ustaw maksymalną liczbę przychodzących połączeń równorzędnych | domyślnie = 84 |
 | -maxoutgoing | Ustaw maksymalne wychodzące połączenia równorzędne | domyślnie = 16 |
 | -maxcontracts | Ustaw maksymalną liczbę kontraktów na transakcję | domyślnie = 99 |
 | -maxsendbuffer | Zapisz sprawdzenie przepełnienia bufora |
 | -maxsendsize | Ustaw maksymalną liczbę bajtów do opróżnienia na 2^16 lub maksymalny bufor gniazda |
 | -marketfee | Aby włączyć i ustawić opłatę za rynek P2P | |
 | -nodns | Dostarczona flaga wyłączająca DNS | |
 | -notificationsthread | Całkowita liczba wątków menedżera | domyślnie = 1 |
 | -pid | (Nexus.pid) Pełna ścieżka pliku PID | |
 | -printstate | Flaga do wyprowadzenia stanu bloku | |
 | -prunefailed | Zabij adres, jeśli nie zostanie znaleziony prawidłowy adres | domyślnie = 0|
 | -printselectcoin | Legacy - 
 | -p2pport | Zmień port p2p |
 | -p2psslport | Zmień port SSL p2p |
 | -port |
 | -private | Włącz węzeł, aby działał jako łańcuch prywatny | |
 | -primemod | Oznaczenie zmniejszające odporność na rzęsy do 1017-bitów, aby zmaksymalizować współczynnik prim | domyślna = fałsz |
 | -registercache | Utwórz instancję bazy danych rejestru |
 | -rpcuser | Uwierzytelnianie RPC — nazwa użytkownika |
 | -rpcpassword | Uwierzytelnianie RPC - hasło |
 | -rpcremote | Włącz zdalny dostęp RPC | 0/1 |
 | -rpcthreads | | domyślnie = 4 |
 | -rpccscore | | domyślnie = 5 |
 | -rpcrscore | | domyślnie = 5 |
 | -rpctimespan | | domyślna = 60 |
 | -rpcport |
 | -rpcconnect | Nawiąż połączenie z serwerem RPC | |
 | -rpcssl | | prawda/fałsz |
 | -rpcsslport | | |
 | -rpcsslrequired | | prawda/fałsz |
 | -rpcmeters | | prawda/fałsz |
 | -rscore |
 | -regtest | Flaga do obsługi bloków testowania regresji | |
 | -runtime | Flaga sprawdzająca, czy baza danych działa | domyślna = fałsz |
 | -rescan | Legacy — Flaga obsługi ponownego skanowania bazy danych | |
 | -reindexheight | Flaga w celu wymuszenia ponownej indeksacji wysokości | |
 | -requirepassword | Flaga, aby wymusić uwierzytelnianie hasła do sesji odblokowania |
 | -safemode | Przelicz nexthash w celu ochrony przed korupcją nexthash |
 | -sessionlocks | Utwórz blokady sesji | domyślnie = 1024 |
 | -serverport |
 | -serversslport |
 | -ssl |
 | -sslport | Zmień port SSL |
 | -sslrequired |
 | -sslcertificate | ssl - lokalizacja certyfikatu | lokalizacja |
 | -sslcertificatekey | ssl - lokalizacja pliku klucza | lokalizacja |
 | -sslcabundle | ssl - lokalizacja kabla | lokalizacja|
 | -stake | Włącz stakowanie w węźle |
 | -sync | Flaga informująca o stanie synchronizacji | |
 | -syncbatchsize | Wykonaj sekwencyjny odczyt, aby uzyskać listę | domyślnie = 3000 |
 | -system/stop | Hasło uwierzytelniania przy zamykaniu rdzenia | hasło |
 | -terminateaut | Sprawdź uwierzytelniony łańcuch sigchain | |
 | -testne | Włącz węzeł jako sieć testową | Numer (0 - 92349234) |
 | -threads | |
 | -timeout | |
 | -timespan | |
 | -trustboost | Wstępnie ustawione zaufanie do testowania w sieci testowej | |
 | -upnp | flaga upnp, która włączy wymagane przekierowanie portów | domyślna = prawda |
 | -verbose | Włącz szczegółowe rejestrowanie | 0, 1, 2, 3 domyślnie = 0|
 | -wallet | Załaduj portfel Legacy | |
 | -walletcheck |
 | -walletclean |