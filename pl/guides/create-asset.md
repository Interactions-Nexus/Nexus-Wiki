---
title: Utwórz Aktywo
description: Utwórz Aktywo za pomocą interfejsu
published: true
date: 2022-12-05T23:34:11.833Z
tags: 
editor: markdown
dateCreated: 2022-10-22T21:48:53.360Z
---

# Utwórz Aktywo

Ten przewodnik pomoże użytkownikom utworzyć **zasób**, popularnie zwany także **NFT**, sprawdzić szczegóły zasobu i przenieść własność za pomocą interfejsu Nexus

Zanim zaczniemy tworzyć zasób, użytkownicy muszą zapoznać się z niektórymi koncepcjami i parametrami używanymi z zasobami.

>Tworzenie zasobu wiąże się z opłatą w wysokości 1 NXS, a „_Nazwa zasobu”_ wiąże się z opłatą w wysokości 1 NXS. Całkowity koszt zasobu o nazwie wyniesie 2 NXS
{.is-info}

## Parametry zasobów

### Nazwa zasobu

Jest to globalnie unikatowa nazwa zasobu. Duplikaty nazw nie będą dozwolone. Jeśli tworzysz grupę zasobów o podobnej nazwie, użyj numeru seryjnego z nazwą.

>Asset Name ma oddzielną opłatę w wysokości 1NXS. Użytkownicy mogą zrezygnować z tworzenia nazwy zasobu i mogą korzystać z adresu rejestracyjnego, aby uzyskać dostęp do zasobu lub go przeszukiwać.
{.is-info}


Konwencja nazewnictwa:
* Użyj unikalnej nazwy, jeśli tworzysz zasób. Preferowane są krótkie nazwy, ale w razie potrzeby używaj długich nazw.
* Nazwy mogą zawierać wielkie i małe litery, cyfry i znaki specjalne.
* Jeśli tworzysz zasób z rzeczywistych zasobów, takich jak nieruchomości, podaj jasne i precyzyjne informacje dla nazwy zasobu&#x20;
* Jeśli tworzysz kilka Zasobów / NFT, na przykład z jednej kolekcji dzieł sztuki, dodaj do nazwy kolekcji unikalny numer seryjny serii Np.: „_Iron Maiden #0001”_

### Dane zasobów

Ta sekcja dotyczy danych lub metadanych zasobów. Podane tutaj informacje pomagają nadać ważność zasobowi i jego wartości. Dane o zasobach muszą być dokładne, kompletne i powinny umożliwiać każdemu sprawdzenie autentyczności zasobu, na którym się on znajduje. Dostarczone dane będą zależeć od zasobu cyfrowego lub fizycznego, który jest wspierany jako zasób blockchain. &#x20;

>Dane zasobów mają limit 1 KB i jest to wiążące. Zasób może zawierać około 990 - 995 znaków ze spacjami. Nie dotyczy to nazwy zasobu.
{.is-info}

Aby łatwo policzyć znaki dla danych Zasobu, użyj poniższego łącza:

{% embed url="https://wordcount.com" %}

>**Nota:** Jeśli tworzysz zasób dzieła sztuki cyfrowej, który zasadniczo jest plikiem graficznym, podaj skrót md5 oryginalnego obrazu, aby każdy mógł sprawdzić autentyczność tego konkretnego pliku. Jeśli wszystkie szczegóły zostaną podane bez skrótu pliku, zasób nie będzie użyteczny, ponieważ nikt nie będzie w stanie potwierdzić autentyczności pliku, który reprezentuje zasób.
{.is-warning}

Dane o zasobach są wprowadzane w polach, które na powyższym obrazku przedstawiają pojedynczą linię.&#x20;

#### Imię:&#x20;

Pierwsza kolumna to nazwa pola, która jest nazwą danych, które zamierzasz dodać, takich jak Opis, Właściciel, Artysta, Hash itp.

#### Wartość:&#x20;

Druga kolumna to wartość pola, na przykład nazwisko właściciela

#### Zmienny:

Trzeci to przycisk radiowy umożliwiający włączenie pola zmiennego (domyślnie jest wyłączone). Zmienne pola mogą być zmieniane w dowolnym momencie przez właściciela łańcucha znaków zasobu. Jest to bardzo pomocne w przypadku, gdy masz dom wybijany jako zasób, a kiedy sprzedasz dom, przekaż zasób nowemu właścicielowi, a on może zmienić pole „Właściciel” na swoje nazwisko.

> Zmieniaj tylko te pola, które naprawdę potrzebują. Np. Podczas tworzenia zasobu, który odnosi się do domu, pole „Właściciel” musi być zmienne, wynika to z lokalizacji, nazwy, numeru rejestracyjnego&#x20;
{.is-info}

#### Rodzaj:

String: Jest to typ danych używany do reprezentowania tekstu. Składa się z zestawu znaków, który może zawierać również spacje i cyfry. Na przykład słowo „hamburger” i wyrażenie „Zjadłem 3 hamburgery” to ciągi znaków. Nawet „12345” można uznać za ciąg znaków.

Typy dat uint8, uint16, uint32, uint64, uint128, uint256, uint512 i uint1024 reprezentują liczbę całkowitą bez znaku przechowywaną z 8, 16, 32 lub 64 bitami.&#x20;

| Wpisz | Liczba bitów | Min. - Maks. wartość |
| ---------- | :--------: | ------------------------------ |
| uint8 | 1 | 0 - 255 |
| jednostka16 | 2 | 0 - 65535 |
| uint32 | 4 | 0 - 4 294 967 295 |
| jednostka64 | 8 | 0 - 18 446 744 073 709 551 615 |
| jednostka256 | 16 | 0 - 2^256-1 |
| uint512 | 32 | 0 - 2^512-1 |
| uint1024 | 64 | 0 - 2^1024-1 |

**Maksymalna długość:**

To pole jest włączone tylko wtedy, gdy pole jest wybrane jako zmienne, a typ jako „ciąg”. Jest to ważne, ponieważ pozwoli to ograniczyć długość pola przy późniejszej zmianie i zmieścić Dane o zasobach w limicie 1 KB.

## Utwórz zasób

Aby utworzyć zasób za pomocą interfejsu, wykonaj poniższe czynności:

* Otwórz interfejs Nexus, upewnij się, że portfel jest w pełni zsynchronizowany. Zaloguj się na konto użytkownika (Sigchain).
* Na stronie Przegląd u dołu kliknij moduł „_User”_. Spowoduje to otwarcie strony użytkownika.
* Na stronie użytkownika po lewej stronie kliknij zakładkę „_Assets_”. Na stronie Zasoby zostaną wyświetlone zasoby należące do Sigchain.
* Na stronie Zasoby kliknij „Utwórz nowy zasób”. Spowoduje to otwarcie strony _Utwórz nowy zasób_.
* Na tej stronie użytkownik musi podać nazwę oraz dane definiujące zasób.&#x20;
   * **Dodaj kolejne pole:** Aby dodać kolejne pole, kliknij przycisk „+DODAJ POLE” pod pierwszym polem.
   * **Usuń pole:** Aby usunąć pole, umieść wskaźnik myszy na tym polu, po lewej stronie pola pojawi się ikona „x”, kliknij ją, aby usunąć pole.
* Po podaniu danych sprawdź, czy wszystko jest w porządku. Na dole możesz zobaczyć szacowany koszt wybicia tego zasobu. Kliknij przycisk „UTWÓRZ ZASOBY” na dole strony.

>Opłaty zostaną automatycznie pobrane z konta „domyślnego”, upewnij się, że masz NXS na pokrycie opłat, w przeciwnym razie aktywa nie zostaną wyemitowane.
{.is-info}

* Po wybiciu zasobu zobaczysz nowy wpis na stronie „Zasoby”.

## Szczegóły zasobu

Użytkownik może sprawdzić szczegóły zasobu, w tym wszystkie dane zasobu zapisane wraz z tym zasobem. Aby sprawdzić szczegóły zasobu, na stronie Zasoby kliknij zasób, co spowoduje otwarcie strony Szczegóły zasobu&#x20;

![](<../../.gitbook/assets/Szczegóły zasobu.png>)

### Historia zasobów

Użytkownik może sprawdzić historię zasobu, historia obejmuje tworzenie, aktualizację, transfer, roszczenie i tokenizację. Aby sprawdzić historię zasobu, na stronie Zasoby kliknij „Zasób”, co spowoduje otwarcie Szczegółów zasobu. W lewym dolnym rogu tej strony kliknij „Wyświetl historię”. Spowoduje to otwarcie strony historii, która zawiera listę wszystkich zmian, które miały miejsce w przypadku tego zasobu. &#x20;

![](<../../.gitbook/assets/Historia zasobów.png>)

### Przenieś zasób

Właściciel zasobu może sprzedać zasób iw tym celu musi przenieść własność zasobu na kupującego.

* Aby przenieść własność zasobu, kliknij ten zasób, co spowoduje otwarcie strony „Szczegóły zasobu”.
* W prawym dolnym rogu strony kliknij „Przenieś własność”. Spowoduje to otwarcie strony „Przenieś zasób”.

![Przenieś stronę zasobów](<../../.gitbook/assets/Transfer Asset.png>)

* Na tej stronie potwierdź nazwę zasobu, adres zasobu iw polu „Przenieś do” wprowadź nazwę użytkownika lub identyfikator użytkownika kupującego.
* Aby potwierdzić, na dole strony kliknij „Przenieś zasób”, co spowoduje przeniesienie zasobu do kupującego.

>Kupujący automatycznie odbierze zasób za pośrednictwem interfejsu. Odbiór będzie obciążony opłatą w wysokości 1 NXS, co spowoduje utworzenie lokalnej nazwy tego zasobu w odbiornikach Sigchain.
{.is-info}