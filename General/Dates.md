# Práce s datumy
* Nastavení v BC ovlivní, jakým formátem jsou datumy zadávány/vypisovány. Ovlivňuje to nastavení oblasti (Region) a jazyka (Language).
  
* Datové typy datumů:
  - [Date](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/date/date-data-type)
    - Pokud chceme do datového typu Date vložit nějakou hodnotu, tak je třeba dodržet syntax:
  
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
      // Tento kod poté v BC vrátí message okno s datumem z operačního systému (např. 12/03/20).
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
      // Tento kod poté v BC vrátí message okno s časem z operačního systému (např. 9:08:03 AM).
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
      // Tento kod poté v BC vrátí message okno s časem z operačního systému (např. 9:08:03 AM)
      ```
  - [WorkDate()](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-workdate-method)
    - **WorkDate** můžeme využít k získání pracovního dne, který můžeme najít v nastavení BC.
      <img src="/General/Images/NastaveniPracDat.png" style="width: 300px;"/> 
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
      // Tento kod poté v BC vrátí message okno s pracovním datumem (např. 04/06/20).
      ```
  - [CalcDate()](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-calcdate-string-date-method)
    - **CalcDate** počítá nové datum dle výrazu (Date Expression) a reference na datum (Reference Date).
      ```al
      NewDate := System.CalcDate(DateExpression: String [, Date: Date])
      ```
    - Výraz může mít jakoukoli délku a čte se zleva doprava po jednom podvýrazu (SubExpression) za druhým. Syntax je následující:
      ```
      - DateExpression = [<SubExpression>][<SubExpression>][<SubExpression>]...
      - <SubExpression> = [<Sign>]<Term>-<Sign> = +|-
      - <Term> = <Number><Unit>|<Unit><Number>|<Prefix><Unit>
      - <Number> = pozitivní ingeter
      - <Unit> = D|WD|W|M|Q|Y  (D=day, WD=weekday, W=week, M=month, Q=quarter, Y= year)
      - <Prefix> = C (C=current)
      ```
    - Výraz se skládá z 0/1/2/3 podvýrazů. Každý podvýraz obsahuje volitelné znaménko (Sign) a termín (Term). Toto jsou typické příklady termínů:
      ```
      - 30D (30 dní (Day) = <Number><Unit>)
      - WD2 (2. den v týdnu (WeekDay2) = <Unit><Number>)
      - CW (aktuální týden (CurrentWeek) = <Prefix><Unit>)
      ```
    - Příklad použití:
      ```al
      var
          Expr1:  Text[30];
          Expr2:  Text[30];
          Expr3:  Text[30];
          RefDate: Date;
          Date1: Date;
          Date2: Date;
          Date3: Date;
          RefDateTxt: Label 'The reference date is: %1\\';
          Expr1Txt: Label 'The expression %2 returns %3\\';
          Expr2Txt: Label 'The expression %4 returns %5\\';
          Expr3Txt: Label 'The expression %6 returns %7\\';
      begin
          Expr1 := '<CQ+1M-10D>'  // Current Quarter + 1 Month - 10 Days
          Expr2 := '<-WD2>'       // The last WeekDay no.2 (last Thuesday)
          Expr3 := '<CM+30D>'     // Current Month + 30 Days
          RefDate := Today;
          Date1 := CalcDate(Expr1, RefDate);
          Date2 := CalcDate(Expr2, RefDate);
          Date3 := CalcDate(Expr3, RefDate);
          Message(RefDateTxt + Expr1Txt + Expr2Txt + Expr3Txt, RefDate, Expr1, Date1, Expr2, Date2, Expr3, Date3);
      end;
      /** Tento kod poté v BC vrátí message okno se zprávou popisující datum (např.
      The reference date is: 12/03/20
      The expression <CQ+1M-10D> returns 01/21/21
      The expression <-WD2> returns 12/01/20
      The expression <CM+30D> returns 01/30/21
      ).
      **/
      ```
  - [Date2DMY()](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-date2dmy-method)
    - **DT2DMY** získá den (Day), měsíc (Month), nebo rok (Year) z datumového typu (Date).
      - Hodnota 1 odpovídá dnu (1-31).
      - Hodnota 2 odpovídá měsíci (1-12).
      - Hodnota 3 odpovídá roku.
      ```al
      Number := System.Date2DMY(Date: Date, Value: Integer)
      ```
    - Příklad použití:
      ```al
      var
          InputDate: Date;
          Day: Integer;
          Month: Integer;
          Year: Integer;
          DateMsg: Label 'Today is a day %1 of month %2 of the year %3';
      begin
          InputDate := Today;
          Day := Date2DMY(InputDate, 1);
          Month := Date2DMY(InputDate, 2);
          Year := Date2DMY(InputDate,3);
          Message(DateMsg, Day, Month, Year);
      end;
      /** Tento kod poté v BC vrátí message okno se zprávou popisující datum (např.
      Today is a day 3 of month 12 of the year 2020
      ).
      **/
      ```
  - [Date2DWY()](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-date2dmy-method)
    - **DT2DWY** získá den v týdnu (DayOfWeek), číslo týdne (WeekNumber), nebo rok (Year) z datumového typu (Date).
      - Hodnota 1 odpovídá dnu v týdnu (1-7, Pondělí = 1).
      - Hodnota 2 odpovídá číslu týdne (1-53).
      - Hodnota 3 odpovídá roku.
      ```al
      Number := System.Date2DWY(Date: Date, Value: Integer)
      ```
    - Příklad použití:
      ```al
      var
          InputDate: Date;
          DayOfWeek: Integer;
          WeekNumber: Integer;
          Year: Integer;
          DateMsg: Label 'The date %1 corresponds to: \\The day of the week: %2 \\The week number: %3 \\ The year: %4';
      begin
          InputDate := Today;
          DayOfWeek := Date2DWY(InputDate, 1);
          WeekNumber := Date2DWY(InputDate, 2);
          Year := Date2DWY(InputDate,3);
          Message(DateMsg, DayOfWeek, WeekNumber, Year);
      end;
      /** Tento kod poté v BC vrátí message okno se zprávou popisující datum (např.
      The date 12/03/20 corresponds to:
      The day of the week: 4
      The week number: 49
      The year: 2020
      ).
      **/
      ```
      
  - [DMY2Date()](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-dmy2date-method)
    - **DMY2Date** získá datum dle dne (Day), měsíce (Month) a roku (Year).
      - Day: Číslo dne v měsíce (1-31).
      - Month: Číslo měsíce v roce (1-12).
      - Year: Čtyřmístné číslo pro rok.
      ```al
      Date := System.DMY2Date(Day: Integer [, Month: Integer] [, Year: Integer])
      ```
    - Příklad použití:
      ```al
      var
          Day: Integer;
          Month: Integer;
          Year: Integer;
          OutputDate: Date;
          DateMsg: Label 'Day number %1, month number %2, and year number %3 corresponds to the date %4. ';
      begin
          Day := 3;
          Month := 12;
          Year := 2020;
          OutputDate := DMY2Date(Day, Month, Year);
          Message(DateMsg, Day, Month, Year, OutputDate);
      end;
      /** Tento kod poté v BC vrátí message okno se zprávou popisující datum (např.
      Day number 3, month number 12, and year number 2020 corresponds to the date 12/03/20.
      ).
      **/
      ```

  - [DWY2Date()](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-dwy2date-method)
    - **DWY2Date** získá datum dle dnu v týdnu (WeekDay), týdnu (Week) a roce (Year).
      - WeekDay: Číslo dne v týdnu (1-7). Pondělí je číslo 1.
      - Week: Číslo týdne. 1. týden je první týden v roce, který má 4 a více dní.
      - Year: Čtyřmístné číslo pro rok.
      ```al
      Date := System.DWY2Date(WeekDay: Integer [, Week: Integer] [, Year: Integer])
      ```
    - Příklad použití:
      ```al
      var
          DayOfWeek: Integer;
          Week: Integer;
          Year: Integer;
          OutputDate: Date;
          DateMsg: Label 'Day %1 of week %2 in the year %3 corresponds to the date %4.';
      begin
          DayOfWeek := 4;
          Week := 49;
          Year := 2020;
          OutputDate := DWY2Date(DayOfWeek, Week, Year);
          Message(DateMsg, DayOfWeek, Week, Year, OutputDate);
      end;
      /** Tento kod poté v BC vrátí message okno se zprávou popisující datum (např.
      Day 4 of week 49 in the year 2020 corresponds to the date 12/03/20.
      ).
      **/
      ```  
      
  - [DT2Time()](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/developer/methods-auto/system/system-dt2time-method)
    - **DT2Time** 
      ```al
      Time := System.DT2Time(Datetime: DateTime)
      ```
    - Příklad použití:
      ```al
      var
          CurrDateTime: DateTime;
          OutputTime: Time;
          TimeMsg: Label 'CurrDateTime is %1, the time part of CurrDateTime is %2.';
      begin
          CurrDateTime := CurrentDateTime;
          OuputTime := DT2Time(CurrDateTime);
          Message(TimeMsg, CurrDateTime, OutputTime);
      end;
      /** Tento kod poté v BC vrátí message okno s přesným časem (např. 
      CurrDateTime is 12/03/20 01:50 PM, the time part of CurrDateTime is 1:50:47 PM.
      ).
      **/
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
      // Tento kod poté v BC vrátí message okno s datumem (např. 11/28/22).
      ```

## Příklady z praxe:
