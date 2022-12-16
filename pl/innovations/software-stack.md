---
title: Stos oprogramowania
description: 7-warstwowy stos oprogramowania
published: true
date: 2022-12-16T22:41:24.593Z
tags: 
editor: markdown
dateCreated: 2022-10-22T21:27:24.849Z
---

# Stos oprogramowania

Architektura Nexusa została zaprojektowana jako siedmiowarstwowy stos oprogramowania, który zawiera 64-bitową maszynę wirtualną procesu opartą na rejestrach. Każda warstwa jest przeznaczona do przeprowadzania wyspecjalizowanego procesu niezależnie od siebie, zapewniając dodatkową funkcjonalność istniejącego stosu internetowego, model OSI. To sprawia, że ​​Nexus jest modułowym łańcuchem bloków.

![Stos oprogramowania 7-warstwowego](/7_layer_stack.png)

Zagłębmy się w działanie każdej z tych warstw z osobna:

## Interfejs

Interfejs to przestrzeń użytkownika, czyli przyciski używane do interakcji z dappem. Tej warstwie mogą towarzyszyć różne technologie od AR/VR po interfejsy mobilne. Nasza oficjalna warstwa interfejsu zapewnia programistom platformę do tworzenia modułów i aplikacji, które są osadzane bezpośrednio w portfelu Nexus.

## Logiczna

Jest to pierwsza warstwa przestrzeni aplikacji deweloperskiej, która tworzy logikę większości aplikacji. Ta warstwa współdziała bezpośrednio z API znajdującym się pod nią i zapewnia funkcjonalność, która nie zależy od bezpośredniego dostępu do łańcucha bloków. Przykładem mogą być proste żądania, takie jak: 'Wyślij wiadomość do tego użytkownika, jeśli inny użytkownik ukończył to zdarzenie'. Postulujemy, że w przyszłości ta warstwa będzie również sterowana przez systemy AI.

## API

Ta warstwa zapewnia interfejs, który umożliwia programistom uzyskanie bezpośredniego dostępu do funkcjonalności blockchain. Opiera się na prostej semantyce czasowników i rzeczowników i akceptuje szeroką gamę kodowań. Jest to brama do łańcucha bloków, z której można korzystać bez bezpośredniego dostępu do niższych poziomów stosu oprogramowania, dzięki czemu programowanie na Nexusie jest tak proste, jak tworzenie aplikacji internetowej.

## Operacje

Operacje to instrukcje lub akcje, które nadają kontekst rejestrom i definiują bardziej złożoną logikę kontraktu. Kontrakt to obiekt zawierający: stan wstępny rejestru (rejestr, na którym jest wykonywana operacja, który został przekazany w górę z warstwy rejestru), operację pierwotną (tylko jedna operacja pierwotna na kontrakt) oraz zestaw warunków (dowolna ilość operacji warunkowych).

### **Operacje prymitywne:**

Bieżąca iteracja warstwy operacyjnej zawiera 16 operacji pierwotnych oraz 54 operacje i typy warunkowe. Operacje prymitywne można najlepiej opisać jako czynności zachodzące na rejestrze takie jak: WRITE, DEBIT, TRANSFER, APPEND itp. Same te czynności powodują, że rejestr zmienia w jakiś sposób lub formę swój stan, w tym jego przemieszczenie z jednego podpisu łańcuch do innego.

### **Kontrakty warunkowe:**

Kontrakty warunkowe to umowy między uczestniczącymi stronami, określające zestaw wymagań, które muszą zostać spełnione, aby transakcja została zakończona. Są to elementy, które pozwalają użytkownikom na wzajemną interakcję, taką jak wygaśnięcie umowy lub wymiana przedmiotów. Możliwe są również bardziej zaawansowane formy depozytu bezpowierniczego lub arbitrażu. Instrukcje warunkowe nie mają ograniczeń co do ich złożoności, ponieważ są w stanie obsługiwać grupy grup warunków, które razem dają prawdę lub fałsz. W przypadku, gdy warunki wrócą jako prawdziwe, pozwala to odbiorcy transakcji zażądać swoich środków lub przedmiotu (w zależności od tego, czy był to PRZELEW czy DEBET). W przypadku, gdy odbiorca nie jest w stanie spełnić warunków, po określonym przez nadawcę terminie transakcja będzie możliwa do zrealizowania.

## Rejestr

Rejestr jest najszybszym nośnikiem pamięci wewnątrz procesora CPU (Central Processing Unit), którego procesor używa do buforowania danych między obliczeniami. Stało się to bardziej pożądaną architekturą do projektowania komputerów jako ulepszenie znacznie starszej architektury zwanej 'stosem'.

Rejestry Nexus to system przechowywania danych, który utrzymuje niezmienny zapis i historię, w tym stan obecny i poprzedni, dzięki czemu można ich używać do rejestrowania stanu aplikacji.

Własność rejestru można przenosić między Sigchainami, a tym samym działać jako aktywa, tokeny lub proste obiekty, takie jak kryptowaluty. Rejestr może być również własnością tokena, tworząc częściową własność aktywa, który reprezentuje. Warstwa rejestrów składa się z trzech głównych elementów: rejestrów obiektów, rejestrów stanów i 64-bitowej maszyny wirtualnej opartej na rejestrach do wykonywania warunków.

Każdy rejestr w łańcuchu bloków Nexusa ma dwie główne właściwości: adres (nazywany adresem rejestru), który służy do określenia lokalizacji danych w bazie danych rejestrów, oraz właściciela, który jest skrótem genezy łańcucha podpisów, który obecnie jest właścicielem rejestru.

### **Rejestry obiektów:**

Rejestry obiektów to programowalne obiekty z bezpiecznym typem zapisane z określoną strukturą, która opisuje zasób, token lub obiekt programisty. Mogą być używane do wielu różnych celów, w tym do akcji firmy, zasobów cyfrowych, certyfikatów, plików danych i kont. Pola danych wewnątrz obiektu przenoszą specyfikatory, które definiują, czy pole może być modyfikowalne, dzięki czemu sam obiekt jest w stanie wymusić, aby niektóre pola miały tylko do odczytu lub zapisu.

`Image ID: 108629084398374`\
`License Type: Enhanced`\
`Image Title: Arizona Sunset`

Powyższy przykład wyświetla format metadanych dla zasobu fotograficznego, który jest przechowywany w programowalnym rejestrze obiektów. Ten format można rozszerzyć o zmienne i niezmienne specyfikatory typu, co oznacza, że pole takie jak 'Tytuł obrazu' w powyższym przykładzie może być modyfikowane i modyfikowane, podczas gdy inne pola pozostaną niezmienne.

### **Rejestr stanu:**

Rejestr stanu to prosty rejestr, który może przechowywać dane w dowolnej kolejności bez wymuszonego formatu przez księgę. Będą one używane przez Dapp do rejestrowania niezmiennego stanu. Rejestry stanu mają dwie formy: RAW i APPEND. Rejestr RAW jest związany swoim początkowym rozmiarem i może być zapisywany w dowolnym momencie, podczas gdy rejestr APPEND może mieć tylko dane dołączone do jego stanu, zachowując oryginalną zawartość niezmienną.

### **Maszyna wirtualna:**

Instrukcje warunkowe są przetwarzane na wierzchu maszyny wirtualnej, która używa rejestrów 64-bitowych do utrzymywania stanu tymczasowych zmiennych warunków podczas ich przetwarzania. Maszyna wirtualna zwiększa wydajność instrukcji warunkowych, ponieważ nie ponosi kosztów 'wypychania i wyskakiwania' ze stosu, tak jak inne maszyny wirtualne. Ta część warstwy rejestru odpowiada za niesamowitą szybkość wykonywania warunkowego, wymagającego średnio tylko 50 nanosekund na instrukcję.

## Księga

Księga jest odpowiedzialna za zapewnienie, że wszystkie dane są tworzone zgodnie z konsensusem i są z natury niezmienne. Zarządza własnością między stronami za pomocą prymitywów kryptograficznych, takich jak hashowanie, podpisy cyfrowe i protokoły konsensusu. Składa się z łańcuchów sygnatur dla państw na poziomie użytkownika oraz proponowanej architektury łańcucha trójwymiarowego (3DC) dla państwa globalnego, z których ta ostatnia jest opracowywana w ramach TAO.

### **Łańcuchy podpisów:**

[Signature Chain](/technology/nexus-innovations/signature-chains) to zdecentralizowane konto blockchain, które umożliwia logowanie się z dowolnego komputera za pomocą nazwy użytkownika, hasła i kodu PIN, bez potrzeby używania plików wallet.dat lub ciągłego ponownego skanowania baza danych. Są one porównywalne z osobistym blockchainem, który umożliwia zdecentralizowany dostęp przez system logowania, eliminując potrzebę przechowywania kluczy prywatnych. Sigchains deterministycznie tworzą matematyczną 'blokadę', którą mogą odblokować tylko Twoje dane logowania.

Zasadniczo łańcuch podpisów oddziela klucz prywatny od konta, dlatego nie jest się związanym posiadaniem ani bezpieczeństwem tego pojedynczego klucza prywatnego. Klucz prywatny staje się przestarzały, gdy generowana jest następna transakcja, zapewniając wyższy poziom bezpieczeństwa w porównaniu z ciągłym ponownym wykorzystaniem klucza prywatnego, jak ma to miejsce w przypadku innych technologii blockchain. Inne korzyści wynikają z wydajności uzyskanej dzięki zmniejszeniu wymogu przechowywania dużej ilości sygnatur na dysku oraz możliwości korzystania z różnych typów kluczy, takich jak FALCON w celu zwiększenia odporności kwantowej.

### **Konsensus:**

Do zabezpieczenia sieci wykorzystywane są dwa kanały Proof of Work (PoW) (Prime i Hashing) oraz jeden kanał Proof of Stake (PoS). Konsensus jest zrównoważony między wszystkimi trzema kanałami, ponieważ opiera się na łącznej wadze łańcucha, zapewniając wyższą odporność na 51% ataków w porównaniu z łańcuchami bloków z jednym algorytmem. W miarę rozwoju struktury TAO, te trzy formy konsensusu staną się trzema warstwami [3DC](broken-reference).

### **Reputacja:**

Nexus implementuje mechanizm reputacji o nazwie 'Trust', który rejestruje spójny czas, w jakim węzeł uczestniczy w procesie walidacji. Zaufanie spada trzy razy szybciej niż się narasta i przekłada się na zmienną nagrodę stawki od 0,5% do 3% rocznie. Zaufanie przynosi również korzyści warstwie sieciowej, w której węzły mogą określać reputację lub niezawodność węzłów, z którymi się łączą, zwiększając bezpieczeństwo przed atakami Sybil.

## Sieć

Sieć jest odpowiedzialna za komunikację typu end-to-end między węzłami, obsługę przekazywania i odbierania danych na poziomie księgi. Nexus rozszerza tę warstwę, używając 'nakładek', które zapewniają sieci funkcjonalność IPv6, co pozwala użytkownikowi kontrolować swój adres IP za pomocą kryptografii.

### **Nakładki:**

Naszą wybraną nakładką jest LISP (Protokół separacji wskaźnika lokalizacji). Zapewnia to lepszą łączność między rówieśnikami, ponieważ nakładka działa jako warstwa 'podwyższonego zaufania' do Internetu w połączeniu z księgą (blockchain), co zwiększa bezpieczeństwo, niezawodność i bezpieczeństwo korzystania z Internetu.

### **IPv6:**

Nakładka LISP łączy kryptograficzne EID IPv6 z łańcuchami sygnatur, umożliwiając w pełni zaszyfrowany system komunikacji peer-to-peer i identyfikację kluczy kryptograficznych za pomocą księgi głównej.

### **Multicast:**

Dzięki aktualizacjom Amine i Obsidian wdrożymy łącza multiemisji do propagacji wiadomości, co zapewni nam wyższy stopień skalowalności (stały czas) w porównaniu z istniejącymi modelami blockchain (czas wykładniczy). Znaczenie routingu o stałym czasie polega na tym, że komunikaty są przekazywane z krawędzi do krawędzi sieci znacznie szybciej, nawet przy dużej liczbie połączonych węzłów.