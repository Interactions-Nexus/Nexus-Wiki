---
title: PROFILE
description: Profile API
published: true
date: 2022-11-01T23:32:05.745Z
tags: 
editor: markdown
dateCreated: 2022-10-24T22:21:17.033Z
---

# PROFILE

Interfejs Profiles API udostępnia metody tworzenia profili i zarządzania nimi. Profil jest synonimem łańcucha podpisów. W pełni obsługiwany punkt końcowy identyfikatorów URI profili jest następujący:

```
profiles/verb/noun/filter/operator
```

Minimalne wymagane składniki identyfikatora URI to:

```
profiles/verb/noun
```

## `Obsługiwane czasowniki`

[`create`](broken-reference) - Generuj nowy obiekt obsługiwanego typu.\
[`update`](broken-reference) - Aktualizuje określone rejestry obiektów.\
[`recover`](broken-reference) - Odzyskuje konto profilu.\
[`status`](broken-reference) — Informacje o stanie profilu.\
[`notifications`](broken-reference) - Lista wszystkich powiadomień, które zmodyfikowały określony obiekt.\
[`transactions`](broken-reference) — Lista wszystkich transakcji, które zmodyfikowały określony obiekt.

## `Obsługiwane rzeczowniki`

W tym zestawie poleceń interfejsu API obsługiwane są następujące rzeczowniki:

\[`master`] — domyślny profil, który kontroluje wszystkie podprofile.\
\[`auth`] - Rejestr obiektów kryptograficznych do uwierzytelniania logowania.\
\[`credentials`] — poświadczenia używane do zabezpieczania profili.\
\[`recovery`] — obiekt reprezentujący odzyskiwanie profilu.

## `create` <a href="#user-content-create" id="user-content-create"></a>

Spowoduje to utworzenie nowego profilu lub zainicjowanie klucza uwierzytelniania dla starszych łańcuchów podpisów, aby były one kompatybilne z profilami określonymi przez rzeczownik.

```
profiles/create/noun
```

To polecenie obsługuje tylko rzeczowniki `master` i `auth`.

#### **utwórz/master**

Spowoduje to utworzenie nowego profilu określonego przez podany rzeczownik. Profil jest zabezpieczony kombinacją „nazwy użytkownika”, „hasła” i „kodu PIN”.

#### **utwórz/uwierzytelnij**

Ta metoda zainicjuje rejestr obiektów kryptograficznych `auth` dla łańcuchów podpisów utworzonych we wczesnej wersji Tritium. To sprawia, że ​​ten łańcuch sygnatur jest kompatybilny z profilami na Tritium++. Obecni użytkownicy mogą być zmuszeni do przekonwertowania swoich starych łańcuchów podpisów, aby były zgodne z logowaniem za pomocą profili Tritium++, jeśli nie są w stanie utworzyć sesji.

### Parametry:

`username` : Wymagane do **utworzenia** nazwy użytkownika. Nazwa użytkownika do powiązania z tym profilem. ProfileID (używane do jednoznacznej identyfikacji profili) to skrót tej nazwy użytkownika, dlatego nazwa użytkownika musi być unikalna w łańcuchu bloków.

`password` : Wymagane do **ustawienia** hasła. Hasło, które ma być powiązane z tym profilem.

`pin` : Wymagany do **ustawienia** pinu. Kod PIN, który ma być powiązany z tym profilem

**NOTATKA:**

* `nazwa użytkownika` musi mieć co najmniej 2 znaki.
* `hasło` musi mieć co najmniej 8 znaków.
* „PIN” musi mieć co najmniej 4 znaki.
* w nazwie użytkownika rozróżniana jest wielkość liter i nie można jej zmienić. Ostrożnie wybierz nazwę użytkownika i zrób jej kopię zapasową wraz z hasłem i kodem PIN.
* Nie używaj dwukropka „:” na końcu nazwy użytkownika.

### Wyniki:

#### **Zwrócona wartość obiektu JSON:**

```
{
    "success": true,
    "txid": "01d872456b966a14796d80f1687fe59a107fe6c3b6edd3558dce146d08f3093837136634022734d9d9b5e877311fd68f847f226ae276a12b8bc3f246513ccd08"
}
```

#### **Zwracane wartości:**

`success` : flaga logiczna wskazująca, że profil został pomyślnie utworzony.

`txid` : Identyfikator (hash) transakcji, która zawiera utworzony obiekt.

## `update` <a href="#user-content-update" id="user-content-update"></a>

Ta metoda zapewnia użytkownikowi możliwość zmiany hasła, kodu PIN lub źródła odzyskiwania dla profilu określonego przez rzeczownik.

```
profiles/update/noun
```

To polecenie obsługuje tylko rzeczowniki `credentials` i `recovery`.

#### **aktualizacja/poświadczenia**

Ta metoda zapewnia użytkownikowi możliwość zmiany hasła, pinu dla tego łańcucha podpisów. Aktualizacja poświadczeń spowoduje również zregenerowanie każdego z kluczy w obiekcie Crypto łańcucha sig na podstawie nowego hasła / kodu PIN.

#### **aktualizacja/odzyskiwanie**

Ta metoda zapewnia użytkownikowi możliwość ustawienia lub zmiany źródła przywracania dla tego łańcucha sygnatur.

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` w celu zidentyfikowania profilu użytkownika.

`hasło` : Wymagane do **uwierzytelnienia**. Istniejące hasło dla tego łańcucha podpisów.

`pin` : Wymagane, jeśli **zablokowane**. Kod PIN do autoryzacji transakcji.

#### **aktualizacja/poświadczenia**

`new_password` : Wymagane przez rzeczownik **credentials**. Nowe hasło do ustawienia dla tego łańcucha podpisów. Jest to opcjonalne, jeśli podano nowy\_pin

`new_pin` : Wymagane przez rzeczownik **poświadczenia**. Nowa szpilka do ustawienia dla tego sygnowanego łańcuszka. Jest to opcjonalne, jeśli podano `nowe_hasło`.

#### **aktualizacja/odzyskiwanie**

`recovery` : Wymagane przez rzeczownik **recovery** Istniejące ziarno odzyskiwania dla tego łańcucha sygnatur. Jest to wymagane tylko wtedy, gdy istniejące źródło odzyskiwania jest aktualizowane za pomocą new\_recovery.

`new_recovery` : Wymagane przez rzeczownik **recovery**. Nowe ziarno odzyskiwania do ustawienia lub zmiany dla tego łańcucha sig. Ziarno odzyskiwania musi mieć co najmniej 40 znaków.

**UWAGA:** w frazie odzyskiwania rozróżniana jest wielkość liter. Pamiętaj, aby poprawnie wpisać frazę odzyskiwania i nie kopiować wklejania, co może dodawać spacje, jeśli nie zostanie wykonane poprawnie. Upewnij się, że wykonałeś kopię zapasową i ponownie sprawdź źródło odzyskiwania oraz utwórz wiele kopii zapasowych w trybie offline.

### Wyniki:

#### **Zwrócona wartość obiektu JSON:**

```
{
    "success": true,
    "txid": "01947f824e9b117d618ed49a7dd84f0e7c4bb0896e40d0a95e04e27917e6ecb6b9a5ccfba7d0d5c308b684b95e98ada4f39bbac84db75e7300a09befd1ac0999"
}
[Completed in 18533.182336 ms]
```

#### **Zwracane wartości:**

`success` : flaga logiczna wskazująca, że profil został pomyślnie zaktualizowany. `txid` : Identyfikator (hash) transakcji dla zaktualizowanego profilu .

## `recover` <a href="#user-content-recover" id="user-content-recover"></a>

To przywraca profil określony przez rzeczownik w przypadku utraty hasła i kodu PIN. Użytkownik musi się wylogować, aby odzyskać swój profil.

```
profiles/recover/noun
```

To polecenie obsługuje tylko rzeczownik `master`.

### Parametry:

`nazwa_użytkownika` : Wymagana do **identyfikacji**. Nazwa użytkownika identyfikująca profil do odzyskania.

`password` : Wymagane do **ustawienia** nowego hasła. Nowe hasło do skojarzenia z tym profilem.

`pin` : Wymagany do **ustawienia** nowego pinu. Nowy kod PIN do powiązania z tym profilem.

`odzyskiwanie` : Wymagane do **uwierzytelnienia**. Istniejący ziarno odzyskiwania dla tego profilu.

### Wyniki:

#### **Zwrócona wartość obiektu JSON:**

```
{
    "success": true,
    "txid": "017fbb86583c0e15c0fb994a1f4c70d97f2c084533748ccfd25cd36e5aef9c2e7f89f15f2ec9f2d73769fef9d7a8a28cd018c9907ebf1bf74e4f89837c900091"
}
[Completed in 15242.801822 ms]
```

#### **Zwracane wartości:**

`success` : flaga logiczna wskazująca, że profil został pomyślnie odzyskany.

`txid` : Identyfikator (hash) transakcji dla odzyskanego obiektu.

## `status` <a href="#status-treści-użytkownika" id="status-treści-użytkownika"></a>

Zwraca informacje o stanie dla żądanego profilu.

```
profiles/status/noun
```

To polecenie obsługuje tylko rzeczownik `master`.

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` w celu zidentyfikowania profilu użytkownika.

### Wyniki:

#### **Zwrócona wartość obiektu JSON:**

```
{
    "genesis": "b7fa11647c02a3a65a72970d8e703d8804eb127c7e7c41d565c3514a4d3fdf13",
    "confirmed": true,
    "recovery": true,
    "crypto": true,
    "transactions": 10
}
[Completed in 0.108500 ms]
```

#### **Zwracane wartości:**

`geneza` : To jest skrót nazwy użytkownika profilu, znany również jako skrót właściciela.

`confirmed` : flaga logiczna wskazująca, czy transakcja genezy dla tego profilu ma co najmniej jedno potwierdzenie.

`recovery` : flaga wskazująca, czy dla tego profilu ustawiono ziarno odzyskiwania.

`crypto` : Flaga wskazująca, czy rejestr obiektów kryptograficznych został ustawiony dla tego profilu.

`transakcje` : Łączna liczba transakcji dla tego profilu

## `notifications` <a href="#user-content-notifications" id="user-content-notifications"></a>

Spowoduje to wyświetlenie listy wszystkich transakcji wysłanych do określonego łańcucha podpisów. Jest to przydatne do identyfikowania transakcji, które musisz zaakceptować, takich jak kredyty.

```
profiles/notifications/noun
```

To polecenie obsługuje tylko rzeczownik `master`.

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` w celu zidentyfikowania profilu użytkownika.

Ta metoda obsługuje parametry sortowania/filtrowania.

### Wyniki:

#### **Zwrócona wartość obiektu JSON:**

```
[
    {
        "id": 0,
        "OP": "DEBIT",
        "from": "8EW4ALiZxtiRHFGqND5Yah8oYiRaXBLEHBcrovshCDLT1ZE5ENk",
        "to": "8C96zrYqeyYYiRDQ9pWZkxgzMhmV7nxDUEeE8fBCufgWfJ4cnJ1",
        "amount": 150.0,
        "token": "8EW4ALiZxtiRHFGqND5Yah8oYiRaXBLEHBcrovshCDLT1ZE5ENk",
        "ticker": "NEX",
        "reference": 0,
        "timestamp": 1654620671,
        "txid": "012e6dc669cad475b0974308ba719bf5d69c0d7623e31399a3d83ca8e095b63ed7ac98709c08a5a15c543dd91c85c7cbb91082c355fa548435545cfb1b912a8f"
    }
]
[Completed in 0.256792 ms]
```

#### **Zwracane wartości:**

`id` : Identyfikator sekwencyjny tej transakcji.

`OP` : Operacja kontraktu. Może być COINBASE, DEBIT, FEE, TRANSFER.

`txid` : Transakcja, która została uznana / zgłoszona.

`suppressed`: Jeśli wywołujący dołączył opcjonalną flagę pominiętych, odpowiedź będzie zawierać to pole, aby wskazać, czy to powiadomienie jest aktualnie pomijane, czy nie.

`from` : Dla transakcji DEBIT, adres rejestru konta, z którego dokonywany jest debet.

`from_name` : W przypadku transakcji DEBIT nazwa konta, z którego dokonywany jest debet. Uwzględniane tylko wtedy, gdy nazwa może zostać rozwiązana.

`to` : W przypadku transakcji DEBIT, adres rejestru konta, na które dokonywany jest debet.

`to_name` : W przypadku transakcji DEBIT nazwa konta, na które jest dokonywany debet. Uwzględniane tylko wtedy, gdy nazwa może zostać rozwiązana.

`amount` : kwota tokena transakcji.

`token` : adres rejestru tokena, którego dotyczy transakcja. Ustaw na 0 dla transakcji NXS

`ticker` : nazwa tokena, którego dotyczy transakcja.

`referencja` : W przypadku transakcji DEBIT jest to referencja podana przez użytkownika, używana przez odbiorcę do powiązania transakcji z numerem zamówienia lub faktury.

`dowód` : adres rejestru konta tokena potwierdzającego debet z tytułu dywidendy podzielonej.

`dividend_payment` : flaga wskazująca, że ​​to obciążenie jest wypłatą dywidendy podzielonej na tokenizowany zasób

## `transakcje` <a href="#transakcje-zawartości-użytkownika" id="transakcje-zawartości-użytkownika"></a>

Spowoduje to wyświetlenie wszystkich transakcji dla żądanego profilu.

```
profiles/transactions/noun
```

To polecenie obsługuje tylko rzeczownik `master`.

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` do określenia sesji użytkownika, która tworzy transakcję.

`verbose` : opcjonalny, **określa**, ile danych transakcji należy uwzględnić w odpowiedzi. Obsługiwane wartości to:

* `domyślny` : hash
* `podsumowanie` : typ, wersja, kolejność, znacznik czasu, operacja i potwierdzenia.
* `detail` : geneza, nexthash, prevhash, pubkey i sygnatura.

Ta metoda obsługuje parametry sortowania/filtrowania.

### Wyniki:

#### **Zwrócona wartość obiektu JSON:**

```
[
    {
        "txid": "01eb59a0c4e6c47dd2a8d3a4aa7d83514aab6f5c976207889f786e5947c0eb971065fe6e0f8fc6b7d75157f9dac0cf0c178c15e441ff360c3046c84e1fe799ca",
        "type": "tritium first",
        "version": 4,
        "sequence": 0,
        "timestamp": 1653674591,
        "blockhash": "dc2712f6598a4a8c60f14c707dae4705f773fb1f60b89efd1e0163ee1d7cf823e8d73e6a3fb9f7eb73e72d7764647eb889abebc2aca34f3090dbe1409af511a301409fb8f04409bf97693dc0d908d05d9b62b949aae423196b508b3840419d1df548e72e006c75a6c69d8075693f2c8f6f7d10213a07c03bf9ff250e55a1eeef",
        "confirmations": 23,
        "contracts": [
            {
                "id": 0,
                "OP": "CREATE",
                "address": "89AVoe5S8gjZpVngYoYtqJbSr9fGsdsoXShxnyNaEGPvMMeDnT6",
                "type": "OBJECT",
                "standard": "CRYPTO",
                "object": {
                    "app1": "0000000000000000000000000000000000000000000000000000000000000000",
                    "app2": "0000000000000000000000000000000000000000000000000000000000000000",
                    "app3": "0000000000000000000000000000000000000000000000000000000000000000",
                    "auth": "02b5dbda57225afab10ca271ff513beab748306cff028798e2b64505db59f252",
                    "cert": "0000000000000000000000000000000000000000000000000000000000000000",
                    "lisp": "0000000000000000000000000000000000000000000000000000000000000000",
                    "network": "025193caf52ce6065951a438d30696f7548e12e0ebadd60359141029c1c4d870",
                    "sign": "02efc8e11c7097520080718b5dd0e92267292401678fcecb317bde79df64311c",
                    "verify": "0000000000000000000000000000000000000000000000000000000000000000"
                }
            }
        ]
    }
]
[Completed in 0.616625 ms]
```

#### **Zwracane wartości:**

`txid` : skrót transakcji.

`typ` : Opis transakcji (starsza | baza trytu | zaufanie | geneza | użytkownik).

`wersja` : wersja serializacji transakcji.

`sequence` : Numer kolejny tej transakcji w łańcuchu podpisów.

`timestamp` : Uniksowy znacznik czasu utworzenia transakcji.

`blockhash` : Hash bloku, w którym zawarta jest ta transakcja. Pusty, jeśli nie został jeszcze uwzględniony w bloku.

`confirmations` : Liczba potwierdzeń uzyskanych przez tę transakcję przez sieć.

`geneza` : To jest skrót nazwy użytkownika profilu, znany również jako skrót właściciela.

`nexthash` : Hash następnej transakcji w sekwencji.

`prevhash` : hash poprzedniej transakcji w sekwencji.

`pubkey` : klucz publiczny.

`podpis` : skrót podpisu.

`contracts` : Tablica kontraktów powiązanych z tą transakcją oraz ich szczegóły z kodami operacyjnymi.\
{\
`id` : Identyfikator sekwencyjny tego kontraktu w ramach transakcji.

`OP` : Operacja kontraktu. Może być DODATEK, ROSZCZENIE, COINBASE, UTWÓRZ, KREDYT, DEBET, OPŁATA, GENESIS, DZIEDZICTWO, PRZELEW, ZAUFANIE, STAWKA, ODSTAWIANIE, NAPISZ.

„for” : dla transakcji KREDYTOWYCH, kontrakt, dla którego utworzono ten kredyt . Może być COINBASE, DEBIT lub LEGACY.

`txid` : Transakcja, która została uznana / zgłoszona.

„kontrakt” : Identyfikator kontraktu w ramach transakcji, która została uznana / zgłoszona.

`dowód`: adres rejestru potwierdzający kredyt.

`from` : Dla transakcji DEBIT, KREDYT, OPŁATY adres rejestrowy konta, z którego dokonywany jest debet.

`from_name` : W przypadku transakcji DEBIT, KREDYT, OPŁATY nazwa rachunku, z którego dokonywany jest debet. Uwzględniane tylko wtedy, gdy nazwa może zostać rozwiązana.

`to` : W przypadku transakcji DEBIT i KREDYT adres rejestru konta odbiorcy.

`to_name` : W przypadku transakcji DEBIT i KREDYT nazwa konta odbiorcy. Uwzględniane tylko wtedy, gdy nazwa może zostać rozwiązana.

`amount` : kwota tokena transakcji.

`token` : adres rejestru tokena, którego dotyczy transakcja. Ustaw na 0 dla transakcji NXS

`token_name` : nazwa tokena, którego dotyczy transakcja.

`referencja` : W przypadku transakcji DEBIT i KREDYT jest to referencja podana przez użytkownika, używana przez odbiorcę do powiązania transakcji z numerem zamówienia lub faktury.

`object` : Zwraca listę wszystkich zaszyfrowanych kluczy publicznych w rejestrze obiektów kryptograficznych dla określonego profilu. Wynik obiektu będzie zawierał dziewięć domyślnych kluczy (app1, app2, app3, auth, cert lisp, network, sign i weryfikacji).\
}