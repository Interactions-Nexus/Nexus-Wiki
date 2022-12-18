---
title: 3-Wymiarowy Łańcuch (przyszłość)
description: Rozwiązanie do skalowania 3DC dla Nexusa
published: true
date: 2022-12-18T23:37:34.809Z
tags: 
editor: markdown
dateCreated: 2022-10-22T21:38:06.925Z
---

# 3-Wymiarowy Łańcuch (przyszłość)

Łańcuch trójwymiarowy (3DC) ma na celu rozwiązanie „Trylematu Blockchain”. Przekształci księgę główną w wielowarstwowy system przetwarzania w celu bezpiecznego skalowania i wysokiego stopnia decentralizacji. Blockchain Trilemma to opinia, że tylko dwie z trzech cech, bezpieczeństwo, decentralizacja i skalowalność, są możliwe do osiągnięcia jednocześnie.

3DC łączy ze sobą prymitywy kryptograficzne w trójwymiarowy niezmienny obiekt (blok 3D) i ma trzy podstawowe wymiary: kanały reputacji (X), niezmienność lub autentyczność (Y) i czas (Z). Ta architektura jest wdrażana za pośrednictwem [platformy TAO](broken-reference).

## Skalowalność

Architektura starszych łańcuchów bloków jest porównywalna do jazdy samochodem po autostradzie jednopasmowej – wraz ze wzrostem liczby samochodów rośnie ruch. Nexus postrzega „skalowalność” jako wymóg, a nie funkcję. Dlatego projektujemy protokoły, które skalują się w miarę dołączania większej liczby węzłów do sieci, przetwarzając bez przeszkód nawet przy wzroście wymagań dotyczących zasobów.

Korzystając z „łańcuchów podpisów”, „agregacji” i „dzielenia obliczeniowego”, 3DC tworzy równoległe ścieżki przetwarzania transakcji w celu wytworzenia warstwy L1, warstwy podstawowej 3DC. Dane są następnie przechowywane między wieloma węzłami przy użyciu tego, co nazywamy „Data Sharding”, co eliminuje potrzebę synchronizacji i przechowywania całego łańcucha bloków. [LISP](broken-reference) (Location Identifier Separation Protocol) i 'LLL' (biblioteka niższego poziomu) razem tworzą wspólny interfejs, który skutkuje zwiększeniem rozproszonego przechowywania danych, ponieważ więcej węzłów dołącza do sieci, zapewniając długoterminowy potencjał skalowania.

## Łańcuchy podpisów

Transakcje Nexus nie korzystają już z architektury UTXO (Unspent Tx Outputs), w której dane wyjściowe z jednej transakcji są danymi wejściowymi do drugiej, co skutkuje dużą liczbą kosztownych weryfikacji podpisów nawet w przypadku małych transakcji. Chociaż UTXO było ważnym kamieniem węgielnym architektury Bitcoin, okazało się, że jest przestarzałe i podatne na wiele różnych rodzajów ataków i ograniczeń skalowania.

Dlaczego warto tego unikać? [50% UTXO Litecoin jest niewydatkowe.](https://www.reddit.com/r/litecoin/comments/9ncqse/what\_should\_we\_do\_about\_the\_50\_of\_litecoins\_utxo/)

Odchodząc od starszej architektury łańcucha bloków, Nexus zaprojektował i wdrożył architekturę o nazwie Łańcuchy podpisów, która działa jak łańcuchy bloków osobistych użytkowników, zawierające wszystkie Twoje dane w jednym unikalnym łańcuchu. Ta architektura zapewnia wyższą charakterystykę skalowania, ponieważ tylko jeden podpis musi zostać zweryfikowany na transakcję. I odwrotnie, pojedyncza transakcja UTXO może zawierać 1000 danych wejściowych (a zatem wymagać 1000 weryfikacji podpisów), aby przeprowadzić transakcję nawet niewielką ilością monet (mniej niż 0,00001). Ponadto łańcuchy podpisów nie wymagają plików wallet.dat, ponieważ są one dostępne za pomocą danych logowania (nazwa użytkownika, hasło i kod PIN). Weryfikuje autentyczność i tożsamość osób korzystających z reputacji w sieci, bez poświęcania prywatności.

## Agregacja

Transakcje w starszych łańcuchach bloków są nie tylko przywoływane w bloku, ale są również z nim transportowane. Chociaż zawiera to pewne pozytywne cechy przetwarzania, ogranicza skalę, ponieważ transakcje wymagają transportu dwa razy, raz podczas tworzenia i ponownie, gdy sam blok jest emitowany. Aby zwalczyć tę nieefektywność, protokół Tritium przechowuje obiekt transakcji oddzielnie od obiektu bloku i odwołuje się do txid wewnątrz bloku. Jest to pierwsza forma 'agregacji', co oznacza, że pojedyncza referencja może reprezentować całą transakcję, zmniejszając w ten sposób dane przesyłane w blokach. Skutkuje to wyższymi poziomami skalowania i poprawą bezpieczeństwa poprzez zmniejszenie prawdopodobieństwa udanych ataków Finneya na sieć.

Co to jest atak Finneya? [Hal Finney odkrył to w 2011 r.](https://bitcointalk.org/index.php?topic=3441.msg48384#msg48384)

### Dzielenie obliczeniowe

Computational Sharding jest niezbędny do podziału pracy między określone typy węzłów, aby stworzyć 'pasy', które przetwarzają dane równolegle, porównywalnie do wielu pasów autostrady. Chociaż sharding obliczeniowy jest potężny, może być mniej bezpieczny, jeśli zostanie nieprawidłowo zaimplementowany. Powodem jest to, że 'shard' będzie łatwiejszy do zdominowania niż cała sieć, ponieważ jest mniejszy. Sposobem na rozwiązanie tego problemu jest użycie wielowarstwowej księgi (wyjaśnionej w sekcji Bezpieczeństwo) nieodłącznie związanej z 3DC. Warstwy konsensusu pozwalają, aby fragmenty poniżej były mniejsze niż te powyżej, chroniąc konflikty przed atakami.

### Dzielenie danych

Data Sharding to podział danych, które mają być przechowywane między wiele węzłów. Można to traktować jako posiadanie wielu magazynów do przechowywania paczek (danych) po ich przetworzeniu i transporcie. Ponieważ każdy obiekt jest 'weryfikowalny' za pomocą skrótu indeksu, 3DC może zapewnić dzielenie danych z ograniczonym zaufaniem do zdalnych węzłów.

Trudność polega na tym, jak zarządza się stanem tak wielu obiektów i shardów? Użycie [LISP](broken-reference) rozwiązuje ten problem. Metoda, za pomocą której 3DC wykonuje dzielenie danych, tworzona jest 'sieć', która istnieje wszędzie, gdzie zamiast adresów 'IP' masz 'hashe'. Można to porównać do wpisywania txid w przeglądarce internetowej i odbierania tej transakcji. Używając LISP w ten sposób, umożliwilibyśmy przeglądarce (lub LLP w kategoriach sieciowych) otwarcie połączenia z hashem, który wskazuje grupę węzłów przechowujących określony fragment danych.

Końcowym rezultatem jest to, że użytkownik może zalogować się do swojego węzła, który nigdy wcześniej nie komunikował się z siecią, wygenerować 'genesis-id' przy użyciu swoich poświadczeń i otworzyć połączenie z hashem, wykorzystując istniejący Internet do przekierowania do węzła który zawiera ten konkretny fragment danych. Piękno tego polega na tym, że sama sieć nie musi dodawać zbędnej synchronizacji danych między węzłami, aby wiedzieć, gdzie są przechowywane dane. Węzły używają nakładki do kierowania żądań węzłów zdalnych, w wyniku czego adresy IP są skrótami danych, które istnieją we wspaniałym świecie Nexusa.

Dzielenie danych na fragmenty jest niezbędnym aspektem 3DC w celu osiągnięcia długoterminowej skalowalności. Amine zapewni węzłom możliwość działania w 'trybie shard', zmniejszając zużycie dysku i pamięci nawet wtedy, gdy sieć jest obciążona. Fragmentacja danych w Obsidianie obejmie krytyczne funkcje sieciowe, co spowoduje, że węzły będą musiały przechowywać tylko część całego łańcucha.

## Multiemisja

Oprócz wyzwań związanych ze strukturą kryptograficzną opisanych w rozdziale Data Sharing, Internet musi mieć możliwość wydajnego routingu. Wykorzystujemy tak zwaną 'IP Multicast', która umożliwia zainicjowanie pojedynczej emisji wiadomości przez węzeł, zamiast konieczności replikowania wiadomości przez każdy węzeł podczas jej weryfikacji. Można to porównać do mówcy publicznego, który transmituje wiadomość do publiczności (multicast), zamiast prowadzić rozmowę jeden na jednego (emisja pojedyncza), w której wiadomość jest następnie plotkowana od jednej osoby do drugiej. Możesz sobie wyobrazić, jak poprawiłoby to nie tylko skalowalność, ale także integralność wiadomości (ponieważ plotki często nie odzwierciedlają oryginalnej rozmowy). Pakiety i transakcje będą kierowane w stałym czasie, bez względu na to, ile węzłów jest częścią systemu.

## Biblioteka niższego poziomu (LLL)

Biblioteka niższego poziomu (LLL) jest podstawą struktury TAO, umożliwiając obsługę innych technologii sieciowych z wysoką niezawodnością, wydajnością i rozszerzalnością. LLL to wysokowydajna 'biblioteka szablonów' zaprojektowana z myślą o zasilaniu powstających technologii internetowych. Większość dzisiejszych technologii internetowych jest niezgrabna, scentralizowana i przekombinowana w wyniku dziesięcioleci rozwoju. LLL jest prosty, wydajny i lekki; wykonane z myślą o modułowości.

Zawiera trzy główne komponenty: kryptografię (LLC), bazę danych (LLD) i protokół (LLP). Komponent Cryptography zawiera kryptografię [Quantum Resistant](broken-reference), komponent Database przewyższa Google LevelDB o rzędy wielkości, a komponent Protocol obsługuje znacznie ponad 450 000 żądań na sekundę.

Baza danych niższego poziomu (LLD) to szybki i modułowy silnik pamięci masowej Nexusa, który według naszej najlepszej wiedzy jest w stanie przewyższyć wydajność większości istniejących wbudowanych silników baz danych. Nasze średnie wyniki wynoszą około 0,33 sekundy dla 100 000 zapisów i odczytów na dysk (jeden, a potem drugi). To rywalizuje z innymi silnikami pamięci masowej, takimi jak LevelDB Google.

Protokół niższego poziomu (LLP) jest podstawowym składnikiem warstwy sieciowej, lekkim i szybkim protokołem, który umożliwia programistom dostosowanie projektu pakietu i interpretacji komunikatów. Zyskuje skalowalność dzięki prostocie i jest w stanie zarządzać dużą liczbą jednoczesnych połączeń.

Kryptografia niższego poziomu (LLC) to lekka i wydajna biblioteka zawierająca wiele przydatnych funkcji kryptograficznych, takich jak kryptografia postkwantowa, AES i Argon2. Biblioteka zapewnia łatwo dostępny zestaw wysokowydajnych funkcji kryptograficznych zapewniających maksymalny potencjał skalowalności. Przykładem mogą być nasze testy porównawcze FALCON (używane w TAO), które zweryfikowały 150 000 podpisów na konsumenckim laptopie Apple, gdzie ECDSA (algorytm podpisu cyfrowego krzywej eliptycznej; używany w Bitcoin, Ethereum itp.) wykonał tylko 4 000 podpisów.

## Bezpieczeństwo

Nexus wykorzystuje wiele systemów konsensusu, które wzajemnie się „sprawdzają i równoważą”. Różnorodność wzmacnia pulę genową gatunku ludzkiego, podobnie jak jest równie ważną właściwością dla bezpieczeństwa systemu zdecentralizowanego. 3DC zaprojektowano jako wiele warstw przetwarzania transakcji lub „konsensusu”, a każda z t