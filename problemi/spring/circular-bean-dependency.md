# Problem su kružne zavisnosti

Npr imam u okviru Spring Security-ja klasu SecurityConfigurer gde sam definisao Bean za PasswordEncoder. Ta klasa takođe koristi UserService jer mu treba to za AuthenticationManagerBuilder-a.
U klasi UserService se koristi PasswordEncoder i Spring to prepoznaje kao kružnu zavisnost.

┌─────┐
| jwtRequestFilter defined in file [/home/lumar26/spring-projects/geneaology_spring_boot/target/classes/rs/ac/bg/fon/np/genealogy_spring_boot/security/filter/JwtRequestFilter.class]
↑     ↓
|  userService defined in file [/home/lumar26/spring-projects/geneaology_spring_boot/target/classes/rs/ac/bg/fon/np/genealogy_spring_boot/user/UserService.class]
↑     ↓
|  securityConfiguration defined in file [/home/lumar26/spring-projects/geneaology_spring_boot/target/classes/rs/ac/bg/fon/np/genealogy_spring_boot/security/config/SecurityConfiguration.class]
└─────┘

### **Rešenje**

Izdvojio sam PasswordEncoder u drugu konfiguracionu klasu, tako da sad ne postoji kruženje.

Takođe, loša je praksa da se autowire radi nad poljima jer to onemogućava da te zavisnosti budu final. Zbog toga je dobra praksa da se Autowire radi nad konstruktorima.
