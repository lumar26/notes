# Requirements draft

Као add-on би могла да се дода интеграција са фирмама које одржавају простор (чисте, опремају итд.), али то је нека додатна функционалност за следеће верзије.

### Улоге

- ***Client***  - онај који издаје простор преко апликације
- ***User*** - онај ко закупљује простор
- ***Admin*** - kontroliše klijente, korisnike i *property*-je
- ***Superadmin*** - kontroliše admine

### Impersonation: *TODO*

Da postoji podrška da se admin uloguje kao User i da radi sve što radi i User. Sve što User radi bitno mora da se loguje, i da se tačno naglasi da je to uradio admin. To je **OPT-OUT**

Ovo se u 50% slučajeva koristi za rešavanje nekih tehničkih problema (resetovanje lozinke i tako još neke aktivnosti) na koje nailazi korisnik a ostalo da bi završili neke konkretne stvari uesto korisnika kao što je rezervacija, otkazivanje i sl. 

**User obavezno mora da ima Country**, jer ćemo na lokaciji da zasnivamo gotovo sve tako da nam je to veoma bitno.

#### Шта фали од функционалности: 

- ~~може да се дода опција да клијент буде физичко лице или нека организација - podrazumeva se da je moguće~~
- ~~Da li je komunikacija preko poruka osnovna funkc - nije, to će da radi zasebni servis~~
- ~~Sistem notifikacija, ali notifikacije kao od sistema - eksterno rešeno~~
- Kako izgleda kada se menja vlasnik propertija?
- ~~Filtriranje i sortiranje~~
- ~~Dodavanje pravila, recimo za otkazivanje. Opcija za opt-out kad npr. naplatimo više ako može opt-out - **Nećemo**~~
- Da li adminu treba omogućiti da menja objave ili da može samo da ih banuje? 

# Definisanje mikroservisa

Treba obratiti pažnju na to da svaki mikroservis bude zamenjiv kompletno, kao i da se lako menja

### Pitanja: 

- Da li su auth i account management dva različita servisa, jer u jednom slučaju imamo klasičnu autentifikaciju a u drugom imamo da superadin dodaje admine.
- Ako razdvajamo mikroservise na osnovu poddomena, da li možemo da narušimo SRP na osnovu domenskog modela...
- Da li chat service treba da zavisi od rezervacije, u smislu da postoje neka ograničenja
- Da li rejting koristi property ili rating servis koristi property management service. Da li kad se oceni property rating mikroservis poziva property management servis.
- Da li property info service i property management koriste istu bazu ili će property info da ima zavisnost ka property management?

**Svaki mikroservis treba da ima svoj logging sistem**

### Mogući problemi

Ako za User imamo **jednu bazu** onda imamo role i primarni ključ će da bude email i rola kao kompleksni ključ. Tada može samo jedan mikroservis. Mora da se pazi oko dupliranja u rolama.

Sve vezano za User Account bi trebalo da bude u jednom mikroservisu zbog CPP!

Neka frontend bude što **gluplji**!