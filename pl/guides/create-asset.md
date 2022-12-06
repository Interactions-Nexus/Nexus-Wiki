---
title: Utwórz Aktywo
description: Utwórz Aktywo za pomocą interfejsu
published: true
date: 2022-12-06T00:11:03.302Z
tags: 
editor: markdown
dateCreated: 2022-10-22T21:48:53.360Z
---

# Utwórz Aktywo

Ten przewodnik pomoże użytkownikom utworzyć **Aktywo**, popularnie zwany także **NFT**, sprawdzić szczegóły aktywa i przenieść własność za pomocą interfejsu Nexus.

Zanim zaczniemy tworzyć aktywo, użytkownicy muszą zapoznać się z niektórymi koncepcjami i parametrami używanymi z aktywami.

>Tworzenie Aktywa wiąże się z opłatą w wysokości 1 NXS i „_Nazwa Aktywa”_ wiąże się z opłatą w wysokości 1 NXS. Całkowity koszt Aktywa z nazwą wyniesie 2 NXS.
{.is-info}

## Parametry Aktywa

### Nazwa Aktywa

Jest to globalnie unikatowa nazwa aktywa. Duplikaty nazw nie będą dozwolone. Jeśli tworzysz grupę aktyw o podobnej nazwie, użyj numeru seryjnego z nazwą.

>Nazwa Aktywa ma oddzielną opłatę w wysokości 1NXS. Użytkownicy mogą zrezygnować z tworzenia nazwy aktywa i mogą korzystać z adresu rejestracyjnego, aby uzyskać dostęp do aktywa lub go przeszukiwać.
{.is-info}


Konwencja nazewnictwa:
* Użyj unikalnej nazwy, jeśli tworzysz aktywo. Preferowane są krótkie nazwy, ale w razie potrzeby używaj długich nazw.
* Nazwy mogą zawierać wielkie i małe litery, cyfry i znaki specjalne.
* Jeśli tworzysz aktywo z rzeczywistych aktyw, takich jak nieruchomości, podaj jasne i precyzyjne informacje dla nazwy aktywa.&#x20;
* Jeśli tworzysz kilka Aktyw / NFT, na przykład z jednej kolekcji dzieł sztuki, dodaj do nazwy kolekcji unikalny numer seryjny serii Np.: „_Iron Maiden #0001.”_

### Dane Aktywa

Ta sekcja dotyczy danych lub metadanych aktywa. Podane tutaj informacje pomagają nadać ważność aktywu i jego wartości. Dane o aktywach muszą być dokładne, kompletne i powinny umożliwiać każdemu sprawdzenie autentyczności aktywa, na którym się on znajduje. Dostarczone dane będą zależeć od aktywa cyfrowego lub fizycznego, który jest wspierany jako aktywo blockchain. &#x20;

>Dane aktywa mają limit 1 KB i jest to wiążące. Aktywo może zawierać około 990 - 995 znaków ze spacjami. Nie dotyczy to nazwy aktywa.
{.is-info}

Aby łatwo policzyć znaki dla danych Aktywa, użyj poniższego łącza:

[wordcount.com](https://wordcount.com)

>**Nota:** Jeśli tworzysz Aktywo dzieła sztuki cyfrowej, który zasadniczo jest plikiem graficznym, podaj skrót md5 oryginalnego obrazu, aby każdy mógł sprawdzić autentyczność tego konkretnego pliku. Jeśli wszystkie szczegóły zostaną podane bez skrótu pliku, aktywo nie będzie użyteczne, ponieważ nikt nie będzie w stanie potwierdzić autentyczności pliku, który reprezentuje aktywo.
{.is-warning}

Dane o aktywch są wprowadzane w polach, które na powyższym obrazku przedstawiają pojedynczą linię.&#x20;

#### Nazwa:&#x20;

Pierwsza kolumna to nazwa pola, która jest nazwą danych, które zamierzasz dodać, takich jak Opis, Właściciel, Artysta, Hash itp.

#### Wartość:&#x20;

Druga kolumna to wartość pola, na przykład nazwisko właściciela.

#### Zmienny:

Trzeci to przycisk radiowy umożliwiający włączenie pola zmiennego (domyślnie jest wyłączone). Zmienne pola mogą być zmieniane w dowolnym momencie przez właściciela łańcucha znaków aktywa. Jest to bardzo pomocne w przypadku, gdy masz dom uznany jako aktywo, a kiedy sprzedasz dom, przekaż aktywo nowemu właścicielowi, a on może zmienić pole „Właściciel” na swoje nazwisko.

> Zmieniaj tylko te pola, które naprawdę potrzebują. Np. Podczas tworzenia aktywa, który odnosi się do domu, pole „Właściciel” musi być zmienne, wynika to z lokalizacji, nazwy, numeru rejestracyjnego.&#x20;
{.is-info}

#### Rodzaj:

String: Jest to typ danych używany do reprezentowania tekstu. Składa się z zestawu znaków, który może zawierać również spacje i cyfry. Na przykład słowo „hamburger” i wyrażenie „Zjadłem 3 hamburgery” to ciągi znaków. Nawet „12345” można uznać za ciąg znaków.

Typy dat uint8, uint16, uint32, uint64, uint128, uint256, uint512 i uint1024 reprezentują liczbę całkowitą bez znaku przechowywaną z 8, 16, 32 lub 64 bitami.&#x20;

|       Type | No of Bits | Min - Max Value                |
| ---------- | :--------: | ------------------------------ |
| uint8      |      1     | 0 - 255                        |
| unit16     |      2     | 0 - 65535                      |
| uint32     |      4     | 0 - 4,294,967,295              |
| unit64     |      8     | 0 - 18,446,744,073,709,551,615 |
| unit256    |     16     | 0 - 2^256-1                    |
| uint512    |     32     | 0 - 2^512-1                    |
| uint1024   |     64     | 0 - 2^1024-1                   |

**Maksymalna długość:**

To pole jest włączone tylko wtedy, gdy pole jest wybrane jako zmienne, a typ jako „ciąg”. Jest to ważne, ponieważ pozwoli to ograniczyć długość pola przy późniejszej zmianie i zmieścić Dane o aktywie w limicie 1 KB.

## Utwórz Aktywo

Aby utworzyć aktywo za pomocą interfejsu, wykonaj poniższe czynności:

* Otwórz interfejs Nexus, upewnij się, że portfel jest w pełni zsynchronizowany. Zaloguj się na konto użytkownika (Sigchain).
* Na stronie Przegląd u dołu kliknij moduł „_User”_. Spowoduje to otwarcie strony użytkownika.
* Na stronie użytkownika po lewej stronie kliknij zakładkę „_Assets_”. Na stronie Aktywa zostaną wyświetlone aktywa należące do Sigchain.
* Na stronie Aktywa kliknij „Utwórz nowe aktywo”. Spowoduje to otwarcie strony _Utwórz nowe aktywo_.
* Na tej stronie użytkownik musi podać nazwę oraz dane definiujące aktywo.&#x20;
   * **Dodaj kolejne pole:** Aby dodać kolejne pole, kliknij przycisk „+DODAJ POLE” pod pierwszym polem.
   * **Usuń pole:** Aby usunąć pole, umieść wskaźnik myszy na tym polu, po lewej stronie pola pojawi się ikona „x”, kliknij ją, aby usunąć pole.
* Po podaniu danych sprawdź, czy wszystko jest w porządku. Na dole możesz zobaczyć szacowany koszt wybicia tego aktywa. Kliknij przycisk „UTWÓRZ AKTYWO” na dole strony.

>Opłaty zostaną automatycznie pobrane z konta „domyślnego”, upewnij się, że masz NXS na pokrycie opłat, w przeciwnym razie aktywa nie zostaną wyemitowane.
{.is-info}

* Po wybiciu aktywa zobaczysz nowy wpis na stronie „Aktywa”.

## Szczegóły aktywa

Użytkownik może sprawdzić szczegóły aktywa, w tym wszystkie dane aktywa zapisane wraz z tym aktywem. Aby sprawdzić szczegóły aktywa, na stronie Aktywa kliknij aktywo, co spowoduje otwarcie strony. Szczegóły aktywa.&#x20;

![](<../../.gitbook/assets/Szczegóły zasobu.png>)

### Historia aktywa

Użytkownik może sprawdzić historię aktywa, historia obejmuje tworzenie, aktualizację, transfer, roszczenie i tokenizację. Aby sprawdzić historię aktywa, na stronie Aktywa kliknij „Aktywo”, co spowoduje otwarcie Szczegółów aktywa. W lewym dolnym rogu tej strony kliknij „Wyświetl historię”. Spowoduje to otwarcie strony historii, która zawiera listę wszystkich zmian, które miały miejsce w przypadku tego aktywa. &#x20;

![](<../../.gitbook/assets/Historia zasobów.png>)

### Przenieś aktywo

Właściciel aktywa może sprzedać aktywo i w tym celu musi przenieść własność aktywa na kupującego.

* Aby przenieść własność aktywa, kliknij to aktywo, co spowoduje otwarcie strony „Szczegóły aktywa”.
* W prawym dolnym rogu strony kliknij „Przenieś własność”. Spowoduje to otwarcie strony „Przenieś aktywo”.

![Przenieś stronę aktywa](<../../.gitbook/assets/Transfer Asset.png>)

* Na tej stronie potwierdź nazwę aktywa, adres aktywa i w polu „Przenieś do” wprowadź nazwę użytkownika lub identyfikator użytkownika kupującego.
* Aby potwierdzić, na dole strony kliknij „Przenieś aktywo”, co spowoduje przeniesienie aktywa do kupującego.

>Kupujący automatycznie odbierze aktywo za pośrednictwem interfejsu. Odbiór będzie obciążony opłatą w wysokości 1 NXS, co spowoduje utworzenie lokalnej nazwy tego aktywa w odbiornikach Sigchain.
{.is-info}