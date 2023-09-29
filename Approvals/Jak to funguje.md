```mermaid
graph LR
A(Vyplním pole číslo bankovního účtu) --Ne--> B[Funkce obsluhy události] -- Ne --> C[Zavolání Power Flow] -- Ne --> D((Approval Request))
G[Zpracování výsledku)

D -- Ne --> E(Approved) -- Ne --> G
D -- Ne --> F(Not Approved) -- Ne --> G
```
