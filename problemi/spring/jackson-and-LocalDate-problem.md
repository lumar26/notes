## Problem:

Javljala se greška da nije podržana konverzija za LocalDate kad koristim ručno ObjectMapper u test klasama.

**com.fasterxml.jackson.databind.exc.InvalidDefinitionException: Java 8 date/time type `java.time.LocalDate` not supported by default**

# Rešenje:

Poenta je bila da se dodaju 3, tačno 3 zavisnosti:

```
     <dependency>
            <groupId>com.fasterxml.jackson.datatype</groupId>
            <artifactId>jackson-datatype-jsr310</artifactId>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.module</groupId>
            <artifactId>jackson-module-parameter-names</artifactId>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.datatype</groupId>
            <artifactId>jackson-datatype-jdk8</artifactId>
        </dependency>
```

i da se direktno iskonfiguriše taj object mapper:

`ObjectMapper om = new ObjectMapper().registerModule(new JavaTimeModule())
            .configure(SerializationFeature.WRITE_DATES_AS_TIMESTAMPS, false);`

Ali ovo izgleda je neophodno kad se radi ručno sa njim, kad konvertuje ovako klasično u kontrolerima tad izgleda radi sve okej


