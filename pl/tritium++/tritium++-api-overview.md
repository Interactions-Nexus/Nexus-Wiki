---
title: Przegląd API Tritium++
description: Przegląd
published: true
date: 2022-10-31T22:08:32.110Z
tags: 
editor: markdown
dateCreated: 2022-10-24T22:00:16.489Z
---

# ⚙ Przegląd Tritium++

## Omówienie interfejsu API Nexusa

Nexus udostępnia kilka interfejsów API, które umożliwiają użytkownikom i programistom łatwą interakcję z funkcjami stosu oprogramowania Nexus. Każdy interfejs API jest logicznie pogrupowanym zbiorem metod, które oddziałują z określoną częścią stosu (np. księgą, rejestrami), według obszaru funkcjonalnego (konta, aktywa, tokeny) lub według konkretnego przypadku użycia w branży (zaopatrzenie, muzyka).

### `Protokół`

Serwer API używa protokołu `HTTP` i obsługuje zarówno metody żądania **`GET`**, jak i **`POST`**.

API używa **`JSON`** (JavaScript Object Notation) jako podstawowego mechanizmu transportu danych zarówno dla danych wejściowych, jak i wyjściowych. Jednak serwer API obsługuje również żądania zakodowane w adresie URL (**`application/x-www-form-urlencoded`**).

### `Port`

Domyślnie serwer API działa na porcie 8080. Można to zmienić, ustawiając `apiport=xxxx` w nexus.conf lub uruchamiając demona z parametrem `-apiport=xxxx`.

### `Bezpieczeństwo`

Interfejs API Nexusa korzysta ze schematu uwierzytelniania `HTTP Basic`. Wymaga to od wywołującego ustawienia nagłówka HTTP `Authorization` z wartością `Basic <credentials>` z częścią `<credendtials>`ustawioną na `apiuser:apipassword` i zakodowane `base64`. Po stronie serwera API uwierzytelnianie jest konfigurowane poprzez dodanie `apiuser=<nazwa użytkownika>` i `apipassword=<hasło>` do nexus.conf.\
**UWAGA**: Jeśli chcesz całkowicie wyłączyć uwierzytelnianie, możesz to zrobić, ustawiając `apiauth=0` w pliku nexus.conf

Uzupełnieniem mechanizmu uwierzytelniania jest implementacja szyfrowania `SSL` (`HTTPS`). Domyślnie serwer API jest uruchamiany z wyłączonym SSL. Aby go włączyć, dodaj `apissl=1` do swojego nexus.conf

### `Sesje wieloużytkownikowe`

Interfejs API Nexusa można skonfigurować tak, aby działał w trybie wielu użytkowników, co pozwala na jednoczesne logowanie wielu łańcuchów sygnatur i jednoczesne korzystanie z interfejsu API. Tę funkcję można włączyć, ustawiając `multiuser=1` w nexus.conf (domyślnie wyłączone). Gdy włączony jest tryb wielu użytkowników, początkowa odpowiedź logowania będzie zawierać wartość identyfikatora sesji. Ten identyfikator sesji musi być następnie uwzględniony we wszystkich kolejnych wywołaniach interfejsu API do punktów końcowych, które wymagają zalogowania się użytkownika.

### `Punkt końcowy`

Każdy punkt końcowy interfejsu API można wywołać za pomocą następującej semantyki:

**`<api>/<verb>/<noun>`**

e.g.

```
http://127.0.0.1:8080/ledger/get/block
```

**UWAGA**: URI są zawsze pisane małymi literami.

### `Obsługa błędów`

W przypadku, gdy wywołanie API zakończy się błędem, obiekt JSON zostanie zwrócony w następującym formacie:

```
{
    "error" :
    {
        "code" : -123,
        "message" : "An error has occurred"
    }
}
```

## Kody błędów DSL

| Kod | Wiadomość                                                                     |
| ---- | ---------------------------------------------------------------------------- |
| 1    | Błąd składni zapytania: zduplikowane symbole wieloznaczne niedozwolone   |
| 2    | Błąd składni zapytania: dla typu \[typename] dozwolone są tylko operatory '=' i '!=' |
| 3    | Błąd składni zapytania: zniekształcona klauzula where w \[clause] |
| 4    | Błąd składni zapytania: należy użyć = bez dodatkowych znaków |
| 5    | Błąd składni zapytania: należy użyć '(and)' do mieszania instrukcji AND/OR |
| 6    | Błąd składni zapytania: brak operatora logicznego dla grupy |
| 7    | Błąd składni zapytania: pusta klauzula where w \[clause] |
| 8    |
| 9    |

## Kody błędów API

| Kod | Wiadomość |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| -1 | Metoda niedostępna: \[message] |
| -2 | Nie znaleziono metody: \[message] |
| -3 | Metoda została przestarzała w wersji \[version]: \[message] |
| -4 | Nie znaleziono API (nazwa API) |
| -5 | Obiekt niedostępny: \[message] |
| -6 | content-type \[content type] nie jest obsługiwany |
| -7 | Nieobsługiwany typ \[typ] dla parametrów. |
| -8 | Nie można wyodrębnić adresu wejściowego |
| -9 | Sesja (session) nie istnieje |
| -10 | Nieprawidłowy identyfikator ID sesji |
| -11 | Użytkownik niezalogowany |
| -12 | Błędne lub brakujące kodowanie obiektów dla \[type] |
| -13 | Nie znaleziono obiektu |
| -14 | Nieprawidłowy adres URL żądania |
| -15 | Obiekt nie jest kontem ani tokenem |
| -16 | Konto nie zostało odblokowane dla transakcji |
| -17 | Nie udało się utworzyć transakcji |
| -18 | Nieprawidłowy format dla standardowego \[name] |
| -19 | Pole \[name] nie istnieje w obiekcie |
| -20 | Pole \[name] jest tylko do odczytu i nie może być aktualizowane |
| -21 | Rozmiar pola \[name] przekracza maksymalną długość \[size] |
| -22 | Pole \[name] to zarezerwowana nazwa pola |
| -23 | Standard obiektu \[name] niedostępny dla polecenia |
| -24 | Nie znaleziono zleceń dla rynku |
| -25 | Nieważna umowa zlecenia rynkowego: message |
| -26 | Nieprawidłowy parametr \[from], \[type] wymaga poprawnego tokena |
| -27 | Nieprawidłowe kodowanie base64 |
| -28 | Brakujący parametr \[name] w poleceniu |
| -29 | Określono nieobsługiwany format \[type] |
| -30 | Operacje nie zostały wykonane |
| -31 | Księga nie może podpisać transakcji |
| -32 | Nie udało się zaakceptować |
| -33 | Nieprawidłowa lub brakująca nazwa/adres |
| -34 | Nie znaleziono aktywa |
| -35 | Nieprawidłowy parametr \[key=type], oczekiwano \[type] |
| -36 | Nieobsługiwany typ \[name] dla polecenia |
| -37 | Brak nazwy/adresu tokena |
| -38 | Brak nazwy/adresu aktywa |
| -39 | Brak name\_from / address\_from |
| -40 | Nie znaleziono poprzedniej transakcji |
| -41 | Nieprawidłowy identyfikator transakcji |
| -42 | Brak ważnych debetów do kupienia od |
| -43 | Brak ważnych umów w tx |
| -44 | Transakcja nie powiodła się |
| -45 | Brak name\_to / address\_to |
| -46 | Brakująca kwota |
| -47 | Brak ceny |
| -48 | Nie znaleziono tokena |
| -49 | Nieobsługiwany typ nazwy/adresu |
| -50 | Brak txid |
| -51 | Brak dostępnych kont tokenowych dla odbiorcy |
| -52 | Nie ma więcej dostępnych kont do debetu |
| -53 | Brak name / address rachunku do zasilenia |
| -54 | Brak name\_proof / address\_proof do zasilenia |
| -55 | Musi mieć co najmniej dwóch odbiorców, aby obciążyć dowolny |
| -56 | Nieprawidłowe user-type enum \[value]  |
| -57 | Nieprawidłowy parametr \[name] |
| -58 | Pusty parametr \[name] |
| -59 | Konto do zasilenia nie jest kontem NXS |
| -60 | \[name] poza zakresem \[max] |
| -61 | Konto dowodowe jest przeznaczone dla innego tokena niż token aktywów |
| -62 | Transakcja Coinbase wydobyta przez innego użytkownika |
| -63 | Nie można pobrać domyślnego konta NXS do zasilenia |
| -64 | Brak konta odbiorcy name\_to / address\_to |
| -65 | Obiekt nie jest kontem |
| -66 | Nie można używać zagregowanych nazw pól z operacjami |
| -67 | -safemode następna niezgodność hash, transmisja zakończona |
| -68 | Zbyt mała kwota |
| -69 | Niewystarczające środki |
| -70 | Nie znaleziono konta trust |
| -71 | Nazwa pola \[name] nie istnieje |
| -72 | Rejestr nie jest kontem trust |
| -73 | Konto trust nie jest kontem NXS |
| -74 | Nie znaleziono rejestrów |
| -75 | Wartość \[key=value] przekracza rozmiar zbioru danych \[size] |
| -76 | Nie można ustawić stawki dla konta trust do czasu transakcji Genesis |
| -77 | Niewystarczające saldo konta trust, aby dodać do stakowania |
| -78 | Stawka niezmieniona |
| -79 | getblockhash wymaga uruchomienia demona z flagą -indexheight |
| -80 | Brak wysokości |
| -81 | \[command] nie może używać parametru \[name] w połączeniu z \[name] |
| -82 | Numer bloku poza zakresem |
| -83 | Nie znaleziono bloku |
| -84 | Brak hash lub wysokości |
| -85 | getblock według wysokości wymaga uruchomienia demona z flagą -indexheight |
| -86 | Brak hash lub txid |
| -87 | Nieprawidłowa lub nieznana transakcja |
| -88 | Brak lub pusta nazwa |
| -89 | Nieprawidłowy register\_address |
| -90 | Namespace już istnieje |
| -91 | Brak nazwy / register\_address |
| -92 | Nie znaleziono nazwy |
| -93 | Brak nazwy namespace |
| -94 | Nieprawidłowa namespace |
| -95 | Namespace nie istnieje: \[namespace] |
| -96 | Nie można utworzyć nazwy w \[namespace], której nie jesteś właścicielem |
| -97 | Obiekt o tej nazwie już istnieje w namespace |
| -98 | Obiekt o tej nazwie już istnieje dla tego użytkownika |
| -99 | Nie znaleziono transakcji przelewu
| -100 | Brak prefiksu nazwy użytkownika przed nazwą |
| -101 | Nieznana nazwa: (name) |
| -102 | Nieprawidłowy adres |
| -103 | Brak register\_address parameter |
| -104 | Nie znaleziono obiektu |
| -105 | Brak adresu |
| -106 | Nieprawidłowa nazwa/adres |
| -107 | Nie znaleziono historii |
| -108 | Nie udało się odczytać transakcji |
| -109 | Określona nazwa/adres nie jest typu (type) |
| -110 | Realizacja kontraktu nie powiodła się |
| -111 | Brakująca genesis / username |
| -112 | Brak username / destination |
| -113 | Użytkownik docelowy nie istnieje |
| -114 | (type) nie znaleziono |
| -115 | Nazwa/adres nie jest typu (type) |
| -116 | Nie można przenieść nazw utworzonych bez przestrzeni nazw |
| -117 | Nie znaleziono przedmiotu |
| -118 | Operator \[type] nie jest obsługiwany dla tego zestawu poleceń |
| -119 |  pole(a) \[name] nie istnieje dla wyniku |
| -120 | Przekroczono maksymalną liczbę kontraktów (99), spróbuj ponownie lub użyj trybu -autotx. |
| -121 | Typ zagregowany \[noun] niedozwolony dla \[verb] |
| -122 | Nieprawidłowy operator \[op] dla polecenia. |
| -123 | \[type] nieobsługiwany dla operatora \[op] |
| -124 | Operator \[op] nie może być użyty na pustym wyniku |
| -125 | Nie znaleziono tokena |
| -126 | Adres nie jest przeznaczony dla konta NXS" |
| -127 | Brak nazwy użytkownika |
| -128 | Brak hasła |
| -129 | Brak kodu PIN |
| -130 | Konto już istnieje |
| -131 | Blokada nie jest obsługiwana w trybie wielu użytkowników |
| -132 | Konto już zablokowane
| -133 | Nazwa użytkownika o zerowej długości |
| -134 | Hasło o zerowej długości |
| -135 | PIN o zerowej długości |
| -136 | Konto nie istnieje |
| -137 | Nie udało się uzyskać transakcji |
| -138 | Nie znaleziono poprzedniej transakcji |
| -139 | Nieprawidłowe poświadczenia |
| -140 | Zalogowano się już pod inną nazwą użytkownika |
| -141 | Już wylogowano |
| -142 | Parametr nazwy użytkownika nie jest obsługiwany dla tej metody. Nazwy można uzyskać tylko dla zalogowanego użytkownika |
| -143 | Brak dostępnych powiadomień |
| -144 | Nie znaleziono transakcji |
| -145 | Odblokowanie nie jest obsługiwane w trybie wielu użytkowników |
| -146 | Konto już odblokowane do wydobywania |
| -147 | Konto już odblokowane dla transakcji |
| -148 | Konto już odblokowane |
| -149 | Nieprawidłowy PIN |
| -150 | Transakcja odrzucona |
| -151 | Transakcja już w bazie danych |
| -152 | Transakcja nie zawiera ważnych przelewów |
| -153 | Nie znaleziono obiektu odbiorcy transferu |
| -154 | Nieprawidłowy typ pola (field) |
| -155 | Surowe zasoby nie mogą być aktualizowane |
| -156 | Nie znaleziono pola w zasobie (field) |
| -157 | Pole niezmienialne w zasobie (field) |
| -158 | Wartość dłuższa niż maksymalna długość (field) |
| -159 | Wartości muszą być przekazywane jako ciągi |
| -160 | Nazwa użytkownika zawiera nieprawidłowe znaki |
| -161 | Nazwa zawiera nieprawidłowe znaki |
| -162 | Przestrzeń nazw może zawierać tylko małe litery, cyfry, kropki (.) |
| -163 | Nie można pobrać domyślnego konta NXS do obciążania opłat |
| -164 | Konto opłat nie jest kontem NXS |
| -165 | Nieprawidłowy address/name\_to
| -166 | Konto to konto NXS. Aby uzyskać dostęp do kont NXS, użyj interfejsu API finansów. |
| -167 | Nieprawidłowe odniesienie |
| -168 | Nieprawidłowy czas wygaśnięcia |
| -169 | Nazwy nie mogą zaczynać się od dwukropka |
| -170 | Nie można tworzyć nazw globalnych w przestrzeni nazw |
| -171 | Nazwy globalne nie mogą zawierać dwukropka |
| -172 | Nie można unieważnić transakcji, która nie należy do Ciebie |
| -173 | Nie można unieważnić transakcji debetowej, ponieważ została już w pełni uznana przez wszystkich odbiorców |
| -174 | Transakcja nie zawiera umów, które można unieważnić |
| -175 | Nieprawidłowa ilość podaży. Podaż musi być liczbą całkowitą |
| -176 | Nieprawidłowa ilość podaży. Maksymalna podaż tokenów to 18446744073709551615 |
| -177 | Nieprawidłowa kwota dziesiętna. Ułamki dziesiętne muszą być wartościami całkowitymi z zakresu od 0 do 8 |
| -178 | Nieprawidłowa podaż/miejsca dziesiętne. Maksymalna podaż/miejsca dziesiętne nie może przekroczyć 18446744073709551615 |
| -179 | Portfel Legacy jest zablokowany. wymagane hasło portfela |
| -180 | Nieprawidłowe hasło do portfela Legacy |
| -181 | Nie znaleziono klucza Trust dla portfela Legacy |
| -182 | Klucz Trust wcześniej migrowany |
| -183 | Poprzednia transakcja dotycząca stawki niedojrzała |
| -184 | Poprzednia transakcja dotycząca stawki nie jest transakcją odziedziczoną |
| -185 | Poprzednia transakcja nie jest transakcją dotyczącą stawki |
| -186 | Poprzednia stawka nie należy do obecnego portfela |
| -187 | Nie udało się uzyskać adresów dla portfela Legacy |
| -188 | Konto Trust ma już genezę |
| -189 | Konto Trust ma już stake |
| -190 | Konto Trust ma już zaufanie |
| -191 | Nazwa użytkownika musi mieć co najmniej 2 znaki |
| -192 | Hasło musi mieć minimum 8 znaków |
| -193 | Pin musi mieć co najmniej 4 znaki |
| -194 | Konto już odblokowane dla powiadomień |
| -195 | Konto już odblokowane do stakowania |
| -196 | Konto już zablokowane do wydobywania |
| -197 | Konto już zablokowane do stakowania |
| -198 | Konto już zablokowane dla transakcji
| -199 | Konto już zablokowane dla powiadomień |
| -200 | Nie można utworzyć przestrzeni nazw z zarezerwowaną nazwą |
| -201 | Nie można tworzyć nazw globalnych z zarezerwowaną nazwą |
| -202 | Łańcuch podpisów nie dojrzał po poprzednim bloku kopania/stawek. Wymagane jest X więcej potwierdzeń. |
| -203 | Nie znaleziono użytkownika automatycznego logowania |
| -204 | Nie można ustawić stawki na ujemną kwotę |
| -205 | Nie można pobrać ostatniej stawki |
| -206 | Nie udało się usunąć wygasłego żądania zmiany stawki |
| -207 | Nie udało się usunąć poprzedniego żądania zmiany stawki |
| -208 | Nie udało się zapisać żądania zmiany stawki |
| -209 | Odbiorca nie jest prawidłowym kontem |
| -210 | Konto odbiorcy jest dla innego tokena |
| -211 | Obiekt odbiorcy nie został tokenizowany |
| -212 | Nieprawidłowy token |
| -213 | Nie można tworzyć transakcji podczas synchronizacji |
| -214 | Niewystarczające środki na uiszczenie opłaty |
| -215 | Przekroczono maksymalną liczbę odbiorców (99) |
| -216 | pole adresatów musi być tablicą |
| -217 | tablica adresatów jest pusta |
| -218 | Hasło użytkownika / kod PIN nie zostały zmienione |
| -219 | Nie można pobrać obiektu Crypto |
| -220 | Brakująca fraza odzyskiwania |
| -221 | Fraza muszą mieć co najmniej 40 znaków |
| -222 | Utworzenie użytkownika oczekuje na potwierdzenie |
| -223 | Fraza nie są ustawione w tym łańcuchu sygnatur |
| -224 | Brak opisu |
| -225 | Brak numeru |
| -226 | Brak odniesienia |
| -227 | Brak nazwy/adresu rachunku płatniczego |
| -228 | Brak szczegółów nadawcy |
| -229 | Brak odbiorcy |
| -230 | Użytkownik odbiorcy nie istnieje |
| -231 | Brak danych odbiorcy
| -232 | Brakujące pozycje |
| -233 | Faktura musi zawierać co najmniej jedną pozycję |
| -234 | Brak opisu przedmiotu |
| -235 | Brak ilości jednostek pozycji |
| -236 | Nieprawidłowa ilość jednostki pozycji |
| -237 | Kwota jednostki pozycji musi być większa niż 0 |
| -238 | Brakująca liczba sztuk jednostek |
| -239 | Nieprawidłowa liczba sztuk jednostek |
| -240 | Jednostki pozycji muszą być większe niż 0 |
| -241 | Nie znaleziono faktury |
| -242 | Dane pod tym adresem nie są fakturą |
| -242 | Dane przekraczają maksymalny rozmiar rejestru |
| -243 | Dane pod tym adresem nie są pozycją zaopatrzenia |
| -244 | Nie można wysłać faktury do siebie |
| -245 | Nie można \[action] faktury, która została już zapłacona |
| -246 | Nie można \[action] faktury, która została już anulowana |
| -247 | Nie można znaleźć transakcji przeniesienia faktury |
| -248 | ------------------------- |
| -249 | ------------------------- |
| -250 | Faktura nie należy do Ciebie |
| -251 | Brak nazwiska lub adresu z |
| -252 | Konto obciążane nie dotyczy wymaganego tokena |
| -254 | ------------------------------- |
| -255 | Nie można przetwarzać powiadomień, dopóki peery nie są połączone |
| -256 | Nie można przetwarzać powiadomień podczas synchronizacji |
| -257 | Walidacja kontraktu nie powiodła się |
| -258 | Nieznana geneza |
| -259 | Musisz określić co najmniej jedną akcję odblokowania |
| -260 | Nieprawidłowa nazwa klucza |
| -261 | Klucz już istnieje |
| -262 | Nieprawidłowy schemat |
| -263 | Klucze prywatne nie mogą być odzyskane tylko dla kluczy w rejestrze kryptograficznym |
| -264 | Klucz nie został jeszcze utworzony
| -265 | Brak klucza publicznego |
| -266 | Źle sformatowany klucz publiczny |
| -267 | Szyfrowanie kluczem wspólnym obsługiwane tylko dla kluczy EC (Brainpool) |
| -268 | Nie udało się wygenerować klucza współdzielonego |
| -269 | Źle sformatowany klucz prywatny |
| -270 | Nie udało się zaszyfrować danych |
| -271 | Nie udało się odszyfrować danych |
| -272 | Nieobsługiwany typ klucza |
| -273 | Nie udało się wygenerować podpisu |
| -274 | Brak podpisu |
| -275 | Brakujący schemat |
| -276 | Błąd generowania skrótu |
| -277 | Nieprawidłowa funkcja skrótu |
| -278 | Program już w użyciu |
| -279 | Nie znaleziono żądania P2P |
| -280 | Serwer P2P nie jest włączony na tym węźle |
| -281 | Brak identyfikatora aplikacji |
| -282 | Nie znaleziono połączenia |
| -283 | Połączenie z tym peerem już istnieje |
| -284 | Nie udało się połączyć z peerem |
| -285 | Brak dostępnych wiadomości |
| -286 | Limit czasu oczekiwania na zaakceptowanie żądania połączenia przez peera |
| -287 | Metoda API nie jest obsługiwana w trybie wielu użytkowników |
| -288 | Nie można odblokować do kopania w trybie wielu użytkowników |
| -289 | Nie można odblokować do stakowania w trybie wielu użytkowników |
| -290 | Nieprawidłowe poświadczenia. Użytkownik wylogował się z powodu zbyt wielu prób podania hasła / kodu PIN |
| -291 | Klucza certyfikatu nie można użyć do utworzenia pary kluczy, ponieważ jest on zarezerwowany dla certyfikatu TLS. Zamiast tego użyj metody API tworzenia/certyfikowania. |
| -292 | Klucza certyfikatu nie można używać do podpisywania danych, ponieważ jest on zarezerwowany dla certyfikatu TLS |
| -293 | Nieprawidłowa nazwa klucza. Klucze w rejestrze kryptograficznym nie mogą być używane do szyfrowania, tylko generowanie i weryfikacja podpisu |
| -294 | Certyfikat nie został jeszcze utworzony dla tego łańcucha podpisów. Proszę użyć crypto/create/key, aby najpierw utworzyć certyfikat |
| -295 | Niezgodność klucza publicznego. Nie można wygenerować certyfikatu |
| -296 | Brak certyfikatu |
| -297 | Nie można się zalogować podczas synchronizacji
| -300 | API może być używane tylko do wyszukiwania danych dla aktualnie zalogowanego łańcucha sygnatur podczas pracy w trybie klienta |
| -301 | gdzie pole musi być tablicą |
| -302 | Brak pola, w którym klauzula |
| -303 | Brak opcji, w której klauzula |
| -304 | Brak wartości w klauzuli gdzie |
| -305 | Nieznany operand, w którym klauzula |
| -306 | Brak dostępnych połączeń |
| -307 | Nie udało się pobrać łańcucha podpisów |
| -308 | Metoda API dostępna tylko w trybie klienta |
| -309 | Błąd ładowania sesji |
| -310 | Nie można wysłać do WSZYSTKICH kont |


