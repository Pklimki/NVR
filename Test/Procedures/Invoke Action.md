> Cílem je vyvolat nějakou akci na stránce - např. kliknutí na tlačítko "Publikovat". U těchto akcí je pak nezbytné nezapomenout na tzv. Handlery, které obsluhují vyskakovací okna, jenž obvykle u podobných událostí vyskakují.


``` csharp
codeunit 78745 "NVR RMWS Order Multiple"
{
    Subtype = Test;
    TestPermissions = Disabled;

    [Test]
    [HandlerFunctions('MessageHandler')]
    procedure TestOrderMultipleForNewItem()
    var
        NVRSTPCProductCatalog: Record "NVR STPC Product Catalog";
        NVRSTPCProductCatalogTestPage: TestPage "NVR STPC Product Catalog";
    begin
        Init();
        // Obvykle práce s daty
        Commit();
        InvokePublish(NVRSTPCProductCatalogTestPage, NVRSTPCProductCatalog);
    end;


    procedure InvokePublish(var NVRSTPCProductCatalogTestPage: TestPage "NVR STPC Product Catalog"; var NVRSTPCProductCatalog: Record "NVR STPC Product Catalog")
    begin
        NVRSTPCProductCatalogTestPage.OpenEdit();                               // Otevře stránku v editačním módu
        NVRSTPCProductCatalogTestPage.GoToRecord(NVRSTPCProductCatalog);        // Nastaví záznam na stránce
        NVRSTPCProductCatalogTestPage.Publish.Invoke();                         // Zavolá akci Publish
        NVRSTPCProductCatalogTestPage.Close();                                  // Zavře stránku
    end;

    [MessageHandler]
    procedure MessageHandler(Message: Text)
    begin
    end;
}
```
