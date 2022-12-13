---
title: Konsensus Nexusa
description: 
published: true
date: 2022-12-13T23:55:28.209Z
tags: 
editor: markdown
dateCreated: 2022-10-21T22:00:40.172Z
---

# Konsensus Nexusa
### Czym jest konsensus?

Blockchain lub rozproszona księga jest rozłożona na węzły, których zadaniem jest weryfikacja transakcji w sieci. Jest to jeden z kluczowych pomysłów na blockchain i nadaje mu unikalny zdecentralizowany smak.

W rezultacie każdy może przesłać informacje, które mają być przechowywane w łańcuchu bloków, dlatego ważne jest, aby istniały procesy, które zapewnią, że wszyscy zgodzą się, jakie informacje dodać, a co odrzucić. Zasady te są zasadniczo znane jako protokoły konsensusu. Weryfikują transakcje i pomagają chronić sieć.&#x20;

### Jak działają protokoły konsensusu?

Protokół konsensusu w sercu sieci blockchain zapewnia konkretną metodę weryfikacji, czy transakcja jest prawdziwa, czy nie. Zapewnia metodę przeglądania i potwierdzania, jakie dane należy dodać do rekordu łańcucha bloków. Ponieważ sieci blockchain zwykle nie mają scentralizowanego organu dyktującego, kto ma rację, a kto nie, wszystkie węzły w łańcuchu bloków muszą zgadzać się na stan sieci, zgodnie z predefiniowanymi regułami lub protokołem.

W przypadku Bitcoin protokołem konsensusu jest Proof-of-work (PoW), proces wyszukiwania bloków, który potwierdza każdą transakcję. Inne rodzaje protokołów konsensusu obejmują dowód stawki (PoS) i dowód uprawnień (PoA).

## Co robią protokoły konsensusu?

### **Zapobiegaj przejęciu kontroli przez jeden podmiot**

Jeśli sieć ma konsensus, wszystkie uczestniczące węzły zgadzają się co do stanu łańcucha bloków. W ten sposób dane są rejestrowane jako „prawda”, a blockchain jest w stanie funkcjonować z coraz większą ilością danych dodawanych w miarę zawierania transakcji lub wykonywania inteligentnych kontraktów.

Pozwala użytkownikom zdecentralizowanym ufać użytkownikom bez kontrolującej strony trzeciej.&#x20;

Protokół konsensusu uniemożliwia pojedynczemu podmiotowi kontrolowanie łańcucha bloków lub zniekształcanie „prawdy” tego, co powinno być rejestrowane.

Podwójne wydatki są przykładem tego, co mogłoby się zdarzyć, gdyby jeden podmiot próbował przejąć kontrolę nad całą siecią, tworząc własną wersję łańcucha bloków. Na przykład atakujący może wydać trochę bitcoinów, a następnie zmienić blok, który ma zostać zapisany w łańcuchu bloków, aby nie wyświetlał wydatków. Atakujący może rozgłaszać swoją wersję łańcucha bloków, pomniejszoną o rekord wydatków. Atakujący użyłby trochę bitcoinów, ale monety nie zostałyby zarejestrowane jako wydane w łańcuchu i mogłyby zostać ponownie wydane.

Protokół konsensusu Bitcoina, PoW, zapobiega temu, ponieważ kiedy ta wersja łańcucha bloków jest porównywana z innymi wersjami przechowywanymi na innych węzłach, będzie się nieco różnić od wszystkich innych, a ta wersja zostanie odrzucona przez inne węzły. &#x20;

### **Jakie są najczęstsze rodzaje protokołów konsensusu?**

**Proof-of-Work (PoW):** Pierwszy blockchain, Bitcoin, wykorzystuje PoW. Aby zweryfikować transakcje z „górnikami” łańcucha bloków Bitcoin, którzy są węzłami, rozwiązują problemy kryptograficzne lub matematyczne za pomocą swoich komputerów. Górnicy, którzy rozwiązują problem, zatwierdzają i włączają rekord blokowy, są nagradzani bitcoinami.

**Dowód stawki (PoS):**&#x20;

W PoS zamiast górników są „fałszerze”. Ci fałszerze stawiają pewną ilość kryptowaluty, która daje im szansę, w oparciu o prawdopodobieństwo, bycia walidatorem bloków. Zwycięski fałszerz otrzymuje w nagrodę odpowiednie opłaty za transakcję blokową. Stawianie własnej kryptowaluty na blok zniechęca fałszerza do próby oszukania sieci, ponieważ stracą stawkę, jeśli okaże się, że nieprawidłowo dodawał transakcje do sieci.

**Delegowany dowód stawki (DPoS):**

Ta metoda działa podobnie do PoS. Ale zamiast korzystać z prawdopodobieństwa, posiadacze kryptowalut mogą oddawać głosy przydzielone do ich udziałów w celu wyznaczenia świadków. Świadkowie ci zabezpieczają i weryfikują blockchain, nie potrzebują własnej kryptowaluty, ale potrzebują głosów. Ten protokół konsensusu jest bardziej scentralizowany niż inne. DPoS jest używany przez BNB, BitShares, Steem i EOS.

**Dowód uprawnień (PoA):**

Prawdopodobnie ponownie bardziej scentralizowany, PoA ma z góry określone walidatory bloków. Nowe bloki w łańcuchu bloków są tworzone tylko wtedy, gdy walidatory mają większość. Protokół jest podobny do PoS. Walidatorzy są publicznie znani i odpowiedzialni za określenie swojej roli i kwalifikowalności do walidacji PoS. Nowszy blockchain, Elysian, wykorzystuje PoA, a także niektóre sieci testowe Ethereum lub testowe łańcuchy bloków.

## Konsensus Nexusa:

Jeśli nie jesteś nowy w kryptowalutach, prawdopodobnie zdajesz sobie sprawę z toczącej się debaty między Proof of Work (PoW), a Proof of Stake (PoS), który jest lepszym mechanizmem konsensusu w celu zabezpieczenia łańcucha bloków. W Nexusie dostrzegamy zalety obu i wierzymy, że różnorodność jest mocną stroną. Właśnie dlatego Nexus łączy obie te cechy, wykorzystując wiele kanałów konsensusu w celu zabezpieczenia stanu księgi. Dywersyfikując charakter naszej struktury konsensusu, unikamy zależności od jednego mechanizmu, poprawiając nasze ogólne bezpieczeństwo.

Więc jak to wygląda? Nexus składa się z trzech kanałów, dwóch PoW i jednego PoS. Pierwszy kanał PoW wykorzystuje algorytm haszujący (podobny do wielu innych łańcuchów bloków) w celu udowodnienia działania, podczas gdy kanał prime wykorzystuje algorytm, w którym górnicy są zobowiązani do wyszukiwania klastrów bardzo dużych liczb pierwszych, oferując unikalną odmianę zasady PoW . Wreszcie kanał PoS przyjmuje energooszczędną, prostą funkcję, w której „moc” wydobywcza użytkowników jest określana na podstawie ich stakowanego salda i wyniku zaufania.

Dlaczego Nexus zdecydował się na wielopłaszczyznowy model konsensusu? Takie podejście ma wiele zalet, ale krótko mówiąc, jest ono bezpieczniejsze, bardziej sprawiedliwe i daje nam większe możliwości dostosowania się do przyszłych wymagań. Maksymaliści szybko zwrócą uwagę, że na razie Bitcoin jest niekwestionowanym królem bezpieczeństwa blockchain, a ponieważ wykorzystuje model konsensusu PoW, wielu zakłada, że ​​oznacza to, że PoW jest również królem konsensusu. Istnieją jednak pewne [rażące obawy](https://hackernoon.com/proof-of-work-or-proof-of-waste-9c1710b7f025) polegające wyłącznie na PoW, nawet bez uwzględnienia powszechnego argumentu podkreślającego niezrównoważone zużycie energii , ponieważ będzie to dyskusyjne w związku z przełomami w energetyce odnawialnej.

Proof of Stake został po raz pierwszy wprowadzony przez PeerCoin i szybko zyskał popularność wśród wschodzących platform blockchain. Choć mocno krytykowany przez maksymalistów PoW, konsensus PoS zyskał natychmiastową wiarygodność, gdy Ethereum, druga co do wielkości kryptowaluta zarówno pod względem kapitalizacji rynkowej, jak i sieci, ogłosiła plany konwersji z modelu PoW na model konsensusu PoS. Jednak PoS nie jest pozbawiony wad i na przestrzeni lat ewoluował w wiele odmian, w szczególności delegowany PoS, ale każda odmiana ma swoje [za i przeciw](https://coincodex.com/article/7142/what-is-proof-of-stake/).

Zamiast zostać złapanym w środku debaty PoW vs PoS i utrudnionym przez ograniczenia któregokolwiek z nich, programiści Nexusa zdecydowali się wdrożyć oba, aby skorzystać z połączonych zalet, jednocześnie minimalizując wady każdego pojedynczego mechanizmu. Ponadto Nexus implementuje reputację jako wartość, która jest związana z tym, ile czasu stakujący konsekwentnie dostarcza zasoby do sieci. Mechanizm o nazwie [Trust](/pl/innovations/trust-npos)  rejestruje przeszłe prace w celu stworzenia systemu ważonej reputacji, znacznie poprawiając ogólne bezpieczeństwo kanału Nexus PoS (nPoS).

Zespół Nexusa przekształca te trzy oddzielne kanały konsensusu w jeden wielowarstwowy system przetwarzania zdolny do obliczeniowego fragmentowania danych. Protokół Tritium jest pierwszym uaktualnieniem [Łańcucha trzech wymiarów (3DC)](/pl/innovations/3-dimensional-chain), który jest wdrażany za pośrednictwem[ frameworka TAO](/pl/fundamentals/tao-framework).