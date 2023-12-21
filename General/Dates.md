# Práce s datumy
* Nastavení v BC ovlivní, jakým formátem jsou datumy zadávány/vypisovány. Ovlivňuje to nastavení oblasti (Region) a jazyka (Language).
  
* Datové typy datumů:
  - [Date](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/date/date-data-type)
    - Pokud chceme do datového typu Date vložit nějakou hodnotu, tak je třeba dodžet syntax:
  
      → ***yyyymmddD*** - ***yyyy*** je rok, ***mm*** je měsíc, ***dd*** je den a pak "***D***", které je nutno zadat

  - [DateTime](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/datetime/datetime-data-type)
 
  - [DateFormula](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/dateformula/dateformula-data-type)

* Užitečné metody pro práci s daty:
  - [CreateDateTime](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-createdatetime-method)
      ```al
      Datetime := System.CreateDateTime(Date: Date, Time: Time);
      ```
  - [Today()](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-today-method)
    - **Today** můžeme využít k získání data z operačního systému. Je to ovlivněno opět nastavením BC. 
      ```al
      Date := System.Today();
      ```
    - Příklad použití:
      ```al
      var
          DateMsg: Label 'The current date is: %1';
          TodayDate: Date;
      begin
          TodayDate := Today;
          Message(DateMsg, TodayDate);  
      end;
      // Tento kod poté v BC vratí message okno s datumem z operačního systému (např. 12/03/20)
      ```
  - [Time()](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-time-method)
    - **Time** můžeme využít k získání času z operačního systému. Je to ovlivněno opět nastavením BC. 
      ```al
      Time := System.Time()
      ```
    - Příklad použití:
      ```al
      var
          TimeMsg: Label 'The current time is: %1';
          CurrentTime: Time;
      begin
          CurrentTime := Time;
          Message(TimeMsg, CurrentTime);  
      end;
      // Tento kod poté v BC vratí message okno s časem z operačního systému (např. 9:08:03 AM)
      ```
  - [CurrentDateTime()](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-currentdatetime-method)
    - **Time** můžeme využít k získání času z operačního systému. Je to ovlivněno opět nastavením BC. 
      ```al
      Time := System.Time()
      ```
    - Příklad použití:
      ```al
      var
          TimeMsg: Label 'The current time is: %1';
          CurrentTime: Time;
      begin
          CurrentTime := Time;
          Message(TimeMsg, CurrentTime);  
      end;
      // Tento kod poté v BC vratí message okno s časem z operačního systému (např. 9:08:03 AM)
      ```
  - [WorkDate()](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-workdate-method)
    - **WorkDate** můžeme využít k získání pracovního dne, který můžeme najít v nastavení BC.  
      ```al
      [WorkDate := ] System.WorkDate([NewDate: Date]));
      ```
    - Příklad použití:
      ```al
      var
          DateMsg: Label 'The work date is: %1';
          WorkDate: Date;
      begin
          WorkDate := WorkDate;
          Message(DateMsg, WorkDate);  
      end;
      // Tento kod poté v BC vratí message okno s pracovním datumem (např. 04/06/20)
      ```
  - [CalcDate()](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-calcdate-string-date-method)
    - **CalcDate** 
      ```al
      NewDate := System.CalcDate(DateExpression: Text [, Date: Date]);
      ```
  - [Date2DMY()](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-date2dmy-method)
  - [Date2DWY()](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-date2dmy-method)
  - [DT2Time()](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-dt2time-method)
    - **DT2Time** 
      ```al
      Time :=   System.DT2Time(Datetime: DateTime)
      ```
    - Příklad použití:
      ```al
      var
          Date1: Date;
          DateTime1: DateTime;
          Time1: Time;
      begin
          DateTime1 := CurrentDateTime;
          Date1 := DT2Time(DateTime1);
          Message(Format(Time1));
      end;
      // Tento kod poté v BC vratí message okno s přesným časem (např. 1:10:47 PM)
      ```
  - [DT2Date()](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-dt2date-method)
    - **DT2Date** 
      ```al
      Date :=   System.DT2Date(Datetime: DateTime)
      ```
    - Příklad použití:
      ```al
      var
          Date1: Date;
          DateTime1: DateTime;
          Time1: Time;
      begin
          DateTime1 := CurrentDateTime;
          Date1 := DT2Date(DateTime1);
          Message(Format(Date1));
      end;
      // Tento kod poté v BC vratí message okno s datumem (např. 11/28/22)
      ```

## Příklady z praxe:
