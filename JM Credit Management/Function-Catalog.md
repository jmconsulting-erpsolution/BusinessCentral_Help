# JM Credit Management - Function Catalog

Catalogo funzionale dell'app `JM Credit Management`, generato dal codice sorgente della cartella `JM Credit Management`.

## Scope
- Cartella sorgente analizzata: `JM Credit Management`
- Publisher: `JM Consulting`
- Versione: `27.0.0.16`
- Oggetti AL rilevati: **11**

## Funzionalità principali
- Logica applicativa centralizzata in 2 codeunit
- Esperienza utente estesa tramite 3 page e 0 page extension
- Modello dati composto da 2 table e 1 table extension
- JM Credit Mgmt. Excel Export: 8 procedure, 0 subscriber, 6 eventi

## Aree tecniche
- Dati: 2 table, 1 table extension
- UI: 3 page, 0 page extension
- Logica: 2 codeunit
- Reporting: 0 report

## Codeunit rilevanti
- `JM Credit Mgmt. Excel Export` (Codeunit62391-JM Credit Mgmt. Excel Export.al): 8 procedure, 0 subscriber, 6 eventi
  - Procedure di esempio: ExportFidoClienti, WriteCustomerRow, OnAfterInsertExcelHeader, OnAfterInsertVATRegExcelHeader, OnAfterInsertBalanceExcelHeader, OnAfterInsertExcelLine
- `JM Credit Management Install` (Codeunit62390-JM Credit Management Install.al): 0 procedure, 0 subscriber, 0 eventi
  - Procedure di esempio: n/d

## Pagine coinvolte
- `Page62390-JM Customer Credit Insurance List.al`: `JM Cust. Credit Insurance List`
- `Page62391-JM Customer Credit Insurance Card.al`: `JM Customer Credit Insurance`
- `Page62393-JM Cust. Credit Ins. Comments.al`: `JM Cust. Credit Ins. Comments`
