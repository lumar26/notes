Problem nastaje pri brisanju entiteta iz baze ako taj entitet ima referencu na druge entitete i za njih je definisan EAGER loading. Tad uopšte i neće da izbriše red u tabeli jer je to kao neko difoltno ponašanje.

Može da se reši tako što se Override-uje ta metoda u repozitorijumu, ručno se napiše query i stavi se @Modifying nad tom metodom.

Ili tako što se stavi LAZY fetching
