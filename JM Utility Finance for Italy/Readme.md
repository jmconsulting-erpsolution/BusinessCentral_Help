# JM Utility Finance for Italy

Estensione specializzata per la gestione finanziaria avanzata in Business Central, con focus su automazioni contabili, gestione delle scadenze differite e funzionalità specifiche per il contesto finanziario italiano.

## Informazioni app
- **Cartella sorgente:** `JM Utility Finance for Italy`
- **Publisher:** `JM Consulting`
- **Versione:** `27.0.0.4`
- **Target:** `Cloud`
- **Dipendenze:** JM Utility Base v27.0.0.0
- **BC Version:** 27.0.0.0 (Platform 27.0.0.0, Runtime 16.0)

---

## Descrizione funzionale

L'app consente di gestire:
1. **Storno semplificato dei movimenti contabili** - Automazione dell'inversione di registrazioni con creazione automatica delle contabilizzazioni inverse
2. **Gestione dell'etichetta Cespite** - Annotazione e tracciamento delle immobilizzazioni con label specifici
3. **Descrizione dettagliata dei pagamenti** - Registrazione strutturata dei pagamenti attraverso la distinta fornitore con identificazione della banca e metodo di pagamento

---

## Funzionalità tecniche principali

### 1. Inversione automatica movimenti del Giornale (Auto-Reverse)
- **Procedure:** `GenJournalAutoReverse()`, `InsertGenJournalLineReverseFromGenJournal()`
- **Funzionalità:**
  - Permette di selezionare righe del giornale generale e invertirle automaticamente
  - Crea controvalori speculari con importi negativi
  - Gestisce documenti e dimensioni in modo automatico
  - Supporta template e batch di giornale con flag "Reverse" abilitati
  - Validazione per righe con documento type Payment/Refund/Blank

### 2. Inversione automatica movimenti contabili (GL Entry Reverse)
- **Procedure:** `GenLdgEntryAutoReverse()`, `InsertGenJournalLineFromGLEntry()`
- **Funzionalità:**
  - Specchiamento di movimenti G/L già contabilizzati
  - Mappatura intelligente tra conto di contropartita (Vendor, Customer, Bank Account)
  - Tracciamento con flag "Reversed"/"Reversed by Entry No." sui G/L Entry
  - Validazioni: esclusione closing entries, Check se controvalori già registrati

### 3. Gestione Scadenze Differite (Deferring Due Dates)
- **Entity:** Table `JM Deferring Due Dates`
- **Funzionalità:**
  - Definizione di periodi di esclusione con formule di calcolo scadenza dinamiche
  - Associazione a Clienti tramite campo "JM Deferring Due Dates Group"
- **Procedure gestione:**
  - `DeleteAndReinsertExclusionPeriods()` - Aggiornamento intelligente periodi per cliente
  - `MassivelyDeleteAndReinsertExclusionPeriods()` - Batch processing per tutti i clienti
  - `JM_DueDateRemainingAmountLCY()` - Calcolo importi scaduti per Entry cliente

### 4. Auto-Descrizione Distinta Fornitore
- **Evento:** `OnBeforePostVendorBillLine` da Vendor Bill List
- **Funzionalità:**
  - Costruzione automatica descrizione su righe registrazione con pattern: "[Banca] [Metodo Pagamento] [Descrizione Setup] [Doc Esterno]"
  - Legame con campi "JM Vendor Bill Description" (Bank Account) e setup fornitore
  - Disponibile su PageExt: `PageExt61423-Vendor Card` e `PageExt61422-Vendor List`

### 5. Autofatture (Self-Invoice)
- **Funzionalità:**
  - Generazione automatica numero riferimento esterno per fornitori contrassegnati "JM Self Invoice Vendor"
  - `SetSelfInvoiceData()` - Assegnazione automatica numero da serie contabilizzazione
  - `SelfInvoiceCheckExternalDocument()` - Validazione coerenza codici su documenti collegati
  - `SelfInvoiceUpdateExternalDocument()` - Allineamento numero esterno su tutti i ledger (GL, Vendor, VAT, Value Entry, GL Book)
  - Procedure supporto: `JMSelfInvoicesetSalesInvoice()`, `JMSelfInvoicesetSalesCrMemo()`

### 6. Sincronizzazione Dimensioni (Customer/Vendor/Employee)
- **Event Subscriber:**
  - OnAfterInsertEvent / OnAfterValidateEvent (Name, Name 2, First/Middle/Last Name)
  - OnAfterDeleteEvent / OnAfterRenameEvent
- **Funzionalità:**
  - Creazione automatica Dimension Value da anagrafe Cliente/Fornitore/Dipendente
  - Associazione Default Dimension con valore posting "Same Code"
  - Ridenominazione/Blocco su modifiche anagrafe cliente/fornitore
  - Policy per tipo (Customer Dimension Code, Vendor Dimension Code, Employee Dimension Code) da JM Setup

### 7. Calcolo Importi Scaduti Clienti
- **Procedure:** `CalcCustomerBalance()`
- **Funzionalità:**
  - Calcolo Detailed Customer Ledger Entry filtrando su data scadenza
  - Supporto filtri: Global Dimension 1, Global Dimension 2, Currency Code
  - Utilizza formula data da JM Setup field "CustomerBalanceFormula"

### 8. Controlli Eliminazione (Customer/Vendor)
- **Event Subscriber:** `OnBeforeDeleteEvent`
- **Tabelle verificate:**
  - Customer: Item Ledger Entry, Value Entry, Service Ledger Entry, Warranty Ledger Entry, G/L Entry, Cust. Ledger Entry, Detailed Cust. Ledg. Entry
  - Vendor: Item Ledger Entry, Value Entry, G/L Entry, Vendor Ledger Entry, Detailed Vendor Ledg. Entry
- **Feature Flag:** JM Setup fields `JM Enable Cust. Del. Checks`, `JM Enable Vend. Del. Checks`

### 9. Abilitazione modifica Numero Contabilizzazione
- **Procedure:** `GetPostingNoEnabled()`
- **Funzionalità:** Flag "JM Enable Posting No." su User Setup per abilitare edit numero contabilizzazione

### 10. Aggiornamento Gruppi di Posting Prodotto
- **Procedure:** `JMUpdateGenProdPostingGroup()`
- **Scope:** Sales Line, Purchase Line, Service Line
- **Funzionalità:** Propagazione modifica Gen. Prod. Posting Group dalle righe su Shipment/Receipt collegati e Value Entry, Item Ledger Entry
- **Integrazione:** Se installato "JM Utility Manufacturing", aggiorna anche custom field JM Gen. Prod. Posting Group su Item Ledger Entry

### 11. Gestione Ritenute Fiscali su Documenti Acquisto
- **Procedure:** `ExcludeWithtaxonPurchDoc()`
- **Funzionalità:** 
  - Gestione esclusione ritenute da documenti di acquisto tramite tabella "Purch. Withh. Contribution"
  - Integrazione con UI per modifica elenco ritenute

### 12. Gestione Cumulative Bank Receipts
- **Event Subscriber:** OnBeforeCustLedgEntryModify
- **Funzionalità:** Sincronizzazione campo "Cumulative Bank Receipts" su Cust. Ledger Entry da edit via Cust. Entry-Edit

---

## Struttura oggetti AL

### Dati (2 Table)
- **Table 60501** - `JM Deferring Due Dates`: Master con Group Code, periodi date, formula di calcolo scadenza
- **Table Extension 60500** - `Cust. Ledger Entry`: Aggiunge campi per ritenuta bancaria

### Interfaccia Utente (3 Page + 20+ Page Extension)
**Pagine native:**
- Page 60500 - `JM Deferring Due Dates Group`: Gestione singolo gruppo scadenze
- Page 60501 - `JM Deferring Due Dates Groups`: Listato gruppi
- Page 60502 - `JM Deferring Due Dates List`: Listato periodi esclusione

**Page Extension principali:**
- PageExt 60500 - Customer Ledger Entries: Visibilità ritenuta bancaria
- PageExt 60501 - Fixed Asset List/Card: Label cespite
- PageExt 60503 - General Ledger Entries: Info inversione
- PageExt 60504 - General Journal: Auto-reverse button
- PageExt 60505 - JM Setup: Configurazione dimensioni e feature
- PageExt 61422/61423 - Vendor List/Card: Descrizione distinta pagamenti
- PageExt 61410-61421 - Sales/Purchase Invoice/Credit Memo: Etichette specifiche

### Logica di Business (1 Codeunit)
- **Codeunit 60500** - `JM Utility Finance Mgt`: 56 procedure, 28 event subscriber
  - Principale gestore automazioni finanziarie e contabili

### Reportistica (7 Report)
- Report 60500 - `JM Update Advance Invoice Data`: Aggiorna dati fatture anticipate cliente
- Report 60501 - `JM FA Label Print`: Stampa etichette cespiti
- Report 60502 - `JM Export Acc. Sched. to Excel`: Esportazione prospetto contabile
- Report 60503 - `JM Delete VAT Settlement`: Eliminazione liquidazioni IVA
- Report 60504 - `JM Delete VAT Register Print`: Eliminazione registri IVA
- Report 60505 - `JM Delete G/L Book Print`: Eliminazione libri contabili
- Report 60506 - `JM Update Deferring Due Dates`: Elaborazione batch scadenze differite
- Report 60507 - `JM Counterposed Balance Sheet`: Prospetto di bilancio comparativo

---

## Configurazione

La configurazione principale avviene tramite **JM Setup** (Page 60505 extension):

| Campo | Descrizione |
|-------|-------------|
| Enable Posted Refund | Abilita le automazioni di storno |
| JM Auto Reverse Origin Code | Codice origine per gli storni automatici |
| Enable Batch Refund | Consente storni batch da lotti |
| CustomerBalanceFormula | Formula data per calcolo saldo scaduto |
| Customer Dimension Code | Dimensione verso cui sincronizzare clienti |
| Vendor Dimension Code | Dimensione verso cui sincronizzare fornitori |
| Employee Dimension Code | Dimensione verso cui sincronizzare dipendenti |
| EnableCustVendorBillDesc | Abilita auto-descrizione distinta pagamenti |
| VendorInvoiceDesc | Testo standard descrizione fatture fornitore |
| JM Enable Cust. Del. Checks | Abilita controlli eliminazione cliente |
| JM Enable Vend. Del. Checks | Abilita controlli eliminazione fornitore |

---

## Cataloghi documentazione
- [Function-Catalog.md](./Function-Catalog.md) - Inventario dettagliato di procedure e subscriber
- [Object-Catalog.md](./Object-Catalog.md) - Catalogo tecnico oggetti AL

## Organizzazione documentazione online
- Nodo documentale consigliato: `.docs/JM Utility Finance for Italy`
- Pubblicare questa pagina come entry-point dell'app
- Collegare i cataloghi Function/Object come sottopagine tecniche

_Generato automaticamente il 2026-05-05._
