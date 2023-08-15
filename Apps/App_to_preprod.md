# Nasazení appky do Pre-produ
>Pre-production = prostředí pro testování funkcionality, které se přesně podobá ostrý.

1. Nasadit aplikaci **do QA** (po schválení Pull Requestu musí doběhnout 4/4 Stage pipeliny) <img src="/Apps/Pics/4stages.png" alt="MarineGEO circle logo" style="height: 23px;"/>
2. Devops → Pipelines → All → Zákazník → Release → najít aplikaci → Run Pipeline
3. - Target enviroment name: Zakaznik_Test
   - Resource: vybrat **master** větev takové verze, kterou chci releasnout
   - Zbytek nechat na výchozím nastavení
4. až doběhne ta Release pipeline je aplikace nasazená v Pre-produ

<img src="/Apps/Pics/Run_preprod.png" alt="MarineGEO circle logo" style="width: 350px;"/>
