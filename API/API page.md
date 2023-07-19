# API

> **A**pplication **P**rogramming **I**nterface je komunikační rozhraní, prostřednictvím kterého si mohou 2 různé aplikace vyměňovat data. API má například i internetové bankovnictví nebo ChatGPT. Když se na nějakou stránku přihlašuješ prostřednictvím facebooku nebo gmailu, tak tato stránka využívá API! Díky API tak můžeš ve své aplikaci využít data jiné aplikace. 


# API (page)

API page programujeme velmi podobným způsobem, jako klasickou page v BC. Jsou zde jen nové vlastnosti, které je nezbytné nastavit, a zároveň existují i nějaké typografické rozdíly.

__**Vlastnosti:**__
``` csharp
PageType = API;                                // Typ stránky = API
Caption = 'customer', Locked = true;           // Popis, Locked IDK ???????????????????????????????????????????????????????????????????
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

``` csharp
layout
    {
        area(Content)
        {
            repeater(control1)
            {
                field(number; Rec."No.")
                {
                    Caption = 'number', Locked = true;
                }
                field(name; Rec.Name)
                {
                    Caption = 'name', Locked = true;
                }
                field(type; Rec."Contact Type")
                {
                    Caption = 'type', Locked = true;
                }
            }
        }
    }
```

## Povinná políčka na stránce
Existují 2 políčka, která **musí být vždy vytažena:**

- Pole **"SystemId"** s názvem **"id"**
- Pole **"SystemModifiedAt"** s názvem **"lastModifiedDateTime"**
    
> Je nezbytné dodržet přesný název pro tato pole!

``` csharp
layout
    {
        area(Content)
        {
            repeater(control1)
            {
                field(id; Rec.SystemId) { }
                field(lastModifiedDateTime; Rec.SystemModifiedAt) { }
            }
        }
    }
```


# Celý kód

Jelikož zatím task na API nebyl, tak jsem si kód vypůjčil z VBHReportingIntegration - CustomerAPI.Page.al


``` csharp
page 79055 "NVR VRI Customer API"
{
    PageType = API;
    Caption = 'customer', Locked = true;
    APIPublisher = 'navertica';
    APIGroup = 'reporting';
    APIVersion = 'v1.0';
    EntityName = 'customer';
    EntitySetName = 'customers';
    SourceTable = Customer;
    DelayedInsert = true;
    ODataKeyFields = SystemId;
    Editable = false;
    InsertAllowed = false;
    DeleteAllowed = false;
    ModifyAllowed = false;

    layout
    {
        area(Content)
        {
            repeater(control1)
            {
                field(id; Rec.SystemId)
                {
                    Caption = 'id', Locked = true;
                }
                field(number; Rec."No.")
                {
                    Caption = 'number', Locked = true;
                }
                field(name; Rec.Name)
                {
                    Caption = 'name', Locked = true;
                }
                field(type; Rec."Contact Type")
                {
                    Caption = 'type', Locked = true;
                }
                field(address; Rec.Address)
                {
                    Caption = 'address', Locked = true;
                }
                field(address2; Rec."Address 2")
                {
                    Caption = 'address2', Locked = true;
                }
                field(city; Rec.City)
                {
                    Caption = 'city', Locked = true;
                }
                field(county; Rec.County)
                {
                    Caption = 'county', Locked = true;
                }
                field(country; Rec."Country/Region Code")
                {
                    Caption = 'country', Locked = true;
                }
                field(postCode; Rec."Post Code")
                {
                    Caption = 'postCode', Locked = true;
                }
                field(phoneNumber; Rec."Phone No.")
                {
                    Caption = 'phoneNumber', Locked = true;
                }
                field(email; Rec."E-Mail")
                {
                    Caption = 'email', Locked = true;
                }
                field(website; Rec."Home Page")
                {
                    Caption = 'website', Locked = true;
                }
                field(salespersonCode; Rec."Salesperson Code")
                {
                    Caption = 'salespersonCode', Locked = true;
                }
                field(balanceDue; Rec."Balance Due")
                {
                    Caption = 'balanceDue', Locked = true;
                }
                field(creditLimit; Rec."Credit Limit (LCY)")
                {
                    Caption = 'creditLimit', Locked = true;
                }
                field(taxLiable; Rec."Tax Liable")
                {
                    Caption = 'taxLiable', Locked = true;
                }
                field(taxAreaId; Rec."Tax Area ID")
                {
                    Caption = 'taxAreaId', Locked = true;
                }
                field(taxAreaDisplayName; TaxAreaDisplayNameGlobal)
                {
                    Caption = 'taxAreaDisplayName', Locked = true;
                }
                field(vatRegistrationNumber; Rec."VAT Registration No.")
                {
                    Caption = 'taxRegistrationNumber', Locked = true;
                }
                field(currencyId; Rec."Currency Id")
                {
                    Caption = 'currencyId', Locked = true;
                }
                field(currencyCode; CurrencyCodeTxt)
                {
                    Caption = 'currencyCode', Locked = true;
                }
                field(paymentTermsId; Rec."Payment Terms Id")
                {
                    Caption = 'paymentTermsId', Locked = true;
                }
                field(shipmentMethodId; Rec."Shipment Method Id")
                {
                    Caption = 'shipmentMethodId', Locked = true;
                }
                field(paymentMethodId; Rec."Payment Method Id")
                {
                    Caption = 'paymentMethodId', Locked = true;
                }
                field(blocked; Rec.Blocked)
                {
                    Caption = 'blocked', Locked = true;
                }
                field(lastModifiedDateTime; Rec.SystemModifiedAt)
                {
                    Caption = 'lastModifiedDateTime', Locked = true;
                }
                field(registrationNoCZL; Rec."Registration No. CZL")
                {
                    Caption = 'Registration No.', Locked = true;
                }
                field(paymentMethodCode; Rec."Payment Method Code")
                {
                    Caption = 'Payment Method Code', Locked = true;
                }
                field(billToCustomerNo; Rec."Bill-to Customer No.")
                {
                    Caption = 'Bill-to Customer No.', Locked = true;
                }
                field(totDefCreditLimit; Rec."NVR VSM Tot. Def. Credit Limit")
                {
                    Caption = 'totDefCreditLimit', Locked = true;
                }
                field(totTempCreditLimit; Rec."NVR VSM Tot. Temp.Credit Limit")
                {
                    Caption = 'totTempCreditLimit', Locked = true;
                }
                field(totalTempCrLFrom; Rec."NVR VSM Total. Temp.Cr.L. From")
                {
                    Caption = 'totalTempCrLFrom', Locked = true;
                }
                field(totalTempCrLTo; Rec."NVR VSM Total. Temp.Cr.L. To")
                {
                    Caption = 'totalTempCrLTo', Locked = true;
                }
                field(tolOfDaysPastDue; Rec."NVR VSM Tol. of Days Past Due")
                {
                    Caption = 'tolOfDaysPastDue', Locked = true;
                }
                field(tempTolOfDays; Rec."NVR VSM Temp. Tol. of Days")
                {
                    Caption = 'tempTolOfDays', Locked = true;
                }
            }
        }
    }

    trigger OnAfterGetRecord()
    begin
        SetCalculatedFields();
    end;

    var
        GraphMgtGeneralTools: Codeunit "Graph Mgt - General Tools";
        LCYCurrencyCode: Code[10];
        CurrencyCodeTxt: Text;
        TaxAreaDisplayNameGlobal: Text;

    local procedure SetCalculatedFields()
    var
        TaxAreaBuffer: Record "Tax Area Buffer";
    begin
        CurrencyCodeTxt := GraphMgtGeneralTools.TranslateNAVCurrencyCodeToCurrencyCode(LCYCurrencyCode, Rec."Currency Code");
        TaxAreaDisplayNameGlobal := TaxAreaBuffer.GetTaxAreaDisplayName(Rec."Tax Area ID");
    end;
}
```
