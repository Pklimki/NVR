# Práce se záznamy v tabulce

Prostě shrnutí toho jak funguje úprava dat v tabulce

- Validate
- Modify
- Init
- Delete

## Validate

Stejný jako **:=** ale navíc triggeruje *OnValidate* !!

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
            CommentLine.Validate(Comment, "Prdel2"); // udělá se OnValidate trigger
        end;                 
    end;
```
