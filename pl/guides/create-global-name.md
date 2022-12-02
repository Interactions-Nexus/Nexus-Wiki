---
title: Utwórz Nazwę Globalną
description: Jak stworzyć globalną nazwę
published: true
date: 2022-12-02T08:06:43.070Z
tags: 
editor: markdown
dateCreated: 2022-10-22T21:52:18.285Z
---

# Utwórz Nazwę Globalną

Ten przewodnik pomoże użytkownikom utworzyć **Nazwę Globalną** za pomocą interfejsu Nexus. Zanim zaczniemy tworzyć **Nazwę Globalną**, użytkownicy muszą zapoznać się z koncepcją i zastosowaniem.

## Nazwa Globalna:

Nazwy globalne nie wymagają nazwy użytkownika ani prefiksu przestrzeni nazw i dlatego są globalnie unikalne. Będą one prawdopodobnie zarezerwowane dla przypadków użycia, w których konieczna jest zwięzła, niepowtarzalna nazwa, na przykład symbol giełdowy tokena. Aby uniknąć niepotrzebnego fałszowania nazw, nazwy globalne wymagają opłaty w wysokości `2000` NXS.


> Utworzenie nazwy globalnej wiąże się z opłatą w wysokości 2000 NXS. Opłaty zostaną pobrane z konta domyślnego.
{.is-warning}


## Użycie Nazwy Globalnej:

Najlepszym przypadkiem użycia globalnej nazwy będą tikery tokenów. W przypadku rynku P2P bardzo pomocne będzie posiadanie globalnego tikera dla tokena, który ułatwi jego listę, a także będzie łatwo rozpoznawalny przez użytkowników.

Tokenami można handlować bez globalnej nazwy, ale będą one adresowane przez adres rejestru, co nie jest zalecane, ponieważ użytkownicy nie będą go łatwo rozróżniać.


## Tritium++:

> W Tritium++, gdy użytkownik tworzy token, domyślnie tworzona jest `global name`, jeśli podany jest parametr `name`.
{.is-info}

&nbsp;
## Parametry Nazw Globalnych:

Parametry wymagane do utworzenia nazwy globalnej.

### Pole nazwy

W tym polu użytkownik podaje nazwę globalną do utworzenia.

### Ares rejestru

W tym polu użytkownik podaje adres rejestru tokena, który będzie powiązany z nazwą globalną.

## Utwórz nazwę:

Aby utworzyć nazwę za pomocą interfejsu, wykonaj następujące czynności:

* Otwórz interfejs Nexus, upewnij się, że portfel jest w pełni zsynchronizowany i zaloguj się na konto użytkownika (Sigchain).
* Na stronie Przegląd u dołu kliknij moduł „_Użytkownik”_. Spowoduje to otwarcie strony użytkownika.
* Na stronie Użytkownik po lewej stronie kliknij zakładkę „_Nazwy_”.
* Na stronie Nazwy kliknij „_Utwórz nową nazwę_”. Spowoduje to otwarcie strony _Utwórz nową nazwę_.
* U góry strony upewnij się, że przycisk „GLOBALNY” jest podświetlony, jeśli nie, kliknij go.
* Na tej stronie użytkownik musi podać „Nazwę” i „adres rejestrowy”, na który wskazuje.&#x20;
* Po podaniu parametrów kliknij przycisk „UTWÓRZ NAZWĘ” na dole strony.
* Dane zostaną przesłane do sieci w celu weryfikacji, a po potwierdzeniu transakcji nowo utworzona nazwa globalna pojawi się na liście.