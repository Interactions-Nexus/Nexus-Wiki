---
title: Utwórz token
description: Utwórz token za pomocą interfejsu Nexusa
published: true
date: 2022-12-07T23:46:48.734Z
tags: 
editor: markdown
dateCreated: 2022-10-22T21:47:14.420Z
---

# Utwórz Token

Ten przewodnik pomoże użytkownikom utworzyć **Token** przy użyciu interfejsu Nexus

Zanim zaczniemy tworzyć token, użytkownicy muszą zapoznać się z niektórymi koncepcjami, właściwościami, parametrami i opłatami za tokeny.

> Tokeny na Nexusie działają zupełnie inaczej niż na innych blockchainach. Istnieje wiele różnic, które użytkownik musi zrozumieć, dlatego zalecamy użytkownikom przeczytanie tego kompletnego przewodnika.
{.is-warning}


## Tokeny na Nexusie:

Aby tworzyć tokeny i przeprowadzać transakcje na Nexusie, użytkownicy muszą najpierw zrozumieć różne konta i właściwości tokenów:

Po utworzeniu tokena, adres generacji tokena zostanie wyświetlony na stronie „Tokeny”. To jest adres generujący token, a nie konto tokena. Adres generujący jest własnością profilu (konta użytkownika), który wystawił token.

> Każdy użytkownik, który chce przeprowadzić transakcję tokenem, musi utworzyć adres tokena powiązany z tym konkretnym tokenem.
{.is-info}

Po utworzeniu token ma następujące właściwości:
- tokenname — Globalna nazwa tokenu, jeśli został utworzony.
- maxsupply - Maksymalna liczba tokenów, które będą istnieć.
- currentsupply - Liczba krążących tokenów, które zostały rozdzielone na konta tokenów.
- balance - Ilość tokenów, które nie zostały jeszcze rozdane (maxsupply - currentsupply).
- decimals - Liczba miejsc dziesiętnych.
- address - Jest to adres rejestru tokena lub adres generowania tokena.

### Adres generowania tokena

Jest to adres rejestru, który generuje ten konkretny token, a tokeny w tym adresie są wycofane z obiegu. Tokeny wysyłane na konto tokenowe wchodzą do obiegu. Użytkownicy mogą odsyłać tokeny z powrotem na adres generacji, aby usunąć je z obiegu.

### Konto tokenowe:

Jest to zwykłe konto tokenowe, które może wysyłać lub odbierać token z adresu generacyjnego lub konta tokenowego. Każde konto tokenowe jest połączone tylko do określonego tokena i nie może otrzymać żadnego innego tokena. Każdy użytkownik musi ręcznie utworzyć konto tokena, aby przeprowadzić transakcję określonym tokenem.


> Konta tokenów mogą otrzymywać tylko ten konkretny token, z którym są połączone. Nie mogą zaakceptować NXS ani żadnego innego tokena. Standardowe konta „domyślne”, „zaufane” lub dowolne konta NXS nie akceptują żadnych tokenów.
{.is-warning}


## Parametry tokena

Parametry tokena definiują token, takie jak nazwa tokena, podaż i miejsca po przecinku. Dowiedz się więcej o nich poniżej:

### NAZWA TOKENU

Nazwa tokena jest inaczej rozpoznawana w tritum i tritium++.

##### Tritium

Jest to nazwa lokalna służąca do identyfikacji tokenu i jest opcjonalna. Ta nazwa znajduje się wewnątrz konta użytkownika (Sigchain) i nie jest ważna poza nim.

Nazwa tokena ma oddzielną opłatę w wysokości `1 NXS`. Emitent może zrezygnować z tworzenia nazwy tokena i może użyć adresu rejestru, aby uzyskać dostęp do aktywów lub je przeszukiwać. To jest nazwa lokalna i nie jest ważna poza Sigchain.

> Jeśli dla tokena potrzebna jest unikalna nazwa globalna (ticker), wystawca musi utworzyć nazwę globalną i powiązać ją z tokenem.
{.is-info}


##### Tritium++ (Nadchodząca aktualizacja)

W tritium++ jest to rozwiązane na nazwę globalną (ticker) w celu identyfikacji tokena i jest opcjonalne. Ta nazwa jest rozpoznawalna na całym świecie w sieci. Profil, który utworzył token o nazwie globalnej, będzie właścicielem i tę nazwę globalną można przenieść do innych profili.

> Globalna nazwa tokena ma oddzielną opłatę w wysokości `2000 NXS`. Wystawca może zrezygnować z tworzenia nazwy tokena i może użyć adresu rejestru, aby uzyskać dostęp do tokena lub go przeszukać.
{.is-info}

### PODAŻ

Jest to łączna liczba wymiennych tokenów, które należy wygenerować. Opłata wzrasta wraz ze wzrostem podaży. Sprawdź opłaty [tutaj]

> Maksymalna ilość tokena nie może zostać zwiększona po wygenerowaniu tokena. Tokeny można spalić, aby usunąć je z obiegu.
{.is-warning}

### DZIESIĘTNA

Jest to liczba miejsc po przecinku dla tokena, zwiększenie liczby miejsc po przecinku również zwiększa opłatę. Jednostki dziesiętne są wymagane dla mikro transakcji i są ustawiane w zależności od użycia tokena i tokenomiki.


## Opłaty za bicie tokenów

Opłata jest oparta na liczbie zdefiniowanych przez Ciebie podzielnych jednostek tokena (kombinacja podaży i miejsc po przecinku). Minimalna opłata wynosi 1 NXS, a następnie obliczenia są liniowe, tak że każda dodatkowa cyfra znacząca kosztuje dodatkowe 100 NXS. Np.

100 jednostek = 1 NXS

1000 jednostek = 100 NXS

1000000 jednostek = 400 NXS

10000000000 jednostek = 800 NXS

Aby uzyskać bardziej szczegółowe informacje, sprawdź [Opłaty.](/pl/economics/fees)

&nbsp;

## Utwórz token

Aby utworzyć token za pomocą interfejsu, wykonaj poniższe czynności:

* Otwórz interfejs Nexus, upewnij się, że portfel jest w pełni zsynchronizowany i zaloguj się do profilu użytkownika (Sigchain).
* Na stronie Przegląd u dołu kliknij moduł `Użytkownik`. Spowoduje to otwarcie strony użytkownika.
* Na stronie Użytkownika, po lewej stronie kliknij w zakładkę `Tokeny`.
* Na stronie Aktywa kliknij `Utwórz nowy token`. Spowoduje to otwarcie strony *Nowy token*.
* Na tej stronie użytkownik musi podać trzy parametry definiujące token. Parametry i ich szczegóły podano poniżej:
* Po podaniu parametrów kliknij przycisk `Utwórz token` na dole strony.
* Po potwierdzeniu tokena w łańcuchu blokowym adres tokena zostanie wyświetlony na stronie `Tokeny`.
* Aby sprawdzić szczegóły dowolnego tokena, kliknij adres tokena na stronie `Tokeny`, a strona szczegółów tokena otworzy się ze szczegółami.