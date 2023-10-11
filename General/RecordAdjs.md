# Práce se záznamy v tabulce

Prostě shrnutí toho jak funguje úprava dat v tabulce

- Validate
- Modify
- Init
- Delete

## Validate

Stejný jako **:=** ale navíc triggeruje [OnValidate](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/triggers-auto/field/devenv-onvalidate-field-trigger) !!

→ Měl by se používat místo :=

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
        end;                 
    end;
```
