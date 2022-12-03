---
title: Alerty Nexusa
description: Nexus Alert Telegram Bot – Odszyfruj informacje
published: true
date: 2022-12-03T17:10:08.821Z
tags: 
editor: markdown
dateCreated: 2022-10-22T21:53:20.736Z
---

# Alerty Nexusa

Nexus Alerts, bot telegramu wyświetli listę transakcji na łańcuchu bloków Nexusa powyżej 1000 NXS lub tokenów. Ten bot zrodził się z prośby społeczności o śledzenie rozwoju sieci, sposób na wycenę Nexusa poprzez śledzenie transakcji online, całkowity NXS w łańcuchu tritium w porównaniu z NXS na giełdach, a także sposób na uświadomienie sobie dużych transakcji prowadzących do pomp i zrzutów.

> Alerty śledzą tylko transakcje w sieci tritium.
{.is-info}

## Dane wyświetlane w alertach:

Każda transakcja odbywająca się w łańcuchu blokowym jest sprawdzana pod kątem kredytu i jest wysyłana jako ostrzeżenie do Nexus Alert Bot. Te dane wyświetlane są z alertami jak poniżej:

![alert_data1.png](/alert_data1.png)

* Ikona ryby wyświetlana zgodnie z [legendą](nexus-alerts.md#legenda).
* `Humpback Whale found on block` : Wysokość bloku.
* `Amount` : Kwota NXS lub tokenów zawartych w transakcji.
* `Token`: Token, dla którego generowany jest `credit`. NXS lub Token (nazwa lub adres).
* `Operation`: Operacja kontraktu. W alertach wyświetlana jest tylko umowa `CREDIT`.
* `For` : Jest to typ powiadomienia, dla którego została przeprowadzona **`Operation`**.
* `Proof`: Adres rejestrowy potwierdzający kredyt lub adres wysyłający dla `debit` z tritium.
* `To`: Adres odbioru.
* `Link`: Łącze eksploratora do szczegółów wysokości bloku.

&nbsp;

## Zrozumienie danych alertu:

Bot alertów jest łatwy do zrozumienia, ale dla niektórych może być mylący. Ten przewodnik pomoże w zrozumieniu dostarczonych danych.\
\
Nexus ma łańcuchy „Tritium” i „Legacy”, wszystkie giełdy używają starszego łańcucha i trudno jest śledzić saldo starszych kont, a najlepsze, co możemy zrobić, to śledzić transakcje w sieci tritium. Alerty ograniczają się tylko do śledzenia transakcji NXS i tokenów powyżej 1000 NXS.

Aby lepiej zrozumieć dane dostarczane przez bota możemy podzielić transakcje na:

* **Transakcje Tritium do Tritium**
* **Transakcje Legacy do Tritium**
* **Transakcje Tritium do Legacy**

&nbsp;

### Transakcje Tritium do Tritium:&#x20;

![tritium_to_tritium1.png](/tritium_to_tritium1.png)

Każda transakcja na tritium jest `obciążeniem` konta nadawcy i `uznaniem` konta odbiorcy. Tworzy to dwie transakcje dla pojedynczego przelewu, podobnie jak w przypadku podwójnego księgowania, ale bot jest zaprojektowany tak, aby ignorować `DEBIT` i pokazywać tylko `CREDIT`, ponieważ jest to pojedynczy przelew, a posiadanie dwóch alertów spowoduje więcej zamieszania.

Łatwo to rozróżnić, ponieważ pole `Operation` to `CREDIT`, a pole `For` to `DEBIT`, co oznacza, że jest to `credit` za odpowiadające mu `debit`. 

&nbsp;

### Transakcje Legacy do Tritium:

![legacy_to_tritium1.png](/legacy_to_tritium1.png)

Transakcje Legacy to Tritium mają miejsce, gdy użytkownik wypłaca NXS z giełdy na swoje konto Tritium. Ta transakcja wyświetli tylko `credit` na koncie Tritium i można ją łatwo rozpoznać, zaznaczając pole `Operation`, które powinno brzmieć `CREDIT`, a pole "`For`" brzmi `LEGACY` , co oznacza, że jest to `credit` dla przychodzącej transakcji `legacy`.

&nbsp;

### Transakcje Tritium do Legacy:

![tritium_to_legacy1.png](/tritium_to_legacy1.png)

Transakcje Tritium do Legacy są przeprowadzane, gdy użytkownik wysyła NXS na konto wymiany lub na osobiste konto tradycyjne. Ta transakcja wyświetli tylko `debit` na koncie Tritium i może być łatwo rozpoznana poprzez zaznaczenie pola `Operation`, które powinno brzmieć `LEGACY`, a także adres `To` będzie zaczynał się od `2`, co oznacza adres Legacy.

&nbsp;

### Legenda:

Aby różnice wizualne były oparte na kwotach, alerty zostały pogrupowane na podstawie kwot transakcji i nazwane na podstawie ryb według rozmiaru.

&#x20;Legenda jest podana poniżej:

* \>= 500 000 NXS: Płetwal błękitny (🐳🐳🐳🐳🐳🐳)
* \>= 250 000 NXS: Kaszalot (🐋🐋🐋🐋🐋🐋)
* \>= 100 000 NXS: Humbak (🐋🐋🐋)
* \>= 80 000 NXS: Rekin wielorybi (🦈🦈🦈🦈🦈🦈)
* \>= 60 000 NXS: Rekin tygrysi (🦈🦈🦈🦈)
* \>= 30 000 NXS: Żarłacz biały (🦈🦈)
* \>= 10 000 NXS: Delfin (🐬🐬)
* \>= 5000 NXS: Tuńczyk (🐟🐟)
* \>= 1000 NXS: Sardynka (🐠🐠)
* < 1000 NXS: Krewetki (🦐🦐 )- (Nie jest teraz używane jako < 1000NXS)