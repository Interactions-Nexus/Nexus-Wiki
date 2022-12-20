---
title: Łańcuch 3-wymiarowy (przyszłość)
description: Rozwiązanie do skalowania 3DC dla Nexusa
published: true
date: 2022-12-20T12:08:45.525Z
tags: 
editor: markdown
dateCreated: 2022-10-22T21:38:06.925Z
---

# Łańcuch 3-wymiarowy (przyszłość)

Łańcuch trójwymiarowy (3DC) ma na celu rozwiązanie 'Trylematu Blockchain'. Przekształci księgę główną w wielowarstwowy system przetwarzania w celu bezpiecznego skalowania i wysokiego stopnia decentralizacji. Blockchain Trilemma to opinia, że tylko dwie z trzech cech, bezpieczeństwo, decentralizacja i skalowalność, są możliwe do osiągnięcia jednocześnie.

3DC łączy ze sobą prymitywy kryptograficzne w trójwymiarowy niezmienny obiekt (blok 3D) i ma trzy podstawowe wymiary: kanały reputacji (X), niezmienność lub autentyczność (Y) i czas (Z). Ta architektura jest wdrażana za pośrednictwem [platformy TAO](broken-reference).

## Skalowalność

Architektura starszych łańcuchów bloków jest porównywalna do jazdy samochodem po autostradzie jednopasmowej – wraz ze wzrostem liczby samochodów rośnie ruch. Nexus postrzega 'skalowalność' jako wymóg, a nie funkcję. Dlatego projektujemy protokoły, które skalują się w miarę dołączania większej liczby węzłów do sieci, przetwarzając bez przeszkód nawet przy wzroście wymagań dotyczących zasobów.

Korzystając z 'łańcuchów podpisów', 'agregacji' i 'dzielenia obliczeniowego', 3DC tworzy równoległe ścieżki przetwarzania transakcji w celu wytworzenia warstwy L1, warstwy podstawowej 3DC. Dane są następnie przechowywane między wieloma węzłami przy użyciu tego, co nazywamy „Data Sharding”, co eliminuje potrzebę synchronizacji i przechowywania całego łańcucha bloków. [LISP](broken-reference) (Location Identifier Separation Protocol) i 'LLL' (biblioteka niższego poziomu) razem tworzą wspólny interfejs, który skutkuje zwiększeniem rozproszonego przechowywania danych, ponieważ więcej węzłów dołącza do sieci, zapewniając długoterminowy potencjał skalowania.

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

Nexus wykorzystuje wiele systemów konsensusu, które wzajemnie się 'sprawdzają i równoważą'. Różnorodność wzmacnia pulę genową gatunku ludzkiego, podobnie jak jest równie ważną właściwością dla bezpieczeństwa systemu zdecentralizowanego. 3DC jest zaprojektowane jako wiele warstw przetwarzania transakcji lub 'konsensusu', a każda z warstw agreguje dane z warstwy poniżej. Węzły wykonujące pracę na L2 rozwiązują wszelkie konflikty we fragmentach L1, używając 'stawki' i 'zaufania' jako 'wagi' w celu ustalenia konsensusu. W przypadku wystąpienia konfliktu rozwiązuje się go poprzez ważność danych, która jest zdefiniowana jako (zaufanie + waga). Warstwa L3 skonsoliduje skróty z L2, aby utworzyć ostateczny blok 3D.

Nexus bardzo poważnie traktuje wykorzystanie kryptografii, ponieważ luka w tych funkcjach może zagrozić bezpieczeństwu całej sieci. Używamy tylko dobrze przetestowanej i dokładnie zweryfikowanej kryptografii, aby wspierać zwiększone poziomy odporności kwantowej.

## Zaufanie i waga

Zaufanie definiuje się jako całkowity czas, jaki dany użytkownik (łańcuch podpisów) wnosi do sieci. Ten czas jest mierzony przez spójność i dostępność węzła do sprawdzania poprawności danych transakcji.

Waga jest zdefiniowana jako wkład zasobów w czasie rzeczywistym, które dany węzeł zapewnił dla jednorazowego procesu transakcyjnego. Można to zmierzyć w cyklach obliczeniowych za pomocą Proof-of-Work (PoW) lub innych zasobów, takich jak 'stake', których zapewnienie wiąże się z kosztami.

## pBFT + kanały reputacji (L1)

Gdy transakcje są odbierane przez sieć, węzły natychmiast zaczynają je weryfikować. Szybkość transakcji w kanałach L1 będzie się różnić w zależności od ryzyka, jakie handlowiec chce przyjąć, od prędkości poniżej sekundy do pięciu sekund. W przypadku transakcji o wyższej wartości zaleca się, aby otrzymały dodatkową wagę z walidacji na następnej warstwie konsensusu: L2, zmniejszając szybkość transakcji do 15 sekund plus.

## pBFT + sieć zaufania PoS (L2)

Jako rozszerzenie istniejącego systemu Proof-of-Stake, L2 utworzy drugą warstwę konsensusu powyżej L1. Warstwa L2 zapewnia bezpieczeństwo i żywotność, komunikację między fragmentami i rozwiązuje konflikty z poziomu warstwy L1. Reprezentuje poziome łańcuchowanie kanałów L1 i jest ważnym krokiem w kierunku prawdziwie zdecentralizowanej i skalowalnej księgi głównej.

## Sprawdzanie i równoważenie

Aby mieć najwyższy stopień bezpieczeństwa, decyzje nie mogą być skoncentrowane w jednej formie, ponieważ stwarza to możliwość 'przymusu'. Jeśli istnieje tylko jedna forma kosztu zapewniająca bezpieczeństwo, system można łatwo zdominować ze względu na ograniczone 'sprawdzanie i równoważenie'. Bitcoin jest doskonałym przykładem ofiary, która cierpi z powodu dominacji zasobów lub 'centralizacji'.

Cztery organizacje kontrolują ponad 51% hashrate Bitcoina, co oznacza, że całe bezpieczeństwo Bitcoina zależy od nich i od decyzji, które podejmują. Ta sytuacja jest przykładem centralizacji wynikającej z dominacji zasobów, która doprowadziła do proponowanych rozwiązań, takich jak UASF (User Activated Soft Fork) i wielu forków Bitcoin, takich jak Bitcoin Cash, Bitcoin SV, Bitcoin Gold itp.

![uasf.png](/uasf.png)<p align="center" style ="color: blue;">*Węzły Bitcoin Sygnalizacja UASF - Segwit/ BIP148*</p>

Choć obiecujący, UASF nie był w stanie osiągnąć poziomu, na którym mógłby być skuteczny, ponieważ wymagany procent zgody górnika był zbyt wysoki.

## Decentralizacja

Wiele protokołów odeszło od PoW ze względu na duże zapotrzebowanie na energię. Niezwykle konkurencyjny charakter prowadzi również do zwiększania ilości zasobów w celu poszukiwania bloku, ponieważ tradycyjny model PoW nagradza tylko zwycięskiego górnika każdego bloku, zachęcając górników do łączenia zasobów.

Delegated Proof of Stake (DPoS), mechanizm konsensusu używany przez EOS, TRON, LISK i inne głównie w celu osiągnięcia ulepszeń skalowania, opiera się na ograniczonej liczbie wybranych producentów bloków i zapewnia niski stopień decentralizacji. Istnieje kilka rozwiązań, które zostały zaproponowane do skalowania łańcucha bloków: na przykład Segregated Witness Bitcoin w połączeniu z Lightning Network i Ethereum Plasma. Choć obiecujące, oba zasadniczo polegają na rozwiązaniach poza łańcuchem, aby zapewnić skalowanie (bardziej scentralizowane podejście). Tworzą kanały płatności lub 'łańcuchy boczne', które polegają na małej grupie weryfikatorów w celu ponownego zatwierdzania zaktualizowanych sald. Młodsze protokoły proponowały systemy wielowarstwowe, chociaż nie znamy żadnych projektów, które kładą taki sam nacisk na decentralizację jak 3DC.

3DC ma na celu osiągnięcie decentralizacji za pomocą wielu metod, które obejmują; Kanały reputacji L1, zdecentralizowane pule w warstwach L2 i L3, struktury zachęt do reputacji i odkrywanie partnerów.

## Kanały reputacji L1

Kanały reputacji L1 są zaprojektowane tak, aby wymagały niewielkiej ilości zasobów w porównaniu z warstwami L2 i L3. Ma to umożliwić korzystanie z mniejszych urządzeń mobilnych, co z kolei zapewni wyższy poziom decentralizacji. Jest to możliwe, ponieważ powyższa warstwa konsensusu L2 zwiększa wagę, aby zapewnić bezpieczeństwo kanałów poniżej. Reputacja jest ostatnim składnikiem, który 3DC wykorzystuje do utrzymania bezpieczeństwa przy jednoczesnym osiągnięciu wysokiego poziomu decentralizacji. Jest agregowany przez wszystkie trzy warstwy 3DC, aby określić ilościowo 'ważność' bloku 3D.

## Zdecentralizowane pule stakowania (L2)

Warstwa L2 jest rdzeniem 3DC, które zarządza agregacją danych i przetwarzaniem kontraktów. Ta warstwa otrzymuje również udziały od górników z warstwy L3 powyżej, w celu akumulacji ich pracy i zbiorowego nagradzania górników. Im więcej udziałów zostanie uwzględnionych z warstwy L3, tym większa będzie skumulowana waga i zaufanie dla danego bloku 3D. Dlatego 3DC zachęca walidatorów L2 do uwzględnienia jak największej liczby udziałów, aby ich blok 3D został zaakceptowany jako najbardziej ważny w łańcuchu 3D.

Warstwa L2 jest sterowana przez ważenie 'Proof-of-Stake', które identyfikuje wszystkie węzły w procesie konsensusu jako uczestników, a zatem zapewnia wyższy stopień decentralizacji w porównaniu z istniejącymi protokołami Proof-of-Stake (PoS). 3DC będzie wymagać niższego minimalnego salda do obstawiania niż obecny protokół PoS.

## Zdecentralizowane pule wydobywcze (L3)

Ta warstwa będzie wykorzystywać udziały wydobywcze oparte na PoW, obliczone na podstawie pracy wykonanej przez węzły warstwy L2. O konsensusie zadecyduje największa wartość udziałów + Zaufanie, w celu osiągnięcia ostatecznego porozumienia co do najistotniejszego bloku 3D.

Zamiast górników posiadających uprawnienia do określenia następnego bloku poprzez znalezienie zwycięskiego skrótu, wydobycie stanie się działaniem obejmującym całą grupę, tworząc warstwę L3 3DC. Górnicy, którzy przesyłają hasze do sieci, wykonują pracę, która blokuje łącza krzyżowe L2. Zapewnia to infrastrukturę dla bardziej zdecentralizowanego procesu konsensusu, a jednocześnie dziedziczy pozytywne właściwości, które oferuje górnictwo.

## Odkrywanie równorzędne

Łańcuchy bloków zazwyczaj polegają na zdolności węzłów do bezpośredniego łączenia się (peer-to-peer) w celu utrzymania zdecentralizowanej i równomiernie rozłożonej topologii. Węzły muszą być wykrywalne przez swoich rówieśników, ponieważ mogą akceptować żądania połączenia. Jest to rzadko osiągane i spowodowało, że Bitcoin ma tylko skromne 10% węzłów, które można wykryć.

Alternatywnie, Nexus używa nakładki [LISP](broken-reference) w celu przechodzenia przez 'NAT' (Network Address Translators) w celu utrzymania wyższego stopnia dostępności węzłów. LISP używa statycznych identyfikatorów punktów końcowych (EID), do których można dotrzeć nawet podczas roamingu między różnymi sieciami (WiFi, wieże komórkowe itp.). Daje to węzłom znacznie większą mobilność, umożliwiając ich lokalizację w dowolnym miejscu w Internecie, za NAT w środowiskach mieszkalnych, u dostawców usług w chmurze i za operatorami komórkowymi, a jednocześnie nadal można je wykryć.

## Struktura zachęt do reputacji

Reputacja jest ważnym wymogiem funkcjonowania zdecentralizowanych systemów, w celu stworzenia zdrowej globalnej sieci. Zaimplementujemy reputację na wszystkich trzech warstwach 3DC, jako drugorzędny składnik wagi, poprawiając ogólny pBFT. Równie ważna jest reputacja, która może poprawić decentralizację poprzez struktury motywacyjne ułatwione przez zmienne nagrody dla węzłów, które zdobyły wyższą reputację. Długoterminowi współtwórcy systemu mogą zyskać wyższą reputację, a co za tym idzie, wyższy zwrot z ich wkładu, co daje podstawy do długofalowego przekonania o Nexusie, że:

`Nie każdy ma pieniądze, ale każdy ma czas.`