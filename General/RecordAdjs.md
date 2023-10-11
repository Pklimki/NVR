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
local procedure GetLastCommentLine(DocumentType: Enum "Sales Document Type"; DocumentNo: Code[20]; DocumentLineNo: Integer): Integer
    var
        CommentLine: Record "Sales Comment Line";
    begin
        CommentLine.SetRange("Document Type", DocumentType);
        CommentLine.SetRange("No.", DocumentNo);
        CommentLine.SetRange("Document Line No.", DocumentLineNo);
        if CommentLine.FindLast() then
            exit(CommentLine."Line No.");
    end;
```
