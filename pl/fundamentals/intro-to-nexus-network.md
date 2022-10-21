---
title: Wprowadzenie do sieci Nexus
description: 
published: true
date: 2022-10-21T21:47:06.736Z
tags: 
editor: markdown
dateCreated: 2022-10-20T14:37:37.674Z
---

# Wprowadzenie do sieci Nexus

Jest to sieć komputerów, na których działa rdzeń (programowa implementacja protokołów blockchain Nexusa) i komunikuje się przez Internet, tworząc jeden _`kanoniczny`_ superkomputer o nazwie Nexus Virtual Machine (NVM). NVM jest _`maszyną stanów`_ i wszyscy uczestnicy zgadzają się i zachowują kopię stanu. Każdy użytkownik może zażądać transakcji w sieci, a kiedy takie żądanie zostanie rozesłane, inni uczestnicy sieci weryfikują, zatwierdzają i wykonują `wykonanie` żądania. To wykonanie powoduje zmianę stanu w NVM, która jest następnie zatwierdzana i propagowana w całej sieci.

Żądania wykonania kontraktu nazywane są żądaniami transakcji; zapis wszystkich transakcji i aktualny stan NVM jest przechowywany w `księdze` łańcucha bloków, która z kolei jest przechowywana i uzgadniana przez wszystkie węzły.

Mechanizmy kryptograficzne zapewniają, że gdy transakcje zostaną zweryfikowane jako ważne i dodane do łańcucha bloków, nie można ich później modyfikować. Te same mechanizmy zapewniają również, że wszystkie transakcje są podpisywane i wykonywane z odpowiednimi „uprawnieniami” (nikt nie powinien mieć możliwości zalogowania się na konto Jana, z wyjątkiem Jana, który ma poświadczenia łańcucha podpisów).

## Co to jest Nexus?

**Nexus (NXS)** to natywna kryptowaluta kosmosu Nexusa. Nexus został zaprojektowany z myślą o darmowych prostych transakcjach. Celem NXS jest umożliwienie prawidłowej grywalizacji sieci. Aby upewnić się, że aktywni uczestnicy otrzymują wynagrodzenie za wykonaną pracę i zapobiegają celowemu zatykaniu sieci przez złośliwych uczestników przez żądanie nieskończonych mikrotransakcji (spamowanie) i przysiadanie nazw. NXS to symbol giełdowy Nexusa.

## Czym są zaawansowane kontrakty?

Kluczową rolę odgrywa 7-warstwowa architektura stosu oprogramowania; z jego operacjami i warstwą rejestru, która zarządza i kontroluje NVM.

Warstwa rejestrów to system przechowywania danych, który utrzymuje niezmienny zapis i historię, w tym stan obecny i poprzedni, dzięki czemu można je wykorzystać do rejestrowania stanu aplikacji. Warstwa rejestru to warstwa danych, która naśladuje pamięć podręczną procesora, która jest najszybszą pamięcią na komputerze.

Warstwa operacyjna zawiera instrukcje lub akcje, które nadają kontekst rejestrom i definiują bardziej złożoną logikę kontraktową. Kontrakt to obiekt zawierający: stan wstępny rejestru (rejestr, na którym jest wykonywana operacja, który został przekazany w górę z warstwy rejestru), operację pierwotną (tylko jedna operacja pierwotna na kontrakt) oraz zestaw warunków (dowolna ilość operacji warunkowych).

Na bardziej podstawowym poziomie umowy zaawansowane są porównywalne z umowami ze świata rzeczywistego, spisanymi na papierze i egzekwowanymi przez sąd. Jest wysoce zaawansowany, ponieważ jest egzekwowany przez kod, jego wiązanie i sprawia, że zaufane strony trzecie są zbędne.

Zaawansowane umowy umożliwiają programistom tworzenie i wdrażanie dowolnie złożonych aplikacji i usług skierowanych do użytkowników, takich jak: rynki P2P, zdecentralizowane instrumenty finansowe, gry itp.