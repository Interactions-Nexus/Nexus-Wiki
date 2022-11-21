---
title: Węzły Początkowe
description: Jak uruchomić węzeł początkowy dla sieci głównej
published: true
date: 2022-11-21T22:39:49.181Z
tags: 
editor: markdown
dateCreated: 2022-11-21T22:39:49.181Z
---

# Węzły Początkowe

Ten przewodnik pomoże Ci skonfigurować nowy węzeł inicjujący lub przekonwertować istniejący węzeł na węzeł inicjujący.

## Co to jest węzeł początkowy?
Kiedy nowy portfel pojawia się online, nie może automatycznie wykryć i połączyć się z siecią Nexus, w tym miejscu na ratunek przychodzą węzły początkowe. Węzeł początkowy DNS jest zakodowany w oprogramowaniu, a po uruchomieniu nowego portfela łączy się z tymi węzłami początkowymi i pobiera listę wszystkich pozostałych węzłów. Gdy nowy węzeł otrzyma listę, zacznie łączyć się z węzłami o najlepszych połączeniach i stanie się częścią sieci.

## Minimalne wymagania
Typowy tani VPS lub współdzielony serwer hostingowy zazwyczaj spełnia te wymagania.

- Wysoka dostępność - węzeł powinien być zawsze włączony i dostępny.
- Publicznie osiągalny - węzeł musi mieć publicznie dostępny adres IP i zaporę ogniową otwartą na portach wymienionych poniżej.
- Wysoka przepustowość — węzeł musi mieć zawsze wysoką przepustowość połączenia internetowego.
- Rozpoznawalna nazwa DNS - Możemy wyświetlić węzeł z jednym z DNS węzła nasion.
    
Aby skonfigurować nowy węzeł, postępuj zgodnie ze wskazówkami dotyczącymi tworzenia węzła sieci głównej w poniższym łączu:

- [Uruchom węzeł sieci głównej *Jak skonfigurować węzeł CLI sieci głównej*](https://wiki.nexus.io/en/mainnet/run-a-mainnet-node)
{.lista-linków}

## Konfiguracja węzła początkowego
Po uruchomieniu węzła wykonaj dodatkowe kroki poniżej:

1. Dodaj następujące elementy do pliku nexus.conf:

```zwykły tekst
#Ujednolicona synchronizacja czasu
zjednoczony = 1
#Zezwalaj wszystkim adresom IP na łączenie się z twoim węzłem
llpallowip=*.*.*.*:9324
#Zwiększ maksymalną liczbę połączeń
maksymalna liczba przychodzących = 303
maksymalna liczba połączeń=333
```
2. Otwórz porty 9324/tcp (ujednolicony czas) i 9888/tcp (główny port danych)

```zwykły tekst
sudo ufw zezwala na 9324/tcp
sudo ufw zezwala na 9888/tcp
```

3. Upewnij się, że twój węzeł ma rozpoznawalną nazwę DNS wskazującą na niego.
4. Skontaktuj się z administratorem grupy roboczej węzła początkowego, aby dołączyć do grupy roboczej. Administratorami są:
    - <a href="https://t.me/aeonwise" target="_blank">@aeonwise</a>
    - <a href="https://t.me/Radient4751" target="_blank">@radient</a>
   
5. Gdy znajdziesz się w grupie roboczej, dodamy nazwę DNS twojego węzła do [seeds.cpp](https://github.com/Nexusoft/LLL-TAO/blob/merging/src/LLP/seeds.cpp) na GitHubie.