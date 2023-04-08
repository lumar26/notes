# Definisanje domenskog modela u okviru front-end aplikacije

### Izvori: 
[O definisanju modela u typescript aplikacijama](https://tech.cornershop.io/domain-modeling-for-frontend-applications-using-typescript-2bc162fd94a0)
[O korišćenju `nterface i type umesto class](https://javascript.plainenglish.io/why-you-should-generally-prefer-typescript-interfaces-and-custom-types-over-classes-d145814218ce)


Prvo: svakako treba da se definiše model.

Drugo: typescript nudi dosta funkcionalnosti koje olakšavaju kreiranje tipova, u smislu proširivanja postojećih, davanje alijasa, ograničavanje mogućih vrednsosti za neki tip na raznovrsne načine, itd...

### Tip 1 

Moguće je proštiriti postojeći tip nekim vrednostime uz pomoć `&` operatora. Ova pojava se zove __intersection__.

```
interface BaseToDo {
  id: string
  title: string
  completed: unknown
}
type CompletedToDo = BaseToDo & {
  completed: true
}
```

### Tip 2

Za sve situacije gde ima imalo smisla da se definiše novi tip podatka, bilo da je proširenje/suženje postojećeg ili novi iz korena, to treba da se uradi. Treba izbeći da se bilo gde u kodu koriste objekti čiji je tip `any` ili nije definisan.

### Tip 3

Kreiranje immutable promenljivih se postiže sa naredbom `as const` nakon definisanja varijable čime se postiže njena nepromenljivost.

```
const example = {
  name: 'JohnDoe',
  isHereToStay: true,
  mother: {
    name: 'JaneDoe',
  },
} as const;
```

Šta sve radi `as const`: 
- It narrows the primitives like strings to exact literal types (e.g., the “JohnDoe” string gets changed into a type that can only have “JohnDoe” as value).
- It applies the readonly modifier to everything (including nested data structures)
- It transforms array literals into readonly tuples
