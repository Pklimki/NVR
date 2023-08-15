# Prolinkování API položek na API stránce

Stejně jako u [Datasetu](/Reports/Dataset.md) lze u [API Page](API%20page.md) položky prolinkovat do sebe. K tomu se, narozdíl od datasetu, používá klíčové slovo **part**. 

Dopsat, až na to budeme mít nějaký příklad.

# [Zadání tasku](https://navertica.visualstudio.com/BusinessCentral/_workitems/edit/92552/)

Na straně BC bude připraveno API, které umožní zpracovat zpětnou notifikaci o vyskladněném množství na prodejní objednávce. 
Endpoint bude mít následující strukturu: 
![Struktura endpointu](Images/Api%20page%20link%20task.png)

# Jak to bude fungovat

Zákazník chce mít v endpointu informace z prodejní objednávky - jak z **hlavičky**, tak samozřejmě **z řádků**. Postup bude obdobný jako u [datasetu](/Reports/Dataset.md) - do políček hlavičky vnoříme řádky. Způsob vnoření bude ale odlišný - budeme muset naprogramovat 2 API page - 1 pro hlavičku a 1 pro řádky. API page pro řádky pak vnoříme do API page pro hlavičku. 



__**PermissionSet:**__

K api page musí vždy být vždycky permission set

__**Vlastnosti:**__
``` csharp
PageType = API;                                // Typ stránky = API
Caption = 'customer', Locked = true;           // Popis, Locked - nevygeneruje se překlad
APIPublisher = 'navertica';                    // Publisher	
APIGroup = 'reporting';                        // Skupina API, která je pak součástí URL dotazu. Používá se pro nějaké logické dělení
APIVersion = 'v1.0';                           // Verze API
EntityName = 'customer';                       // Jednotné číslo entity
EntitySetName = 'customers';                   // Množné číslo entity
SourceTable = Customer;                        // Zdrojová tabulka
DelayedInsert = true;                          // Povinná vlastnost na editovatelné API stránce (Editable = true). Funguje tak, že se nejprve zadají hodnoty všech polí a poté se záznam vloží najednou.
ODataKeyFields = SystemId;                     // Vlastnost, která říká, podle čeho bude jednoznačně identifikovatelný daný záznam. V případě API je doporučeno používat SystemId, neboť bude pro daný záznam vždy stejný. SystemId je nějaké ID generované BC.
Editable = false;                              // Editovatelná API page
InsertAllowed = false;                         // Povoleno vkládání záznamů
DeleteAllowed = false;                         // Povoleno odstraňování záznamů
ModifyAllowed = false;                         // Povolena modifikace záznamů
```

# Políčka na stránce

Zde nejsou žádné povinné vlastnosti. Název políčka, který bude viditelný na API page **musí začínat malým písmenem** - tzv. __**camelCasing**__. Pokud přidáme caption, tak také platí camelCasing pravidlo.

Stejně jako u [Datasetu](/Reports/Dataset.md) lze položky prolinkovat do sebe. K tomu se, narozdíl od datasetu, používá klíčové slovo `parts`. Podrobněji popsáno v návodu na [Linkování API položek na API stránce](Linkovani%20api%20polozek.md)


