---
title: Jak działa API - Tritium++
description: Tritium++
published: true
date: 2022-10-29T22:44:08.003Z
tags: 
editor: markdown
dateCreated: 2022-10-24T21:57:59.610Z
---

# Jak-działa-API: Tritium++
&nbsp;
### Interfejs API Nexusa

Dostęp do interfejsu API Nexusa to bezproblemowe i proste doświadczenie. Aby uzyskać dostęp do API, możesz skorzystać z jednej z trzech opcji:
&nbsp;
#### Użyj przeglądarki internetowej z żądaniem opartym na adresie URL:

Wyślij żądanie **GET** z parametrami w adresie URL, jak pokazano poniżej.

````
http://localhost:8080/<api>/<method>?<key>=<value>&<key1>=<value1>
````

Interfejs API wykorzystuje kodowanie formularzy, więc możesz używać dowolnych znaków. Jedyną rzeczą, o której należy pamiętać, jest użycie w kodowaniu znaku „+”, który działa jako znak ucieczki dla spacji, a także „%20”. Interfejs API wykryje to zachowanie, o ile formularz zakoduje kodowanie znaku + w formularzu. Czasami wysyłając żądanie **GET**, przeglądarka zakłada, że ​​+ to spacja i nie koduje jej, to samo dotyczy „%” podczas żądania **GET**.
&nbsp;
#### Użyj przeglądarki internetowej z żądaniem opartym na **POST**

Treść POST zawiera parametry i przechodzi do punktu końcowego, takiego jak:

````
http://localhost:8080/<api>/<method>
````

Przykładowy formularz internetowy wyglądałby tak:

```
<form action='http://localhost:8080/<api>/<method>' method='post'>
<input type = 'text' name = '<key>'  value = '<value>' >
<input type = 'text' name = '<key1>' value = '<value2>'>
<input type = 'submit'>
</form>
```

Umożliwi to zintegrowanie interfejsu API Nexusa z istniejącymi formularzami internetowymi. Pozwala to wykorzystać moc Nexus Blockchain we wszystkich istniejących usługach internetowych.
&nbsp;
#### Użyj wiersza poleceń nexusa :

Aby to zadziałało, demon Nexus musi już działać. Upewnij się, że jesteś w tym samym katalogu, co demon Nexus.

````
./nexus <api>/<method> <key>=<value> <key1>=<value1>
````

Spowoduje to zwrócenie wszystkich danych w formacie JSON do Twojej konsoli.
&nbsp;
#### Wyniki JSON

Odpowiedź JSON, którą otrzymasz, będzie zawierać jeden z dwóch kluczy, wynik lub błąd. Po pomyślnym wykonaniu polecenia otrzymasz ciąg JSON, taki jak:

````
{"result":{"genesis":"69c2479c6780782448f419a0865542002ee85fec39228275b2db44bb6d3aa503","session":4940881975319897416}}
````

Będziesz musiał przeanalizować wartości obiektu wynikowego w wybranym przez siebie języku. Jeśli zdarzy ci się otrzymać awarię, będzie to wyglądać tak:

````
{"error":{"code":-24,"message":"Missing Password"}}
````

Zauważ, że teraz będziesz analizować klucz błędu i nie będzie żadnych wyników. Umożliwia to programiście wybór sprawdzania istnienia klucza „błędu” w celu sprawdzenia błędów lub sprawdzenia istnienia klucza „wyniku”, aby sprawdzić, czy został wykonany pomyślnie. Wybór należy do Ciebie, jak sobie z tym poradzisz, po prostu wiedz, że jest to sytuacja albo / lub. Dostaniesz tylko jeden lub drugi.

&nbsp;

## Profiles API

Interfejs Profiles API jest odpowiedzialny za utrzymanie funkcji na poziomie konta użytkownika. NIE UŻYWAJ tego interfejsu API na węźle zagranicznym, którego nie jesteś menedżerem. Twoja nazwa użytkownika i hasło są przechowywane w bezpiecznych alokatorach, ale zdalny punkt końcowy może nadal zbierać Twoje poświadczenia podczas przesyłania wywołania interfejsu API. Ten interfejs API jest przeznaczony tylko dla węzła usługi, który kontrolujesz.

Interfejs Profiles API można znaleźć pod poniższym linkiem:

[Profiles API](https://wiki.nexus.io/pl/tritium++/profiles)


>**UWAGA** : Sesje logowania nie są zachowywane po ponownym uruchomieniu węzła. Są one przechowywane w bezpiecznym alokatorze tylko w pamięci, nie buforuj ich na dysku, w przeciwnym razie możesz otworzyć potencjalne problemy z bezpieczeństwem.
{.is-info}

&nbsp;

## Sessions API

Interfejs Sessions API jest odpowiedzialny za utrzymanie funkcji na poziomie konta użytkownika. NIE UŻYWAJ tego interfejsu API na węźle zagranicznym, którego nie jesteś menedżerem. Twoja nazwa użytkownika i hasło są przechowywane w bezpiecznych alokatorach, ale zdalny punkt końcowy może nadal zbierać Twoje poświadczenia podczas przesyłania wywołania interfejsu API. Ten interfejs API jest przeznaczony tylko dla węzła usługi, który kontrolujesz.

Interfejs User API można znaleźć w następującej ścieżce repozytorium:

[Sessions API](https://wiki.nexus.io/pl/tritium++/sessions)

&nbsp;

## Finance API

Finance API udostępnia metody tworzenia tokenów, kont, wysyłania i otrzymywania monet NXS lub innych tokenów pomiędzy użytkownikami/kontami oraz zarządzania stakowaniem.

Finance API można znaleźć w następującej ścieżce repozytorium:

[Finance API](https://wiki.nexus.io/en/tritium++/finance)

>UWAGA: Wszystkie polecenia w tym API wymagają LOGIN. Upewnij się, że używasz interfejsu Session API do tworzenia sesji przed użyciem poleceń wymaganych przez sesję.
{.is-info}

&nbsp;

## Assets API

Interfejs Asset API jest przeznaczony do zarządzania aktywami cyfrowymi poprzez rejestrowanie metadanych reprezentujących konkretne aktywo. Zapewnia również funkcję tokenizacji samych aktywów w związku z posiadaniem aktywów należących do wielu osób.

Interfejs Assets API można znaleźć pod poniższym linkiem:

[Assets API](https://wiki.nexus.io/en/tritium++/assets)

>UWAGA: Wszystkie polecenia w tym interfejsie API wymagają LOGIN. Upewnij się, że używasz interfejsu API użytkownika do logowania przed użyciem wymaganych poleceń LOGIN.
{.is-info}

&nbsp;

## Tokeny API

API tokenów umożliwia tworzenie tokenów i kont w celu wzajemnego wysyłania i odbierania tokenów. Jest to również warunek wstępny tworzenia tokenów, które mają być udziałami w zasobie cyfrowym lub firmie (STO).

Interfejs Tokens API można znaleźć w następującej ścieżce repozytorium:

LLL-TAO/docs/API/TOKENS.MD

{% wskazówka style="informacje" %}
UWAGA: niektóre polecenia w tym API wymagają LOGIN. Upewnij się, że używasz interfejsu API użytkownika do logowania przed użyciem wymaganych poleceń LOGIN.
{% podpowiedzi %}

&nbsp;

## API księgi

Interfejs API księgi zapewnia dostęp do księgi głównie w celu tworzenia i pobierania bloków i transakcji, ale także w celu uzyskania informacji o stanie księgi.

&nbsp;

## Dostawa API

Supply API odpowiada za obsługę logistyki łańcucha dostaw. Jego głównym celem jest zarządzanie trasami i ruchami wzdłuż łańcucha dostaw, wraz z przeglądaniem historii zdarzeń związanych ze zmianami nadzoru.

{% wskazówka style="informacje" %}
UWAGA: niektóre polecenia w tym API wymagają LOGIN. Upewnij się, że używasz interfejsu API użytkownika do logowania przed użyciem wymaganych poleceń LOGIN.
{% podpowiedzi %}

&nbsp;

## Systemowe API

Interfejs API systemu zapewnia publiczny dostęp do informacji o tym węźle. Obejmuje to dane, takie jak wersja oprogramowania, na którym działa węzeł, stan księgi i pamięci, adres IP węzła i połączeni równorzędni.

System API można znaleźć w poniższym linku:

{% content-ref url="../tritium++-overview/how-to-api-tritium++/tritium++-api/system (1).md" %}
[system (1).md](<../tritium++-overview/jak-to-api-tritium++/tritium++-api/system (1).md>)
{% ref. treści końcowej %}

&nbsp;

## Faktury API

Invoices API zapewnia użytkownikom i programistom aplikacji możliwość wystawiania i opłacania faktur na blockchainie Nexusa. Ten interfejs API jest demonstracją, w jaki sposób rejestry mogą być używane do przechowywania dowolnych danych użytkownika, a kontrakty warunkowe mogą być używane do implementacji reguł przypadków użycia. Faktury można tworzyć, a następnie wysyłać do łańcucha podpisów odbiorców w celu zapłaty. API obsługuje faktury wystawione w NXS lub dowolnym innym tokenie na blockchainie Nexus.