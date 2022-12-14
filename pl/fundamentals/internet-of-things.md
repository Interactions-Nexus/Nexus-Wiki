---
title: Internet rzeczy - IoT
description: 
published: true
date: 2022-12-14T22:45:02.736Z
tags: 
editor: markdown
dateCreated: 2022-10-21T22:16:27.921Z
---

# Internet rzeczy (IoT)

`LX-OS` pozwoli komputerom na głębszą interakcję z protokołem Nexus (NP) niż było to wcześniej możliwe. Biblioteka niższego poziomu (LLL) stanowi podstawę całego NP, wyjaśniając, w jaki sposób powstała początkowa tymczasowa nazwa LLL-OS. Nexus integruje weryfikację z LxOS poprzez przeplatanie konsensusu w przestrzeni użytkownika i jądra. Wykorzystuje łańcuchy podpisów (SigChains) i księgę główną do uwierzytelniania systemu plików, pamięci wykonawczej i wszelkich zmian w stanie jądra. Dziedziczenie rozproszonej bazy danych, księgi rachunkowej i protokołów z Nexusa stanowi formę rozproszonej wirtualizacji. Oprócz właściwości bezpieczeństwa pojawiają się inne pożądane funkcje, takie jak weryfikacja tożsamości w trybie offline i synchronizacja urządzeń roamingowych.

Szczegółowe czytanie o SigChains pomaga konceptualizować LX-OS. Krótko mówiąc, SigChains służą jako wbudowany schemat tożsamości i dostępu. SigChain reprezentuje pojedynczy węzeł, kontroluje konta, tokeny, aktywa (tokeny niezamienne lub NFT) oraz dostęp do kilku narzędzi kryptograficznych wymuszających „uwierzytelnione” środowisko.

Ogólnie rzecz biorąc, egzekwowanie zgodności rozproszonej księgi rachunkowej w całym systemie LX-OS pomaga w rozpoznawaniu złośliwego kodu, który „pozwala jądru poznać samo siebie” — Colin Cantrell (9). Urządzenia IoT używające LX-OS wykorzystują SigChains do identyfikacji na poziomie urządzenia i zarządzania połączeniami sieciowymi. Protokół separacji identyfikatora lokalizacji (LISP) umożliwia urządzeniom Nexus jednoczesną interakcję z wieloma sieciami wirtualnymi (IP/NP) przy jednoczesnym utrzymywaniu sesji poprzez oddzielenie tożsamości od lokalizacji. LISP reprezentuje innowację sieciową, która według zespołu Nexusa odegra kluczową rolę w ewolucji Internetu.

Wiele urządzeń IoT jest wprowadzanych na rynek w pośpiechu, bez uwzględnienia implikacji związanych z bezpieczeństwem. Pospieszne projekty i cięcie rogów odgrywają dużą rolę, ale jak dotąd niewiele standardów okazało się skutecznych w tej dziedzinie. Nawet sama myśl o byciu szpiegowanym przez [termostat Nest](https://www.computerworld.com/article/2476599/black-hat-nest-thermostat-turned-into-a-smart-spy-in-15-seconds.html?ref=hackernoon.com) podnosi nam temperaturę!

[Zhakowanie termostatu Google Nest](http://www.thelowdownblog.com/2014/07/hacking-googles-nest-thermostat-and.html)


Używanie deterministycznej identyfikacji sprzętu do uwierzytelniania na poziomie urządzenia (np. [International Mobile Equipment Identity – IMEI](https://en.wikipedia.org/wiki/International\_Mobile\_Equipment\_Identity?ref=hackernoon.com)) z kryptograficznym Identity oparty na SigChains, to innowacyjny mechanizm kontroli bezpieczeństwa dla branży IoT. Społeczność Nexus ma na celu zapewnienie solidnych otwartych standardów w celu promowania stabilnego przejścia do świata zdominowanego przez IoT. Początkowo LX-OS będzie ukierunkowany tylko na przypadki użycia IoT, ale ostatecznie pojawi się wersja konsumencka na komputery stacjonarne, tablety i urządzenia mobilne.

Łącząc urządzenia z Nexusem, pojawia się zupełnie nowa klasa potencjalnych aplikacji. Środowiskowy, przemysłowy i konsumencki. Przypadki użycia IoT w coraz większym stopniu definiują doświadczenie życiowe w XXI wieku, a LX-OS zapewnia społeczności Nexus sukces w tym szybko zmieniającym się świecie. Ponadto wiele potencjalnych przypadków użycia obsługiwanych przez łańcuch blokowy Nexus jest istotnych dla Internetu Rzeczy i można by je ulepszyć poprzez włączenie LX-OS jako podstawowego komponentu.