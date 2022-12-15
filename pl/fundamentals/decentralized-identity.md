---
title: Zdecentralizowana tożsamość
description: Zdecentralizowana tożsamość na Nexusie
published: true
date: 2022-12-15T22:40:52.982Z
tags: 
editor: markdown
dateCreated: 2022-10-21T22:18:24.098Z
---

# Zdecentralizowana tożsamość

Nexus zapewnia zaawansowaną technologicznie podstawę dla nowej generacji zdecentralizowanej tożsamości. To skutecznie umożliwia większą kontrolę informacji dla osób i organizacji, które cenią sobie bezpieczeństwo i suwerenność.

Według World Wide Web Consortium (W3C), „DID, czyli zdecentralizowany identyfikator, to identyfikator URI składający się z trzech części: schematu „did:”, identyfikatora metody oraz unikalnego, specyficznego dla metody identyfikatora generowanego przez DID metoda. DID można przetłumaczyć na dokumenty DID. Adres URL DID rozszerza składnię podstawowego identyfikatora DID o inne standardowe składniki URI (ścieżka, zapytanie, fragment) w celu zlokalizowania określonego zasobu — na przykład klucza publicznego w dokumencie DID lub zasobu dostępnego poza DID dokument."

![did.png](/did.png)

Dzięki Nexusowi standardy World Wide Web Consortium (W3C) zostały rozszerzone, ponieważ wszystkie konta są pseudoanonimowe. Żadna osoba nie może powoływać się na odpowiednie imię i nazwisko, datę lub numer ubezpieczenia społecznego w celu ujawnienia informacji umożliwiających identyfikację. Osoby fizyczne i organizacje kontrolują dane, co oznacza, że jeśli ktoś zdecyduje się przedstawić prawo jazdy lub licencję biznesową, jest to możliwe. Każdy podmiot jest właścicielem swoich danych i może kontrolować, komu i czym udostępnia, na przykład dokumenty medyczne.

Jeśli porównamy to z dostępnymi obecnie systemami identyfikacji fizycznej, wspólny identyfikator, taki jak prawo jazdy, jest informacją uprzywilejowaną, a zatem właściciel zachowuje kontrolę nad tym, komu go ujawnia. Podczas zarządzania rachunkami informacje można przypisać tylko wtedy, gdy autoryzowano odbiorcę za pomocą dowodów kryptograficznych, gwarantujących co najmniej, że posiadacz konta jest rzeczywiście tym, który autoryzował transmisję danych. Eliminuje to ogromny potencjał korupcji tkwiący w scentralizowanych systemach identyfikacji.

## Technologia

Nexus wykorzystuje łańcuchy podpisów, które pod względem architektonicznym są porównywalne z posiadaniem „osobistego łańcucha bloków”. Umożliwia to tworzenie DApps o wysokim stopniu bezpieczeństwa i elastyczności, a także zapewnia funkcjonalność nazwy użytkownika i hasła wzmocnioną przez osobisty numer identyfikacyjny (PIN). Ta technologia w połączeniu z zarządzaniem zasobami stanowi podstawę dla zdecentralizowanych systemów identyfikacji. Zobacz poniższą ilustrację w celu uzyskania dalszych wyjaśnień.

Wykorzystanie przez Nexusa protokołu LISP (Location Identifier Separation Protocol) zapewnia ulepszone możliwości identyfikacji w warstwie IP sieci. Oddzielenie identyfikatora punktu końcowego (EID) od adresu IP umożliwia urządzeniu swobodne przemieszczanie się między sieciami, ponieważ zmienia się tylko lokalizator (twój adres IP), a nie identyfikator. Jest to kluczowa funkcja bezpieczeństwa, ponieważ EID jest powiązany z Sigchain, tworząc identyfikator na poziomie sieci, który jest kryptograficznie powiązany z daną tożsamością. Znaczne ograniczenie oszustw, fałszowania adresów IP i kradzieży tożsamości to oczekiwane rezultaty wykorzystania LISP i Sigchain w aplikacjach blockchain.

## Przypadki użycia tożsamości

Prawnie zdecentralizowana tożsamość cyfrowa z doskonałymi zabezpieczeniami i integralnością otwiera drzwi do wielu możliwości. Zapewnienie uwierzytelniania i Know Your Customer (KYC) dla istniejących DApps i starszej infrastruktury łączącej się z rozwiązaniami blockchain jest prawdopodobnie najbardziej widoczne. Funkcja generowania kont witryn internetowych i uwierzytelniania jest obecnie dostępna i jest opracowywana pod kątem integracji z nowymi aplikacjami DApps. Podstawowe funkcje integralności plików (sumy kontrolne) i szyfrowania są możliwe, chociaż na tym etapie będą wymagać logicznego opracowania.

Siedmiowarstwowy stos oprogramowania Nexusa i uproszczony interfejs API RESTful umożliwiają stronom trzecim integrację kontrolowanych przez klienta danych uwierzytelniających, danych dotyczących tożsamości, zasobów i nie tylko; przybliża nas o kolejny krok do szerszego przyjęcia zdecentralizowanej technologii. Ta koncepcja może potencjalnie zapewnić szerokie usługi związane z tożsamością suwerenną. Deweloperzy mogą korzystać z naszego interfejsu API, aby uprościć tworzenie DApps, które kontrolują wiele rodzajów zapisów cyfrowych, na przykład:

* Identyfikacja osobista, zawodowa i rządowa
* Licencje mieszkaniowe, profesjonalne i rządowe
* Certyfikaty edukacyjne, zawodowe, rządowe
* Osobiste i zawodowe referencje i rekomendacje
* Zdecentralizowane finanse (DeFi) i Internet rzeczy (IoT)
* Dokumentacja medyczna, weryfikacja i zwolnienia
* Podpisy cyfrowe i oceny reputacji
* Zasoby (tytuły, rejestracje firm, domeny TNS itp.)

Sytuacyjne mikrokosmosy związane z ostateczną łatwością użytkowania są odzwierciedlone poniżej:

![identityuc.png](/identityuc.png)

## Scentralizowany system poświadczeń

Suwerenna tożsamość jest podstawowym prawem człowieka ustanowionym przez większość krajów rozwiniętych na całym świecie. Organizacja Narodów Zjednoczonych, [Konwencja o prawach dziecka](https://www.unicef.org/child-rights-convention/convention-text), Artykuł 8, określa prawo dziecka do zachowania swojej tożsamości. Jako osoba dorosła bez ważnego dokumentu tożsamości będzie trudno, jeśli nie niemożliwe, głosowanie, posiadanie własności, zdobycie pracy, otrzymywanie zasiłków, otwarcie konta bankowego (ilustracja poniżej) lub wiele innych zobowiązań, które wielu z nas uważa za oczywiste.

![ccs.png](/ccs.png)


Globalna tożsamość dla wszystkich do 2030 roku to numer [16.9 Celów Zrównoważonego Rozwoju Organizacji Narodów Zjednoczonych (SDGs)](https://www.un.org/sustainabledevelopment/peace-justice/). Jednak, jak widzieliśmy w autorytatywnych reżimach w przeszłości i obecnie, rządy chętnie naruszają to „podstawowe prawo człowieka” do wywierania nacisku jako wszechobecnego mechanizmu kontroli. W związku z rozwojem ostatnich wydarzeń niektórzy już rozważają zbieranie danych za pośrednictwem obowiązkowego obywatela i [pracownika](https://www.eeoc.gov/wysk/what-you-should-know-about-covid-19-and-ada-rehabilitation-act-and-other-eeo-laws?mod=article\_inline) testowanie infekcji, [śledzenie kontaktów](https://www.jurist.org/commentary/2020/04/theo-wilson-compulsory-contact-tracing/), szczepienia oraz jako warunek wjazdu lub [podróży](https://www.npr.org/sections/coronavirus-live-updates/2020/04/15/834999076/emirates-airlines-begins-conducting-rapid-covid-19-tests-for-boarding-passengers) do określonych miejsc.

W 2009 r. rząd Indii zaczął rejestrować ponad miliard osób w największej bazie danych [identyfikacji biometrycznej](https://time.com/5409604/india-aadhaar-supreme-court/) w historii. Zebrali dane biometryczne (skany tęczówki i odciski palców) od całej populacji i wydali tożsamość cyfrową, której można było używać do otrzymywania świadczeń socjalnych i świadczeń socjalnych. „Choć rzekomo dobrowolny, krytycy stwierdzili, że program w coraz większym stopniu narzucał się życiu prywatnemu obywateli”, donosi [Time](https://time.com/5409604/india-aadhaar-supreme-court/).

To nasuwa pytanie, gdzie prawo do tożsamości przecina się ze świadomą zgodą? Umowy licencyjne użytkownika końcowego (EULA) są powszechnie akceptowane na stronach internetowych i w oprogramowaniu bez ich pełnego zrozumienia. 23andMe, Ancestry i podobne firmy zbierają tożsamość genealogiczną, przejmują własność i sprzedają oferentom, którzy zaoferują najwyższą cenę, z innymi [prawdopodobnie szkodliwymi lukami](https://youtu.be/PXLHdNlU3F8). Dodatkowo można było przeoczyć podania o pracę, polisy ubezpieczeniowe, umowy kredytowe i inne drobne druki z powodu konieczności, braku czasu lub niezrozumienia terminologii. Są to przykłady tego, jak nieświadomie można zawierać potencjalnie szkodliwe umowy [(Niebezpieczny precedens YouTube)](https://townhall.com/columnists/vijayjayaraj/2020/04/26/youtubes-policy-on-covid19-and-climate-change-sets-dangerous-precedent-n2567584). Co więcej, w jaki sposób odróżniamy świadomą zgodę od wytworzonej podczas przesyłania naszej tożsamości? Cóż, zazwyczaj opiera się to na indywidualnym [zaufaniu i wiarygodności źródła](https://tech.nexus.io/trust) w celu podejmowania świadomych decyzji.

![ula.png](/ula.png)

## Ryzyko centralizacji

Biorąc pod uwagę wagę tożsamości jasno określoną przez „władze, które były”, można uznać ochronę tych danych za najwyższy priorytet. Niestety, podmioty te przyjmują technologię i zarządzanie zasadniczo oparte na centralizacji, która jest z natury nieskalowalna i obarczona większymi kosztami niż korzyściami. Niezwykłym przykładem jest [atak na amerykańskie Biuro Zarządzania Personelem (OPM)](https://www.csoonline.com/article/3318238/the-opm-hack-explained-bad-security-practices-meet-chinas-Captain-America.html), baza danych zawierająca poufne informacje o pracownikach rządowych. Zupełne zaniedbanie, ignorancja i brak powiadomienia ofiary o zaistniałej sytuacji ostatecznie zakończyły się sporem sądowym.

W miarę ewolucji scentralizowanego [Zarządzania Tożsamością (IdM) lub Zarządzania Tożsamością i Dostępem (IAM)](https://www.csoonline.com/article/2120384/what-is-iam-identity-and-access-management-explained.html) wychodzi poza ustawienia lokalne do rozwiązań dostawcy usług w chmurze (CSP), luki w zabezpieczeniach rosną wykładniczo. Repozytoria danych uwierzytelniających, uważane za klucze do królestwa, historycznie izolowane w ściśle zlokalizowanych przedziałach, są teraz powierzane zewnętrznym, globalnie dostępnym, zwirtualizowanym środowiskom obsługującym wielu użytkowników. Nie tylko zwiększa się ryzyko [włamań](https://www.secsignal.org/en/news/how-i-hacked-a-whole-ec2-network-during-a-penetration-test/), ale prawdopodobieństwo [przypadkowego](https://www.arnnet.com.au/article/670469/microsoft-misconfiguration-exposed-250m-users-data/) narażenia jest znacznie zwiększone. Co więcej, dostawcy CSP oferują teraz możliwości Identity as a Service (IDaaS), jednocześnie reklamując atrakcyjne modele a la carte, które w dłuższej perspektywie mogą być finansowo wygórowane. Poniższa ilustracja ilustruje złożoność związaną z tymi rozwiązaniami.

![azure.png](/azure.png)


Źródło: [_https://docs.microsoft.com_](https://docs.microsoft.com/)

Z osobistego punktu widzenia poleganie na poczcie e-mail w chmurze, mediach społecznościowych i podobnych usługach wymaga tożsamości do interakcji. Single Sign-On (SSO) zapewnia większą łatwość użytkowania, czyniąc te platformy bardziej atrakcyjnymi dla mas. Jednak za kulisami wykorzystują tę tożsamość do śledzenia każdego działania w Internecie w oparciu o indywidualną umowę EULA firmy. Ponadto te firmy zewnętrzne sprzedają Twoją tożsamość, historię internetu i powiązane dane oferentom, którzy zaoferują najwyższą cenę, często w niepozorny sposób za pomocą [funkcji śledzenia Google](https://www.wired.com/story/google-tracks-you-privacy/ ) oraz [kontrowersje związane z Cambridge Analytica](https://arstechnica.com/tech-policy/2018/03/facebooks-cambridge-analytica-scandal-explained/).

W [raporcie Google z 2017 r.](https://mashable.com/2017/11/13/google-releases-year-long-password-security-study/#Har9jWiUaOqi) stwierdzono, że 3,3 miliarda danych uwierzytelniających zostało wydobytych podczas zewnętrznej naruszeń, podczas gdy tylko 12 milionów z nich można było przypisać atakom typu phishing. „Między styczniem a wrześniem 2019 r. ujawniono ponad 7,9 miliarda [rekordów danych](https://pages.riskbasedsecurity.com/hubfs/Reports/2019/Data%20Breach%20QuickView%20Report%202019%20Q3%20Trends.pdf) — wzrost o 33% w porównaniu z tym samym okresem w 2018 r.”, zgodnie z artykułem z [IdentityForce](https://www.identityforce.com/blog/2020-data-breaches). Raport [Verizon](https://enterprise.verizon.com/resources/executivebriefs/2020-dbir-executive-brief.pdf) z początku 2020 r.  stwierdza: „Kradzież danych uwierzytelniających, ataki społecznościowe (tj. błędy powodują większość naruszeń (67% lub więcej)”. Nie trzeba dodawać, że scentralizowane systemy są zepsute.


![informationib.png](/informationib.png)


Źródło: [_https://informationisbeautiful.net_](https://informationisbeautiful.net/)

Wyzwania związane z centralizacją rozwiązań typu blockchain to rosnący trend. Te rozwijające się konfrontacje są sprzeczne z fundamentalną zasadą braku zaufania, obchodząc istotę tej innowacyjnej technologii. Podczas gdy termin kryptowaluta zyskał negatywną konotację z powodu zabójstw głównych postaci, niektóre [słusznie](https://digitalguardian.com/blog/history-ransomware-attacks-biggest-and-worst-ransomware-attacks-all-time), ma być uosobieniem decentralizacji; eliminując pośredników. Centralizacja to władza, „władza korumpuje, a władza absolutna korumpuje absolutnie”.

Wraz z pojawieniem się systemów cyfrowej identyfikacji, które obecnie wychodzą na jaw, ten suwerenny system, jeśli nie zostanie sprawdzony, może zostać wciągnięty w cyfrową pułapkę, która może pochłonąć ostatnie części pozostałej integralności. Nie jest to z pewnością najbardziej pożądany wniosek z możliwych i podkreśla znaczenie ochrony tej suwerenności za pomocą praw matematycznych.