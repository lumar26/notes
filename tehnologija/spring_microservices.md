# Микросервиси користећи *Spring Boot*

## Микросервисна архитектура

Миркосервисна архитектура подразумева да се апликација састоји из више независних сервиса, од којих је сваки сервис независна апликација, који су међусобно оркестрирани и сарађују. Ово се односи на време извршавања апликације тј. апликација у продукцији се састоји из више сервиса/пројеката. Уколко се нека апликација састоји из више пројеката или више апликација које се не развијају одједном она и даље може да буде монолитна. Суштина је да се архитектура уочава (у смислу да се посматра резултат) тек у време извршавања, а не у време развоја.