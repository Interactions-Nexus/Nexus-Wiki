---
title: Łańcuchy podpisów
description: Konta lub profile użytkowników
published: true
date: 2022-12-16T22:57:29.587Z
tags: 
editor: markdown
dateCreated: 2022-10-22T21:29:44.036Z
---

# Łańcuchy podpisów

## Zarządzanie kluczami — Problem

Główną zaletą korzystania z kryptowalut jest bezpieczeństwo uzyskane dzięki zastosowaniu kryptografii klucza publicznego. Chociaż jest to ogromna poprawa w stosunku do scentralizowanych systemów logowania, ta korzyść wiąże się z wadą zarządzania kluczami. W celu zarządzania kluczami większość portfeli kryptowalutowych korzysta z pliku bazy danych o nazwie 'wallet.dat', w którym rejestrowane są wszystkie klucze, które były lub będą używane do uzyskiwania dostępu do monet.

Wierzymy, że przyjęcie kryptowaluty i technologii blockchain zawsze będzie ograniczone, jeśli polega się na takim modelu, ze względu na niedogodności związane z koniecznością regularnego tworzenia kopii zapasowych portfela, utratą lub kradzieżą dysków twardych oraz ryzykiem wysyłania środków na adresy, których nie można wydać. Systemy te są podatne na błędy ludzkie, co wróży potrzebę posiadania złożonego sprzętu zaprojektowanego specjalnie do bezpiecznego przechowywania kluczy prywatnych. Chociaż urządzenia te stanowią krok w kierunku przyjazności dla użytkownika, zawierają zastrzeżony sprzęt i oprogramowanie, które nadal mogą zostać zgubione lub skradzione, a zatem nie stanowią niezawodnego zamiennika systemów autoryzacji.

## Łańcuch podpisów — Rozwiązanie&#x20;

Nexus zaprojektował system do automatyzacji zarządzania kluczami poprzez zdecentralizowany system logowania, który nazywamy Łańcuchami Podpisów (SigChains). Dzięki temu użytkownicy mogą logować się do portfela Nexus za pomocą nazwy użytkownika, hasła i kodu PIN. Łańcuchy podpisów nadal wykorzystują kryptografię klucza publicznego, ale zamiast przechowywać klucze na dysku lub w chmurze, są one przechowywane w 'matematycznej hiperprzestrzeni', co oznacza, że Twoje dane uwierzytelniające stają się 'kluczem' do 'wirtualnej przestrzeni', którą posiadają użytkownicy za pomocą łańcucha podpisów . Eliminuje to również obciążenie związane z zarządzaniem kluczami podczas korzystania z DApps, które często wymagają wtyczek innych firm, takich jak MetaMask.

Łańcuchy podpisu oddzielają klucz prywatny od konta użytkownika, dlatego nie ma ograniczeń co do posiadania lub bezpieczeństwa pojedynczego klucza prywatnego. Klucz prywatny staje się przestarzały, gdy generowana jest następna transakcja, zapewniając wyższy poziom bezpieczeństwa w porównaniu z ciągłym ponownym wykorzystaniem klucza prywatnego, jak ma to miejsce w przypadku innych technologii blockchain.

Łańcuchy podpisów (SigChains) są porównywalne z 'osobistym łańcuchem bloków' i stanowią podstawę dla DApps, które zarządzają wszystkimi rodzajami własności cyfrowej. Integrują się z istniejącymi strukturami aplikacji, które już opierają się na systemach autoryzacji za pomocą kombinacji nazwy użytkownika i hasła, a tym samym zapewniają programistom DApps możliwość integracji funkcjonalności blockchain jako podwyższonej warstwy z istniejącymi aplikacjami przy minimalnych modyfikacjach architektury. Można je również zintegrować z różnymi środkami bezpieczeństwa, takimi jak biometria i sprzętowe menedżery haseł.

Dodatkowe korzyści to wydajność uzyskana dzięki ograniczeniu wymogu przechowywania dużej ilości sygnatur na dysku oraz możliwość wykorzystania różnych typów kluczy, takich jak FALCON do kwantowej rezystancji.

### Szybkość i skalowalność

Sigchains wykorzystują model oparty na kontach, który zastępuje niezgrabną architekturę UTxO (wyjście niewykorzystanych transakcji), którą wprowadził Bitcoin. Łańcuchy Sigchain zawierają wszystkie dane użytkownika w unikalnym łańcuchu i zapewniają wyższy poziom skalowalności, ponieważ do weryfikacji transakcji wymagany jest tylko jeden podpis.

Wraz z łańcuchami Sigchain, transakcje Nexus są oddzielone od bloku, co oznacza, że w danych na poziomie bloku wymagany jest tylko jeden skrót lub 'dowód' na transakcję, a nie cała transakcja. Powoduje to zakwaterowanie około 31 728 transakcji na blok 2 MB. Razem te innowacje tworzą lekkie bloki i wydajne przetwarzanie transakcji, bez wymogu skalowania poza łańcuchem (warstwa 2).

### Przycinanie

Łańcuch podpisu jest tak nazwany, ponieważ jest łańcuchem nexthash, skrótem podpisu i klucza publicznego. Ponieważ jest to spójny łańcuch zdarzeń, których nie można zmienić, zapewnia dodatkowe korzyści skalowania, wymagając tylko dwóch podpisów do weryfikacji całego Sigchain: pierwszej i ostatniej transakcji. Oznacza to, że wszystkie podpisy pomiędzy nimi można odrzucić wraz z kluczami publicznymi, oszczędzając dużą ilość miejsca w pamięci bez poświęcania bezpieczeństwa. Dzieje się tak dlatego, że Sigchain jest niezmiennym łańcuchem transakcji. Prawidłowy podpis na początku transakcji w łańcuchu dowodzi, że cały łańcuch jest ważny, ponieważ blokuje cały Sigchain przed modyfikacją.

Zwykle ten podpis jest największą częścią transakcji, dlatego wyeliminowanie konieczności zapisywania go na dysku poprawia skalowalność Nexus Blockchain. W przypadku Bitcoin średni rozmiar danych wejściowych wynosi 186 bajtów, przy czym sygnatura zajmuje 146 z tych bajtów, co powoduje, że 77% łańcucha bloków Bitcion składa się z sygnatur przechowywanych na dysku. Jak widać, łączenie sygnatur ma ogromny wpływ na walkę z rozdęciem łańcucha bloków.

### Bezpieczna tożsamość cyfrowa

Identyfikator punktu końcowego (EID) jest podobny do adresu protokołu internetowego (IP) i jest formą tożsamości w warstwie sieciowej. Dzięki zastosowaniu [LISP](broken-reference) EID staje się identyfikatorem, podczas gdy RLOC (Routing Locator) staje się lokalizacją. To oddzielenie umożliwia urządzeniu swobodne przemieszczanie się między sieciami, ponieważ zmienia się tylko RLOC, a nie EID. Jest to sprzeczne z tym, jak obecnie funkcjonuje Internet, w którym zarówno identyfikator, jak i lokalizacja są powiązane w jednym adresie IP.

EID jest krytyczną cechą bezpieczeństwa, ponieważ można go połączyć z Sigchain, który sprawia, że identyfikator sieci jest kryptograficznie powiązany z księgą główną. EID, Sigchains i wykorzystanie reputacji razem tworzą podwyższoną warstwę zaufania do Internetu, ponieważ można z całą pewnością zweryfikować, że druga strona jest tym, za kogo się podaje, bez potrzeby korzystania z usług stron trzecich, takich jak urzędy certyfikacji (CA). Dzięki tej technologii przewiduje się ograniczenie oszustw, włamań, fałszywych kont i kradzieży tożsamości zarówno dla konsumentów, jak i dostawców usług.

### Odporność kwantowa

Sigchains zwiększa odporność na ataki ze strony zarówno klasycznych, jak i teoretycznych komputerów kwantowych. Osiąga się to poprzez oddzielenie tożsamości konta od powiązanej z nim kryptografii, podobnie jak [LISP](broken-reference) oddziela identyfikator od lokalizacji. Daje to przewagę architektoniczną polegającą na zmianie pary kluczy, która jest używana do uzyskiwania dostępu do Sigchain przy każdej transakcji i ukrywaniu klucza publicznego, dopóki nie zostanie użyty. Kiedy osoba fizyczna tworzy transakcję w sieci, rości sobie prawo własności, ujawniając klucz publiczny NextHash (skrót klucza publicznego) poprzez złożenie ważnego podpisu na podstawie jednorazowego klucza prywatnego. To znacznie skraca okno czasowe ataku, naturalnie zwiększając moc obliczeniową wymaganą do pomyślnego przejęcia łańcucha sygnatur za pomocą ataków MITM (Man in the Middle). Więcej informacji można znaleźć w [Rezystancja kwantowa](broken-reference).

Ponieważ tożsamość konta jest oddzielona od kryptografii, Sigchain obsługuje wiele schematów podpisów, takich jak FALCON (Fast Fourier Lattice-Based Compact Signatures Over NTRU) lub Brainpool. Ponieważ FALCON jest nadal badany i oceniany przez NIST (National Institute of Standards and Technology), ogólnie zaleca się, aby był używany wyłącznie w produkcji w tak zwanym 'schemacie podpisu hybrydowego', co oznacza, że nie polegasz wyłącznie na bezpieczeństwo FALCON dla bezpieczeństwa systemu. W naszym wdrożeniu Sigchain działa jak hybrydowy schemat podpisu, dzięki czemu korzystanie z FALCON jest bezpieczne dla naszego środowiska produkcyjnego.