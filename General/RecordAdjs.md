# Práce se záznamy v tabulce

Prostě shrnutí toho jak funguje úprava dat v tabulce

- Validate
- Modify
- Init
- Delete

## [Validate](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/record/record-validate-method)

Stejný jako **:=** ale navíc triggeruje [OnValidate](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/triggers-auto/field/devenv-onvalidate-field-trigger) !!

→ Pro úpravu záznamu ho používat místo :=

```al
// Funkce která změní hodnotu komentáře podle čísla dokumentu
local procedure ChangeCommentToPrdel(DocumentNo: Code[20]) 
    var
        CommentLine: Record "Sales Comment Line"; // Proměnná záznamu
    begin
        CommentLine.SetRange("No.", DocumentNo); // Filtrace
        if CommentLine.FindFirst() then begin
            CommentLine.Comment := "Prdel"; // neudělá se OnValidate trigger
            CommentLine.Validate(Comment, "Prdel"); // udělá se OnValidate trigger
            <span style="color: red;">CommentLine.Comment := "Prdel";</span> // This part will be red
            // tady chybí 1 řádek → viz Modify
        end;                 
    end;
```

## [Modify](https://learn.microsoft.com/en-us/dynamics-nav/modify-function--record-)

Když sem udělal nějaký změny nad záznamem a **chci je propsat do tabulky**

→ Pokud sem použil Validate, tak chci použít i Modify

> jako parametr má Boolean který říká zda se má zavolat [OnModify](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/triggers-auto/table/devenv-onmodify-table-trigger) trigger

```al
Funkce která změní hodnotu komentáře podle čísla dokumentu
//local procedure ChangeCommentToPrdel(DocumentNo: Code[20]) 
//    var
//        CommentLine: Record "Sales Comment Line";
//    begin
//        CommentLine.SetRange("No.", DocumentNo);
//        if CommentLine.FindFirst() then begin
//            CommentLine.Comment := "Prdel";
//            CommentLine.Validate(Comment, "Prdel");
              CommentLine.Modify(true); // Když to neudělám, Validate bude k prdu
//        end;                 
//    end;
```

