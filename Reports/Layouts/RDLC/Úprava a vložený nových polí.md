# Úprava a vložení nových polí
## Zadání
Zákazník chtěl na fakturách zaměnit určitá pole za jiná nebo je úplně smazat. V průběhu tasku bylo také zjištěno, že bude i potřeba vytvořit nové pole pro servisní e-mail (toto pole bylo potřeba u dvou faktur).

V rámci tasku se měly upravit tři faktury -> Layouty:
| Nabídka Servisu                                                                                         | Servisní Zakázka                                                             | Provedený Servis - náhled |                
| ----------------------                                                                                  | ----------------------                                                       | ---------------------- |
| <img src="/Reports/Images/Dataset/NabidkaServisu.png" style="width: 500px;"/>                           | <img src="/Reports/Images/Dataset/ServisZakazka.png" style="width: 500px;"/> | <img src="/Reports/Images/Dataset/NahledServisu.png" style="width: 500px;"/> |

## Postup

1. Zjištění Appek, ve kterých se reporty s layouty nachází (včetně kde je najít v BC).
   * Při hledání, kde se reporty v BC tisknou může pomoc "Výběr Sestav" a "Rozvržení Sestav".
   * Pokud je ta faktura tisknuta Microsoftí Appkou, tak bude třeba udělat rozšíření daného Reportu a vytvořit nový layout, do kterého zkopírujeme obsah toho oficiálního. Poté můžeme provádět změny.
     
2. Přidání potřebných polí do reportu.
   * Příklad jak vypadá implementace nových polí do reportu:
    ```al
    reportextension 71895 "NVR IRPCZ Service Order CZL" extends "Service Order CZL"
    {
      RDLCLayout = './Src/Layouts/NVRIRPCZServiceOrderCZL.rdl'; // Tady je vidět jaký Layout je výchozí pro tento Report
      dataset
      {
          add("Service Header")
          {
              column(NVRIRPCZ_BusinessCaseNoLbl; BusinessCaseNoLbl) // Label pro námi přidané pole (musí se deklarovat níže ve var)
              {
              }
              column(NVRIRPCZ_BusinessCaseNo; "NVR IBGBC Business Case No.") // Tady se získá obsah toho pole
              {
              }
              ...
      }
     var
        BusinessCaseNoLbl: Label 'Business Case No.'; // Zde je deklarovaná proměnná label pro naše pole
        ...
      ```
    * **Potřebuju více layoutů v jednom reportu**?
      > Tak nahradím "RDLCLayout = ..." a "DefaultLayout = ..." za **"DefaultRenderingLayout = ..."**. Namísto "..." zadáme defaultní layout, který vytvoříme vytvořením **rendering** sekce (na stejné úrovní jako dataset). 
V **rendering** poté upřesníme jaké layouty budeme v tomto reportu používat (viz. příkladový kód).
      
      - Příklad aplikování více layoutů:
      ```al
      report 71976 "NVR IRP Service Quote"
      {
        DefaultRenderingLayout = ServiceQuote;
        ...
        rendering
        {
          layout(ServiceQuote)
          {
              Type = RDLC;
              Caption = 'Service Quote';
              LayoutFile = './Src/Layouts/ServiceQuote.rdl';
          }
  
          layout(ServicesProvided)
          {
              Type = RDLC;
              Caption = 'Services Provided - preview';
              LayoutFile = './Src/Layouts/ServicesProvided.rdl';
          }
         }
        ...
      ```
4. Úprava layoutu v Report Builderu.
   * "Open Externally" na daném layoutu.
   * Hodnoty polí v layoutu jsou buďto vložena přímo (v "Expression" na poli vidíme název pole + ".Value"). V ten moment je záměna/tvoření nových polí jednoduchá (stačí změnit tyto hodnoty). Dále mohou být data tahána z tvz. neviditelných polí (v Builderu jsou vidět jako růžová). 
To znamená že v Expression pole vidíme "Code.GetData(x)".
     - Zaměnění polí:
       > Pokud tady chceme změnit obsah pole za jiný obsah, musíme jít do Expression růžového pole a tam odpočítat pole na x-tém pořadí (dle Get.Data(x)). Poté změníme název pole za naše.
     - Nová pole:
       > Pokud chceme nové pole přidat. Přidáme ho do růžového pole na x-té místo (většinou nakonec), a kde chceme data z pole, zadáme "Code.GetData(x)".
   * Nesmíme zapomenout toto udělat jak pro **labely** tak pro **hodnoty** polí.
   
