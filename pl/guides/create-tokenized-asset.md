---
title: Utwórz Tokenizowane Aktywo
description: Utwórz tokenizowane aktywo na Nexusie
published: true
date: 2022-12-04T23:24:26.986Z
tags: 
editor: markdown
dateCreated: 2022-10-22T21:50:39.750Z
---

# Utwórz Tokenizowane Aktywo

### Czym jest tokenizacja zasobów

„Tokenizacja aktywów”, zwana także „tokenami zabezpieczonymi aktywami” lub „zasobami tokenizowanymi”, to nowa koncepcja, która wykorzystuje tokeny cyfrowe do frakcjonowania własności aktywów, takich jak własność, biżuteria lub dzieła sztuki, i wykorzystuje kontrakty na blockchain do zarządzania tymi prawami własności

Ten przewodnik pomoże użytkownikom utworzyć ***tokenizowany zasób*** za pomocą interfejsu Nexus.

Zanim zaczniemy tworzyć tokenizację zasobów, użytkownicy muszą zapoznać się z niektórymi koncepcjami i parametrami.

Aby tokenizować zasób, użytkownik musi utworzyć zasób i token zgodnie z przewodnikami, do których prowadzą linki poniżej.

- [Utwórz zasób](/en/guides/create-asset)
- [Utwórz token](/en/guides/create-token)

> Nazwij odpowiednio zasób i token, aby można je było łatwo zidentyfikować.

## Utwórz tokenizację zasobów

Aby utworzyć tokenizowany zasób za pomocą interfejsu, wykonaj poniższe czynności:

Otwórz interfejs Nexusa i upewnij się, że portfel jest w pełni zsynchronizowany. Zaloguj się na konto użytkownika (Sigchain).

Na stronie Przegląd u dołu kliknij moduł „*Użytkownik”*. Spowoduje to otwarcie strony *Użytkownika*.

Na stronie Użytkownik po lewej stronie kliknij zakładkę „*Zasoby*”.

Na stronie Zasoby zostaną wyświetlone wszystkie zasoby należące do konta użytkownika / Sigchain.

Kliknij zasób, który ma zostać poddany tokenizacji, otworzy się strona „Szczegóły zasobu”.

![](/asset_details.png)

Szczegóły aktywów

W prawym dolnym rogu tej strony kliknij „Tokenizacja”. Spowoduje to otwarcie strony „Tokenizacja”.

W tym oknie możesz wybrać Token do tokenizacji zasobu, dostęp do listy dostępnych tokenów można uzyskać za pomocą rozwijanej strzałki.

Po wybraniu odpowiedniego tokena kliknij przycisk „Tokenizuj” na dole strony.

## Wypłata aktywów

Główną użytecznością tokenizowanych aktywów jest umożliwienie częściowej własności i dzielenie się przychodami z posiadaczami tokenów. Aby wysłać wypłatę do posiadaczy tokenów, użytkownik wysyła ekwiwalent wartości NXS do wygenerowanego przychodu na adres aktywów, który zostanie automatycznie rozdzielony zgodnie z procentem posiadania tokenów przez każdego posiadacza.

{% tips style="ostrzeżenie" %}
Wypłata jest rozdzielana, przyjmując maksymalną dostawę jako 100% tokenów. Jeśli jakieś tokeny nadal znajdują się w adresie generowania tokenów, procent wypłaty odpowiadający tokenom salda zostanie zwrócony nadawcy.