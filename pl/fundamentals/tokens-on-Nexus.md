---
title: Tokeny na Nexusie
description: Wszystko o tokenach
published: true
date: 2022-12-14T21:57:19.642Z
tags: 
editor: markdown
dateCreated: 2022-10-21T22:04:18.352Z
---

# Tokeny

## Co to jest token?

W szerszym znaczeniu tokeny można traktować jako wirtualne waluty istniejące w łańcuchu bloków.

## Do czego można używać tokenów?

Mogą być wykorzystywane do różnych zastosowań, takich jak:

- Reprezentujący własność aktywów, takich jak firma, własność, prawa do dzieła sztuki lub muzyki.
- Narzędzia
- Programy lojalnościowe
- Tokeny do gier
- Prawa głosu DAO

**Czym różni się token utworzony na blockchainie Nexusa od tokenów utworzonych na Ethereum, Waves, NEO, NEM, Stellar itp.?**

Podstawową różnicą jest prostota. Aby utworzyć token na Ethereum lub większości innych platform tokenowych, użytkownicy muszą napisać inteligentną umowę – kod napisany w określonym języku programowania – aby zdefiniować token i sposób, w jaki będzie używany/dystrybuowany. Wymaga to od użytkownika umiejętności programowania, a zadanie często może być dość skomplikowane. Nexus przyjął inne podejście, upraszczając proces, umożliwiając użytkownikom utworzenie tokena w jednym krótkim poleceniu konsoli / żądaniu API. Interfejs portfela idzie o krok dalej, zapewniając prosty interfejs, który prowadzi użytkowników przez proces.

## Jak utworzyć token?

Tokeny można łatwo tworzyć za pomocą portfela Nexus lub konsoli/CLI. Użytkownik definiuje nowy token, aby można go było dystrybuować, handlować lub używać do tokenizacji aktywów.

Aby utworzyć nowy Token, przejdź do modułu Użytkownika w Portfelu i postępuj zgodnie z poniższymi instrukcjami:

1. Kliknij Tokeny.
2. Kliknij opcję Utwórz nowy token.
3. Wybierz nazwę tokena.
4. Wybierz łączną liczbę Tokenów, które mają zostać utworzone.
5. Wybierz ilość cyfr znaczących, które będzie miał Token.
6. W górnej części pola w NXS zostanie wyświetlona opłata za utworzenie podaży tokenów.
7. Kliknij opcję Utwórz token.
8. Zapłać opłaty.

Aby osiągnąć to samo za pomocą konsoli, użyj następującego polecenia:

```
finance/create/token name=My_Token supply=100 decimals=2 pin=1234
```

Kompromisem dla prostoty jest elastyczność. Token utworzony z tradycyjnego inteligentnego kontraktu pozwala programistom na zdefiniowanie dowolnych reguł dystrybucji i używania tokena, które są zakodowane w kontrakcie definicji tokena. Ta elastyczność jest z pewnością przydatna, ale jest zbyt skomplikowana dla osób bez umiejętności programowania.

Nexus oddziela zasady umowy od definicji tokena, dzięki czemu tworzenie tokena jest znacznie prostsze, ale zapewnia dalsze kroki, jeśli potrzebne są bardziej złożone zasady. W przypadkach użycia, które wymagają bardziej złożonego narzędzia tokena, użytkownicy Nexusa mogą dodać reguły kontraktowe jako warunki transakcji debetowych tokena.

Jeśli reguły są zbyt złożone, aby mogły być obsługiwane przez warunek transakcji, programiści mogą zapisać te reguły w swojej warstwie aplikacji.

Kiedy po raz pierwszy tworzysz token, musisz określić podaż (maksymalną liczbę całych tokenów, które będą dostępne) i miejsca po przecinku (liczbę miejsc po przecinku, jaką może mieć kwota tokena).

Połączenie tych dwóch wartości daje liczbę podzielnych jednostek tokena, które będą dostępne (odpowiednik własności Bitcoina Satoshi). Na przykład wartość dziesiętna 3 oznacza, że każdy token można podzielić na 10^3 (1000) części. Dlatego token utworzony z podażą 1 000 000 i liczbą dziesiętną 3 dałby 1 000 000 000 (1 000 000 x 1 000) podzielnych jednostek tokena. Jest to ważne, ponieważ ta liczba jest używana do obliczenia opłaty stosowanej podczas tworzenia tokena.

Po utworzeniu token ma trzy ważne właściwości:

* maxsupply - maksymalna liczba tokenów, które będą istnieć
* currentsupply - liczba krążących tokenów, które zostały rozdysponowane na konta tokenów
* balance - ilość tokenów, które nie zostały jeszcze rozdane (maxsupply - currentsupply)

## Opłaty
Opłata jest oparta na liczbie zdefiniowanych przez Ciebie podzielnych jednostek tokena (kombinacja podaży i miejsc po przecinku). Minimalna opłata wynosi 1 NXS, a następnie obliczenia są liniowe, tak że każda dodatkowa cyfra znacząca kosztuje dodatkowe 100 NXS. Np.

100 jednostek = 1 NXS

1000 jednostek = 100 NXS

1000000 jednostek = 400 NXS

10000000000 jednostek = 800 NXS

Początkowo cała podaż tokenów jest przechowywana w saldzie tokena. Dystrybucja tokena do innych użytkowników jest wtedy bardzo podobna do wysyłania NXS. Pierwszym krokiem jest to, że użytkownicy otrzymujący muszą utworzyć nowe konto dla Twojego typu tokena, a następnie podać nazwę/adres konta. Następnie możesz użyć interfejsu portfela, aby wysłać je tak, jak wysyłasz NXS, wybierając token z listy Wyślij z. Alternatywnie możesz użyć konsoli za pomocą następującego polecenia:

```
finance/debit/token from=My_Token to=paul:tokenaccount amount=1000 pin=1234
```

Maksymalnej podaży nie można zmienić po utworzeniu tokena.

**Jak używać tokena do reprezentowania częściowej własności aktywa cyfrowego lub rzeczywistego?**

Jednym z najważniejszych przypadków użycia tokenów jest możliwość tokenizacji aktywa. Tokenizowane aktywa zapewniają możliwość automatycznego rozdzielania wspólnych dochodów w formie płatności NXS między częściowych właścicieli aktywów, w oparciu o procent posiadanych tokenów. Jest to przydatne w przypadkach użycia, takich jak automatyczna wypłata dywidend za tokenizowane aktywa oraz do dystrybucji tantiem z przychodów uzyskanych z aktywów, takich jak album muzyczny.