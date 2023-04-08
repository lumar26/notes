### Kako da promenimo verziju neke zavisnosti koju koristi spring boot a koja je već definisana u **starter** paketu

samo se doda u okviru `properties` taga verzija za konkretnu zavisnost
npr: 
`<hibernate.version>5.6.5.Final</hibernate.version>`

Inače greška je nastala kod Spring Data Jpa upita koji imaju u sebi predikat sa LIKE, startsWith ili endsWith gde je neki problem sa keširanjem i onda nakon prvog odrađenog upita u prvom sledećem dodaje neke \ karaktere nepotrebne
