# JM Pick And Stock - Functional Documentation

**Application Name:** JM Pick And Stock  
**Publisher:** JM Consulting  
**Version:** 27.0.1.1  
**App ID:** 33a49749-ebb8-4b74-8585-4921b6a6c846  
**Target Platform:** Business Central 27.0.0.0  
**Target Cloud:** Yes

---

## 1. Executive Summary

**JM Pick And Stock** is a comprehensive warehouse management application designed to extend Business Central's picking and stocking functionality. The application provides a complete solution for managing logistic operations including:

- **Pick Management:** Streamlined picking process for sales orders, transfers, returns, and production orders
- **Stock Management:** Efficient stocking and inventory management for inbound and outbound operations
- **Barcode Integration:** Advanced barcode scanning and tracking capabilities for warehouse operations
- **Parcel Management:** Parcel tracking and shipment management
- **Logistic Lines Processing:** Item tracking with lot, serial, and package numbers through warehouse operations
- **Multi-Document Support:** Support for sales orders, purchase orders, transfers, service orders, production orders, assembly orders, and job planning

The application integrates seamlessly with Business Central's standard warehouse module while providing advanced logistic tracking, activity management, and flexible workflow configurations for warehouse personnel.

---

## 2. Core Functionality

### 2.1 Pick Management System

**Primary Purpose:** Enable efficient execution of picking activities across multiple document types with real-time tracking and quality control.

**Key Features:**
- **Pick Line Processing:** Create, manage, and execute pick lines from various source documents
- **Lot and Serial Number Tracking:** Track items by lot number, serial number, and package number during picks
- **Quantity Management:** Real-time quantity tracking and validation during picking operations
- **Status Workflow:** Multiple status levels (Open, Checked, Processed) for pick quality control
- **Bin Management:** Support for warehouse bin assignments and relocation during picking
- **Barcode Scanning:** Quick entry of item/lot/serial data via barcode scanning interface
- **Pick Confirmation:** Confirm and validate completed picks before posting

**Supported Document Types:**
- Sales Orders and Order Subforms
- Sales Order Archive Subforms
- Transfer Orders and Subforms
- Purchase Return Orders
- Service Orders and Lines
- Production Order Components
- Assembly Orders
- Warehouse Shipments and Posted Shipments
- Job Planning Lines and Archives
- Purchase and Sales Order main headers

### 2.2 Stock Management System

**Primary Purpose:** Manage inbound inventory receipt, storage, and inventory reclassification activities.

**Key Features:**
- **Stock Line Processing:** Create and manage stock activities for warehouse receipt and put-away operations
- **Warehouse Bin Assignment:** Assign stock items to appropriate warehouse bins
- **Reclassification Support:** Support for inventory reclassification between bins, locations, or classifications
- **Quantity Tracking:** Track received, stocked, and reclassified quantities
- **Status Workflow:** Workflow stages (Open, Checked, Processed) for stock activity verification
- **Barcode Support:** Barcode scanning for rapid stock entry and verification
- **Stock Confirmation:** Confirm stock activities before final posting

**Supported Document Types:**
- Purchase Orders and Order Subforms
- Purchase Return Order Subforms
- Transfer Orders and Subforms
- Warehouse Receipts and Posted Receipts
- Production Order Lines and Subforms
- Assembly Orders
- Item Reclassification Journals
- Service Orders

### 2.3 Logistic Lines Management

**Core Processing Engine:** The "JM Logistic Lines" table serves as the central processing engine for all pick and stock activities.

**Activity Types:**
- **Pick Activity:** Used for outbound operations (sales, transfers, returns, service, production, assembly)
- **Stock Activity:** Used for inbound operations (receipts, reclassification, internal transfers)

**Logistic Line Attributes:**
- Item tracking (Item No., Variant Code)
- Quantity management (Quantity per unit, Quantity, Processed Quantity)
- Warehouse details (Location Code, Bin Code, To Bin Code)
- Lot/Serial/Package tracking (Lot No., Serial No., Package No.)
- Source document reference (Warehouse Document Type, Warehouse Document No., Line No.)
- Activity status (Status: Open, Checked, Processed)
- User assignment and timestamps

**Key Pages:**
- **JM Logistic Lines (Main View):** Administration view for all logistic line activity
- **JM Logistic Lines Pick:** Filtered view for pick activities only
- **JM Logistic Lines Stock:** Filtered view for stock activities only

### 2.4 Parcel Management

**Purpose:** Track shipments and parcels through the warehouse and outbound logistics process.

**Key Features:**
- **Parcel Creation:** Automatic or manual parcel creation from sales orders and shipments
- **Parcel Weight/Dimension Tracking:** Capture and validate package physical characteristics
- **Shipment Tracking:** Track parcel status from pick through delivery
- **Multi-parcel Support:** Support for split shipments across multiple parcels
- **Weight Recalculation:** Recalculate parcel weights based on actual picked quantities
- **Parcel Numbering:** Automatic parcel number assignment via configurable numbering series

**Configuration:**
- **JM Parcel Nos.:** Numbering series for automatic parcel number assignment
- **Allow Transfer Shipment Posting:** Enable/disable posting of transfer shipments
- **Allow Transfer Receipt Posting:** Enable/disable posting of transfer receipts
- **Allow Sales Shipment Posting:** Enable/disable posting of sales shipments
- **Allow Purchase Receipt Posting:** Enable/disable posting of purchase receipts

### 2.5 Inbound Operations Management

**Purpose:** Manage receipt and initial processing of incoming goods.

**Pages:**
- **JM Inbound Lines:** List and management of inbound logistics activities

**Key Actions:**
- **Plan:** Create logistic lines from inbound source documents
- **Update:** Update inbound line descriptions and metadata
- **Complete Line:** Mark inbound activities as complete
- **Logistic Data:** Link to logistic line processing interface
- **Open Source Document:** Navigate to source purchase receipt or transfer receipt
- **Reopen Line:** Revert completed inbound lines for correction
- **Barcode Scan:** Quick entry of item data via barcode scanning

### 2.6 Outbound Operations Management

**Purpose:** Manage picking and shipment preparation for outgoing orders.

**Pages:**
- **JM Outbound Lines:** List and management of outbound logistics activities

**Key Actions:**
- **Calculate Inventory:** Verify available inventory for outbound orders
- **Plan:** Create logistic lines from outbound source documents
- **Update:** Update outbound line descriptions and metadata
- **Complete Line:** Mark outbound activities as complete
- **Logistic Data:** Link to logistic line processing interface
- **Open Source Document:** Navigate to source sales order or service order
- **Reopen Line:** Revert completed outbound lines for correction
- **Barcode Scan (V1 & V2):** Multiple barcode scanning interface options

### 2.7 Barcode Integration

**Purpose:** Accelerate data entry and improve accuracy through barcode scanning.

**Barcode Scanning Features:**
- **Item Barcode Scanning:** Scan item numbers for quick entry
- **Lot Number Scanning:** Scan lot numbers for traceability
- **Serial Number Scanning:** Scan serial numbers for high-value items
- **Package/Parcel Scanning:** Scan package codes for shipment tracking
- **Reclassification Support:** Support for barcode-guided inventory reclassification
- **Multiple Scanning Interfaces:** V1 and V2 scanning implementations for different workflows

**Barcode Scan Reclassification Type:** Configurable reclassification behavior during barcode scanning (scans, jumps, or other business logic)

---

## 3. Core Objects and Architecture

### 3.1 Core Codeunit

**JM Pick And Stock Mgt (ID: 61940)**

Central business logic engine managing all pick and stock operations:
- Pick/Stock line creation and confirmation
- Quantity management and validation
- Warehouse bin operations
- Reclassification processing
- Item tracking operations
- Event handling for source document changes

**Key Procedures:**
- `ConfirmPick()` - Confirm pick activity
- `CheckPick()` - Validate pick data
- `ReclassCheckPick()` - Process reclassification checking
- `ProcessPick()` - Final pick posting
- And many more supporting procedures for stock operations

### 3.2 Core Tables

The application extends Business Central's standard tables with JM-specific fields:

**Table Extensions:**
- **User Setup (61940-61943):** Pick & Stock user permissions
  - Enable Pick Management
  - Enable Checked Pick
  - Enable Processed Pick
  - Enable Stock Management
  - Enable Checked Stock
  - Enable Processed Stock
  - Delete Lines Process Closed
  - Template Reclassification Item
  - Batch Reclassification Item
  - Auto-Post Reclassification
  - Pick & Stock SuperUser

- **JM Setup (61940-61947):** System-level Pick & Stock configuration
  - Parcel Numbering Series
  - Transfer Shipment Posting Control
  - Transfer Receipt Posting Control
  - Sales Shipment Posting Control
  - Purchase Receipt Posting Control
  - Barcode Scan Reclassification Type

### 3.3 Core Enumerations

**JM Activity Type (Enum 61940)**
- **Pick:** Outbound picking activities
- **Stock:** Inbound stocking activities

---

## 4. Core Pages

### 4.1 Main Pages (User-Facing)

| Page | ID | Type | Purpose |
|------|----|----|---------|
| JM Inbound Lines | 61940 | List | Receive and manage inbound inventory activities |
| JM Logistic Lines | 61941 | List | Central view of all pick and stock activities |
| JM Outbound Lines | 61942 | List | Manage outbound picking and shipment activities |
| JM Parcels | 61943 | List | Track parcels and shipments |
| JM Logistic Lines Pick | 61944 | List (Filtered) | Pick activity execution interface |
| JM Logistic Lines Stock | 61945 | List (Filtered) | Stock activity execution interface |

### 4.2 Page Extensions

The application extends 27 pages across Business Central modules with logistic line access and actions:

**User Setup & Configuration:**
- User Setup page extension (61940)
- JM Setup page extension (61941)

**Sales Documents:**
- Sales Order Subform (61942)
- Sales Order Archive Subform (61943)
- Sales Order main page (62027)
- Sales Return Order Subform (61955)
- Sales Return Order main page (62029)

**Purchase Documents:**
- Purchase Order Subform (61954)
- Purchase Order main page (62028)
- Purchase Return Order Subform (61945)
- Purchase Return Order main page (62320)

**Warehouse Documents:**
- Warehouse Receipt (62324)
- Warehouse Receipt Subform (61958)
- Posted Warehouse Receipt Subform (61959)
- Warehouse Shipment (62325)
- Warehouse Shipment Subform (61950)
- Posted Warehouse Shipment Subform (61951)

**Production Documents:**
- Production Order Components (61948)
- Production Order Line List (61956)
- Released Production Order Lines (61957)
- Finished Production Order Lines (62020)

**Service & Other:**
- Service Orders (62322)
- Service Lines (61946)
- Service Order Archive Lines (61947)
- Transfer Order (62321)
- Transfer Order Subform (61944)
- Assembly Order Subform (61949)
- Job Planning Lines (61952)
- Job Planning Archive Lines (61953)
- Item Reclassification Journal (62323)

**Role Centers:**
- Business Manager Role Center (62023)
- Order Processor Role Center (62024)
- Warehouse Manager Role Center (62025)
- Warehouse Basic Role Center (62026)

---

## 5. Page Extension Actions

The application adds "Logistic Line" actions to document pages, providing direct access to:
- **JMLogisticLinePick:** Opens pick logistic lines for the current document line
- **JMLogisticLineStock:** Opens stock logistic lines for the current document line
- **JMLogisticLine:** Opens logistic line activity (warehouse operations)

These actions appear in document subforms with captions like:
- "Logistic Line (Pick JM)"
- "Logistic Line (Stock JM)"
- "Logistic Line (JM)"

---

## 6. Workflow and Processing

### 6.1 Typical Pick Workflow

```
1. Source Document Creation
   - Sales Order, Service Order, or Transfer Order is created and released

2. Logistic Line Generation
   - User navigates to document subform
   - Clicks "Logistic Line (Pick JM)" action
   - Logistic lines are created from source document lines

3. Pick Activity Execution
   - Navigate to JM Logistic Lines (Pick) page
   - Scan or enter Item No., Lot No., Serial No., Package No.
   - Enter quantity to pick
   - Validate bin locations and quantities

4. Pick Checking
   - User selects "Check Pick" action
   - System validates all required fields and quantities
   - Corrects any discrepancies

5. Pick Confirmation
   - User selects "Confirm Pick" action
   - Quantities are reserved against inventory
   - Status changes from Open to Checked

6. Pick Processing
   - User selects "Process Pick" action
   - Logistic lines are marked as Processed
   - Pick activities are linked to warehouse documents

7. Shipment Posting
   - Warehouse shipment or sales shipment is posted
   - Inventory is reduced and orders are fulfilled
```

### 6.2 Typical Stock Workflow

```
1. Inbound Document Receipt
   - Purchase Receipt, Transfer Receipt, or Warehouse Receipt is created

2. Logistic Line Generation
   - User navigates to receipt document
   - Creates logistic lines from receipt lines
   - Logistic lines indicate stock activity type

3. Stock Activity Execution
   - Navigate to JM Logistic Lines (Stock) page
   - Scan or enter Item No., Destination Bin, Lot No.
   - Enter quantity to stock
   - Validate bin locations and available space

4. Stock Checking
   - User selects "Check Stock" action
   - System validates bin assignments and quantities
   - Corrects any issues

5. Stock Confirmation
   - User selects "Confirm Stock" action
   - Stock activities are confirmed
   - Status changes from Open to Checked

6. Stock Processing
   - User selects "Process Stock" action
   - Items are moved to assigned bins
   - Inventory locations are updated
   - Status changes to Processed

7. Receipt Posting
   - Warehouse receipt is posted
   - Inventory is added to bins
   - Inbound operation is complete
```

### 6.3 Reclassification Workflow

**Purpose:** Move items between bins, locations, or reclassify within existing inventory.

**Workflow Steps:**
1. Open Item Reclassification Journal
2. Use barcode scan action to quickly enter items
3. Specify source and destination locations/bins
4. Logistic lines are created for reclassification activity
5. Items are moved and reclassified per barcode scan reclassification type
6. Reclassification journal is posted to update inventory

---

## 7. User Permissions and Setup

### 7.1 User Setup Fields

Administrators configure per-user permissions in User Setup page:

| Field | Purpose |
|-------|---------|
| Enable Pick Mgt. | Allow user to create and execute pick activities |
| Enable Checked Pick | Allow user to validate and check completed picks |
| Enable Processed Pick | Allow user to mark picks as processed |
| Enable Stock Mgt. | Allow user to create and execute stock activities |
| Enable Checked Stock | Allow user to validate and check completed stock activities |
| Enable Processed Stock | Allow user to mark stock activities as processed |
| Delete Lines Process Closed | Allow user to delete logistic lines marked as processed/closed |
| Template Riclass Item | Default template for item reclassification |
| Batch Riclass Item | Batch processing settings for reclassification |
| Enable AutoPost Riclass. | Automatically post reclassification after processing |
| Pick & Stock SuperUser | Unrestricted access to all pick & stock operations |

### 7.2 System Setup Configuration

Configure system-level settings in JM Setup page (Pick & Stock section):

| Field | Purpose | Values |
|-------|---------|--------|
| Parcel Nos. | Numbering series for parcel assignment | Numbering Series Code |
| Allow Tran. Ship. Posting | Enable/disable transfer shipment posting | Yes/No |
| Allow Tran. Rcpt. Posting | Enable/disable transfer receipt posting | Yes/No |
| Allow Sales Ship. Posting | Enable/disable sales shipment posting | Yes/No |
| Allow Purch. Rcpt. Posting | Enable/disable purchase receipt posting | Yes/No |
| BarcodeScan Recalss. Type | Barcode scanning behavior for reclassification | Defined Type |

---

## 8. Integration Points

### 8.1 Business Central Integration

**Document Integration:**
- Directly linked to Sales Orders, Purchase Orders, Transfer Orders
- Integrated with Service Orders and Job Planning Lines
- Connected to Production Orders and Assembly Orders
- Works with Warehouse Receipts, Shipments, and standard BC warehouse documents

**Inventory Integration:**
- Updates Item Ledger Entries upon posting
- Manages Item Tracking (Lot No., Serial No.) through standard BC item tracking system
- Interacts with Bin Contents for warehouse bin management
- Affects reservations and quantity availability

**User Integration:**
- Permission-based access through standard BC User Setup
- Activity tracking with User ID and timestamps
- Role Center integration for quick access

### 8.2 JM Utility Base Integration

**Dependency:** JM Pick And Stock depends on JM Utility Base (v27.0.0.0)

This provides core utilities and shared functionality for:
- Dialog box management (JM Dialog page)
- Common business logic
- Standard field definitions
- Shared setup tables

---

## 9. Key Features and Capabilities

### 9.1 Multi-Level Status Management

Logistic lines track status across three processing stages:
- **Open:** Initial state, awaiting processing
- **Checked:** Validated and approved for further processing
- **Processed:** Completed and ready for posting

### 9.2 Flexible Quantity Management

- **Quantity per Unit:** Support for items with variable unit conversions
- **Processed Quantity Tracking:** Track what has been completed vs. remaining
- **Partial Processing:** Support for picking/stocking less than full line quantity
- **Overpick Handling:** Configurable handling of picks exceeding reserved quantities

### 9.3 Advanced Lot/Serial/Package Support

- **Lot Number Tracking:** Full lot traceability for pick and stock operations
- **Serial Number Support:** Support for individually serialized items
- **Package/Parcel Tracking:** Link picks and receipts to specific parcels
- **Multi-Dimension Tracking:** Combine lot, serial, and package tracking in single operations

### 9.4 Warehouse Bin Integration

- **Bin Assignment:** Assign items to specific warehouse bins during picking/stocking
- **Bin Validation:** Validate bin locations and capacity constraints
- **Bin-to-Bin Movement:** Support transfers between bins via "To Bin Code"
- **Bin Content Updates:** Automatic bin content synchronization

### 9.5 Quality Control Workflow

- **Check Stage:** Validate completed picks/stock before proceeding
- **Status Progression:** Enforced workflow preventing premature processing
- **Quantity Validation:** Verify picked/stocked quantities match expectations
- **Discrepancy Handling:** Ability to reopen and correct activities before posting

---

## 10. Role Center Integration

The application extends four warehouse-related role centers with:
- Quick access to JM Logistic Lines pages
- Summary information on pick and stock activities
- Navigation shortcuts to inbound/outbound operations

**Extended Role Centers:**
1. Business Manager Role Center
2. Order Processor Role Center
3. Warehouse Manager Role Center
4. Warehouse Basic Role Center

---

## 11. Barcode Scanning Capabilities

### 11.1 Scanning Interfaces

**V1 Interface:** Standard barcode scanning for item entry

**V2 Interface:** Enhanced barcode scanning with additional validations and confirmations

### 11.2 Scanned Data Support

- Item Numbers
- Lot Numbers
- Serial Numbers
- Package/Parcel Numbers
- Bin Codes
- Location Codes

### 11.3 Reclassification Type

Configurable behavior determines how the system handles barcode scans during reclassification:
- Automatic reclassification
- Jump to next item
- Prompt for additional input
- Batch process similar items

---

## 12. Technical Specifications

### 12.1 Platform Requirements

- **Business Central Version:** 27.0.0.0 or later
- **Cloud Deployment:** Yes
- **Features:** NoImplicitWith, TranslationFile
- **Runtime:** 16.0
- **Allow Debugging:** Yes
- **Allow Source Download:** No
- **Include Symbols:** No

### 12.2 Object ID Ranges

| Range | Purpose |
|-------|---------|
| 61940-61949 | Pick and Stock core objects |
| 61950-61959 | Additional warehouse extensions |
| 62020-62029 | Production and order document extensions |
| 62320-62329 | Advanced warehouse and order extensions |

### 12.3 Suppressed Compiler Warnings

- LC0010 - Text constant localization
- LC0090 - Text constant formatting

---

## 13. Dependencies

**Required:**
- JM Utility Base (v27.0.0.0) - Core utility functions and shared setup

**No other external dependencies required**

---

## 14. Localization

**Supported Languages:**
- English (en-US) - Full support
- Italian (it-IT) - Full support

Localization includes all page captions, action labels, field descriptions, and error messages.

---

## 15. Best Practices

### 15.1 Pick & Stock Setup Best Practices

1. **Configure User Permissions Carefully:** Review each user's role and assign appropriate pick/stock permissions
2. **Set Up Numbering Series:** Configure parcel numbering series in JM Setup before using parcel functionality
3. **Establish Posting Controls:** Decide whether to allow/disallow shipment and receipt posting based on process requirements
4. **Define Reclassification Type:** Set barcode scan reclassification type to match warehouse workflow

### 15.2 Operational Best Practices

1. **Create Logistic Lines Early:** Generate logistic lines as soon as source documents are released
2. **Complete Checking Before Processing:** Don't skip the "Check" stage; it validates data accuracy
3. **Use Barcode Scanning:** Leverage barcode scanning to reduce data entry errors
4. **Monitor Status Progression:** Keep logistic lines moving through Open → Checked → Processed workflow
5. **Verify Quantities:** Always validate that picked/stocked quantities match source document requirements

### 15.3 Warehouse Management Best Practices

1. **Bin Planning:** Assign bins based on location accessibility and inventory turnover
2. **Parcel Tracking:** Use parcel numbers for complete shipment traceability
3. **Batch Operations:** For high-volume transfers, use batch reclassification to improve efficiency
4. **Quality Control:** Enforce checking at each stage to catch errors early
5. **Regular Reviews:** Monitor logistic line status to identify bottlenecks or stuck activities

---

## 16. Common Workflows and Scenarios

### 16.1 Processing a Sales Order Pick

```
1. Sales Order released in standard BC workflow
2. Navigate to Sales Order subform
3. Click "Logistic Line (Pick JM)" on selected lines
4. Logistic lines created showing items to pick
5. Warehouse personnel open JM Logistic Lines (Pick) page
6. Scan/enter item and lot details
7. Enter quantities being picked from bins
8. Initiate "Check Pick" action to validate data
9. Click "Confirm Pick" to reserve quantities
10. Click "Process Pick" to finalize
11. Post Sales Shipment in BC standard process
12. Logistic lines are marked as completed
```

### 16.2 Processing a Warehouse Receipt

```
1. Purchase Order received as Warehouse Receipt
2. Receipt lines created in BC warehouse module
3. Navigate to Warehouse Receipt page
4. Create logistic lines for inbound stock activity
5. Warehouse personnel open JM Logistic Lines (Stock) page
6. Scan items as received
7. Assign items to appropriate bins
8. Enter quantities being stocked
9. Initiate "Check Stock" action
10. Click "Confirm Stock" when quantities match receipt
11. Click "Process Stock" to complete activity
12. Post Warehouse Receipt in BC standard process
13. Inventory is updated with new bin locations
```

### 16.3 Item Reclassification Between Bins

```
1. Open Item Reclassification Journal
2. Use "Barcode Scan" action to quickly add items
3. Scan item barcodes to populate item numbers
4. System creates logistic stock lines for reclassification
5. Enter source and destination bin codes
6. Barcode scan reclassification type determines flow:
   - May prompt for additional input
   - May automatically advance to next item
   - May batch similar items
7. Warehouse personnel move items between bins
8. Confirm activities as complete
9. Process reclassification lines
10. Post journal to update inventory bin contents
```

---

## 17. Troubleshooting and Support

### 17.1 Common Issues

**Issue: Cannot create logistic lines from order**
- Verify order status is Released
- Check that source document has at least one line
- Confirm user has "Enable Pick Mgt." or "Enable Stock Mgt." permission

**Issue: Logistic lines not appearing**
- Verify logistic line status filters (Open/Checked/Processed)
- Check Activity Type is correct (Pick vs. Stock)
- Confirm source document reference is correct

**Issue: Cannot process or confirm pick**
- Verify "Check Pick" status shows green checkmark
- Ensure all required fields are populated
- Check that quantities don't exceed source document amounts
- Verify user permissions include "Enable Checked Pick" or "Enable Processed Pick"

### 17.2 Support Resources

- Configuration documentation: docs/JM Pick And Stock/
- Setup instructions: In-app help
- Contact: http://www.jmconsulting.it/

---

## 18. Version Information

| Version | Date | Key Features |
|---------|------|--------------|
| 27.0.1.1 | Current | Production release for BC 27 |
| 27.0.1.0 | Earlier | Previous production version |

---

**Document Version:** 1.0  
**Last Updated:** 2024  
**Status:** Current
