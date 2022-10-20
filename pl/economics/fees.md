---
title: Opłaty
description: Publiczna sieć Nexus – opłaty
published: true
date: 2022-10-20T22:06:07.601Z
tags: 
editor: markdown
dateCreated: 2022-10-20T22:06:07.601Z
---

# Opłaty

Nexus pobiera opłaty za różne operacje w łańcuchu publicznym, takie jak tworzenie aktywów, faktur, nazw i tokenów. Ma to na celu utrzymanie bezpieczeństwa sieci, zapobieganie nadużyciom, spamowi i przycięciu zasobów.

> Opłaty dotyczą tylko sieci głównej.
{.is-info}



Podział opłat dla wszystkich rodzajów operacji przedstawia się następująco:

| Akcja                                          | Koszt | Notatka  |                                   
|---|---|---|
| Wysyłanie NXS lub innych tokenów                     |   0  |      |
| Odbieranie NXS lub innych tokenów                   |   0  | Jeżeli uznawany debet ma warunki umowne, za wykonanie tych warunków może zostać naliczona opłata w zależności od ich złożoności. Bezpłatny próg warunków oznacza, że proste warunki umowy, takie jak dodanie wygaśnięcia do debetu, będą oznaczać ich uznanie za darmo |                                                         
| Przenoszenie aktywów (NFT) i innych rejestrów  |   0  |              |
| Dochodzenie własności aktywów lub innych rejestrów |   0  | Jeśli zgłaszany rejestr jest rejestrem nazwanym, tj. istnieje dla niego lokalna nazwa w łańcuchu podpisów poprzednich właścicieli, podczas zgłaszania roszczenia tworzona jest dla niego odpowiednia nazwa lokalna. To stworzenie nazwy pociąga za sobą opłatę 1 NXS  |
| Dochodzenie własności aktywów lub innych rejestrów |   0  | Jeżeli żądana cesja ma warunki umowne, może zostać naliczona opłata za wykonanie tych warunków, w zależności od ich złożoności. Bezpłatny próg warunków oznacza, że proste warunki umowy, takie jak dodanie wygaśnięcia do przelewu, będą oznaczać, że dochodzenie ich będzie bezpłatne              |
| Tworzenie konta NXS lub tokena                 |   0  | Jeśli konto ma nazwę, pobierana jest opłata 1 NXS za utworzenie rejestru nazw              |
| Tworzenie aktywów lub innego rejestru             |  1+  | Opłata naliczana jest na podstawie wielkości danych zapisanych w rejestrze na poziomie 0,001 NXS za bajt. Istnieje jednak minimalna opłata 1 NXS i (w momencie pisania) maksymalny rozmiar rejestru 1Kb, co oznacza, że opłata będzie się różnić od 1 do 1,024 NXS         |
| Aktualizacja aktywów lub innego rejestru             |   0  |          |
| Tworzenie nazwy lokalnej                           |   1  |          |
| Tworzenie nazwy globalnej                          | 2000 |          |
| Tworzenie przestrzeni nazw                            | 1000 |          |
| Tworzenie tokena                                |  1+  | <p>Naliczenie opłaty za utworzenie tokena opiera się na liczbie całkowitej podaży podzielnych jednostek tokena, która z kolei jest wyliczana z podaży tokena i liczby miejsc po przecinku w definicji tokena. <br>Na przykład token z podażą 1 000 000 i 2 miejscami po przecinku ma w sumie 100 000 000 podzielnych jednostek. Rzeczywista kalkulacja opłaty jest skalą logarytmiczną opartą na tej liczbie, według wzoru:</p><p>Opłata = (log10(podzielne jednostki) – 2) * 100</p><p>Zawsze obowiązuje minimalna opłata 1 NXS. Daje to następujące opłaty w oparciu o liczbę podzielnych jednostek</p><p>100 = 1 NXS<br>1,000 = 100 NXS<br>100,000 = 300 NXS<br>1,000,000 = 400 NXS<br>1,000,000,000 = 700 NXS<br>1,000,000,000,000 = 1000 NXS</p> |
| Opłata transakcyjna                                 |  0-1 | <p>Opłata transakcyjna jest naliczana za każdym razem, gdy transakcja jest tworzona w ciągu 10 sekund od ostatniej transakcji w łańcuchu podpisów. Opłata jest naliczana na podstawie liczby kontraktów w ramach transakcji po kursie 0,01 NXS za kontrakt, których może być maksymalnie 100 (w momencie pisania tego tekstu). Dlatego opłata transakcyjna będzie wynosić od 0 do 1 NXS.</p><p><br>Opłata transakcyjna jest stosowana dodatkowo do innych opłat opisanych w tej tabeli</p>           |

&nbsp;

## Zaawansowana opłata za wykonanie umowy:

W przypadku uruchomienia kontraktów zaawansowanych, z wyjątkiem kontraktów podstawowych (które są już bezpłatne) za wykonanie kontraktu zostanie naliczona opłata, ponieważ wymagają one cykli obliczeniowych, a opłata zostanie naliczona przed realizacją, a użytkownik zapłaci dokładnie pokazaną opłatę, w przeciwieństwie do GAS na Ethereum. &#x20;