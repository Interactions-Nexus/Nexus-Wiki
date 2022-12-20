---
title: JEDEN Stos (przyszłość)
description: Jedno Wykonanie Nexusa
published: true
date: 2022-12-20T12:24:13.792Z
tags: 
editor: markdown
dateCreated: 2022-10-22T21:41:40.275Z
---

# ONE - Stos (przyszłość)

Akronim ONE oznacza One Nexus Execution, stos zaprojektowany w celu zastąpienia modelu referencyjnego OSI (Open System Interconnect). Jest to podstawowy model odniesienia dla protokołu Nexus. Stos ONE składa się z 7 warstw, z których dwie pochodzą z obecnego OSI.

Obejrzyj prezentację stosu ONE autorstwa Colina Cantrella, link poniżej:

[Prezentacja ONE Stack autorstwa Colina Cantrella](https://www.youtube.com/watch?t=197s&v=BS3Cfo784z8)

## Warstwy stosu ONE

Poniższy obraz pokazuje, w jaki sposób stos ONE współdziała ze stosem oprogramowania Nexus, a także stosem OSI.

![Interakcja ONE Stack ze stosem oprogramowania Nexus](../../.gitbook/assets/ONE-Stack-Dark.png)

### SYGNAŁ

Warstwa sygnału odnosi się do komunikacji między satelitami a stacjami naziemnymi. Warstwa sygnału odpowiada za fizyczną modulację fali nośnej. jest podłączony bezprzewodowo do anten fazowanych. Wykorzystuje nielicencjonowane pasmo 5,8 GHz do komunikacji w celu otwartego wdrażania infrastruktury naziemnej i orbitalnej. Będzie podążać za MCS (schemat modulacji i kodowania) do MCS-11, używając 1024-QAM.

### LOKALIZACJA

Druga warstwa to warstwa Locator, która odpowiada za kierowanie pakietu do właściwej lokalizacji geograficznej. Będzie miał wiele typów lokalizatorów, z których najważniejsze to Geo-Spatial Locator (GSL), Wide Radius Locator (WRL) i Internet Protocol Locator (IPL). Routing jest topologicznie niezależny i nie wymaga zarządzania jakimkolwiek stanem w celu uzyskania kompletnej trasy. Współpracuje ze starszym Internetem, IP, jako kolejny zestaw lokalizatorów

### IDENTYFIKATOR

Warstwa identyfikatora to miejsce, do którego faktycznie adresowane są pakiety. To jak komputer ze stałym numerem telefonu, z którym każdy może się skontaktować, niezależnie od sieci, w której znajduje się ten konkretny komputer. Identyfikatory są unikalne i uwierzytelniane kryptograficznie, co oznacza, że nie można ich sfałszować. Rozszerza 128-bitową dostępną przestrzeń liczbową dla IPV6, ale wykorzystuje ją tylko jako wspólny interfejs między IP/NP.

### SESJA

Warstwa sesji jest przenoszona z OSI. Protokoły takie jak UDP i TCP będą nadal używane w NP. Nadal będą wykorzystywane zabezpieczenia warstwy sesji, takie jak TLS. Nadal będzie istniał ten sam interfejs gniazda, nawet podczas uruchamiania LX-OS przez IP, ponieważ zawsze będziesz otwierać TCP/NP/IP na ich 128-bitowy identyfikator. Oznacza to, że użytkownik może korzystać z IP lub NP i będzie to tak, jakby korzystał z jednego dużego internetu.

Warstwa sesji tworzy kanały komunikacji, zwane sesjami, pomiędzy urządzeniami. Odpowiada za otwieranie sesji, dbanie o to, aby pozostały otwarte i funkcjonalne podczas przesyłania danych oraz zamykanie ich po zakończeniu komunikacji. Warstwa sesji może również ustawiać punkty kontrolne podczas przesyłania danych — jeśli sesja zostanie przerwana, urządzenia mogą wznowić przesyłanie danych od ostatniego punktu kontrolnego.

### TRANSPORT

Warstwa transportowa jest przenoszona z OSI. Warstwa transportowa pobiera dane przesyłane w warstwie sesyjnej i dzieli je na „segmenty” po stronie nadawczej. Odpowiada za ponowne złożenie segmentów po stronie odbiorczej, przekształcając je z powrotem w dane, które mogą być używane przez warstwę sesji. Warstwa transportowa realizuje kontrolę przepływu, wysyłając dane z szybkością dostosowaną do szybkości łącza urządzenia odbierającego oraz kontrolę błędów, sprawdzając, czy dane zostały odebrane nieprawidłowo, a jeśli nie, żądając ich ponownie.

### KONSENSUS

Warstwa konsensusu jest odpowiedzialna za tworzenie warstwy zaufania zarówno na IP, jak i NP. Jest to wspólny punkt odniesienia prawdy do zarządzania korzeniami zaufania, takimi jak certyfikaty bezpieczeństwa. Składa się z trzech warstw stosu oprogramowania Nexus: Ledger, Register i Operations. Tutaj otrzymujemy wykonanie One Nexus.

### PODANIE

Warstwa aplikacji to warstwa interakcji człowiek-komputer, w której aplikacje mogą uzyskiwać dostęp do usług sieciowych, takich jak przeglądarki internetowe i klienci poczty e-mail. Zapewnia protokoły, które umożliwiają oprogramowaniu wysyłanie i odbieranie informacji oraz przedstawianie użytkownikom znaczących danych. Kilka przykładów protokołów warstwy aplikacji to Hypertext Transfer Protocol (HTTP), File Transfer Protocol (FTP), Post Office Protocol (POP), Simple Mail Transfer Protocol (SMTP) i Domain Name System (DNS).