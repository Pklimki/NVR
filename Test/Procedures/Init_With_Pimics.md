``` csharp
codeunit 78745 "NVR RMWS Order Multiple"
{
    Subtype = Test;
    TestPermissions = Disabled;

    var
        UnitofMeasure: Record "Unit of Measure";
        NoSeries: Record "No. Series";
        NoSeriesLine: Record "No. Series Line";
        PIMXCatalogSetup: Record "PIMX Catalog Setup";
        LibraryInventory: Codeunit "Library - Inventory";
        LibraryUtility: Codeunit "Library - Utility";
        Inited: Boolean;


    [Test]
    procedure TestOrderMultipleForNewItem()
    begin
        Init();
        // TODO SOME TEST
    end;


    procedure Init()
    begin
        if Inited then
            exit;
        LibraryInventory.CreateUnitOfMeasureCode(UnitofMeasure);
        LibraryUtility.CreateNoSeries(NoSeries, true, false, false);
        LibraryUtility.CreateNoSeriesLine(NoSeriesLine, NoSeries.Code, '0001', '9999');
        PIMXCatalogSetup.Init();
        PIMXCatalogSetup."Item Group Numbers Sale" := NoSeries.Code;
        PIMXCatalogSetup.Insert();

        Clear(NoSeries);
        LibraryUtility.CreateNoSeries(NoSeries, true, false, false);
        LibraryUtility.CreateNoSeriesLine(NoSeriesLine, NoSeries.Code, '0001', '9999');

        PIMXCatalogSetup."Variant Nos." := NoSeries.Code;
        PIMXCatalogSetup.Modify();

        Inited := true;

    end;
}
```
