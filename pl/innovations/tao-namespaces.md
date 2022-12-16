---
title: Przestrzenie nazw TAO
description: System nazewnictwa TAO
published: true
date: 2022-12-16T23:08:26.917Z
tags: 
editor: markdown
dateCreated: 2022-10-22T21:31:45.200Z
---

# TAO - Przestrzenie nazw

## Nazwy i Przestrzenie nazw

Nazwy i przestrzenie nazw to specjalne rodzaje rejestrów obiektów, które są używane jako lokalizatory innych rejestrów obiektów w łańcuchu bloków. Kiedy rejestr obiektów jest tworzony po raz pierwszy (na przykład aktywo), wywołujący może podać nazwę rejestru. Jeśli podano nazwę, tworzony jest również rejestr obiektu Nazwa z jego adresem rejestru na podstawie skrótu nazwy. Obiekt Name posiada również pole adresu, które jest wypełniane adresem rejestru (aktywa, tokena, konta itp.), na który 'wskazuje' nazwa. W ten sposób obiekty mogą być pobierane według nazwy, najpierw mieszając nazwę, aby uzyskać adres obiektu Nazwa, pobierając obiekt Nazwa, a następnie używając zapisanego w nim adresu, aby pobrać rejestr obiektów. Nazwa jest więc najlepiej traktowana jako nazwany indeks do rejestrów obiektów.

System nazewnictwa TAO (TNS) umożliwia tworzenie obiektów nazw w jednym z trzech różnych kontekstów lub przestrzeni nazw — `local`, `namespaced` i `global`. Nazwy muszą być unikalne w przestrzeni nazw, w której zostały zdefiniowane.

## NAZWY:

Nazwy lokalne to nazwy utworzone w kontekście łańcucha sygnatur. Aby użyć nazwy lokalnej, musisz poprzedzić nazwę nazwą użytkownika właściciela oddzieloną pojedynczym dwukropkiem, np. `bob:savings`. Jest to równoznaczne z powiedzeniem „spójrz na wszystkie nazwy zarejestrowane w  sigchain `bob` i znajdź jedną o nazwie `savings`, a następnie zobacz, na jaki rejestr obiektów wskazuje”. Może istnieć tylko jedna nazwa o nazwie `savings` w łańcuchu sig `bob`, ale inny użytkownik `alice` może również utworzyć lokalną nazwę o nazwie `savings`.

## PRZESTRZEŃ NAZW:

Przestrzenie nazw umożliwiają użytkownikom nadawanie przyjaznych dla użytkownika nazw rejestrów obiektów bez konieczności ujawniania nazwy użytkownika. Jest to przydatne ze względu na prywatność, ale także umożliwia powiązanie nazw z firmą lub innym znaczącym kontekstem. Aby uniknąć zajmowania nazw, rejestracja przestrzeni nazw wiąże się z wysoką opłatą (`1000 NXS`). Jednak po zarejestrowaniu tworzenie Nazw w tej przestrzeni nazw kosztuje tylko `1 NXS`.

### Z przestrzenią nazw:

Nazwy utworzone w kontekście przestrzeni nazw nazywane są przestrzeniami nazw, co samo w sobie jest globalnie unikalnym słowem kluczowym. Aby użyć nazwy z przestrzenią nazw, musisz poprzedzić nazwę przestrzenią nazw oddzieloną podwójnym dwukropkiem, np. `bobscoffeeshop::payments`. W tym przykładzie Bob najpierw zarejestrowałby przestrzeń nazw `bobscoffeeshop` i utworzył konto do otrzymywania płatności (które można nazwać czymkolwiek). Następnie tworzy Nazwę z parametrami `namespace=bobscoffeeshop` i `address=(register address of the account)`. Od tego momentu każdy może używać nazwy `bobscoffeeshop::payments` i zostanie ona rozwiązana na adres rejestracyjny konta.

## NAZWY GLOBALNE:

Nazwy globalne nie wymagają nazwy użytkownika ani prefiksu przestrzeni nazw i dlatego są globalnie unikalne. Będą one prawdopodobnie zarezerwowane dla przypadków użycia, w których konieczna jest zwięzła, niepowtarzalna nazwa, na przykład symbol giełdowy tokena. Aby uniknąć niepotrzebnego zajmowania nazw, globalne nazwy wiążą się z wysoką opłatą (`2000 NXS`).

Interfejs Names API umożliwia wywołującym dostęp do nazw i przestrzeni nazw oraz zarządzanie nimi. Nazwy mogą być tworzone tak, aby „wskazywały” dowolny adres rejestru, niezależnie od tego, czy wywołujący jest właścicielem rejestru, czy nie. Jest to przydatne na przykład, jeśli ktoś poda Ci adres rejestrowy konta NXS do otrzymywania płatności i chcesz dodać do niego przyjazną Nazwę do wykorzystania w przyszłości.

Przestrzenie nazw można przenosić do innych łańcuchów sygnatur, otwierając możliwość kupna i sprzedaży przestrzeni nazw na rynku wtórnym (podobnie jak nazwy domen internetowych).

Nazwy globalne i nazwy, które zostały utworzone w przestrzeni nazw, mogą być również przenoszone do innych łańcuchów sygnatur. Nie można przenosić nazw lokalnych.

W przyszłości, gdy narodzi się Safenet, zdecentralizowany Internet, przestrzeń nazw może być używana jako nazwa domeny.