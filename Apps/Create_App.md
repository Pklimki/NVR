# Vytvoření nové aplikace

> Pokud zadání tasku obsahuje i vytvoření nové appky, je potřeba udělat několik kroků, ve kterých musím mít informace od konzultanta a architekta

## Spuštění [Pipeliny na vytváření appek](https://navertica.visualstudio.com/BusinessCentral/_build?definitionId=313) s parametry:

1. Target Project: BCčko / Summit (podle zákazníka)
2. Application Name: Jméno appky (zadá konzultant)
3. Repository Name: Jako jméno appky ale bez mezer
4. Prefix: NVR + (mezera) + 3 znaky, vychází z názvu appky (první písmenka názvu appky, [zkontrolovat že už to neexistuje → lze najít v Boards → Queries → Column options:](https://navertica.visualstudio.com/BusinessCentral/_queries/query/b821b1f9-1d3f-4b77-ac7a-3c07516eb7c1/) ve sloupečku Prefix)
5. Object count: nechat 50
6. Object start ID: vyplní se automaticky
7. Branch: Nejnovější [najít v Enviroments]
8. Extension Type: PTE

**RUN**

<img src="/Apps/Pics/vytvoreni_app.png" alt="MarineGEO circle logo" style="width: 250px;"/>

## Přiřazení na které vrstvě bude aplikace
9. Boards → Recently created → najít tu právě vytvořenou appku → Otevřít (je vedená jako **Feature**)
10. Přiřadit architekta, který je na tom projektu (najdu v UserStory)
11. Přepnout do záložky NVR
12. Area: změnit podle zákazníka (např. Business Central/Summit)
13. Application Layer: zvolit správnou vrstvu (měl by mi to říct architekt)

<img src="/Apps/Pics/vytvoreni_app1.png" alt="MarineGEO circle logo" style="height: 350px;"/>

## Přiřazení Featuru k User Story, ve kterém se řeší Task
15. Vpravo dole Related World dát **add link** → Related→ najít tu app
