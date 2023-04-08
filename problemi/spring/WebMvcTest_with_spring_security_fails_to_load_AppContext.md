# Problem: neće da se učita aplikacioni konteks kad hoću da testiram kontroler

Stvar je u tome što sve može da se pročita lepo iz error log-a.

Bio je slučaj da nije moglo da nađe neki Bean (JwtUtil) koji doduše jeste bio definisan kao komponenta, dakle i kao Bean... Ali iz nekog nepoznatog razloga nije htelo.

### **Rešenje**

Pristup je bio da u custom konfiguraciji ručno definišem JwtUtil Bean, i da bi taj bean bio dostupan u test klasi, tu test klasu sam morao da anotiram sa @Import(Config.class).

Nakon toga sam uspeo da pokrenem ApplicationContext.
