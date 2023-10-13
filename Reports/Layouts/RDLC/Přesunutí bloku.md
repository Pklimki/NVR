# Přesunutí tabulky v RDLC layoutu

V rámci tasku bylo potřeba na faktuře přesunout tabulku na jinou pozici na stránce tak, aby tabulka **držela pohromadě** → pokud by např. byly 2 řádky na konci 1. stránky a 3 řádky na začátku druhé, musí se přesunout celá tabulka na 2. stránku pohromadě.


<img src="/Reports/Images/Dataset/Presunuti_bloku.png" style="width: 700px;"/>

## Postup

1. Pokud je layout .rdl tak ho přejměnovat na .rdlc
2. Otevřít layout pomocí Visual Studia (ne code, velké visuálko - pozn. potřeba mít rozšíření Microsoft RDLC Report Designer)
3. Najít si tu tabulku pro přesunutí <img src="/Reports/Images/Dataset/Presunuti_bloku1.png" style="width: 900px;"/>
4. Kliknout do tabulky aby se zobrazili obdélníky na označování řádků (po levé straně), sloupců (nahoře) a **celé tabulky** (vlevo nahoře) <img src="/Reports/Images/Dataset/Presunuti_bloku2.png" style="width: 400px;"/>
5. Kliknout na označení celé tabulky levým → Na okraj tabulky pravým → Rectangle Properties → General → zaškrtnout **"Keep contents together if possible"**
6. Krok 5 opakovat pro všechny řádky a sloupečky tabulky (Levým na označení řádku → pravým → Tablix properties → General → Keep together on one page if possible)
7. Potom už stačí označit celou tabulku a přesunout ji na požadované místo
8. Uložit, zavřít, pokud byl původně layout .rld přejmenovat ho zpět na .rld
