---
title: Zaawansowane kontrakty
description: 
published: true
date: 2022-12-20T22:51:18.796Z
tags: 
editor: markdown
dateCreated: 2022-10-22T20:24:35.056Z
---

# 馃搩 Zaawansowane kontrakty
Maszyna wirtualna Nexusa (NVM) to **`maszyna stan贸w`** i istnieje jako pojedyncza jednostka obs艂ugiwana przez setki po艂膮czonych w臋z艂贸w Nexusa.

Stos oprogramowania Nexusa istnieje wy艂膮cznie w celu utrzymania nieprzerwanego, nieprzerwanego i niezmiennego dzia艂ania tej specjalnej maszyny stan贸w. To 艣rodowisko, w kt贸rym dzia艂aj膮 wszystkie konta Nexus i umowy zaawansowane. W dowolnym punkcie 艂a艅cucha Nexus ma jeden i tylko jeden stan **`kanoniczny`**, a NVM definiuje zasady obliczania nowego wa偶nego stanu od bloku do bloku.

Mimo 偶e wszystkie platformy inteligentnych kontrakt贸w s膮 maszynami stanowymi, obsesja na punkcie skalowalno艣ci do u偶ytku w 艣wiecie rzeczywistym doprowadzi艂a do powstania odr臋bnej architektury NVM. Aby 艂atwo odr贸偶ni膰 lepsz膮 architektur臋, konieczne by艂o nazwanie kontrakt贸w na Nexusie kontraktami zaawansowanymi. Poni偶ej rozwik艂amy architektur臋.

## Architektura NVM

NVM jest zaprojektowany jako `64-bitowy`, `oparty na rejestrze`. Ten projekt zosta艂 wybrany, poniewa偶 pasuje do 64-bitowego procesora i na艣laduje rejestry pami臋ci podr臋cznej procesora.

Taka konstrukcja sprawia, 偶e 鈥嬧?婲VM jest bardzo szybki w por贸wnaniu do EVM, poniewa偶 zosta艂 zaprojektowany dla wsp贸艂czesnych procesor贸w. M贸wi膮c w liczbach, EVM zajmuje 1,7 miliona nanosekund na instrukcj臋, a NVM zajmuje 33 nanosekundy na instrukcj臋. EVM ma ogromn膮 wad臋, poniewa偶 uko艅czenie instrukcji zajmuje 4 cykle ze wzgl臋du na d艂ugo艣膰 256 bit贸w na 64-bitowym procesorze, a tak偶e na przestarza艂y projekt stosu.

NVM zosta艂 celowo zaprojektowany tak, aby nie by艂 kompletny, decyzja ta wynika r贸wnie偶 z faktu, 偶e Nexus jest silnikiem **`Weryfikacji`**. Ten projekt ma ogromn膮 zalet臋 i polega na darmowych prostych transakcjach, podczas gdy EVM potrzebuje gazu do kontrolowania 偶膮da艅 obliczeniowych z powodu z艂ego kodu umowy, kt贸ry mo偶e spowodowa膰 zatrzymanie sieci. Dzi臋ki projektowi NVM zaawansowane kontrakty b臋d膮 mia艂y przewidywalne op艂aty, kt贸re zostan膮 obliczone przed wykonaniem kontraktu.

Nexus b臋dzie mia艂 r贸偶ne rodzaje kontrakt贸w, dla interfejs贸w API wy偶szego poziomu zostan膮 dostarczone szablony, kt贸re u偶ytkownik mo偶e wybra膰 z listy rozwijanej. W przypadku zaawansowanych u偶ytkownik贸w umowy rozszerzone umo偶liwi膮 im korzystanie z um贸w z wyborem j臋zyka specyficznego dla domeny. Rozszerzone kontrakty b臋d膮 dost臋pne w p贸藕niejszym terminie. Aby uzyska膰 wi臋cej informacji, zapoznaj si臋 z [map膮 drogow膮](https://nexus.io/roadmap).

## Operacje i warstwy rejestru

W du偶ym uproszczeniu kontrakty to 偶膮danie wykonania okre艣lonego typu dyspozycji na danych, kt贸re skutkuje zmian膮 danych. W stosie oprogramowania Nexus `Warstwa operacji` zawiera instrukcje lub akcje, kt贸re nadaj膮 kontekst rejestrom i definiuj膮 bardziej z艂o偶on膮 logik臋 kontraktow膮, a `Warstwa rejestru` to warstwa danych. Kontrakt to obiekt zawieraj膮cy: stan wst臋pny rejestru (rejestr, na kt贸rym jest wykonywana operacja, kt贸ry zosta艂 przekazany w g贸r臋 z warstwy rejestru), operacj臋 pierwotn膮 (tylko jedna operacja pierwotna na kontrakt) oraz zestaw warunk贸w (dowolna ilo艣膰 operacji warunkowych).

### Prymitywne operacje

Bie偶膮ca iteracja warstwy operacyjnej zawiera 16 operacji pierwotnych oraz 54 operacje i typy warunkowe. Operacje prymitywne mo偶na najlepiej opisa膰 jako czynno艣ci zachodz膮ce na rejestrze takie jak: ZAPIS, DEBET, PRZELEW, DO艁膭CZ itp. Same te czynno艣ci powoduj膮, 偶e rejestr zmienia w jaki艣 spos贸b lub form臋 sw贸j stan, w tym jego przemieszczenie z jednego podpisu 艂a艅cuch do innego.

### Kontrakty warunkowe

Kontrakty warunkowe to umowy mi臋dzy uczestnicz膮cymi stronami, okre艣laj膮ce zestaw wymaga艅, kt贸re musz膮 zosta膰 spe艂nione, aby transakcja zosta艂a zako艅czona. S膮 to elementy, kt贸re pozwalaj膮 u偶ytkownikom na wzajemn膮 interakcj臋, tak膮 jak wyga艣ni臋cie umowy lub wymiana przedmiot贸w. Mo偶liwe s膮 r贸wnie偶 bardziej zaawansowane formy depozytu bezpowierniczego lub arbitra偶u. Instrukcje warunkowe nie maj膮 ogranicze艅 co do ich z艂o偶ono艣ci, poniewa偶 s膮 w stanie obs艂ugiwa膰 grupy grup warunk贸w, kt贸re razem daj膮 prawd臋 lub fa艂sz. W przypadku, gdy warunki wr贸c膮 jako prawdziwe, pozwala to odbiorcy transakcji za偶膮da膰 swoich 艣rodk贸w lub przedmiotu (w zale偶no艣ci od tego, czy by艂 to PRZELEW czy DEBET). W przypadku, gdy odbiorca nie jest w stanie spe艂ni膰 warunk贸w, po okre艣lonym przez nadawc臋 terminie transakcja b臋dzie mo偶liwa do zrealizowania.


> Wi臋cej informacji zostanie podanych w przysz艂o艣ci po wydaniu nowych aktualizacji.
{.is-info}


## Warstwa API

Warstwa API ekstrapoluje z um贸w (rejestr贸w i warstw operacyjnych). Deweloperzy mog膮 z 艂atwo艣ci膮 korzysta膰 z API, zamiast kodowa膰 `inteligentny kontrakt`. Mimo 偶e warstwa interfejsu API nie jest warstw膮 kontraktu, u偶ywa tych samych warstw kontraktu, do kt贸rych mo偶na uzyska膰 bezpo艣redni dost臋p za pomoc膮 j臋zyk贸w specyficznych dla domeny (DSL), do tworzenia niestandardowych kontrakt贸w. Podkre艣la to genialn膮 architektur臋 stosu oprogramowania, poniewa偶 te same umowy mog膮 by膰 udost臋pniane programistom bez kodu, programistom internetowym lub integracji z istniej膮cymi aplikacjami, jednocze艣nie abstrahuj膮c je od z艂o偶ono艣ci kodu lub 艂a艅cucha blok贸w.

# Kontrakty na Nexusie

Nexus opracowa艂 wielop艂aszczyznowe podej艣cie do rozwoju na Nexusie. Daje to ka偶demu mo偶liwo艣膰 budowania i integracji prawdziwie zdecentralizowanych rozwi膮za艅. Poni偶ej podano szczeg贸艂y r贸偶nych um贸w dotycz膮cych Nexusa

## Zapytanie DSL

Query DSL to jeden z j臋zyk贸w kontraktowych, kt贸ry dodaje mo偶liwo艣ci podobne do zapyta艅 SQL, w tym wyszukiwanie z u偶yciem symboli wieloznacznych i operatory logiczne, umo偶liwiaj膮ce wyszukiwanie lub filtrowanie dowolnych zasob贸w cyfrowych lub token贸w w Nexusie bezpo艣rednio przez interfejs API. Na przyk艂ad mo偶na wyszuka膰 tytu艂y w艂asno艣ci w Arizonie. Ta funkcja stanowi podstaw臋 zdecentralizowanej wyszukiwarki.

Query DSL umo偶liwia wyszukiwanie dowolnego aspektu 艂a艅cucha, mo偶na r贸wnie偶 filtrowa膰, a nawet operowa膰 na 偶膮danym zestawie danych. Obs艂ugiwane operatory to: `min, max, mean, mode, sum, floor, array, sdev, median`. Wi臋cej operator贸w b臋dzie dost臋pnych w p贸藕niejszym terminie.

Query zasadniczo udost臋pnia funkcjonalno艣膰 SQL w zestawie danych blockchain. Operatorzy sprawiaj膮, 偶e ma on mi臋dzy innymi funkcjonalno艣膰 Excela. To naprawd臋 pot臋偶ne narz臋dzie dla programist贸w. Mo偶e nawet przeszuka膰 ca艂y 艂a艅cuch:

```
register/list/names where='object.name=l*' 
```

Powy偶ej poka偶e si臋 ka偶da nazwa, kt贸ra zaczyna si臋 na liter臋 `l`. Nast臋pnie mo偶e uruchamia膰 na tym operatory, odfiltrowuj膮c pola:

````
register/list/names/name/array where='object.name=l*'
````

Da to ten sam zestaw danych, ale da tablic臋 JSON z nazwami zaczynaj膮cymi si臋 od `l`, bez innych p贸l. Obs艂uguje r贸wnie偶 wiele filtr贸w:

````
register/list/names/name,owner where='object.name=l*'
````

Spowoduje to odpowied藕 z polami nazwy i w艂a艣ciciela, podobnie jak w zapytaniu SQL, w kt贸rym wybierasz nazw臋 Z nazw. Daje wi臋c programi艣cie mo偶liwo艣ci modelowania danych opr贸cz funkcjonalno艣ci blockchain.

Globalne wyszukiwanie ca艂ego 艂a艅cucha zajmuje od 1 do 2 sekund. Uruchamianie pierwszego polecenia rejestru, kt贸re otrzymuj臋:

`[Completed in 1862.234494 ms]`

Aby uzyska膰 wi臋cej informacji, sprawd藕 poni偶szy link:

- [Zapytania *Zapytanie sk艂adni przypominaj膮ce SQL DSL*](/pl/tritium++/queries)
- [API rejestru *API rejestru*](/pl/tritium++/register)
{.links-list}

## Kontrakty warunkowe

Kontrakty warunkowe to binarne szablony kontrakt贸w, u偶ytkownicy b臋d膮 mogli wybra膰 standard kontraktu do wys艂ania. Doprowadzi to do dynamicznej alokacji standard贸w kontraktowych i standard贸w obiekt贸w na zestaw polece艅. Standaryzacja, w ramach kt贸rej mo偶emy alokowa膰 nowe kontrakty, kt贸re automatycznie zape艂ni膮 si臋 na listach standard贸w, bez konieczno艣ci aktualizacji portfela.

Oznacza to, 偶e b臋dziemy mogli wdra偶a膰 nowe standardy kontraktowe bez konieczno艣ci wypuszczania nowego portfela. Odczyta publiczny 艂a艅cuch znak贸w, kt贸ry rejestruje standardy um贸w i obiekt贸w. Doprowadzi to r贸wnie偶 do dynamicznych sta艂ych, takich jak op艂aty, dzi臋ki czemu b臋dziemy mogli dostosowa膰 krytyczne warto艣ci konsensusu bez potrzeby stosowania hard fork贸w lub aktualizacji podstawowego demona.

Gdy u偶ytkownik wysy艂a 艣rodki za pomoc膮 interfejsu Nexus, otrzymuje dodatkowe menu, kt贸re pozwala wybra膰 z listy standardowych szablon贸w um贸w do wys艂ania. To du偶y krok w kierunku wykorzystania inteligentnych kontrakt贸w w 艣wiecie rzeczywistym.

## Umowy warunkowe DSL (przysz艂o艣膰)

Kontrakty warunkowe DSL, nowy standard do napisania w j臋zyku wy偶szego poziomu i skompilowania do kodu bajtowego. Przeznaczony dla u偶ytkownik贸w, kt贸rzy b臋d膮 opracowywa膰 nowe standardy API lub kontraktowe. Umo偶liwia zapisywanie kontrakt贸w warunkowych bezpo艣rednio do API przy u偶yciu j臋zyka angielskiego, co jest kluczowym krokiem w realizacji pe艂nego potencja艂u funkcjonalno艣ci kontrakt贸w Tritium. Takie podej艣cie pozwala r贸wnie偶 ludziom czyta膰 lub interpretowa膰 umowy. Ujawni to programistom wiele nowych funkcji.

Dotychczas utrzymywali艣my standardowe kontrakty jako sta艂e osadzone w bazie kodu. Zdolno艣膰 programist贸w do kodowania nowych kontrakt贸w daje mo偶liwo艣膰 dynamicznej standaryzacji przy u偶yciu Nexusa do zarz膮dzania tym stanem, podobnie jak w przypadku dynamicznego modelowania obiektowego.


## Rozszerzone kontrakty (mapa drogowa: 2023-2025)

Dla zaawansowanych programist贸w, kt贸rzy potrzebuj膮 pe艂nej kontroli nad kreatywno艣ci膮, opracowali艣my rozszerzone kontakty, kt贸re mog膮 by膰 u偶ywane z dowolnym wybranym j臋zykiem domeny. Dzi艣 mamy Umowy Warunkowe, Operatory Prymitywne i Rejestry.

Warunkowa maszyna wirtualna b臋dzie podzbiorem Augmented, tak jak w mojej funkcji mam instrukcj臋 `if`, kt贸ra jest wykonywana jako warunek. Ale rozszerzony pozwoli na pisanie skomplikowanego kodu. Na przyk艂ad mam konto, wykonuj臋 funkcj臋 przeci膮偶enia operatora dla `DEBIT`, kt贸ra mo偶e doda膰 dodatkowe wymagania dla debetu z tego konta, takie jak maksymalna kwota na przedzia艂 czasu itp. M贸g艂bym doda膰 inn膮 publiczn膮 metod臋, kt贸ra mo偶e by膰 wywo艂ana przez innego u偶ytkownika do pobrania kwoty na moje konto, je艣li spe艂ni okre艣lony warunek, i tak dalej. B臋dzie to pe艂na implementacja naszego interpretera, w kt贸rej b臋dziemy mieli funkcjonalno艣膰 wi臋kszo艣ci j臋zyk贸w, takich jak Java i C++.

Rozszerzone kontrakty to drugi rodzaj kontrakt贸w, kt贸re b臋d膮 dost臋pne w Protokole Trytowym. Tego typu umowy rozszerzaj膮 Warunkow膮 VM (maszyn臋 wirtualn膮, kt贸ra przetwarza instrukcje warunkowe), zapewniaj膮c dodatkowe korzy艣ci, w tym mi臋dzy innymi metody, funkcje, przeci膮偶anie operacji i hermetyzacj臋. Rozszerzone umowy dodaj膮 warstw臋 z艂o偶ono艣ci i przetwarzania, wi臋c wi膮偶膮 si臋 z wy偶sz膮 op艂at膮 za wykonanie. B臋dzie to wymaga艂o wi臋cej przetwarzania w 艂a艅cuchu, ale og贸lnie sprawi, 偶e nasz silnik kontrakt贸w b臋dzie znacznie pot臋偶niejszy.

Celem kontrakt贸w rozszerzonych jest zapewnienie wzgl臋dnych mo偶liwo艣ci z艂o偶onych j臋zyk贸w, takich jak C++, wi臋c b臋dziemy obs艂ugiwa膰 polimorfizm, przeci膮偶anie operator贸w, funkcje, metody, publiczne, prywatne, chronione, unikalne itp. rozszerzone kontrakty opieraj膮 si臋 na istniej膮cej maszynie wirtualnej i rejestrze architektura oparta. Bardziej programowalne j臋zyki i rzeczy takie jak mapy, wektory, funkcje itp. b臋d膮 dostarczane z rozszerzonymi umowami.

> Wi臋cej informacji zostanie podanych, gdy b臋d膮 dost臋pne.
{.is-info}