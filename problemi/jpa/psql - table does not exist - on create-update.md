Kada se u application properties stavi `spring.jpa.hibernate.ddl-auto=create` dobija se greška pri izvršavanju ddl naredbi.

`Caused by: org.postgresql.util.PSQLException: ERROR: relation "users" does not exist` kad treba da se doda spoljni ključ nekoj tabeli koja ima referencu ka `User` klasi.

__Rešenje__

Suštinski samo se nije kreirala tabela `users` jer je bila greška u definisanju boolean polja. Definisao sam neki _tinyint_ tip koji ne postoji...  
