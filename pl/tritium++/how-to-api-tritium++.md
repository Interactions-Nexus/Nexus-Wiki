---
title: Jak działa API - Tritium++
description: Tritium++
published: true
date: 2022-10-29T22:23:21.369Z
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