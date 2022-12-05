---
title: Utwórz Tokenizowane Aktywo
description: Utwórz tokenizowane aktywo na Nexusie
published: true
date: 2022-12-05T00:12:08.015Z
tags: 
editor: markdown
dateCreated: 2022-10-22T21:50:39.750Z
---

# Utwórz Tokenizowane Aktywo

### Czym jest tokenizacja aktywa

`Tokenizacja aktywa`, zwana także `tokenami zabezpieczonymi aktywami` lub `aktywami tokenizowanymi`, to nowa koncepcja, która wykorzystuje tokeny cyfrowe do frakcjonowania własności aktywów, takich jak własność, biżuteria lub dzieła sztuki, i wykorzystuje kontrakty na blockchain do zarządzania tymi prawami własności.

Ten przewodnik pomoże użytkownikom utworzyć ***tokenizowane aktywo*** za pomocą interfejsu Nexus.

Zanim zaczniemy tworzyć tokenizację aktywa, użytkownicy muszą zapoznać się z niektórymi koncepcjami i parametrami.

Aby tokenizować aktywo, użytkownik musi utworzyć aktywo i token zgodnie z przewodnikami, do których prowadzą linki poniżej.

- [Utwórz aktywo](/pl/guides/create-asset)
- [Utwórz token](/pl/guides/create-token)

> Nazwij odpowiednio Aktywo i Token, aby można je było łatwo zidentyfikować.

## Utwórz tokenizację aktywa

Aby utworzyć tokenizowane aktywo za pomocą interfejsu, wykonaj poniższe czynności:

Otwórz interfejs Nexusa i upewnij się, że portfel jest w pełni zsynchronizowany. Zaloguj się na konto użytkownika (Sigchain).

Na stronie Przegląd u dołu kliknij moduł „*Użytkownik”*. Spowoduje to otwarcie strony *Użytkownika*.

Na stronie Użytkownik po lewej stronie kliknij zakładkę „*Aktywa*”.

Na stronie Aktywa zostaną wyświetlone wszystkie aktywa należące do konta użytkownika / Sigchain.

Kliknij Aktywo, które ma zostać poddane tokenizacji, otworzy się strona „Szczegóły Aktywa”.

![](/asset_details.png)

_Szczegóły Aktywa_

W prawym dolnym rogu tej strony kliknij „Tokenizacja”. Spowoduje to otwarcie strony „Tokenizacja”.

W tym oknie możesz wybrać Token do tokenizacji aktywa, dostęp do listy dostępnych tokenów można uzyskać za pomocą rozwijanej strzałki.

Po wybraniu odpowiedniego tokena kliknij przycisk „Tokenizuj” na dole strony.

## Wypłata aktywa

Główną użytecznością tokenizowanych aktywów jest umożliwienie częściowej własności i dzielenie się przychodami z posiadaczami tokenów. Aby wysłać wypłatę do posiadaczy tokenów, użytkownik wysyła ekwiwalent wartości NXS do wygenerowanego przychodu na adres aktywów, który zostanie automatycznie rozdzielony zgodnie z procentem posiadania tokenów przez każdego posiadacza.


>Wypłata jest rozdzielana, przyjmując maksymalną podaż jako 100% tokenów. Jeśli jakieś tokeny nadal znajdują się w adresie generowania tokenów, procent wypłaty odpowiadający tokenom salda zostanie zwrócony nadawcy.
{.is-warning}