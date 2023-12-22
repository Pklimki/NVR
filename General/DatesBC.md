# Práce s datumy v Business Centralu
  

## Datumy pro **Sales/Shipping**
  * Datumy z **Sales Header**:
    - **Document Date** = Datum vytvoření objednávky. Toto datum se používá k výpočtu data splatnosti platby zákazníka a finančních poplatků.
    - **Order Date** = Datum vytvoření objednávky. Obvykle se ponechá prázdné, aby se vyplnilo pracovní datum Business Central.
    - **Posting Date** = Datum odeslání objednávky do záznamů hlavní knihy, zákazníka a položky knihy.
    - **Requested Delivery Date** = Datum, kdy si zákazník přeje doručit objednávku na zákazníkovu doručovací adresu uvedenou v objednávce. Bude použito ve výpočtech data prodejní linky.
To může být požadováno zákazníkem nebo vypočteno Business Centralem na základě nastavení a kalendářů.
    - **Promised Delivery Date** = Datum, kdy bylo dodání slíbeno.

* Datumy z **ShipmentDates** a **Times**:
    - **Planned Delivery Date** = Datum, kdy společnost plánovala dodání objednávky.
    - **Planned Shipment Date** = Datum, které zákazník požadoval, mínus čas odeslání. Toto datum vypočítá Business Central, ale lze jej změnit.
    - **Outbound Warehouse Handling Time** = Čas, který je potřeba k vyzvednutí, zabalení a označení položek v objednávce.
    - **Shipping Time** = Doba mezi odesláním zboží ze skladu a doručením na doručovací adresu zákazníka.
    - **Shipment Date** =Datum, kdy je zboží „vyzvednuto“ nebo opustí sklad.
