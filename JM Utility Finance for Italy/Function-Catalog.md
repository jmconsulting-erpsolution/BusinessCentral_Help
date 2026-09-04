# JM Utility Finance for Italy - Function Catalog

Catalogo funzionale dettagliato dell'app `JM Utility Finance for Italy`, generato dal codice sorgente della cartella `JM Utility Finance for Italy`.

## Scope
- Cartella sorgente analizzata: `JM Utility Finance for Italy`
- Publisher: `JM Consulting`
- Versione: `27.0.0.4`
- Oggetti AL rilevati: **13 principali + 35+ extension**

## Funzionalità principali
- Logica applicativa centralizzata in 1 codeunit con 56 procedure pubbliche
- Esperienza utente estesa tramite 25+ page extension
- Modello dati composto da 2 table base + 13 table extension
- Automazioni/reportistica disponibile con 7 report + 2 report extension
- **JM Utility Finance Mgt** (Codeunit 60500): 56 procedure, 28 event subscriber, 0 business event

## Aree tecniche

### 1. Auto-Reverse Contabilità
**Procedure principali:**
- `GenJournalAutoReverse()` - Inversione batch da General Journal
- `GenLdgEntryAutoReverse()` - Inversione da G/L Entry già contabilizzati
- `InsertGenJournalLineReverseFromGenJournal()` - Creazione linee inverse da registro
- `InsertGenJournalLineFromGLEntry()` - Creazione linee inverse da movimenti G/L
- `JMModifyEntries()` - Aggiornamento propagato su Item/Value/Service Ledger Entry

**Event Subscriber:**
- `OnAfterInsertGlobalGLEntry` su Gen. Jnl.-Post Line - Tracciamento flag Reversed/Reversed Entry No.

**Oggetti interessati:** Gen. Journal Line, G/L Entry, GL Book Entry, GL Entry Buffer

### 2. Gestione Scadenze Differite Clienti
**Tabella principale:**
- `JM Deferring Due Dates` (Table 60501) - Groupe di periodi esclusione con formula calcolo scadenza

**Procedure:**
- `DeleteAndReinsertExclusionPeriods()` - Refresh periodi per singolo cliente
- `DeleteExclusionPeriods()` - Eliminazione periodi per cliente
- `InsertNewExclusionPeriods()` - Inserimento nuovi periodi da gruppo template
- `MassivelyDeleteAndReinsertExclusionPeriods()` - Batch su tutti clienti
- `MassivelyDeleteExclusionPeriods()` - Eliminazione massiva periodi
- `MassivelyInsertNewExclusionPeriods()` - Inserimento massivo da template
- `CheckCustomerDeferringFields()` - Validazione coerenza dati cliente
- `JM_DueDateRemainingAmountLCY()` - Calcolo importi scaduti per Cust. Ledger Entry

**Extension Table:**
- `Cust. Ledger Entry` - Calcolo saldo scaduto intelligente
- `Customer` - Campi `JM Deferring Due Dates Group`, `JM Include in Excl. Paym. Per.`
- `Payment Methods` - Flag `JM Exclusion Paym. Periods`

**Event Subscriber:**
- `OnAfterValidateEvent` Payment Method Code, Deferring Due Dates Group, Include Excl. Paym. Per.
- `OnAfterDeleteEvent` JM Tables (Type='DEFERRALDUEDATES')

### 3. Auto-Descrizione Distinta Fornitore
**Procedure:**
- `C_12173_OnBeforePostVendorBillLine()` - Composizione automatica descrizione righe
- `C_12173_OnBeforePostBalanceAccount()` - Stessa logica per conto di contropartita

**Pattern descrizione:** `[Bank Description] [Payment Method] [Vendor Invoice Desc] [External Doc No]`

**Extension Table:**
- `Bank Account` - Campo `JM Vendor Bill Description`
- `Vendor` - Utilizzo nella composizione
- `Gen. Journal Line` - Popolazione automatica Description

**Utilizzo:**
- PageExt: `Vendor List` (61422), `Vendor Card` (61423)

### 4. Autofatture (Self-Invoice)
**Procedure supporto:**
- `SetSelfInvoiceData()` - Assegnazione automatica numero da serie contabilizzazione
- `SelfInvoiceCheckExternalDocument()` - Validazione coerenza su Purch. Inv./Cr. Memo Header
- `SelfInvoiceUpdateExternalDocument()` - Propagazione numero esterno su ledger
- `JMSelfInvoicesetSalesInvoice()` - Allineamento retro-attivo su Posted Purchase Invoice
- `JMSelfInvoicesetSalesCrMemo()` - Allineamento retro-attivo su Posted Purchase Credit Memo

**Extension Table:**
- `Vendor` - Flag `JM Self Invoice Vendor`
- `Purch. Inv. Header` - Calcolato `JM Self Inv. Sales Doc. No.`
- `Purch. Cr. Memo Hdr.` - Calcolato `JM Self Inv. Sales Doc. No.`
- `Purchase Header` - Supporto
- `Gen. Journal Line` - Supporto

**Tabelle ledger aggiornate:**
- G/L Entry - `External Document No.`
- GL Book Entry - `External Document No.`
- Vendor Ledger Entry - `External Document No.`, `Payment Reference`
- Value Entry - `External Document No.`
- VAT Entry - `External Document No.`

**Event Subscriber:**
- OnBeforePostPurchaseDoc da Purch.-Post
- OnBeforeCreateElectronicDocument da JM Utility Base

### 5. Sincronizzazione Dimensioni
**Procedure:**
- `JMOnAfterInsert()` - Creazione automatica Dimension Value da anagrafe
- `JMModifyDim()` - Update Description, Blocco, Ridenominazione

**Event Subscriber (multipli per table):**
- **Customer (Table 18):**
  - OnAfterInsertEvent
  - OnAfterValidateEvent (Name, Name 2)
  - OnAfterDeleteEvent
  - OnAfterRenameEvent
  
- **Vendor (Table 23):**
  - OnAfterInsertEvent
  - OnAfterValidateEvent (Name, Name 2)
  - OnAfterDeleteEvent
  - OnAfterRenameEvent
  
- **Employee (Table 5200):**
  - OnAfterInsertEvent
  - OnAfterValidateEvent (First Name, Middle Name, Last Name)
  - OnAfterDeleteEvent
  - OnAfterRenameEvent

**Configuration:** Tramite JM Setup (TableExt 60501)
- Customer Dimension Code
- Vendor Dimension Code
- Employee Dimension Code

### 6. Calcolo Saldi Scaduti
**Procedure:**
- `CalcCustomerBalance()` - Somma Detailed Cust. Ledg. Entry filtrando su data scadenza

**Parametri:**
- Customer No.
- Global Dim 1 Filter
- Global Dim 2 Filter
- Currency Code Filter

**Configurazione:** `CustomerBalanceFormula` su JM Setup per limite data

### 7. Controlli Eliminazione Entità
**Procedure:**
- `CheckCustomerDeletetion()` - Validazione pre-cancellazione cliente
- `CheckVendorDeletetion()` - Validazione pre-cancellazione fornitore

**Tabelle verificate per Customer:**
- Item Ledger Entry, Value Entry, Service Ledger Entry, Warranty Ledger Entry
- G/L Entry, Cust. Ledger Entry, Detailed Cust. Ledg. Entry

**Tabelle verificate per Vendor:**
- Item Ledger Entry, Value Entry, G/L Entry
- Vendor Ledger Entry, Detailed Vendor Ledg. Entry

**Feature Flag:** 
- `JM Enable Cust. Del. Checks`
- `JM Enable Vend. Del. Checks`

**Event Subscriber:**
- OnBeforeDeleteEvent su Customer e Vendor

### 8. Funzionalità Ausiliarie

#### Abilitazione modifica Numero Contabilizzazione
- Procedure: `GetPostingNoEnabled()`
- Tabella: User Setup Extension (60504)
- Campo: `JM Enable Posting No.`

#### Aggiornamento Gruppi di Posting Prodotto
- Procedure: `JMUpdateGenProdPostingGroup()`
- Supporta: Sales Line, Purchase Line, Service Line
- Propaga su: Shipment/Receipt Lines, Value Entry, Item Ledger Entry
- Integrazione con JM Utility Manufacturing (custom field JM Gen. Prod. Posting Group)

#### Gestione Ritenute Fiscali
- Procedure: `ExcludeWithtaxonPurchDoc()`
- Tabella: Purch. Withh. Contribution
- Feature per documenti acquisto

#### Sincronizzazione Cumulative Bank Receipts
- Event Subscriber: OnBeforeCustLedgEntryModify
- Copia da FromCustLedgEntry

#### Modifica Cumulative Bank Receipts
- Event Subscriber: OnBeforeCustLedgEntryModify (ERPS-224)

---

## Permessi table (Codeunit 60500)

Il codeunit ha permessi espliciti su 43 tabelle:

**Read (r):**
- G/L Entry (rm), Vendor Ledger Entry (rm), Detailed Vendor Ledg. Entry (r)
- VAT Entry (rm), Purch. Inv. Line/Header, Purch. Cr. Memo
- JM Setup, General Ledger Setup, Gen. Journal Batch/Template
- Bank Account, Payment Method, User Setup
- Detailed Cust. Ledg. Entry, Cust. Ledger Entry, Customer Posting Group
- Vendor, Purchase Header, Warranty/Service/Item Ledger Entry
- Bank Account Posting Group, Purch. Withh. Contribution

**Read-Modify-Insert (rim):**
- Gen. Journal Line, Dimension Value, Default Dimension

**Read-Modify-Delete-Insert (rmdi):**
- Deferring Due Dates, JM Deferring Due Dates, Customer

---

## Codeunit rilevanti
- `JM Utility Finance Mgt` (Codeunit 60500): 56 procedure, 28 event subscriber
  - Procedure di esempio: InsertGenJournalLineFromGLEntry, InsertGenJournalLineReverseFromGenJournal
  - Subscriber evento: OnBeforePostVendorBillLine, OnAfterValidateEvent (multipli)

---

## Pagine coinvolte (UI da 3 native + 25+ extension)

### Pagine Native
- `Page60500-JM Deferring Due Dates Group.al`: Gestione singolo gruppo scadenze
- `Page60501-JM Deferring Due Dates Groups.al`: Listato gruppi
- `Page60502-JM Deferring Due Dates List.al`: Listato periodi esclusione

### Page Extension - Reporting/Admin
- PageExt 60501 - Fixed Asset: Label cespiti
- PageExt 60503 - G/L Entries: Info inversione
- PageExt 60504 - General Journal: Pulsante auto-reverse
- PageExt 60505 - JM Setup: Configurazione dimensioni
- PageExt 60506 - Gen. Journal Batches: Flag Reverse batch
- PageExt 60507 - Bank Account: Descrizione distinta pagamenti
- PageExt 60508 - Acc. Schedule Overview: Prospetti contabili
- PageExt 60509 - User Setup: Modifica numero contabilizzazione

### Page Extension - Vendite/Acquisti/Servizi
- PageExt 61410-61415 - Sales/Purchase/Service Invoice & Credit Memo Listati
- PageExt 61416-61421 - Sales/Purchase/Service Invoice & Credit Memo Card
- PageExt 61422/61423 - Vendor List/Card: Descrizione distinta pagamenti
- PageExt 61424-61427 - Posted Purchase Documents
- PageExt 61428 - Payment Methods: Flag esclusione periodi
- PageExt 61429 - Customer Card Listing
- PageExt 61740 - Customer List Listing
- PageExt 61741-61745 - Sales/Purchase/Service Document Subform

---

_Generato automaticamente il 2026-05-05._
