---
title: Węzły Początkowe (seed nodes)
description: Jak uruchomić węzeł początkowy dla sieci głównej
published: true
date: 2022-11-24T22:48:55.062Z
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

- Wysoka dostępność - Węzeł powinien być zawsze włączony i dostępny.
- Publicznie osiągalny - Węzeł musi mieć publicznie dostępny adres IP i zaporę ogniową otwartą na portach wymienionych poniżej.
- Wysoka przepustowość — Węzeł musi mieć zawsze wysoką przepustowość połączenia internetowego.
- Rozpoznawalna nazwa DNS - Możemy wyświetlić węzeł z jednym z DNS węzła początkowego.
    
Aby skonfigurować nowy węzeł, postępuj zgodnie ze wskazówkami dotyczącymi tworzenia węzła sieci głównej w poniższym łączu:

- [Uruchom Węzeł Sieci Głównej *Jak skonfigurować węzeł CLI sieci głównej*](https://wiki.nexus.io/pl/mainnet/run-a-mainnet-node)
{.links-list}

## Konfiguracja węzła początkowego
Po uruchomieniu węzła wykonaj dodatkowe kroki poniżej:

1. Dodaj następujące elementy do pliku nexus.conf:

```plaintext
#Unified time synchronization
unified=1
#Allow all IP's to connect to your node
llpallowip=*.*.*.*:9324
#Increase your maximum connections
maxincoming=303
maxconnections=333
```
2. Otwórz porty 9324/tcp (ujednolicony czas) i 9888/tcp (główny port danych)

```plaintext
sudo ufw allow 9324/tcp
sudo ufw allow 9888/tcp
```

3. Upewnij się, że twój węzeł ma rozpoznawalną nazwę DNS wskazującą na niego.
4. Skontaktuj się z adminem grupy roboczej węzła początkowego, aby dołączyć do grupy roboczej. Adminami są:
    - <a href="https://t.me/aeonwise" target="_blank">@aeonwise</a>
    - <a href="https://t.me/Radient4751" target="_blank">@radient</a>
   
5. Gdy znajdziesz się w grupie roboczej, dodamy nazwę DNS twojego węzła do [seeds.cpp](https://github.com/Nexusoft/LLL-TAO/blob/merging/src/LLP/seeds.cpp) na GitHubie.