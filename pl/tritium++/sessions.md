---
title: SESJE
description: API sesji
published: true
date: 2022-11-03T23:18:49.377Z
tags: 
editor: markdown
dateCreated: 2022-10-24T22:22:46.231Z
---

# SESJE

Session API udostępnia metody tworzenia sesji i zarządzania nimi. Sesja jest równoznaczna z logowaniem użytkownika do łańcucha sygnatur. W pełni obsługiwany punkt końcowy identyfikatora URI sesji jest następujący:

```
sessions/verb/noun
```

Minimalne wymagane składniki identyfikatora URI to:

```
sessions/verb/noun
```
---
&nbsp;

## Obsługiwane czasowniki (verbs)

Następujące czasowniki są obecnie obsługiwane przez ten zestaw poleceń interfejsu API:

[`create`](#create) - Generuj nowy typ sesji określony przez rzeczownik.\
[`unlock`](#unlock) - Odblokuj sesję, aby wykonać określone operacje.\
[`lock`](#lock) - Zablokuj sesję, aby zatrzymać określone operacje.\
[`save`](#save) - Zapisz określoną sesję w lokalnej bazie danych.\
[`load`](#load) - Załaduj określoną sesję z lokalnej bazy danych.\
[`terminate`](#terminate) - Kończy sesję określoną przez rzeczownik.\
[`status`](#status) — Zwraca informacje o stanie sesji określonej przez rzeczownik.

---
&nbsp;

## Obsługiwane rzeczowniki (nouns)

W tym zestawie poleceń interfejsu API obsługiwane są następujące rzeczowniki:

`local` — Lokalizacja sesji.

---
&nbsp;

## create <a href="#create" id="create"></a>

Utwórz nową sesję określoną przez podany rzeczownik.

```
sessions/create/noun
```

To polecenie obsługuje tylko rzeczownik `local`.

### Parametry:

`username` : Wymagane do **identyfikacji** profilu, dla którego ma zostać utworzona sesja.

`password` : Wymagane do **uwierzytelnienia** hasła do utworzenia sesji.

`pin` : Wymagany do **uwierzytelnienia** `PIN` do utworzenia sesji.

### Wyniki:

#### Zwracana wartość obiektu JSON:

```
{
    "genesis": "b7fa11647c02a3a65a72970d8e703d8804eb127c7e7c41d565c3514a4d3fdf13",
    "session": "0aad63e028dd9e0f31f0b566831fea9dfc7db68fc2ba482a8ce975656971a67e"
}
[Completed in 1659.509829 ms]
```

#### Zwracane wartości:

`genesis` : To jest hash nazwy użytkownika profilu, znany również jako hash właściciela.

`session` : Podczas korzystania z trybu API wielu użytkowników, zwracana jest dodatkowa wartość sesji, która musi być podana w kolejnych wywołaniach API, aby umożliwić zarządzanie wieloma sesjami logowania.

---
&nbsp;

## unlock <a href="#unlock" id="unlock"></a>

Spowoduje to odblokowanie sesji określonej przez dany rzeczownik i buforowanie kodu PIN w zaszyfrowanej pamięci, który będzie używany do wszystkich kolejnych wywołań API dla określonych operacji.

```
sessions/unlock/noun
```

Te polecenia obsługują tylko rzeczownik `local`.

### Parametry:

`pin` : Wymagany do **uwierzytelnienia**. Kod PIN tego profilu.

`session` : Wymagane przez **argument** `-multiuser=1` w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika nie należy podawać sesji.

`mining` : Wymagane do **odblokowywania** transakcji kopania. Ta wartość logiczna odblokowuje sesję do wydobywania.

`notifications` : Wymagane do **odblokowywania** powiadomień. Ta wartość logiczna odblokowuje sesję w celu automatycznego przetwarzania przychodzących powiadomień.

`staking` : Wymagane do **odblokowywania** transakcji stakowania. Ta wartość logiczna odblokowuje sesję do stakowania.

`transactions` : Wymagane do **odblokowywania** transakcji. Ta wartość logiczna odblokowuje sesję, aby umożliwić tworzenie lub zgłaszanie transakcji.

### Zwroty:

#### Zwracana wartość obiektu JSON:

```
{
    "unlocked": {
        "mining": false,
        "notifications": true,
        "staking": true,
        "transactions": false
    }
}
[Completed in 1664.238652 ms]
```

#### Zwracane wartości:

`unlocked` : Zawiera elementy potomne opisujące, dla których funkcji sesja jest aktualnie odblokowana.

`mining` : Flaga logiczna wskazująca, czy łańcuch sygnatur użytkowników jest odblokowany do kopania.

`notifications` : Flaga logiczna wskazująca, czy łańcuch sygnatur użytkowników jest odblokowany do przetwarzania powiadomień.

`staking` : Flaga logiczna wskazująca, czy łańcuch sygnatur użytkowników jest odblokowany do stakowania.

`transactions` : Flaga logiczna wskazująca, czy łańcuch sygnatur użytkowników jest odblokowany do tworzenia jakichkolwiek transakcji (z wyjątkiem tych tworzonych automatycznie przez powiadomienia o wydobywaniu/przetwarzaniu, jeśli są one odblokowane).

---
&nbsp;

## lock <a href="#lock" id="lock"></a>

Spowoduje to zablokowanie określonej sesji poprzez wyczyszczenie kodu PIN przechowywanego w zaszyfrowanej pamięci, uniemożliwiając korzystanie z niego, chyba że zostanie odblokowany lub kod PIN zostanie przekazany do wszystkich żądań API.

```
sessions/lock/noun
```

Te polecenia obsługują tylko rzeczownik `local`.

### Parametry:

`pin` : Wymagany do **uwierzytelnienia**. Kod PIN tego profilu.

`session` : Wymagane przez **argument** `-multiuser=1` w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika nie należy podawać sesji.

`mining` : Wymagane do **blokowania** transakcji kopania. Ta wartość logiczna blokuje sesję do wydobywania.

`notifications` : Wymagane do **blokowania** powiadomień. Ta wartość logiczna blokuje sesję przed przetwarzaniem powiadomień przychodzących.

`staking` : Wymagane do **blokowania** transakcji tyczenia. Ta wartość logiczna blokuje sesję do stakowania.

`transactions` : Wymagane do **blokowania** transakcji. Ta wartość logiczna blokuje sesję tworzenia lub zgłaszania transakcji.

### Zwroty:

#### Zwracana wartość obiektu JSON:

```
{
    "unlocked": {
        "mining": false,
        "notifications": true,
        "staking": true,
        "transactions": false
    }
}
[Completed in 1664.238652 ms]
```

#### Zwracane wartości:

`unlocked` : Zawiera elementy potomne opisujące, dla których funkcji sesja jest aktualnie odblokowana

`mining` : Flaga logiczna wskazująca, czy łańcuch sygnatur użytkowników jest odblokowany do kopania.

`notifications` : Flaga logiczna wskazująca, czy łańcuch sygnatur użytkowników jest odblokowany do przetwarzania powiadomień.

`staking` : Flaga logiczna wskazująca, czy łańcuch sygnatur użytkowników jest odblokowany do stakowania.

`transactions` : Flaga logiczna wskazująca, czy łańcuch sygnatur użytkowników jest odblokowany do tworzenia jakichkolwiek transakcji (z wyjątkiem tych tworzonych automatycznie przez powiadomienia o wydobywaniu/przetwarzaniu, jeśli są one odblokowane).

---
&nbsp;

## save <a href="#save" id="save"></a>

Spowoduje to zapisanie sesji użytkownika w lokalnej bazie danych, umożliwiając wznowienie sesji w późniejszym czasie bez konieczności logowania lub odblokowywania. Kod PIN użytkownika jest wymagany, ponieważ jest używany (w połączeniu z genezą) do szyfrowania danych sesji przed utrwaleniem ich w lokalnej bazie danych.

```
sessions/save/noun
```

Te polecenia obsługują tylko rzeczownik `local`.

**NOTATKA:**

* Zapisz sesję, zapisuje określoną aktywną sesję na dysku lokalnym.
* Zapisane sesje są zapisywane na stałe, dopóki nie zostaną usunięte ręcznie.
* Zapisane sesje zostaną wznowione w tym samym stanie (zablokowane lub odblokowane), w jakim zostały zapisane.

### Parametry:

`pin` : Wymagane do **uwierzytelnienia**. Kod PIN tego profilu.

`session` : Wymagane przez **argument** `-multiuser=1` w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika nie należy podawać sesji.

### Wyniki:

#### Zwracana wartość obiektu JSON:

```
{
    "genesis": "b7fa11647c02a3a65a72970d8e703d8804eb127c7e7c41d565c3514a4d3fdf13",
    "success": true
}
[Completed in 2.962459 ms]
```

#### Zwracane wartości:

`genesis` : To jest hash nazwy użytkownika profilu, znany również jako hash właściciela.

`success` : Flaga logiczna wskazująca, że sesja została pomyślnie zapisana.

---
&nbsp;

## load <a href="#load" id="load"></a>

Spowoduje to wznowienie zapisanej sesji z lokalnej bazy danych, umożliwiając wznowienie zapisanej sesji bez konieczności logowania lub odblokowania. Nazwa użytkownika profilu lub geneza i PIN są wymagane do odszyfrowania i wznowienia zapisanej sesji.

```
sessions/load/noun
```

Te polecenia obsługują tylko rzeczownik `local`.

**NOTATKA:**

* Jeśli istnieje aktywna sesja, nie zostanie załadowana zapisana sesja.
* Można załadować tylko wcześniej zapisaną sesję.
* Po wznowieniu zapisanej sesji tworzy nowy identyfikator sesji.
* Zapisane sesje można wznowić nawet po ponownym uruchomieniu rdzenia lub węzła.

### Parametry:

`pin` : Wymagany, jeśli **uwierzytelniamy**. Kod PIN tego profilu.

`username`: Wymagany do **identyfikacji** profilu, dla którego ma zostać załadowana sesja. Jest to opcjonalne, jeśli podano `genesis`.

`genesis` : Wymagany do **identyfikacji** profilu, dla którego ma zostać załadowana sesja. Jest to opcjonalne, jeśli podano `username`.

### Wyniki:

#### Zwracana wartość obiektu JSON:

```
{
    "genesis": "b7fa11647c02a3a65a72970d8e703d8804eb127c7e7c41d565c3514a4d3fdf13",
    "session": "2ef9de11b19af82984ddf93275e7ba22c11fe9659d0667f79311c46732bbb7a4"
}
[Completed in 0.072625 ms]
```

#### Zwracane wartości:

`genesis` : To jest hash nazwy użytkownika profilu, znany również jako hash właściciela.

`session` : Podczas korzystania z trybu API wielu użytkowników zwracana jest dodatkowa wartość sesji, która identyfikuje sesję.

---
&nbsp;

## terminate <a href="#terminate" id="terminate"></a>

Spowoduje to zakończenie aktywnej sesji określonej przez podany rzeczownik.

```
sessions/terminate/noun
```

To polecenie obsługuje tylko rzeczownik `local`.

**NOTATKA:** To nie usuwa zapisanej sesji

### Parametry:

`pin` : Wymagany do **uwierzytelnienia**. Kod PIN tego profilu.

`session` : Wymagane przez **argument** `-multiuser=1` w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika nie należy podawać sesji.

### Wyniki:

#### Zwracana wartość obiektu JSON:

```
{
    "success": true
}
[Completed in 1656.089478 ms]
```

#### Zwracane wartości:

`success` : Flaga logiczna wskazująca, że aktywna sesja została pomyślnie zakończona.

---
&nbsp;

## status <a href="#status" id="status"></a>

Pobierz stan sesji określony przez podany rzeczownik.

```
sessions/status/noun
```

To polecenie obsługuje tylko rzeczownik `local`.

### Parametry:

`session` : Wymagane przez **argument** `-multiuser=1` w celu identyfikacji sesji użytkownika. W przypadku trybu API pojedynczego użytkownika nie należy podawać sesji.

### Wyniki:

#### Zwracana wartość obiektu JSON:

```
{
    "genesis": "b7fa11647c02a3a65a72970d8e703d8804eb127c7e7c41d565c3514a4d3fdf13",
    "accessed": 1653680627,
    "location": "local",
    "unlocked": {
        "mining": false,
        "notifications": true,
        "staking": false,
        "transactions": false
    }
}
[Completed in 0.080333 ms]
```

#### Zwracane wartości:

`genesis` : To jest hash nazwy użytkownika profilu, znany również jako hash właściciela.

`accessed` : Uniksowy znacznik czasu, w którym ostatnio uzyskano dostęp do profilu.

`location` : Lokalizacja sesji.

`unlocked` : Zawiera elementy potomne opisujące funkcje, dla których sesja jest aktualnie odblokowana.

`mining` : Flaga logiczna wskazująca, czy łańcuch sygnatur użytkowników jest odblokowany do kopania.

`notifications` : Flaga logiczna wskazująca, czy profil użytkownika jest odblokowany do przetwarzania powiadomień.

`staking` : Flaga logiczna wskazująca, czy profil jest odblokowany do stakowania.

`transactions` : Flaga logiczna wskazująca, czy profil jest odblokowany do tworzenia jakichkolwiek transakcji (z wyjątkiem tych tworzonych automatycznie przez powiadomienia o wydobywaniu/przetwarzaniu, jeśli są one odblokowane).













