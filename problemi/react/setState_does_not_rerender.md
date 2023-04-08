# Nakon što se pozove setState komponenta neće da se rerenderuje.

Problem nastaje kad npr imamo objekat **obj** koji treba da se izmeni. I npr. ako uradimo `obj.id = newId` i onda nakon toga `setObj(obj)` react neće da prepozna to kao novo stanje jer smo prosledili isti objekat kao što je do tad i bio, bez obzira što je izmenjen.

Rešenje je da se u setState stavi novi objekat npr. ovako: `setObj({...obj})`. 

Isto važi i za nizove, treba da se postojeći mapira u novi.
