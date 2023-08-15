# Vytvoření nové aplikace

> Pokud zadání tasku obsahuje i vytvoření nové appky, je potřeba několik detailů od konzultanta, zbytek udělá pipelina

Spuštěním [Pipeliny na vytváření appek](https://navertica.visualstudio.com/BusinessCentral/_build?definitionId=313) s parametry:

1. Target Project: BCčko / Summit (podle zákazníka)
2. Application Name: Jméno appky (zadá konzultant)
3. Repository Name: Jako jméno appky ale bez mezer
4. Prefix: Vychází z názvu appky (zeptat konzultanta)
5. Object count: nechat 50
6. Object start ID: vyplní se automaticky
7. Branch: Podle QA zákazníka [najít v Enviroments](https://navertica.visualstudio.com/BusinessCentral/_search?text=QA*&type=workitem&lp=workitems-Project&filters=Projects%7BBusinessCentral%7DWork%20Item%20Types%7BEnvironment%7D&pageSize=25&includeFacets=false)
8. Extension Type: PTE

**RUN**

<img src="/Apps/Pics/vytvoreni_app.png" alt="MarineGEO circle logo" style="width: 250px;"/>

