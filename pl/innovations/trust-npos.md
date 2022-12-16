---
title: Zaufanie - nPoS
description: Dowód stawki oparty na TRUST (Reputacji)
published: true
date: 2022-12-16T23:19:54.989Z
tags: 
editor: markdown
dateCreated: 2022-10-22T21:33:07.356Z
---

# ZAUFANIE

Publiczny blockchain jest często opisywany jako 'niezaufany', ponieważ nie wymaga 'zaufanej' strony trzeciej. Jak na ironię, zaufanie jest nadal czynnikiem w systemach pozbawionych zaufania, przy czym zaufanie pochodzi nie z systemu centralnego, ale ze zdecentralizowanego konsensusu.

Koszt ataku na zdecentralizowany mechanizm konsensusu jest bezpośrednio związany z jego bezpieczeństwem. Aby zwiększyć bezpieczeństwo, Nexus wprowadza reputację jako koszt, który jest powiązany z tym, ile spójny czas wkłada gracz w zasoby. Mechanizm o nazwie 'Zaufanie' rejestruje dotychczasową pracę w celu stworzenia systemu reputacji, który dodaje kolejną wagę do bezpieczeństwa protokołu Nexus i jest obecnie wdrażany na kanale Nexus Proof-of-Stake (nPoS) i będzie używany na każdej warstwie [3DC](broken-reference).

Kluczem do dobrego systemu reputacji jest wysiłek potrzebny do zdobycia reputacji w porównaniu do względnej łatwości jej utraty. Połączenie zachęty ekonomicznej z większym zaufaniem, takim jak wyższe zwroty z weryfikacji, wiąże się z niebanalnym kosztem utraty reputacji.

Wynik zaufania jest definiowany jako całkowity czas, w którym określony użytkownik wniósł wagę lub zasoby czasu rzeczywistego do sieci. Ocena zaufania jest budowana stopniowo w czasie, gdy ktoś konsekwentnie obsługuje węzeł w uczciwy, godny zaufania i terminowy sposób, aby weryfikować dane transakcji, uruchamiając portfel Nexus na komputerze ze stałym połączeniem internetowym (24 godziny na dobę, 7 dni w tygodniu). W niektórych okolicznościach, na przykład gdy węzeł przechodzi w tryb offline na dłuższy czas, ocena zaufania węzła zostanie obniżona. Dlatego ma się motywację do ciągłego i konsekwentnego obsługiwania węzła zapewniającego bezpieczeństwo sieci Nexus.

## Nexus Proof-of-Stake

Nexus obecnie implementuje protokół nPOS oparty na reputacji lub zaufaniu, który utrzymuje losową selekcję nieodłączną od czystego konsensusu Nakamoto, ale także nakłada reputację na każdy węzeł sprawdzający poprawność. Reputacja węzła w połączeniu z jego stawką daje wagę, która określa prawdopodobieństwo znalezienia następnego bloku. Aby zapewnić odpowiednie zachęty dla walidatorów do zdobycia zaufania, stopa zwrotu wynosi od 0,5% do 3,0%. Zaufanie do naszego wdrożenia zdobywamy dzięki konsekwentnej produkcji bloków w ciągu trzech dni ruchomych. Jeśli ten czas zostanie przekroczony, wartość Trustu spada w tempie 3x, co oznacza, że jeśli węzeł przegapi jeden dzień stakingu, otrzymuje karę w wysokości trzech dni utraconego Trustu. Mechanizm ten stanowi podstawową podstawę rozeznawania jakości węzłów.

Zaufanie dodaje warstwę ochrony przed atakami, która jeszcze bardziej zwiększa Bizantyjską tolerancję na awarie (BFT) sieci Nexus. Wraz z pozostałymi dwoma kanałami wydobywczymi Nexusa, ograniczeniami częstotliwości blokowania, dziesięciominutowymi zdecentralizowanymi punktami kontrolnymi, jest bardzo mało prawdopodobne, aby atakujący przeprowadził udany atak 51%, ponieważ zdobycie wystarczającej ilości zaufania wymagałoby ogromnej ilości zasobów i czasu z sieci, aby przejąć kontrolę nad wszystkimi trzema kanałami. Trust nie tylko zwiększa bezpieczeństwo protokołu, ale także zwiększa jego wydajność, a tym samym jego potencjał skalowalny.

Zaufanie wspiera pogląd, że „nie każdy ma pieniądze, ale każdy ma czas”, co sugeruje, że każdy może zbudować zaufanie, jeśli ma trochę czasu, ponieważ do rozpoczęcia budowania wyniku zaufania wymagana jest tylko minimalna ilość sprzętu i NXS.

### Reputacja

Reputacja jest ważnym zasobem, który należy wziąć pod uwagę przy rozpoznawaniu matematycznej prawdy zdecentralizowanego konsensusu. Dzięki wiedzy, którą zdobyliśmy podczas naszych obecnych wdrożeń, planujemy rozszerzyć nasze obecne systemy reputacji na wiele innych obszarów. Poprzez naszą architekturę zwaną „TAO” (Tritium, Amine i Obsidian) wprowadzamy reputację do prymitywów 3DC jako część niezmienności i autentyczności.

Reputacja w Tritium wykracza poza klucze zaufania dzięki wdrożeniu [Signature Chains](broken-reference). Łańcuchy podpisów to hybrydowy schemat podpisów, który wykorzystuje łączenie skrótów i kryptografię asymetryczną w celu utworzenia prymitywnego łańcucha bloków na poziomie użytkownika. Ten łańcuch zawiera wszystkie działania użytkownika, bez ujawniania jego faktycznej tożsamości. Rezultatem jest przejrzysta księga zdarzeń powiązanych z Łańcuchem Podpisów danego użytkownika, która może zapewnić zestaw danych do tworzenia bardziej złożonych systemów reputacji interpretowanych na podstawie tej serii zdarzeń. Egzekwowanie reputacji w warstwie księgi odbywa się poprzez aktualnie zaimplementowany stosunek stakingu 1:3 oraz system relacji w warstwie sieci.

### Reputacja górnika

Górnicy zauważą poprawę swojej reputacji dzięki konsekwentnym działaniom wykonywanym w sieci wydobywczej w miarę zbliżania się premiery Amine i Obsidian. Da to podobny model zmiennej nagrody jak nPoS, ale z wymaganiem mocy wydobywczej w celu wytworzenia spójnych bloków w czasie. Te modele reputacji będą faworyzować węzły o spójnej historii i karać węzły, które przeskakują z łańcucha bloków do łańcuchów w pogoni za zyskiem. Ponieważ reputacja będzie czynnikiem wpływającym na rentowność wydobycia, zachęty dostosują górników do wniesienia bardziej spójnej mocy do konsensusu sieciowego, zapewniając większe bezpieczeństwo. Reputacja górników może zapewnić większą odporność na ataki 51%, podobnie jak reputacja może poprawić model pBFT (Praktyczna Byzantyjska Tolerancja na Błędy) o 20% lub więcej.

Obecnie istnieje kilka mechanizmów konsensusu, które zostały zaprojektowane w celu tworzenia zdecentralizowanych sieci. Chociaż wszystkie te mechanizmy służą do ochrony przed atakami Sybil i podwójnymi wydatkami, wiele z nich ma ograniczoną zdolność do przechwytywania reputacji węzłów w sieci. Większość podąża za pBFT, stosując ważenie oparte na stawkach. Chociaż te mechanizmy konsensusu mają BFT poniżej 33%, można to poprawić poprzez wdrożenie systemu reputacji, który wykorzystuje czas jako równie dostępną wagę, co może zwiększyć bezpieczeństwo konwencjonalnych mechanizmów konsensusu.

Chociaż zdecentralizowane mechanizmy konsensusu są odporne na manipulacje, stają się podatne na ataki, gdy jedna ze stron zaczyna kontrolować co najmniej 33% węzłów dla pBFT lub 51% mocy obliczeniowej sieci dla PoW (Proof-of-Work). Badając te zagrożenia, odkryliśmy, że włączenie reputacji jako części procesu konsensusu może poprawić pBFT. Więcej informacji na ten temat można znaleźć w poniższym linku, który proponuje protokół reputacji, który zapewnia 20% wzrost tolerancji na błędy.

[Guru: Universal Reputation Module for Distributed Consensus Protocols](https://eprint.iacr.org/2017/671.pdf)

### Relacje

Obecny system Trust toleruje błędy bizantyjskie poprzez dystrybucję walidatorów i implementację relacji między węzłami. W Nexusie reputacja jest zaprojektowana jako publiczny wskaźnik historii węzła, podczas gdy relacje są prywatnym wskaźnikiem relacji węzła z innymi węzłami. Pod tym względem łatwiej jest zapobiec bizantyńskiej usterce, jeśli znane jest prawdopodobieństwo zakładanej winy. Mówiąc prościej, oznacza to, że węzeł może łatwiej odróżnić błąd bizantyjski od uczciwego węzła na podstawie wcześniejszych błędów.

Zauważyliśmy kilka zalet utrzymywania przez węzły historii ich subiektywnych relacji między sobą, czyli prywatnego wskaźnika jakości danych i komunikacji między węzłami. Nie nadaje się to do krytycznych reguł konsensusu, ale raczej do wykrywania złośliwych węzłów w systemie. Rezultatem tego, dzięki niektórym naszym podstawowym wdrożeniom, jest zdolność sieci do zniechęcania do nieuczciwych zachowań bez doświadczania błędów konsensusu. Pozwala to na niedoskonałość w wykrywaniu jakości 'dobrych i złych', przy jednoczesnym wykryciu z wyprzedzeniem potencjalnych wad bizantyjskich i możliwości ich nierozpowszechniania. Jeśli inne węzły w sieci propagują nieuczciwe bloki i opierają się na nich, byłyby wtedy postrzegane jako ważna część łańcucha blokowego i zrealizowany fałszywy alarm. Dlatego węzły wykrywają nieuczciwe bloki i są zachęcane do ich nieprzekazywania.