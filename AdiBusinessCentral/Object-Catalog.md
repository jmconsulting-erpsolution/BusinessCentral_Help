# AdiBusinessCentral - Object Catalog

## App Metadata
- Source folder: AdiBC
- Publisher: JM Consulting
- Version: 27.0.0.22
- Brief: AdiBC_R008_R007
- Description: L'app AdiBC ha lo scopo di connetere Business Central con Adiuto permettendo di: - Definire le tipologie di documento da salvare automaticamente su Adiuto mediante la generazione dei report su Business Central  - Definire le famiglie documentali di Adiuto nelle quali archiviare i documenti generati in Business Central - Visualizzare i documenti salvati in Adiuto direttamente su Business Central - Impostare procedure di controllo sui bar-code dei documenti di entrata merce e sui bar-code delle fatture di acquisto
- Target: Cloud
- Runtime: 16.0
- Application: 27.0.0.0
- Platform: 27.0.0.0
- ID ranges: 76000-76500
- Total AL objects: 169

## Dependencies
- None declared

## Object Summary
| Type | Count |
|---|---:|
| Codeunit | 3 |
| Enum | 10 |
| Page | 7 |
| PageExt | 119 |
| PermissionSet | 1 |
| Table | 4 |
| TableExt | 25 |

## Codeunit API Overview
| File | ID | Procedures | TryFunction | Events |
|---|---:|---:|---:|---:|
| Codeunit76000-JM Adiuto Web Service.al | 76000 | 108 | 3 | 2 |
| Codeunit76001-JM Adiuto Event Handler.al | 76001 | 35 | 0 | 0 |
| Codeunit76002-JM Adiuto Documents.al | 76002 | 58 | 1 | 9 |

### Codeunit76000-JM Adiuto Web Service.al
- Object name: JM Adiuto Web Service
- Procedure count: 108
- TryFunction attributes: 3
- Event attributes: 2
- Sample procedures: GetProtocol, GetSdkProtocol, GetBaseUrl, GetBaseSdkUrl, GetError, GetErrorInfo, GetErrorInfo, GetErrorInfo, GetErrorInfo, GetIdSessionAdijedWS, GetIdSessionSDKService, DoCallRESTWebService, ...

### Codeunit76001-JM Adiuto Event Handler.al
- Object name: JM Adiuto Event Handler
- Procedure count: 35
- TryFunction attributes: 0
- Event attributes: 0
- Sample procedures: Adiuto_GetLargeContent, Adiuto_ExecuteQuery, FormatResponse, FormatResponse, Adiuto_GetLargeContent_WithKey, Codeunit_SalesPost_OnAfterCheckMandatoryFields, Codeunit_ReleaseSalesDocument_OnAfterManualReleaseSalesDoc, Codeunit_ReleasePurchaseDocument_OnAfterManualReleasePurchaseDoc, Codeunit_ReleaseServiceDocument_OnAfterPerformManualRelease, Codeunit_ReleaseTransferDocument_OnAfterReleaseTransferDoc, Codeunit_PurchPost_OnAfterCheckMandatoryFields, Codeunit_WhsePostReceipt_OnInitSourceDocumentHeaderOnBeforePurchHeaderModify, ...

### Codeunit76002-JM Adiuto Documents.al
- Object name: JM Adiuto Documents
- Procedure count: 58
- TryFunction attributes: 1
- Event attributes: 9
- Sample procedures: ConfirmMessage, ViewDocuments, ViewDocumentsFromVariantRec, ViewDocumentsFromVariantRec, RunSDK, InsertDocumentFromVariantRec_OnAfterPrintDocument, InsertDocumentFromVariantRec, InsertDocumentStandardPrint, InsertDocumentFromSetupDetail, InsertDocumentLoop, InsertDocumentFromVariantRec, GetRecordTypeFromVariantRec, ...

## Full Object Inventory
### Codeunit
- [76000] Codeunit76000-JM Adiuto Web Service.al - JM Adiuto Web Service
- [76001] Codeunit76001-JM Adiuto Event Handler.al - JM Adiuto Event Handler
- [76002] Codeunit76002-JM Adiuto Documents.al - JM Adiuto Documents

### Enum
- [76000] Enum76000-JM Adiuto Version.al - JM Adiuto Version
- [76001] Enum76001-JM Adiuto Data Function.al - JM Adiuto Data Function
- [76002] Enum76002-JM Adiuto Field Type.al - JM Adiuto Field Type
- [76003] Enum76003-JM Adiuto Upload Doc. Type.al - JM Adiuto Upload Doc. Type
- [76004] Enum76004-JM Adiuto Upld. Doc. Duplicate.al - JM Adiuto Upld. Doc. Duplicate
- [76005] Enum76005-JM Adiuto Setup View Type.al - JM Adiuto Setup View Type
- [76006] Enum76006-JM Adiuto Dialog Type.al - JM Adiuto Dialog Type
- [76007] Enum76007-JM Adiuto Search Type.al - JM Adiuto Search Type
- [76008] Enum76008-JM Adiuto Json Field.al - JM Adiuto Json Field
- [76009] Enum76009-JM Adiuto Link. Tbl. Funct..al - JM Adiuto Link. Tbl. Funct.

### Page
- [76000] Page76000-JM Adiuto Setup.al - JM Adiuto Setup
- [76001] Page76001-JM Adiuto Setup Detail.al - JM Adiuto Setup Detail
- [76002] Page76002-JM Adiuto Family List.al - JM Adiuto Family List
- [76003] Page76003-JM Adiuto Setup Detail Lines.al - JM Adiuto Setup Detail Lines
- [76004] Page76004-JM Adiuto Linked Table Field.al - JM Adiuto Linked Table Field
- [76005] Page76005-JM Adiuto Dialog.al - JM Adiuto Dialog
- [76006] Page76006-JM Adiuto Setup Detail Card.al - JM Adiuto Setup Detail Card

### PageExt
- [76000] PageExt76000-Purchase Invoice.al - PageExt76000 extends
- [76001] PageExt76001-Posted Purchase Invoice.al - PageExt76001 extends
- [76002] PageExt76002-Purchase Credit Memo.al - PageExt76002 extends
- [76003] PageExt76003-Posted Purchase Credit Memo.al - PageExt76003 extends
- [76004] PageExt76004-Sales Order List.al - PageExt76004 extends
- [76005] PageExt76005-Posted Sales Invoice.al - PageExt76005 extends
- [76006] PageExt76006-Posted Sales Credit Memo.al - PageExt76006 extends
- [76007] PageExt76007-Posted Sales Invoices.al - PageExt76007 extends
- [76008] PageExt76008-Posted Sales Credit Memos.al - PageExt76008 extends
- [76009] PageExt76009-Item Card.al - PageExt76009 extends
- [76010] PageExt76010-Item List.al - PageExt76010 extends
- [76011] PageExt76011-Req. Worksheet.al - PageExt76011 extends
- [76012] PageExt76012-Planning Worksheet.al - PageExt76012 extends
- [76013] PageExt76013-Purchase Order Subform.al - PageExt76013 extends
- [76014] PageExt76014-Purchase Quote Subform.al - PageExt76014 extends
- [76015] PageExt76015-Sales Quotes.al - PageExt76015 extends
- [76016] PageExt76016-Sales Orders.al - PageExt76016 extends
- [76017] PageExt76017-Sales Quote.al - PageExt76017 extends
- [76018] PageExt76018-Sales Order.al - PageExt76018 extends
- [76019] PageExt76019-Posted Sales Shipment.al - PageExt76019 extends
- [76020] PageExt76020-Posted Sales Shipments.al - PageExt76020 extends
- [76021] PageExt76021-Purchase Invoices.al - PageExt76021 extends
- [76022] PageExt76022-Sales Invoice List.al - PageExt76022 extends
- [76023] PageExt76023-Sales Credit Memos.al - PageExt76023 extends
- [76024] PageExt76024-Purchase Credit Memos.al - PageExt76024 extends
- [76025] PageExt76025-Posted Purchase Invoices.al - PageExt76025 extends
- [76026] PageExt76026-Posted Purchase Cr.Memos.al - PageExt76026 extends
- [76027] PageExt76027-Warehouse Receipt.al - PageExt76027 extends
- [76028] PageExt76028-Purchase Order.al - PageExt76028 extends
- [76029] PageExt76029-Posted Purchase Receipt.al - PageExt76029 extends
- [76030] PageExt76030-Posted Purchase Receipts.al - PageExt76030 extends
- [76031] PageExt76031-Posted Return Receipt.al - PageExt76031 extends
- [76032] PageExt76032-Posted Return Receipts.al - PageExt76032 extends
- [76033] PageExt76033-Posted Transfer Receipt.al - PageExt76033 extends
- [76034] PageExt76034-Posted Transfer Receipts.al - PageExt76034 extends
- [76035] PageExt76035-Warehouse Receipts.al - PageExt76035 extends
- [76036] PageExt76036-Purchase Order List.al - PageExt76036 extends
- [76037] PageExt76037-Purchase Quote List.al - PageExt76037 extends
- [76038] PageExt76038-Posted Service Invoice.al - PageExt76038 extends
- [76039] PageExt76039-Posted Service Credit Memo.al - PageExt76039 extends
- [76040] PageExt76040-Posted Service Invoices.al - PageExt76040 extends
- [76041] PageExt76041-Posted Service Credit Memos.al - PageExt76041 extends
- [76042] PageExt76042-Transfer Order.al - PageExt76042 extends
- [76043] PageExt76043-Transfer Orders.al - PageExt76043 extends
- [76044] PageExt76044-Posted Transfer Shipment.al - PageExt76044 extends
- [76045] PageExt76045-Posted Transfer Shipments.al - PageExt76045 extends
- [76046] PageExt76046-Report Selection - Sales.al - PageExt76046 extends
- [76047] PageExt76047-Report Selection - Purchase.al - PageExt76047 extends
- [76048] PageExt76048-Sales Quote Subform.al - PageExt76048 extends
- [76049] PageExt76049-Sales Order Subform.al - PageExt76049 extends
- [76050] PageExt76050-User Setup.al - PageExt76050 extends
- [76051] PageExt76051-Machine Center Card.al - PageExt76051 extends
- [76052] PageExt76052-Machine Center List.al - PageExt76052 extends
- [76053] PageExt76053-Work Center Card.al - PageExt76053 extends
- [76054] PageExt76054-Work Center List.al - PageExt76054 extends
- [76055] PageExt76055-Resource Card.al - PageExt76055 extends
- [76056] PageExt76056-Resource List.al - PageExt76056 extends
- [76057] PageExt76057-Employee Card.al - PageExt76057 extends
- [76058] PageExt76058-Employee List.al - PageExt76058 extends
- [76059] PageExt76059-Job Card.al - PageExt76059 extends
- [76060] PageExt76060-Job List.al - PageExt76060 extends
- [76061] PageExt76061-Production BOM.al - PageExt76061 extends
- [76062] PageExt76062-Production BOM List.al - PageExt76062 extends
- [76063] PageExt76063-Production BOM Lines.al - PageExt76063 extends
- [76064] PageExt76064-Planned Production Order.al - PageExt76064 extends
- [76065] PageExt76065-Planned Production Orders.al - PageExt76065 extends
- [76066] PageExt76066-Planned Prod. Order Lines.al - PageExt76066 extends
- [76067] PageExt76067-Prod. Order Components.al - PageExt76067 extends
- [76068] PageExt76068-Simulated Production Order.al - PageExt76068 extends
- [76069] PageExt76069-Simulated Production Orders.al - PageExt76069 extends
- [76070] PageExt76070-Simulated Prod. Order Lines.al - PageExt76070 extends
- [76071] PageExt76071-Firm Planned Prod. Order.al - PageExt76071 extends
- [76072] PageExt76072-Firm Planned Prod. Orders.al - PageExt76072 extends
- [76073] PageExt76073-Firm Planned Prod. Order Lines.al - PageExt76073 extends
- [76074] PageExt76074-Released Production Order.al - PageExt76074 extends
- [76075] PageExt76075-Released Production Orders.al - PageExt76075 extends
- [76076] PageExt76076-Released Prod. Order Lines.al - PageExt76076 extends
- [76077] PageExt76077-Finished Production Order.al - PageExt76077 extends
- [76078] PageExt76078-FinishedProduction Orders.al - PageExt76078 extends
- [76079] PageExt76079-Finished Prod. Order Lines.al - PageExt76079 extends
- [76080] PageExt76080-Service Quotes.al - PageExt76080 extends
- [76081] PageExt76081-Service Orders.al - PageExt76081 extends
- [76082] PageExt76082-Service Quote.al - PageExt76082 extends
- [76083] PageExt76083-Service Order.al - PageExt76083 extends
- [76084] PageExt76084-Service Contracts.al - PageExt76084 extends
- [76085] PageExt76085-Service Contract.al - PageExt76085 extends
- [76086] PageExt76086-Posted Service Shipment.al - PageExt76086 extends
- [76087] PageExt76087-Posted Service Shipments.al - PageExt76087 extends
- [76088] PageExt76088-Service Invoice List.al - PageExt76088 extends
- [76089] PageExt76089-Service Invoice.al - PageExt76089 extends
- [76090] PageExt76090-Service Credit Memos.al - PageExt76090 extends
- [76091] PageExt76091-Service Credit Memo.al - PageExt76091 extends
- [76092] PageExt76092-Service Item List.al - PageExt76092 extends
- [76093] PageExt76093-Service Item Card.al - PageExt76093 extends
- [76094] PageExt76094-Service Quote Subform.al - PageExt76094 extends
- [76095] PageExt76095-Service Order Subform.al - PageExt76095 extends
- [76096] PageExt76096-Lot No. Information Card.al - PageExt76096 extends
- [76097] PageExt76097-Lot No. Information List.al - PageExt76097 extends
- [76098] PageExt76098-Sales Return Order.al - PageExt76098 extends
- [76099] PageExt76099-Sales Invoice.al - PageExt76099 extends
- [76100] PageExt76100-Sales Credit Memo.al - PageExt76100 extends
- [76101] PageExt76101-Report Selection - Service.al - PageExt76101 extends
- [76102] PageExt76102-Sales Quote Archive.al - PageExt76102 extends
- [76103] PageExt76103-Sales Quote Archive Subform.al - PageExt76103 extends
- [76104] PageExt76104-Sales Quote Archives.al - PageExt76104 extends
- [76105] PageExt76105-Sales Order Archive.al - PageExt76105 extends
- [76106] PageExt76106-Sales Order Archive Subform.al - PageExt76106 extends
- [76107] PageExt76107-Sales Order Archives.al - PageExt76107 extends
- [76108] PageExt76108-Cust. Ledger Entry.al - PageExt76108 extends
- [76109] PageExt76109-Vendor Ledger Entry.al - PageExt76109 extends
- [76110] PageExt76110-Item Ledger Entry.al - PageExt76110 extends
- [76111] PageExt76111-General Ledger Entries.al - PageExt76111 extends
- [76112] PageExt76112-FA Ledger Entries.al - PageExt76112 extends
- [76113] PageExt76113-Customer Card.al - PageExt76113 extends
- [76114] PageExt76114-Customer List.al - PageExt76114 extends
- [76115] PageExt76115-Vendor Card.al - PageExt76115 extends
- [76116] PageExt76116-Vendor List.al - PageExt76116 extends
- [76117] PageExt76117-Purchase Return Order.al - PageExt76117 extends
- [76118] PageExt76118-Posted Return Shipment.al - PageExt76118 extends

### PermissionSet
- [76000] PermissionSet76000-JM Permission Set.al - PermissionSet76000

### Table
- [76000] Table76000-JM Adiuto Setup.al - JM Adiuto Setup
- [76001] Table76001-JM Adiuto Setup Detail.al - JM Adiuto Setup Detail
- [76002] Table76002-JM Adiuto Setup Detail Lines.al - JM Adiuto Setup Detail Lines
- [76003] Table76003-JM Adiuto Linked Table Field.al - JM Adiuto Linked Table Field

### TableExt
- [76000] TableExt76000-Sales Header.al - TableExt76000 extends
- [76001] TableExt76001-Sales Shipment Header.al - TableExt76001 extends
- [76002] TableExt76002-Sales Invoice Header.al - TableExt76002 extends
- [76003] TableExt76003-Sales Cr.Memo Header.al - TableExt76003 extends
- [76004] TableExt76004-Sales Header Archive.al - TableExt76004 extends
- [76005] TableExt76005-Return Receipt Header.al - TableExt76005 extends
- [76006] TableExt76006-Purchase Header.al - TableExt76006 extends
- [76007] TableExt76007-Purch. Rcpt. Header.al - TableExt76007 extends
- [76008] TableExt76008-Purch. Inv. Header.al - TableExt76008 extends
- [76009] TableExt76009-Purch. Cr. Memo Hdr..al - TableExt76009 extends
- [76010] TableExt76010-Purchase Header Archive.al - TableExt76010 extends
- [76011] TableExt76011-Return Shipment Header.al - TableExt76011 extends
- [76012] TableExt76012-Warehouse Receipt Header.al - TableExt76012 extends
- [76013] TableExt76013-Transfer Header.al - TableExt76013 extends
- [76014] TableExt76014-Transfer Receipt Header.al - TableExt76014 extends
- [76015] TableExt76015-Transfer Shipment Header.al - TableExt76015 extends
- [76016] TableExt76016-Posted Warehouse Receipt Header.al - TableExt76016 extends
- [76017] TableExt76017-Warehouse Header.al - TableExt76017 extends
- [76018] TableExt76018-Report Selection.al - TableExt76018 extends
- [76019] TableExt76019-User Setup.al - TableExt76019 extends
- [76020] TableExt76020-Service Header.al - TableExt76020 extends
- [76021] TableExt76021-Service Shipment Header.al - TableExt76021 extends
- [76022] TableExt76022-Service Invoice Header.al - TableExt76022 extends
- [76023] TableExt76023-Service Cr.Memo Header.al - TableExt76023 extends
- [76024] TableExt76024-Posted Whse. Shipment Header.al - TableExt76024 extends

