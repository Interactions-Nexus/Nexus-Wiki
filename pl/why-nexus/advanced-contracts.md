---
title: Zaawansowane kontrakty
description: 
published: true
date: 2022-10-29T09:36:44.005Z
tags: 
editor: markdown
dateCreated: 2022-10-22T20:24:35.056Z
---

# 📃 Zaawansowane kontrakty
Maszyna wirtualna Nexusa (NVM) to **`maszyna stanów`** i istnieje jako pojedyncza jednostka obsługiwana przez setki połączonych węzłów Nexusa.

Stos oprogramowania Nexusa istnieje wyłącznie w celu utrzymania nieprzerwanego, nieprzerwanego i niezmiennego działania tej specjalnej maszyny stanów. To środowisko, w którym działają wszystkie konta Nexus i umowy zaawansowane. W dowolnym punkcie łańcucha Nexus ma jeden i tylko jeden stan **`kanoniczny`**, a NVM definiuje zasady obliczania nowego ważnego stanu od bloku do bloku.

Mimo że wszystkie platformy inteligentnych kontraktów są maszynami stanowymi, obsesja na punkcie skalowalności do użytku w świecie rzeczywistym doprowadziła do powstania odrębnej architektury NVM. Aby łatwo odróżnić lepszą architekturę, konieczne było nazwanie kontraktów na Nexusie kontraktami zaawansowanymi. Poniżej rozwikłamy architekturę.

## Architektura NVM

NVM jest zaprojektowany jako „`64-bitowy”`, „`oparty na rejestrze”`. Ten projekt został wybrany, ponieważ pasuje do 64-bitowego procesora i naśladuje rejestry pamięci podręcznej procesora.

Taka konstrukcja sprawia, że ​​NVM jest bardzo szybki w porównaniu do EVM, ponieważ został zaprojektowany dla współczesnych procesorów. Mówiąc w liczbach, EVM zajmuje 1,7 miliona nanosekund na instrukcję, a NVM zajmuje 33 nanosekundy na instrukcję. EVM ma ogromną wadę, ponieważ ukończenie instrukcji zajmuje 4 cykle ze względu na długość 256 bitów na 64-bitowym procesorze, a także na przestarzały projekt stosu.

NVM został celowo zaprojektowany tak, aby nie był kompletny, decyzja ta wynika również z faktu, że Nexus jest silnikiem **`Weryfikacji`**. Ten projekt ma ogromną zaletę i polega na darmowych prostych transakcjach, podczas gdy EVM potrzebuje gazu do kontrolowania żądań obliczeniowych z powodu złego kodu umowy, który może spowodować zatrzymanie sieci. Dzięki projektowi NVM zaawansowane kontrakty będą miały przewidywalne opłaty, które zostaną obliczone przed wykonaniem kontraktu.

Nexus będzie miał różne rodzaje kontraktów, dla interfejsów API wyższego poziomu zostaną dostarczone szablony, które użytkownik może wybrać z listy rozwijanej. W przypadku zaawansowanych użytkowników umowy rozszerzone umożliwią im korzystanie z umów z wyborem języka specyficznego dla domeny. Rozszerzone kontrakty będą dostępne w późniejszym terminie. Aby uzyskać więcej informacji, zapoznaj się z [mapą drogową](https://nexus.io/roadmap).

## Operacje i warstwy rejestru

W dużym uproszczeniu kontrakty to żądanie wykonania określonego typu dyspozycji na danych, które skutkuje zmianą danych. W stosie oprogramowania Nexus `Warstwa operacji` zawiera instrukcje lub akcje, które nadają kontekst rejestrom i definiują bardziej złożoną logikę kontraktową, a `Warstwa rejestru` to warstwa danych. Kontrakt to obiekt zawierający: stan wstępny rejestru (rejestr, na którym jest wykonywana operacja, który został przekazany w górę z warstwy rejestru), operację pierwotną (tylko jedna operacja pierwotna na kontrakt) oraz zestaw warunków (dowolna ilość operacji warunkowych).

### Prymitywne operacje

Bieżąca iteracja warstwy operacyjnej zawiera 16 operacji pierwotnych oraz 54 operacje i typy warunkowe. Operacje prymitywne można najlepiej opisać jako czynności zachodzące na rejestrze takie jak: ZAPIS, DEBET, PRZELEW, DOŁĄCZ itp. Same te czynności powodują, że rejestr zmienia w jakiś sposób lub formę swój stan, w tym jego przemieszczenie z jednego podpisu łańcuch do innego.

### Kontrakty warunkowe

Kontrakty warunkowe to umowy między uczestniczącymi stronami, określające zestaw wymagań, które muszą zostać spełnione, aby transakcja została zakończona. Są to elementy, które pozwalają użytkownikom na wzajemną interakcję, taką jak wygaśnięcie umowy lub wymiana przedmiotów. Możliwe są również bardziej zaawansowane formy depozytu bezpowierniczego lub arbitrażu. Instrukcje warunkowe nie mają ograniczeń co do ich złożoności, ponieważ są w stanie obsługiwać grupy grup warunków, które razem dają prawdę lub fałsz. W przypadku, gdy warunki wrócą jako prawdziwe, pozwala to odbiorcy transakcji zażądać swoich środków lub przedmiotu (w zależności od tego, czy był to PRZELEW czy DEBET). W przypadku, gdy odbiorca nie jest w stanie spełnić warunków, po określonym przez nadawcę terminie transakcja będzie możliwa do zrealizowania.


> Więcej informacji zostanie podanych w przyszłości po wydaniu nowych aktualizacji.
{.is-info}


## Warstwa API

Warstwa API ekstrapoluje z umów (rejestrów i warstw operacyjnych). Deweloperzy mogą z łatwością korzystać z API, zamiast kodować `inteligentny kontrakt`. Mimo że warstwa interfejsu API nie jest warstwą kontraktu, używa tych samych warstw kontraktu, do których można uzyskać bezpośredni dostęp za pomocą języków specyficznych dla domeny (DSL), do tworzenia niestandardowych kontraktów. Podkreśla to genialną architekturę stosu oprogramowania, ponieważ te same umowy mogą być udostępniane programistom bez kodu, programistom internetowym lub integracji z istniejącymi aplikacjami, jednocześnie abstrahując je od złożoności kodu lub łańcucha bloków.

# Kontrakty na Nexusie

Nexus opracował wielopłaszczyznowe podejście do rozwoju na Nexusie. Daje to każdemu możliwość budowania i integracji prawdziwie zdecentralizowanych rozwiązań. Poniżej podano szczegóły różnych umów dotyczących Nexusa

## Zapytanie DSL

Query DSL to jeden z języków kontraktowych, który dodaje możliwości podobne do zapytań SQL, w tym wyszukiwanie z użyciem symboli wieloznacznych i operatory logiczne, umożliwiające wyszukiwanie lub filtrowanie dowolnych zasobów cyfrowych lub tokenów w Nexusie bezpośrednio przez interfejs API. Na przykład można wyszukać tytuły własności w Arizonie. Ta funkcja stanowi podstawę zdecentralizowanej wyszukiwarki.

Query DSL umożliwia wyszukiwanie dowolnego aspektu łańcucha, można również filtrować, a nawet operować na żądanym zestawie danych. Obsługiwane operatory to: `min, max, mean, mode, sum, floor, array, sdev, median`. Więcej operatorów będzie dostępnych w późniejszym terminie.

Query zasadniczo udostępnia funkcjonalność SQL w zestawie danych blockchain. Operatorzy sprawiają, że ma on między innymi funkcjonalność Excela. To naprawdę potężne narzędzie dla programistów. Może nawet przeszukać cały łańcuch:

```
register/list/names where='object.name=l*' 
```

Powyżej pokaże się każda nazwa, która zaczyna się na literę `l`. Następnie może uruchamiać na tym operatory, odfiltrowując pola:

````
register/list/names/name/array where='object.name=l*'
````

Da to ten sam zestaw danych, ale da tablicę JSON z nazwami zaczynającymi się od `l`, bez innych pól. Obsługuje również wiele filtrów:

````
register/list/names/name,owner where='object.name=l*'
````

Spowoduje to odpowiedź z polami nazwy i właściciela, podobnie jak w zapytaniu SQL, w którym wybierasz nazwę Z nazw. Daje więc programiście możliwości modelowania danych oprócz funkcjonalności blockchain.

Globalne wyszukiwanie całego łańcucha zajmuje od 1 do 2 sekund. Uruchamianie pierwszego polecenia rejestru, które otrzymuję:

`[Ukończono w 1862,234494 ms]`

Aby uzyskać więcej informacji, sprawdź poniższy link:

- [Zapytania *Zapytanie składni przypominające SQL DSL*](/pl/tritium++/queries)
- [API rejestru *API rejestru*](/pl/tritium++/register)
{.links-list}

## Kontrakty warunkowe

Kontrakty warunkowe to binarne szablony kontraktów, użytkownicy będą mogli wybrać standard kontraktu do wysłania. Doprowadzi to do dynamicznej alokacji standardów kontraktowych i standardów obiektów na zestaw poleceń. Standaryzacja, w ramach której możemy alokować nowe kontrakty, które automatycznie zapełnią się na listach standardów, bez konieczności aktualizacji portfela.

Oznacza to, że będziemy mogli wdrażać nowe standardy kontraktowe bez konieczności wypuszczania nowego portfela. Odczyta publiczny łańcuch znaków, który rejestruje standardy umów i obiektów. Doprowadzi to również do dynamicznych stałych, takich jak opłaty, dzięki czemu będziemy mogli dostosować krytyczne wartości konsensusu bez potrzeby stosowania hard forków lub aktualizacji podstawowego demona.

Gdy użytkownik wysyła środki za pomocą interfejsu Nexus, otrzymuje dodatkowe menu, które pozwala wybrać z listy standardowych szablonów umów do wysłania. To duży krok w kierunku wykorzystania inteligentnych kontraktów w świecie rzeczywistym.

## Umowy warunkowe DSL (przyszłe)

Kontrakty warunkowe DSL, nowy standard do napisania w języku wyższego poziomu i skompilowania do kodu bajtowego. Przeznaczony dla użytkowników, którzy będą opracowywać nowe standardy API lub kontraktowe. Umożliwia zapisywanie kontraktów warunkowych bezpośrednio do API przy użyciu języka angielskiego, co jest kluczowym krokiem w realizacji pełnego potencjału funkcjonalności kontraktów Tritium. Takie podejście pozwala również ludziom czytać lub interpretować umowy. Ujawni to programistom wiele nowych funkcji.

Dotychczas utrzymywaliśmy standardowe kontrakty jako stałe osadzone w bazie kodu. Zdolność programistów do kodowania nowych kontraktów daje możliwość dynamicznej standaryzacji przy użyciu Nexusa do zarządzania tym stanem, podobnie jak w przypadku dynamicznego modelowania obiektowego.


## Rozszerzone kontrakty (mapa drogowa: 2023-2025)

Dla zaawansowanych programistów, którzy potrzebują pełnej kontroli nad kreatywnością, opracowaliśmy rozszerzone kontakty, które mogą być używane z dowolnym wybranym językiem domeny. Dziś mamy Umowy Warunkowe, Operatory Prymitywne i Rejestry.

Warunkowa maszyna wirtualna będzie podzbiorem Augmented, tak jak w mojej funkcji mam instrukcję `if`, która jest wykonywana jako warunek. Ale rozszerzony pozwoli na pisanie skomplikowanego kodu. Na przykład mam konto, wykonuję funkcję przeciążenia operatora dla `DEBIT`, która może dodać dodatkowe wymagania dla debetu z tego konta, takie jak maksymalna kwota na przedział czasu itp. Mógłbym dodać inną publiczną metodę, która może być wywołana przez innego użytkownika do pobrania kwoty na moje konto, jeśli spełni określony warunek, i tak dalej. Będzie to pełna implementacja naszego interpretera, w której będziemy mieli funkcjonalność większości języków, takich jak Java i C++.

Rozszerzone kontrakty to drugi rodzaj kontraktów, które będą dostępne w Protokole Trytowym. Tego typu umowy rozszerzają Warunkową VM (maszynę wirtualną, która przetwarza instrukcje warunkowe), zapewniając dodatkowe korzyści, w tym między innymi metody, funkcje, przeciążanie operacji i hermetyzację. Rozszerzone umowy dodają warstwę złożoności i przetwarzania, więc wiążą się z wyższą opłatą za wykonanie. Będzie to wymagało więcej przetwarzania w łańcuchu, ale ogólnie sprawi, że nasz silnik kontraktów będzie znacznie potężniejszy.

Celem kontraktów rozszerzonych jest zapewnienie względnych możliwości złożonych języków, takich jak C++, więc będziemy obsługiwać polimorfizm, przeciążanie operatorów, funkcje, metody, publiczne, prywatne, chronione, unikalne itp. rozszerzone kontrakty opierają się na istniejącej maszynie wirtualnej i rejestrze architektura oparta. Bardziej programowalne języki i rzeczy takie jak mapy, wektory, funkcje itp. będą dostarczane z rozszerzonymi umowami.

> Więcej informacji zostanie podanych, gdy będą dostępne.
{.is-info}