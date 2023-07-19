# Mám dát do parametrů procedury parametr s var nebo bez var?


# Parametr s var
> Jako parametr předávám odkaz na proměnnou/záznam v tabulce. Předávám tedy nějakou adresu, kde se hodnota nachází. Procedura hodnotu může nějak upravit a "ji vrátí". To znamená, že pokud já z místa A zavolám proceduru, která se nachází v nějaké CU, a jako parametr ji předám odkaz na Quantity (Quantity = 10), tak pokud ji procedura na místě B (CodeUnita) svou vnitřní logikou upraví na 15, tak já při dalším vykonávání kódu pracuji s hodnotou Quantity = 15.