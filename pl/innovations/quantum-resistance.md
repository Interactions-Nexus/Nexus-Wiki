---
title: Odporność kwantowa
description: Zaprojektowany z myślą o kwantowej przyszłości.
published: true
date: 2022-12-16T23:28:28.907Z
tags: 
editor: markdown
dateCreated: 2022-10-22T21:34:23.825Z
---

# Odporność kwantowa

Wraz ze wzrostem mocy komputerów klasycznych i pojawieniem się komputerów kwantowych klucze publiczne stają się coraz bardziej podatne na ataki. Większość adresów kryptowalut jest tworzona przez haszowanie lub ukrywanie klucza publicznego. Jednak gdy użytkownik dokonuje transakcji, klucz publiczny jest ujawniany w łańcuchu bloków. W dziedzinie klasycznej informatyki ryzyko związane z tą metodą jest niewielkie. Jednak komputer kwantowy z algorytmem Shora mógłby złamać większość kryptografii klucza publicznego w krótkim czasie, powodując kradzież funduszy. Chociaż większość przypuszczeń waha się od pięciu do dziesięciu lat, zanim zabezpieczenia mogą zacząć się łamać, Nexus przygotował się, integrując szereg innowacji kryptograficznych, które wspierają zwiększony poziom odporności kwantowej.

Opracowaliśmy architekturę o nazwie [Signature Chains](broken-reference), która zwiększa bezpieczeństwo istniejącego algorytmu DSA (Digital Signature Algorithm), haszując klucz publiczny, dopóki nie zostanie on użyty, podczas zmiany pary kluczy przy każdej transakcji. Zintegrowaliśmy również następujące funkcje kryptograficzne: FALCON (drugi kandydat do konkursu NIST Post-Quantum cryptography), Argon2 (zwycięzca konkursu na haszowanie haseł i doskonała alternatywa dla S-Crypt lub B-Crypt) oraz Keccak (zwycięzca konkursu SHA3).

## Komputery klasyczne kontra kwantowe

Klasyczne obliczenia wykorzystują szereg tranzystorów. Tranzystory te tworzą serce komputera (procesor). Każdy tranzystor może być włączony lub wyłączony, a stany te są używane do reprezentowania wartości liczbowych 1 i 0. Liczba stanów cyfr binarnych (bitów) zależy od liczby dostępnych tranzystorów, zgodnie ze wzorem (2^n ) + 1, gdzie n to liczba tranzystorów. Klasyczne komputery mogą znajdować się tylko w jednym z tych stanów w danym momencie, więc prędkość twojego komputera jest ograniczona do tego, jak szybko może zmieniać stan.

Z drugiej strony komputery kwantowe używają tak zwanych bitów kwantowych lub 'kubitów', które są reprezentowane przez kwantowy spin elektronów lub fotonów. Cząstki te są umieszczane w stanie zwanym superpozycją, co pozwala kubitowi na jednoczesne przyjęcie wartości 1 i 0, co generalnie skutkuje wykładniczym wzrostem mocy obliczeniowej w porównaniu z ich klasycznymi odpowiednikami.

## Łańcuch podpisów

Nexus jest dostępny za pośrednictwem zaprojektowanej przez nas technologii o nazwie Signature Chains, zdecentralizowanego konta blockchain, które umożliwia logowanie z dowolnego komputera za pomocą nazwy użytkownika, hasła i kodu PIN. Są one porównywalne z osobistym łańcuchem bloków, który umożliwia zdecentralizowany dostęp za pośrednictwem systemu logowania, eliminując konieczność przechowywania klucza prywatnego. Sigchains w sposób deterministyczny tworzą matematyczną 'blokadę', którą mogą odblokować tylko twoje dane logowania.

Zasadniczo Sigchain oddziela klucz prywatny od konta użytkownika, dlatego nie jest związany posiadaniem ani bezpieczeństwem pojedynczego klucza prywatnego. Kiedy ktoś tworzy transakcję w sieci, rości sobie prawo własności, ujawniając klucz publiczny NextHash (skrót twojego klucza publicznego) i tworzy podpis z jednorazowego klucza prywatnego. Klucz prywatny staje się przestarzały, gdy generowana jest następna transakcja, zapewniając wyższy poziom bezpieczeństwa w porównaniu z ciągłym ponownym wykorzystaniem klucza prywatnego, jak ma to miejsce w przypadku innych technologii blockchain. Przyszłe wykorzystanie generowania biometrycznych nazw użytkownika wzmocni Twoje dane uwierzytelniające i dostęp do łańcucha podpisów.

## Zarządzanie kluczami

Łańcuchy podpisu oddzielają klucze od konta użytkownika, co oznacza, że w dowolnym momencie możesz zmienić typ klucza używanego na koncie. Daje to użytkownikom możliwość korzystania z kryptografii postkwantowej, takiej jak FALCON, lub opcji korzystania z bardziej sprawdzonych krzywych Brainpool. Jeśli w którymś z tych schematów kryptograficznych zostaną znalezione jakiekolwiek wady, Twoje konto będzie bezpieczne przy użyciu łańcucha podpisów. Zabezpieczenia te są ważne, aby chronić systemy w czasie, ponieważ trwające analizy kryptograficzne zawsze znajdują luki w zabezpieczeniach i wektory ataków, które zaczną łamać raz bezpieczne standardy kryptograficzne (np. SHA1).

[Large Bitcoin Collider znajduje kolejny klucz prywatny Bitcoin](https://bitcoinwhoswho.com/blog/2017/09/13/are-your-bitcoins-safe-large-bitcoin-collider-finds-another-private-key/)

## FALCON

Uzupełnieniem tego jest wykorzystanie FALCON (Fast-Fast-Fourier Lattice-Based Compact-Signatures Over NTRU) jako opcjonalnego ustawienia, które wykorzystuje kryptografię opartą na sieci w celu zapewnienia bezpieczeństwa kont w epoce postkwantowej. Wymagania obliczeniowe wynoszą co najmniej 1/40 algorytmu podpisu cyfrowego krzywej eliptycznej (ECDSA), co oznacza, że możesz weryfikować podpisy znacznie szybciej niż ECDSA. Jednak wadą jest to, że wymaga około 1,5 KB zarówno dla klucza publicznego, jak i podpisu. Chociaż Falcon opiera się na starej i sprawdzonej matematyce (sieci NTRU), nie przeszedł tak wielu kryptoanaliz jak kryptografia krzywych eliptycznych (ECC) czy Rivest Shamir Adleman (RSA).

## Argon2

Jest funkcją mieszania haseł typu open source, którą zintegrowaliśmy w celu generowania kluczy i nazw użytkowników. Argon2 to algorytm haszujący hasło o zmiennej złożoności, co oznacza, że może kontrolować, ile sekund zajmuje wygenerowanie klucza lub nazwy użytkownika. To drastycznie zwiększa czas i zasoby potrzebne hakerowi offline do brutalnego wymuszenia łańcucha sygnatur. Ponieważ czas wygenerowania skrótu Argon2 jest ograniczony opóźnieniem pamięci, wyspecjalizowane urządzenie do 'łamania haseł' nie ma przewagi nad procesorem ogólnego przeznaczenia.

Nasze domyślne ustawienia Argon2 wymagają co najmniej 0,3 – 0,5 sekundy, aby wygenerować nowy klucz, co oznacza, że można wypróbować tylko dwa do trzech haseł na sekundę. Łącząc to z minimalnym wymogiem co najmniej 8 znaków alfanumerycznych \[a-Z, 0-9] na hasło, nawet jeśli nazwa użytkownika i PIN były znane atakującemu, czas wymagany do złamania hasła byłby rzędu 5 milionów lata.

## Keccak

Zgodnie z zaleceniami NIST (National Institute for Standards in Technology) wymagania bitowe dla symetrycznych schematów szyfrowania i funkcji haszujących muszą być co najmniej dwukrotnie większe dla równoważnej rezystancji kwantowej (np. 512 vs 256). Ta rekomendacja stanowi inspirację dla naszego standardowego skrótu: 256 bitów dla rejestrów, 512 bitów dla transakcji i 1024 bitów dla bloków dla odpowiednio 128-bitowej, 256-bitowej i 512-bitowej rezystancji kwantowej.

## Redundancja kryptograficzna

Nie opieramy się na bezpieczeństwie tylko jednej funkcji kryptograficznej dla bezpieczeństwa całego systemu, a każdy klucz publiczny traktujemy jako jednorazowy po użyciu. Oznacza to, że nasze zabezpieczenia wykorzystują wiele różnych warstw nadmiarowości w celu zapewnienia ochrony na wypadek, gdyby jedna z nich stała się podatna na ataki. Poleganie na jednym kluczu prywatnym dla bezpieczeństwa to tykająca bomba zegarowa, chociaż to podejście jest w dużej mierze stosowane przez większość aplikacji blockchain.

[Wady kryptograficzne znalezione w IOTA](https://medium.com/@neha/cryptographic-vulnerabilities-in-iota-9a6a9ddc4367)

## Odziedziczona luka w zabezpieczeniach

Mentalność kopiowania/wklejania kodu źródłowego używanego do tworzenia wielu projektów kryptowalut doprowadziła dziś do przeniknięcia wielu luk w zabezpieczeniach. Poniżej znajduje się jeden taki przykład, który stworzył pandemonium dla setek projektów, które odziedziczyły wadę po Zcoin.

[Wady krytyczne mogą być osadzone we wszystkich monetach prywatności](https://micky.com.au/expert-warning-fatal-flaw-embedded-in-all-privacy-coins/)