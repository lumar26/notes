# Scrum

## Uvodni pregled

Разбијање пројекта на целине по Скраму. Направи који би били епици, за сваки епик је стори 

Таксови се могу разбити и на слојеве у архитектури за сваки *story*, па то има подтаскове (*feature*, *bug*) и сваки подтаск траје идеално око 4 сата. У оквиру подтаска постоје чекпоинти нпр прављење ентитета, релација у бази, пул захтев. Груминг је разбијање процеса на таскове и подтаскове. Тек после ~~груминга~~ који је естимација, ради се планирање спринтова и временски се одређује кад, шта и ко ради.

***Backlog*** је листа таскова са естимацијама по приоритету.

У току спринта не сме да се дода нови таск, формално

Скрам мастер само прати процес, није задужен за то како изгледа софтвер

На крају се ради *review* (шта је тачно урађено), ретроспекитва (добро, лоше, унапређења) и демо.

## Stories

*Story* treba da predstavlja opis jednog nedeljivog slučaja korišćenja iz korisničkog ugla posmatranja.

*Story* treba da sadrži par rečenica u običnom svakodnevnom jeziku koji opisuje jednu akciju koju može da preduzme krajnji korisnik sistema. *Story* treba da naglasi koji je **rezultat** preduzete akcije - šta je očekivani izlaz.

*Story* treba da bude u sastavu ***epic***-a, koji su opet deo **inicijative**, koji su opširniji gradivni blokovi nekog projekta. *Epic* treba da ima minimum **8** *story*-ja a neke dobre prakse kažu da treba da ih sadrži **15**ak.

Šta donosi definisanje priča:

- Fokus na kranjem korisniku
- Omogućavaju saradnju u okviru tima pri realizaciji
- Deljenje procesa razvoja na etape i čekpointe

Sadržaj priče: 

- Definisanje kada je priča gotova: kada je uspešno završena a kada neuspešno (alternativni scenariji);
- Navođenje očiglednih koraka iz kojih se priča sastoji i ko ih izvršava;
- Ko je / su krajnji korisnik/ci
- Ako je priča previše kompleksna napisati koje su podpriče sadržane u njoj ali u odgovarajućem redosledu;
- Procena vremena koje je potrebno da se priča implementira. Trebalo bi da jedan *story* može da se implementira ceo u toku jednog *sprint*-a
- Potrebno je da *story* bude testabilan

Standardne greške:

- Nema opisa ~~korisničkog interfejsa~~ već samo **ciljeva**;
- *Story* ne sme da zavisi od ostalih *story*-ja tj. mora da bude nezavisna celina.

Moguća struktura priče bi izgledala ovako: `Kao klijent, želim da ... kako bih ...`.

​				**PERSONA + NEED + PURPOSE**

# Confluence

Једном **спејсу** одговара један тим или један већи пројекат. Ту се складишти сва документација. Практично ћемо да имамо један спејс који ће да се зове Nomadesk и у оквиру њега једну страну која може да се зове вербална спецификација. ***Ипак не!*** Malkier ће да нам буде спејс што значи да би страница требала да буде *nomadesk*

### Makroi

Makroi se nalaze tako što se najpre ukuca `/` ili `//`pa se odabere neki od ponuđenih makroa, ili krenemo da kucamo ako znamo napamet kako se zove

`/status` je isto zgodan makro za prikaz statusa nečega

Postoje i razni makroi za pojedine Jira funkcionalnosti kao što je npr *Project Roadmap*

`Page Properties` makro je zgodan za tabelu koja tgreba da opiše tu stranu. Npr. poželjno je imati stranu za opis projekta koja će na početku da ima tabelu sa svim bitnim informacijama poput glavnog i odgovornog, kontributora, cilja, datumi početka i očekivanog završetka, glavni rezultati projekta, statusa, nedeljni *update*-ovi...

`Date` makro je zgodan za prikaz datuma u odgovarajućem formatu.

### TO DO

- Bilo bi poželjno da svaki epic ima jedan dokument uvodni koji ga opisuje. Gde postoji prvo tabela sa svim info, pa onda neki kratak opis
- Na svakom *page*-u treba da postoji uvodna *Properties table* sa najbitnijim informacijama o dokumentu