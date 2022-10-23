---
title: Interfejs
description: Interfejs modułów
published: true
date: 2022-10-23T15:23:18.905Z
tags: 
editor: markdown
dateCreated: 2022-10-23T15:23:18.905Z
---

# Interfejs
Moduł `Przegląd` to strona główna portfela. Celem globusa jest pokazanie lokalizacji węzłów, z którymi połączony jest portfel.

&nbsp;

## Poniżej znajduje się wyjaśnienie atrybutów po lewej stronie modułu:

* **Saldo (NXS):** Łączne saldo NXS na wszystkich kontach w łańcuchu podpisów.
* **Saldo (USD):** Wartość wszystkich sald NXS w USD - obliczona przez pomnożenie _Saldo (NXS) x Cena Rynkowa (USD)_. W portfelu domyślną walutą jest USD. Walutę podstawową można zmienić w następującej lokalizacji: _Ustawienia -> Aplikacja -> Waluta podstawowa._
* **Salda przychodzące (NXS):** Ta wartość pokazuje wartość NXS, która trafia do portfela i nie została jeszcze potwierdzona i w pełni odebrana.
* **Cena rynkowa (USD):** Wartość 1 NXS w wybranej domyślnej walucie bazowej (w tym przypadku USD).
* **Cena rynkowa (USD):** Oblicza się ją, mnożąc _Cena rynkowa (USD) x całkowita podaż NXS w obiegu._
* **Zmiana 24-godzinna (% USD):** Zmiana wartości rynkowej w NXS w ciągu ostatnich 24 godzin.

&nbsp;

## Poniżej znajduje się wyjaśnienie atrybutów po prawej stronie modułu:

* **Połączenia:** Odnosi się to do liczby losowych „węzłów”, które są połączone. Domyślnie twój węzeł może wykonać do 16 połączeń wychodzących i 84 przychodzących (łącznie 100). Jeśli jesteś za routerem w domu, połączenia przychodzące będą mogły być nawiązywane tylko wtedy, gdy włączysz UPnP w portfelu (a router to obsługuje) lub jeśli ręcznie ustawisz przekierowanie portów na porcie 9888. Możesz zmienić konfigurację na mieć więcej niż 16 wychodzących (przy maxoutgoing=xx), ale nie jest to konieczne, 16 jest wystarczające.
* **Liczba bloków:** Liczba bloków to „wysokość” łańcucha bloków. Ta liczba odzwierciedla liczbę bloków węzłów lokalnych, którą można zweryfikować na podstawie bieżącej wysokości bloku Eksploratora Nexus (co oznacza, że ​​portfel jest aktualny). Jeśli wartość bloku w portfelu nie jest zgodna z wartością Nexus Explorera, oznacza to, że nie jest zsynchronizowana z publicznym łańcuchem bloków. Użyj opcji „Pobierz najnowszą bazę danych” (Plik -> Pobierz najnowszą bazę danych), aby załadować najnowszą wersję. Inną metodą weryfikacji synchronizacji jest spojrzenie na lewą ikonę w prawym górnym rogu portfela. Jeśli jest napisane „Synchronizacja”, oznacza to, że nie jest aktualny. Z drugiej strony, jeśli jest napisane „Zsynchronizowane”, oznacza to, że jest aktualne.
* **Stake Rate:** Ta wartość reprezentuje aktualną stawkę stosowaną do obliczenia nagrody za wydobycie bloku Proof of Stake, wyrażoną w formie rocznej stopy zwrotu NXS (%). Stawka zaczyna się od 0,5% i może wzrosnąć do 3,0% po 12 miesiącach ciągłego obstawiania.
* **Waga bloku:** Po otrzymaniu transakcji geneza wartość ta zacznie powoli rosnąć, osiągając 100% w ciągu 3 dni. Za każdym razem, gdy otrzymujesz transakcję tyczenia, waga bloku jest resetowana.
* **Waga zaufania:** Wskazuje, jak bardzo sieć ufa węzłowi. Zaczyna się od 1,11% i rośnie w sposób nieliniowy, tak jak ma to miejsce w przypadku stawki. Poziom zaufania zwiększa wagę stawki (poniżej), zwiększając w ten sposób ogólne szanse na wydobycie bloków i otrzymanie nagród za stakowanie. Im większa wartość, tym łatwiej jest utrzymać zaufanie.
* **Waga stawki:** Im wyższa waga stawki portfela, tym większe szanse na otrzymanie transakcji zaufania. Dokładna wartość pochodzi z wagi zaufania i wagi bloku.



Aby dowiedzieć się więcej o warunkach obstawiania, zapoznaj się z [najczęstszymi pytaniami i słowniczkiem](https://nexus.io/ResourceHub/general-FAQ).