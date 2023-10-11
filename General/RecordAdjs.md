# Práce se záznamy v tabulce

Shrnutí metody pro úpravu dat v tabulce:

- Validate
- Modify
- Init & Insert
- Delete

Příklad: Mějme tento nefunkční kód, ve kterém se pokoušíme změnit záznam v tabulce
```al
// Funkce která změní hodnotu komentáře podle čísla dokumentu
local procedure ChangeComment(DocumentNo: Code[20]) 
    var
        CommentLine: Record "Sales Comment Line"; // Proměnná záznamu
    begin
        CommentLine.SetRange("No.", DocumentNo); // Filtrace
        if CommentLine.FindFirst() then begin
            CommentLine.Comment := "Komentář obecný"; // pokus o změnu hodnoty komentáře
        end;                 
    end;
```

## [Validate](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/record/record-validate-method)

Funkčně stejný jako **:=** ale navíc se stane [OnValidate](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/triggers-auto/field/devenv-onvalidate-field-trigger) trigger.

→ Pro úpravu dat by se měl používat namísto :=

```al
//local procedure ChangeComment(DocumentNo: Code[20]) 
//    var
//        CommentLine: Record "Sales Comment Line";
//    begin
//        CommentLine.SetRange("No.", DocumentNo);
//        if CommentLine.FindFirst() then begin
            CommentLine.Comment := "Komentář obecný"; // provede se OnValidate trigger
            CommentLine.Validate(Comment, "Komentář obecný"); // neprovede se OnValidate trigger
//        end;                 
//    end;
```

## [Modify](https://learn.microsoft.com/en-us/dynamics-nav/modify-function--record-)

Slouží pro **propsání změn provedených nad záznamem do tabulky**.

> Pokud byl použit Validate, pravděpodobně by měl být použit i Modify, pokud neměl být pouze zavolán OnValidate trigger

> Jako parametr má Boolean který říká zda se má zavolat [OnModify](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/triggers-auto/table/devenv-onmodify-table-trigger) trigger.

```al
//local procedure ChangeComment(DocumentNo: Code[20]) 
//    var
//        CommentLine: Record "Sales Comment Line";
//    begin
//        CommentLine.SetRange("No.", DocumentNo);
//        if CommentLine.FindFirst() then begin
//            CommentLine.Validate(Comment, "Komentář obecný");
              CommentLine.Modify(true); // bez Modify by se Validate změna nepropsala do taublky
//        end;                 
//    end;
```

## [Init](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/record/record-init-method) & [Insert](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/record/record-insert--method)

**Init** = Inicializuje záznam

***POZOR!*** - mezi Init a Insert je potřeba <ins>nastavit VŠECHNY PRIMÁRNÍ KLÍČE</ins> záznamu

**Insert** = Vloží záznam do tabulky

→ Např. pokud jsem nafiltroval, záznam jsem nenalezl a tudíž ho chci vytvořit = záznam inicializuji, nastavím mu PK, vložím ho do tabulky

> Pozn.: **Rec** znamená ***aktuální stav záznamu*** - tzn. záznam, nad kterým jsou momentálně prováděny změny

```al
Funkce která změní hodnotu komentáře podle čísla dokumentu
//local procedure ChangeComment(DocumentNo: Code[20]) 
//    var
//        CommentLine: Record "Sales Comment Line";
//    begin
//        CommentLine.SetRange("No.", DocumentNo);
//        if CommentLine.FindFirst() then begin
//            CommentLine.Validate(Comment, "Prdel");
//            CommentLine.Modify(true); // Když to neudělám, Validate bude k prdu
//        end
//        else begin
              CommentLine.Init(); // Inicializace záznamu

              CommentLine.Validate("Document Type", Rec."Document Type"); // Nastavení PK1
              CommentLine.Validate("No.", Rec."No."); // Nastavení PK2
              CommentLine.Validate(Comment, "Komentář obecný"); // komentář
              
              CommentLine.Insert(true); // Vložení záznamu do tabulky + zavolání onInsert
//        end;                
//    end;
```
## [Delete](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/record/record-delete-method)

Pro smazání existujícího záznamu z tabulky.

```al
 
//local procedure ChangeComment(DocumentNo: Code[20]) 
//    var
//        CommentLine: Record "Sales Comment Line";
//    begin
//        CommentLine.SetRange("No.", DocumentNo);
          CommentLine.SetRange("Comment", 'Nevhodný komentář');
//        if CommentLine.FindFirst() then begin
            CommentLine.Delete(true);
//        end;                
//    end;
```
