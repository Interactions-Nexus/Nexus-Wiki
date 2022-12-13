---
title: Maszyna wirtualna Nexus
description: Wprowadzenie do NVM
published: true
date: 2022-12-13T23:27:02.663Z
tags: 
editor: markdown
dateCreated: 2022-10-20T14:42:58.085Z
---

# Maszyna wirtualna Nexus

Wirtualna maszyna Nexusa (NVM) jest **`maszyną stanową`** i istnieje jako pojedyncza jednostka obsługiwana przez setki połączonych węzłów Nexusa.

Stos oprogramowania Nexusa istnieje wyłącznie w celu utrzymania ciągłego, nieprzerwanego i niezmiennego działania tej specjalnej maszyny stanowej; to środowisko, w którym działają wszystkie konta Nexus i kontrakty zaawansowane. W dowolnym punkcie łańcucha Nexus ma jeden i tylko jeden stan **`kanoniczny`**, a NVM określa zasady obliczania nowego prawidłowego stanu z bloku na blok.

Mimo że wszystkie platformy inteligentnych kontraktów są maszynami stanowymi, obsesja na punkcie skalowalności do użytku w świecie rzeczywistym osiągnęła punkt kulminacyjny w odrębnej architekturze NVM. Aby łatwo odróżnić lepszą architekturę, konieczne było nazwanie umów na Nexusie jako Kontrakty zaawansowane. Poniżej rozwikłamy architekturę.

### Architektura NVM

NVM jest zaprojektowany jako `64-bitowy`, `oparty na rejestrach`; ten projekt został wybrany, ponieważ pasuje do 64 bitów procesora i naśladuje rejestry pamięci podręcznej procesora.

Ta konstrukcja sprawia, że NVM jest bardzo szybki w porównaniu do EVM, ponieważ jest przeznaczony dla dzisiejszych procesorów. Ujmując to w liczbach, EVM zajmuje 1,7 miliona nanosekund/instrukcję, a NVM zajmuje 33 nanosekundy/instrukcję. EVM ma ogromną wadę, ponieważ wykonanie instrukcji zajmuje 4 cykle ze względu na 256-bitową długość na 64-bitowym procesorze, a także przestarzały projekt stosu.

NVM jest celowo zaprojektowany tak, aby nie był kompletny z turingiem. Decyzja ta wynika również z faktu, że Nexus jest silnikiem **`Weryfikacji`**. Ten projekt ma ogromną zaletę, a mianowicie darmowe proste transakcje, podczas gdy EVM potrzebuje Gas do kontrolowania żądań obliczeniowych z powodu złego kodu, który może zatrzymać sieć. Dzięki projektowi NVM zaawansowane umowy będą miały przewidywalne opłaty, które zostaną obliczone przed wykonaniem umowy.

Nexus będzie posiadał różne rodzaje umów, dla API wyższego poziomu dostępne będą szablony, które użytkownik będzie mógł wybrać z rozwijanej listy. Zaawansowanym użytkownikom rozszerzone umowy umożliwią im korzystanie z umów z wyborem języka specyficznego dla domeny. Rozszerzone kontrakty będą dostępne w późniejszym terminie. Aby uzyskać więcej informacji, zapoznaj się z [mapą drogową](https://nexus.io/roadmap).