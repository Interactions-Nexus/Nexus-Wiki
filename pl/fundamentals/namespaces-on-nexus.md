---
title: Przestrzenie nazw na Nexusie
description: System nazewnictwa TAO
published: true
date: 2022-12-14T22:35:49.299Z
tags: 
editor: markdown
dateCreated: 2022-10-21T22:13:36.006Z
---

# Przestrzeń nazw na Nexusie

Podążając śladami [Domain Naming System (DNS)](https://www.networkworld.com/article/3268449/what-is-dns-and-how-does-it-work.html), Nexus Tritium , Anime i Obsidian (TAO) Framework zapewnia wielopoziomowy system nazewnictwa, który oferuje unikalne na całym świecie możliwości identyfikacji, personalizacji i budowania marki. System nazewnictwa TAO (TNS), być może zasługujący na krótkie uznanie w porównaniu z istniejącymi i przewidywanymi postępami technologicznymi w Nexusie, zachęca ludzką kreatywność do wykorzystania tej wyjątkowej struktury nazewnictwa i własności.

W TNS istnieją trzy kategorie: **nazwy lokalne**, **przestrzenie nazw** i **nazwy globalne**. Nazwy, niezależnie od kategorii, technicznie istnieją jako rejestry obiektów, które kierują do adresu innego rejestru, takiego jak token, konto lub aktywo. Mówiąc prościej, nazwy można dołączać i odłączać od rejestrów. Kategoria nazwy określa ograniczenia dotyczące routingu, przenoszenia i formatu adresu.

## Nazwy lokalne

Lokalne nazwy są odwzorowywane na rejestry należące do danej osoby [Signature Chain (SigChain)](/pl/innovations/signature-chains). Nazwy te kosztują 1 NXS i zawsze rozpatrują się w rejestrach. Nazwy lokalne mają format *username:local_name*; nazwy lokalne są zawsze poprzedzone nazwą użytkownika SigChain.

Nazwy lokalne nie mogą być przenoszone do innych SigChainów, ani nie mogą wskazywać na adresy, które nie należą do właściciela. Oznacza to mniejszą wartość zaklepanych nazw SigChain, ponieważ nazwane konta nie mogą być sprzedawane ani podarowane alternatywnym właścicielom, chyba że ktoś zrezygnuje z poświadczeń SigChain. Nazwy użytkowników i nazwy lokalne wymagają mniej rygorystycznych znaków niż przestrzenie nazw; dopuszczalne są spacje, symbole, cyfry oraz wielkie/małe litery.

Nexus jest otwarty i dostępny, ponieważ każdy może uzyskać dostęp do nazw lokalnych za pośrednictwem swojego SigChain, ale oferuje również przestrzenie nazw i nazwy globalne, które zaspokajają bardziej ambitne perspektywy organizacyjne.

![name1.png](/name1.png)<p align=center>*Rejestr obiektu przestrzeni nazw*</p>

Karta Historia pokazuje przeszłe prawa własności i wydarzenia. Własność może zostać przeniesiona na dowolny inny identyfikator Genesis lub nazwę użytkownika.

## Przestrzenie nazw

Z drugiej strony przestrzenie nazw są przeznaczone do celów organizacyjnych lub biznesowych. Podstawowa różnica między przestrzeniami nazw, a nazwami lokalnymi wynika z możliwości przeniesienia własności nazwy i wskazania dowolnego adresu rejestru. Ponieważ własność nazw utworzonych w przestrzeni nazw może być przenoszona, właściciele przestrzeni nazw mogą tworzyć, a następnie sprzedawać nazwy, tak jak właściciele mogą sprzedawać swoje domeny DNS blank.com. Przestrzenie nazw można z grubsza porównać do domen najwyższego poziomu .org, .com i .info, podczas gdy nazwa działa jak konkretny adres domeny. Przestrzenie nazw wymagają również bardziej rygorystycznych wymagań dotyczących znaków niż nazwy użytkowników, ograniczając możliwe opcje do małych liter, cyfr i kropek.


#### Nazwy z przestrzeni nazw

Nazwy utworzone w przestrzeni nazw są adresowane jako namespace::name, w przeciwieństwie do formatu pojedynczego dwukropka w nazwach lokalnych. W porównaniu z nazwami lokalnymi, nazwy utworzone z przestrzeni nazw mają unikalne właściwości dostosowane do możliwości biznesowych i organizacyjnych. Możliwość przekierowania do rejestrów, nad którymi właściciel nie ma kontroli, może pomóc właścicielom firm w organizacji listy płac i innych wydatków.

![name2.png](/name2.png)<p align=center>*Oto szczegóły z rejestru nazw obiektów (nazwa love) w przestrzeni nazw luna. Zobacz, jak nazwa otrzymuje swój własny adres, wskazując na inny.*</p>

Zarówno nazwy lokalne, jak i nazwy w przestrzeni nazw mogą wskazywać ten sam rejestr kont, co oznacza, że można utworzyć dowolną liczbę różnych nazw i kierować je do tego samego rejestru. „Wskazywanie” oznacza automatyczne kierowanie transakcji na adres docelowy. Tak długo, jak nazwa trafia do rejestru, otrzyma kontrolę nad środkami adresowanymi do nazwy.

Właściciel nazwy kontroluje, gdzie wskazuje nazwa. Więc jeśli ktoś kupił `luna::nexus`, mógł dołączyć tę nazwę do dowolnego konta, tokena lub aktywa, niezależnie od właściciela. Mogli również sprzedać tę nazwę dowolnemu innemu użytkownikowi. Gdy właściciel przestrzeni nazw przeniesie nazwę, nie ma nad nią żadnej władzy, więc pierwotny właściciel przestrzeni nazw `luna` nie może w ogóle kontrolować `luna::nexus` po przeniesieniu własności na inny SigChain.

## Nazwy globalne

Nazwy globalne z kolei reprezentują całkowicie unikalne, samodzielne nazwy odpowiadające adresowi rejestrowemu wybranemu przez właścicieli. Intencją jest, aby nazwy globalne reprezentowały wartości, takie jak paski tokenów, ale osoby kreatywne znajdą inne zastosowania. Na przykład, jeśli ktoś rozpoczynał tokenizowany biznes o nazwie SMART Corporation i chciał rozpoznawalnej i prostej nazwy dla kapitału tokena, mógłby stworzyć globalną nazwę `SMART` i wskazać tę nazwę na rejestr tokenów wybrany do reprezentowania kapitału. Tak długo, jak nazwa globalna jest wskazywana na rejestr tokenów, każdy będzie mógł znaleźć i wejść w interakcję z tokenem poprzez nazwę `SMART`.

W przeciwieństwie do przestrzeni nazw, nazwy globalne nie ograniczają się do małych liter, kropek i cyfr. Jednak globalna własność nazw może być przenoszona, podobnie jak przestrzenie nazw i ich nazwy, stwarzając możliwości również dla rynków wtórnych.