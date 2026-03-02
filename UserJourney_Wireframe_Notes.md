# Supplier Portal — User Journey Wireframe Analysis Notes

## Purpose
Capturing all wireframe screenshots shared by user for generating complete E2E User Journey Flow Diagrams and Swimlane Architecture Diagrams.

---

## BATCH 1 — Supplier Manager: Supplier Management

### Image 1.1: Title Slide
- **Section:** Supplier Management
- **Persona:** Supplier Manager (HighRadius client user)

### Image 1.2: AP Automation Dashboard (Apollo Platform)
- **URL:** cloud2g.highradius.com/RRDMSProject/dms/Home.do
- **Platform:** Apollo by HighRadius
- **Module:** AP Automation
- **Top Filters:** Assigned Invoices (My Invoices), Company (All), Year (All), Month (All), Critical Invoices (All), Apply/Reset
- **Left Panel — "Invoices needs Attention":**
  - All Assigned: 421
  - Exceptions: 166
  - In Approval: 34
- **Left Panel — "Invoice Status" (Donut Chart):**
  - Total: 413 Invoices
  - Exception: 26.50% (109)
  - Ready for Approval: 22.58% (93)
  - In Approval: 29.52% (123)
  - Approved: 21.12% (87)
  - On Hold: 0.28% (1)
- **Right Panel — "Invoices Automation":**
  - All Incoming Invoices: 413
  - STP: 18
  - Non STP: 34
- **Right Panel — "Upcoming" (Bar + Line Chart):**
  - Categories: < 10 Days, 10-30 Days, > 30 Days
  - Legend: AI Data Processed, AI Data Processing, Approved, Exception, In Approval, On Hold
- **Right Panel — "Overdue" (Bar + Line Chart):**
  - Same categories and legend as Upcoming
- **Navigation Dropdown (Products):**
  - Products: Accounts Payable, **Supplier Portal** (separate module)
  - Services: LiveCube Explorer, Data Catalog, Object Manager
- **Key Insight:** Supplier Portal is a SEPARATE product module within the Apollo platform, accessible from the AP Automation navigation

### Image 1.3: Supplier List / Worklist (Supplier Portal)
- **Module Header:** Supplier Portal (Apollo / HighRadius)
- **Page Title:** All Suppliers (10)
- **Top Actions:** Actions dropdown, Filters dropdown, refresh, export, sort icons, "+ Add Supplier" button (blue), LiveCube link
- **Pagination:** 1-10 of 10
- **Left Navigation Tree:**
  - Tabs: All | My
  - All Suppliers (10)
  - Onboarded (03)
  - Invited (03) — expandable:
    - Tin Check
    - Bank Account Validation
    - Sanctions Screening
    - Need Review
  - Inactive (04)
- **Grid Columns:** Checkbox, Supplier ID, Supplier Name, Onboarding Status, Email, Date Initiated, Date Activated
- **Sample Data:**
  | Supplier ID | Supplier Name | Status | Email | Date Initiated | Date Activated |
  |---|---|---|---|---|---|
  | SUP-001 | HighRadius Corp | Onboarded | ar@highradius.com | 5 Feb, 2025 | 10 Mar, 2025 |
  | SUP-002 | ACME Corp | Invited | ar@acme.com | 17 Mar, 2025 | 17 Mar, 2025 |
  | SUP-003 | Shell Oil | Onboarded | receivables@shell.com | 7 Apr, 2025 | 7 Apr, 2025 |
  | SUP-004 | Stark Manufacturers | Inactive | john@stark.com | 20 Apr, 2025 | 21 Jun, 2025 |
  | SUP-005 | Ravi Steel | Inactive | sagi@ravisteel.com | 2 May, 2025 | 2 May, 2025 |
  | SUP-006 | Accel Power Tools | Inactive | ram@accel.com | 3 May, 2025 | 14 Jul, 2025 |
  | SUP-007 | Accel Power Tools | Inactive | michael@accel.com | 19 May, 2025 | 19 May, 2025 |
  | SUP-008 | Ravi Steel | Invited | ar@ravisteel.com | 2 Jun, 2025 | 2 Dec, 2025 |
  | SUP-009 | Ravi Steel | Invited | ar@ravisteel.com | 11 Jun, 2025 | 11 Jul, 2025 |
  | SUP-0010 | Stark Manufacturers | Onboarded | ar@stark.com | 19 Jun, 2025 | 23 Jun, 2025 |
- **Onboarding Status Values:** Onboarded (green), Invited (blue), Inactive (grey)
- **Key Insight:** Left nav tree shows the supplier lifecycle stages — from Invited (with sub-stages: TIN Check, Bank Account Validation, Sanctions Screening, Need Review) → Onboarded → Inactive

### Image 1.4: Supplier Onboarding Invitation E-Form (Modal)
- **Modal Title:** "Supplier Onboarding Invitation E-Form"
- **Fields (all required *):**
  - Supplier Name * (text input — "Enter Name")
  - Supplier E-mail * (text input — "john.doe@company.com" placeholder)
  - Confirm E-mail * (text input — "john.doe@company.com" placeholder)
  - ERP / Company * (dropdown — "Select ERP/ Company")
  - Supplier Category * (dropdown — "Select Category")
- **Actions:** Cancel, Send Invitation (blue button, enabled when form valid)
- **Filled Example:**
  - Supplier Name: James Doe
  - Supplier E-mail: james.doe@nike.com
  - Confirm E-mail: james.doe@nike.com
  - ERP/Company: AOPS001
  - Supplier Category: C- Supplier
- **Trigger:** "+ Add Supplier" button on Supplier List
- **Key Insight:** ERP/Company is a required field — confirms multi-tenant/multi-ERP design. Supplier Category maps to approval routing logic.

---

## BATCH 2 — Supplier: New Supplier Registration (Complete Multi-Step Form)

### Image 2.1: Title Slide
- **Section:** New Supplier Registration
- **Persona:** Supplier

### Image 2.2: Email Invitation Received (Gmail)
- **Email Subject:** "[External Sender] Welcome to Supplier Portal Registration" (tagged External)
- **From:** noreply <noreply@qas.com>
- **Body:**
  - "Dear James Doe,"
  - "Please click below link to complete the vendor registration process."
  - **CTA Link:** "Proceed To Complete Vendor Registration Process"
  - "If you have any questions or require further information about Vendor Registration, please feel free to contact us."
  - "Sincerely, QAS Supplier Portal Team"
- **Key Insight:** Email contains secure link to registration form (https://registrationsupplier.com/). Time-limited link. No credentials in email — link-based access.

### Image 2.3: Registration Form — Step 1: General Supplier Information (Empty + Filled)
- **URL:** https://registrationsupplier.com/
- **Form Title:** "Supplier Registration E-Form"
- **Left Stepper Navigation (5 steps):**
  1. General Supplier Information (current — filled dot)
  2. Purchase Information
  3. Remittance Information
  4. Payment Information
  5. Upload Document
- **Section: "General Supplier Information"**
  - **Sub-section: "Supplier Identity"** — "Key information about the supplier's identity"
    - Supplier Name * (pre-filled: "James Doe")
    - Doing Business As * (placeholder: "Business Name" / filled: "Corporation")
    - Supplier E-mail * (pre-filled: "james.doe@nike.com" — from invitation)
    - Operating Unit * (pre-filled: "AOPS001" — from invitation ERP/Company)
  - **Sub-section: "Tax Information"** — "Key information regarding legal obligations and compliance requirements"
    - TIN / Foreign TIN * (placeholder: "XX-XXXXXX" / filled: "21-GHTDRT")
    - Classification Type * (dropdown: "Select Classification Type" / filled: "Corporation")
    - Form Type * (dropdown: "Select Form Type" / filled: "W-8BEN")
    - Form Signature Date * (date picker: "dd/mm/yyyy" / filled: "01/01/2026")
- **Footer:** "Last auto-saved at 10:42 AM" | Reset | Next (blue button)
- **Key Insights:**
  - Supplier Name, Email, Operating Unit are PRE-FILLED from invitation data
  - Auto-save functionality visible ("Last auto-saved at 10:42 AM")
  - TIN field has format mask (XX-XXXXXX) — triggers TIN validation
  - W-8BEN form type indicates international supplier support

### Image 2.4: Registration Form — Step 2: Purchase Information (Empty + Filled)
- **Section: "Purchase Information"**
  - **Sub-section: "Sales Representative"** — "Details of the internal representative managing this account"
    - Contact Name * (filled: "John Smith")
    - Phone Number * (filled: "+1 (555) 234-5678" — format mask: +1 (XXX) XXX-XXXX)
  - **Sub-section: "Billing & Shipping Details"** — "Where should the invoice be sent and the goods delivered?"
    - Email Address * (filled: "billing@acmecorp.us")
    - Street Address * (filled: "123 Main St")
    - Address Line 2 (Optional) (filled: "G-4 Apartment, Suit 100")
    - Country * (dropdown, filled: "United States")
    - State / Province * (filled: "California")
    - City * (filled: "San Francisco")
    - Postal / Zip Code * (filled: "23415")
- **Key Insight:** Address data collected here feeds into Address Verification screening check

### Image 2.5: Registration Form — Step 3: Remittance Information
- **Section: "Remittance Information"**
- **Initial State:** Empty grid with columns: Remit to Address Name, Address 1, City, Country, Status, Actions
  - "No Remittance Address Added — Get started by clicking on 'Add New'"
  - "+ Add New" button
- **"Add New Remittance" Modal (empty + filled):**
  - Remit to Address Name * / Phone Number *
  - Email Address *
  - Address 1 * / Address 2 (Optional) / Address 3 (Optional) / Address 4 (Optional)
  - Country * / State/Province *
  - City * / Postal/Zip Code *
  - Status * (Active toggle — ON by default)
  - Cancel / Submit (blue button)
  - **Filled example:** peterson.21@corpus.com, 123 Street Road High Street, Near Handmark Store, United States, California, San Francisco, 23415, Active
- **After Submit:** Grid shows row — Peterson | 123 Street Road, High St... | San Francisco | United States | Active | Edit/Delete icons
- **Key Insight:** Multiple remittance addresses supported (grid-based). Each has Active/Inactive status.

### Image 2.6: Registration Form — Step 4: Payment Information (Empty + Filled)
- **Section: "Payment Information"**
  - **Sub-section: "Payment Method"** — "Information about the internal representative handling this account."
    - Payment Method * (dropdown: "Select Payment Method" / filled: "Wire Transfer")
    - Nickname * (filled: "WI")
    - Account Number / IBAN Number * (placeholder: "XX-XXXXX" / filled: "HP-347598")
    - Re-enter Account Number / IBAN Number * (confirmation field — filled: "HP-347598")
    - ABA * (filled: "BB")
  - **Sub-section: "Bank Details"** — "Information which provide your banking details"
    - Bank Name * (filled: "HSBC")
    - Bank Account Type * (dropdown: "Select Account Type" / filled: "Checking")
    - Bank Address 1 * (filled: "Home Street")
    - Bank Address 2 (Optional) (filled: "Near Church Street Road")
    - Country * (dropdown, filled: "United States")
    - State / Province * (dropdown, filled: "California")
- **Key Insights:**
  - Account Number has confirmation field (re-enter) — prevents bank detail errors
  - Bank details collected here feed into Bank Account Validation agent
  - Payment Method dropdown suggests multiple methods supported (Wire Transfer, ACH, Check, etc.)

### Image 2.7: Registration Form — Step 5: Upload Document (Empty + Filled + File Picker + Submit)
- **Section: "Upload Document"**
  - Document Type * (dropdown: "Select Document Type" / filled: "XLSX")
  - Drag-and-drop area: "Drag and drop files here or **Browse** your files"
  - Document grid columns: File Name, User, Date Created, Document Type, Preview, Action
  - **Initial state:** "No Documents Uploaded Yet — Use the upload area above to add your required files."
  - **File picker dialog:** Shows selecting 3 XLSX files: aqc_corp.xlsx, jan_feb.xlsx, March_april.xlsx
  - **After upload:** Grid shows 3 rows:
    | File Name | User | Date Created | Document Type | Preview | Action |
    |---|---|---|---|---|---|
    | aqc_corp | James Doe | 21/01/2026 | XLSX | Eye icon | Edit/Delete |
    | jan_feb | James Doe | 12/12/2025 | XLSX | Eye icon | Edit/Delete |
    | March_april | James Doe | 23/12/2025 | XLSX | Eye icon | Edit/Delete |
  - **Certification Checkbox:** "I certify that I have reviewed the information provided and it is true and correct to the best of my knowledge." (must be checked to enable Submit)
  - **Footer:** Reset | Previous | Submit (blue, enabled when checkbox checked)
- **Success Toast:** Green banner — "Application Submitted Successfully — Your application has been submitted successfully. We have sent a confirmation email to you." (with X to dismiss)
- **Post-submit state:** All 5 stepper steps show green checkmarks. Auto-save timestamp changes to "12:03 PM"
- **Key Insights:**
  - Multi-file upload supported (batch upload via file picker)
  - Document versioning visible (edit icon per document)
  - Legal certification required before submission
  - Confirmation email sent on submission
  - This is the FINAL step — submission triggers Screening Agent

---

## BATCH 3 — Supplier: Dashboard (Post-Login)

### Image 3.1: Title Slide
- **Section:** Dashboard
- **Persona:** Supplier Logged in to portal

### Image 3.2: Supplier Dashboard (Supplier Portal — Apollo)
- **Module:** Supplier Portal (Apollo / HighRadius)
- **Top Filters:** Company (All), Year (All), Month (All), Critical (All), Apply/Reset
- **Left Panel — "Financial Summary":**
  - Total Due: $19,345
  - Overdue: $9,345
  - Invoices in Processing: $5,200
  - Unbilled PO Amount: $6,800
  - Awaiting Payment: $4,800
- **Left Panel — "My Tasks & Alerts":**
  - New POs: 3
  - Rejected Invoices: 5
  - Information Requested: 23
  - Expiring Documents: 2
- **Right Panel — "Invoice Status Pipeline" (Bar Chart):**
  - X-axis categories: Draft, Submitted, Rejected, In Progress, Paid
  - Draft: ~2.5 (orange + yellow bars)
  - Submitted: ~2 (olive bar)
  - Rejected: ~8.5 (red bar — highest)
  - In Progress: ~3 (blue bar)
  - Paid: ~2 (green bar)
  - Y-axis: No of Invoices (0–10)
- **Key Insights:**
  - This is the SUPPLIER's view (not Manager's) — shows their own financial data
  - Financial Summary gives supplier visibility into payment lifecycle
  - Tasks & Alerts section drives supplier actions (New POs to acknowledge, Rejected Invoices to fix, Info Requested to respond to, Expiring Documents to renew)
  - Invoice Status Pipeline visualizes the full invoice lifecycle
  - Filters allow multi-company/multi-year view (confirms multi-tenant supplier access)

## BATCH 4 — Supplier: Purchase Orders & Invoices

### Image 4.1: Title Slide
- **Section:** Looking through Purchase Orders
- **Persona:** Supplier logged in and looking into purchase orders

### Image 4.2: Invoice List (Supplier Portal — Apollo)
- **Module:** Supplier Portal (Apollo / HighRadius)
- **Page Title:** All Invoices (16)
- **Top Actions:** Filters dropdown, refresh, sort/export icons, "+ Add Invoice" button
- **Pagination:** 1-16 of 16
- **Left Navigation Tree:**
  - Tabs: All | My
  - All Invoices (16)
  - Draft (03)
  - Submitted (02)
  - In Progress (06)
  - Rejected (01)
  - Paid (04)
- **Grid Columns:** Checkbox, Invoice No., PO No., Status, Source, Invoice Date, Payment Terms, Due Date, Currency, Invoice Amount (partially visible)
- **Sample Data:**
  | Invoice No. | PO No. | Status | Source | Invoice Date | Payment Terms | Due Date | Currency |
  |---|---|---|---|---|---|---|---|
  | INV-2025-001 | PO-1001 | Paid | Created | 2025-06-01 | Net 30 | 2025-07-01 | USD |
  | INV-2025-002 | PO-1002 | Submitted | Received | 2025-06-05 | Net 45 | 2025-07-20 | USD |
  | INV-2025-003 | — | Draft | Received | 2025-06-07 | Net 15 | 2025-06-22 | USD |
  | INV-2025-004 | PO-1003 | In Progress | Received | 2025-06-10 | Net 30 | 2025-07-10 | USD |
  | INV-2025-005 | PO-1004 | Rejected | Created | 2025-06-12 | Net 60 | 2025-08-11 | USD |
  | INV-2025-006 | — | Void | Created | 2025-06-15 | Net 30 | 2025-07-15 | USD |
  | INV-2025-007 | PO-1005 | Paid | Created | 2025-05-20 | Net 30 | 2025-06-19 | USD |
  | INV-2025-008 | PO-1006 | Submitted | Received | 2025-06-20 | Net 45 | 2025-08-04 | USD |
  | INV-2025-009 | — | Draft | Received | 2025-06-22 | Net 15 | 2025-07-07 | USD |
  | INV-2025-010 | PO-1007 | Submitted | Received | 2025-06-25 | Net 60 | 2025-08-24 | USD |
  | INV-2025-011 | PO-1008 | In Progress | Received | 2025-06-26 | Net 30 | 2025-07-26 | USD |
  | INV-2025-012 | — | Draft | Created | 2025-06-27 | Net 30 | 2025-07-27 | USD |
  | INV-2025-013 | PO-1009 | Rejected | Received | 2025-06-03 | Net 30 | 2025-07-03 | USD |
  | INV-2025-014 | PO-1010 | In Progress | Created | 2025-06-08 | Net 45 | 2025-07-23 | USD |
  | INV-2025-015 | PO-1011 | Paid | Received | 2025-06-18 | Net 30 | 2025-07-18 | USD |
  | INV-2025-001 | PO-1001 | Paid | Received | 2025-06-01 | Net 30 | 2025-07-01 | USD |
- **Status Values:** Paid (green), Submitted (orange), Draft (yellow), In Progress (blue), Rejected (red), Void (grey)
- **Source Values:** Created (supplier-created), Received (from buyer/ERP)
- **Key Insights:**
  - Left nav mirrors invoice lifecycle: Draft → Submitted → In Progress → Rejected / Paid
  - "Void" status visible in data but NOT in left nav categories — likely a terminal/archive state
  - Some invoices have no PO No. (—) — confirms manual invoice creation without PO reference
  - Source "Created" vs "Received" distinguishes supplier-created invoices from ERP-originated ones
  - Payment Terms vary: Net 15, Net 30, Net 45, Net 60 — confirms multi-payment-term support
  - "+ Add Invoice" button confirms supplier self-service invoice creation
  - All amounts in USD — single currency visible in this view

### Image 4.3: Purchase Order List (Supplier Portal — Apollo)
- **Module:** Supplier Portal (Apollo / HighRadius)
- **Page Title:** Purchase Orders
- **Top Actions:** Actions dropdown, Filters dropdown, refresh, sort/export icons
- **Pagination:** 1-8 of 8
- **Grid Columns:** Checkbox, Purchase Order No., Status, Buyer, PO Date, Currency, Total PO Amount, Total Order Amount, Total Billed Amount (partially visible)
- **Sample Data:**
  | PO No. | Status | Buyer | PO Date | Currency | Total PO Amount | Total Order Amount |
  |---|---|---|---|---|---|---|
  | PO-00181 | Acknowledgment Pending | Global Corp | 06/20/2025 | USD | $15,500.00 | $15,500.00 |
  | PO-00163 | Acknowledgment Pending | Tech Innovate | 05/10/2025 | USD | $50,000.00 | $50,000.00 |
  | PO-00158 | Acknowledgment Pending | Local Biz | 06/25/2025 | USD | $2,500.00 | $2,500.00 |
  | PO-00166 | Acknowledged | Global Corp | 06/20/2025 | USD | $15,500.00 | $15,500.00 |
  | PO-00170 | Acknowledged | Tech Innovate | 05/10/2025 | USD | $50,000.00 | $50,000.00 |
  | PO-00144 | Acknowledgment Pending | Local Biz | 06/25/2025 | USD | $2,500.00 | $2,500.00 |
  | PO-00128 | Acknowledgment Pending | Global Corp | 06/20/2025 | USD | $15,500.00 | $15,500.00 |
  | PO-00190 | Acknowledged | Tech Innovate | 05/10/2025 | USD | $50,000.00 | $50,000.00 |
- **Status Values:** Acknowledgment Pending (orange badge), Acknowledged (green text)
- **Key Insights:**
  - PO statuses are simple: Acknowledgment Pending vs Acknowledged
  - Multiple buyers visible (Global Corp, Tech Innovate, Local Biz) — confirms multi-customer/multi-buyer PO support
  - Total PO Amount = Total Order Amount in all rows — no partial billing shown yet
  - No left nav tree on PO list (unlike Invoice List) — simpler navigation
  - "Total Billed Amount" column partially visible — tracks invoice coverage against PO

### Image 4.4: Purchase Order Detail (PO-00181)
- **Page Header:** ← PO-00181 | Acknowledgment Pending (orange badge) | **Acknowledge** button (blue) | 3-dot menu | "2 of 8" pagination with < > arrows
- **Section: "Billing & Summary"** (collapsible accordion)
  - **Billing Sub-section:**
    - PO Type: Standard PO
    - Purchase Type: Goods
    - Created by: John Doe (user icon)
    - Supplier ID: SUP-001
    - Tax Identification Number: — (empty)
  - **Summary Sub-section:**
    - Business Unit: Manufacturing
    - PO No.: PO-2025-0567
    - Currency: USD
    - PO Amount: $15,500.00
    - Payment Terms: Net 45
    - Shipping To: 789 Industrial Rd, Detroit, MI
    - Legal Entity ID: LE-001
    - Legal Entity: Aerospace Parkway
- **Section: "Line Items"** (collapsible accordion)
  - Pagination: 1-2 of 2
  - Grid Columns: Checkbox, ID, Line ID, Item Code, Item Description, Qty Ordered, Open Qty, UoM, Unit Price, Tax Code, Tax % (partially visible)
  - Data:
    | ID | Line ID | Item Code | Item Description | Qty Ordered | Open Qty | UoM | Unit Price | Tax Code |
    |---|---|---|---|---|---|---|---|---|
    | PO-0340-L1 | 1 | ABC-100 | Laptop Pro 15 | 1 | 1 | EA | $1,200.00 | GST-18% |
    | PO-0340-L2 | 2 | XYZ-201 | Ergonomic Keyboard | 1 | 1 | EA | $150.00 | GST-18% |
- **Key Insights:**
  - PO Detail shows full billing context: PO Type, Purchase Type, Business Unit, Legal Entity — rich ERP metadata
  - Line items have Open Qty field — enables partial invoicing (PO-flip with partial quantities)
  - Tax Code at line-item level (GST-18%) — supports tax calculation during invoice creation
  - "Acknowledge" button is the primary CTA — confirms supplier acknowledge/reject flow
  - 3-dot menu likely contains: Reject, Download, Print, etc.
  - Navigation arrows (2 of 8) allow browsing through POs without returning to list
  - Supplier ID (SUP-001) links PO to supplier record

### Image 4.5: PO List — Bulk Selection Flow
- **Scenario:** Supplier selects 2 POs for bulk acknowledgment
- **Step 1:** 2 rows selected (PO-00181 and PO-00128) — highlighted in yellow/gold
- **Selection Bar:** "2 Records Selected" | "Select all 8 records" link | "Clear selection" link
- **Step 2:** Actions dropdown expanded → "Acknowledge Orders" option visible
- **Step 3:** After bulk acknowledge — Success toast: "✓ 2 Purchase orders acknowledged" (green banner with X dismiss)
- **Post-Action State:** PO-00181 and PO-00128 now show "Acknowledged" (green) instead of "Acknowledgment Pending"
- **Key Insights:**
  - Bulk PO acknowledgment supported via checkbox selection + Actions dropdown
  - Selection state visually highlighted (yellow row background)
  - "Select all 8 records" link for full-page bulk selection
  - Success confirmation via toast notification
  - Status updates in real-time after bulk action (no page reload needed)
  - This flow demonstrates the self-service PO acknowledgment capability described in the proposal

---

## BATCH 5 — Supplier: Invoice Detail & Management

### Image 5.1: Title Slide
- **Section:** Looking through Invoices
- **Persona:** Supplier logged in and looking at Invoices

### Image 5.2: Invoice List (Supplier Portal — Apollo)
- Same Invoice List as Batch 4 Image 4.2 — confirms consistent screen across both PO and Invoice navigation contexts
- **Note:** This is the same screen navigated from the Invoice module (left sidebar "Invoices" section) rather than from PO context

### Image 5.3: Invoice Detail — PO-Based Invoice (INV-2025-004, In Progress)
- **Page Header:** ← INV-2025-004 | In Progress (green badge) | "4 of 16" pagination with < > arrows
- **Section: "Billing, Summary & Supplier"** (collapsible accordion)
  - **Billing Sub-section:**
    - Bill to: MHC : Lifting Business
    - Legal Entity ID: 47
    - Bill to Address: 21, Aerospace PKY Cleveland, OH 44142
    - Ship to: Mazella Tennessee Sling 31702
    - Ship to Address: 529 4995 Outland Center Drive Suite 111, Dolomite, AI US 256061
    - Location: LB Memphis
  - **Summary Sub-section:**
    - Invoice No.: INV-2025-004
    - Invoice Date: 08/15/2024
    - Payment Terms: Net 30
    - Type: PO
    - PO Number: PO-1003
    - Currency: USD
    - Amount: $3,200.00
    - Due date: 10/24/2024
  - **Supplier Sub-section:**
    - Supplier: Apex Systems
    - Supplier ID: S-3543
    - Supplier Address: 415 Group 4300 Canton, OH US 44178
    - Supplier Tax Identification No: 27-3216794
- **Section: "Line Items"** (collapsible accordion)
  - Actions dropdown, refresh button
  - Grid Columns: Checkbox, Line ID, Item Code, Item Description, UoM, Unit Price, Tax Code, Tax Percentage, Tax Amount, Freight Charges (partially visible)
  - Data partially visible (1 line item row truncated)
- **Key Insights:**
  - Invoice Detail shows THREE sections: Billing, Summary, and Supplier — richer than PO Detail
  - "Type: PO" field confirms this invoice is PO-linked (vs. Non-PO for manual invoices)
  - Supplier TIN visible on invoice detail — compliance data carried through
  - Ship-to and Bill-to addresses are separate — supports complex shipping scenarios
  - No edit buttons visible on "In Progress" invoice — read-only once submitted
  - Navigation pattern same as PO Detail (4 of 16 with arrows)

### Image 5.4: Invoice Detail — Non-PO Draft Invoice (INV-2025-009, Draft) — View Mode
- **Page Header:** ← INV-2025-009 | Draft (yellow badge) | **Submit** button (blue) | **Delete** button (outline) | "9 of 16" pagination
- **Tabs:** Details | Files
- **Section: "Billing, Summary & Supplier"** (with edit pencil icon ✏️ at top right)
  - **Billing Sub-section:**
    - Bill to: Digi Solutions
    - Legal Entity ID: 47
    - Bill to Address: Cons Services, Sydney, NSW, AU
    - Ship to: Digi Solutions
    - Ship to Address: Cons Services, Sydney, NSW, AU
    - Location: AU Sydney
  - **Summary Sub-section:**
    - Invoice No.: INV-2025-009
    - Invoice Date: 06/22/2025
    - Payment Terms: Net 15
    - PO Type: Non-PO
    - Currency: USD
    - Amount: $1,100.00
    - Due date: 07/07/2025
  - **Supplier Sub-section:**
    - Supplier: Apex Systems
    - Supplier ID: S-8456
    - Supplier Address: 415 Group 4300 Canton, OH US 44178
    - Supplier Tax Identification No: 27-3216794
- **Section: "Line Items"**
  - Actions dropdown, refresh, "+ Add Line Item" button, edit pencil icon
  - Pagination: 1-2 of 2
- **Key Insights:**
  - Draft invoices have Submit and Delete actions — confirms draft lifecycle
  - "Details | Files" tabs — confirms document attachment capability on invoices
  - Edit pencil icon (✏️) on Billing section — confirms in-place editing for drafts
  - "PO Type: Non-PO" — confirms manual invoice creation without PO reference
  - "+ Add Line Item" button visible — confirms dynamic line item management
  - International addresses visible (Sydney, AU) — confirms multi-country support

### Image 5.5: Invoice Detail — Non-PO Draft Invoice (INV-2025-009, Draft) — Edit Mode
- **Same invoice as 5.4 but in EDIT MODE:**
  - "Cancel" and "Save" buttons appear at top-right of Billing section
  - Summary fields become editable:
    - Invoice No.: editable text field (INV-2025-009)
    - Invoice Date: editable date picker (06/22/2025)
    - Payment Terms: editable dropdown (Net 15)
    - PO Type: Non-PO (read-only)
    - Currency: USD (read-only)
  - Amount and Due date remain displayed but not editable inline
- **Key Insights:**
  - Edit mode is inline (not modal) — pencil icon toggles between view/edit
  - Cancel/Save pattern for edit confirmation
  - Some fields are editable (Invoice No, Date, Payment Terms) while others are read-only (PO Type, Currency)
  - This demonstrates the full CRUD lifecycle for draft invoices: Create → Edit → Save → Submit / Delete

### Image 5.6: Invoice List — Return to List After Detail View
- Same Invoice List view — confirms navigation back from detail preserves list state

---

## BATCH 6 — Supplier: Flipping PO to Create Invoice (PO-Flip Flow)

### Image 6.1: Title Slide
- **Section:** Flipping PO to Create Invoice
- **Persona:** Supplier logged in and Creating invoice by flipping Purchase order details

### Image 6.2: Purchase Order List (Starting Point)
- Same PO List as Batch 4 (Image 4.3) — 8 POs with Acknowledgment Pending / Acknowledged statuses
- **Context:** Supplier navigates to PO List to begin PO-flip flow
- **Key:** Only "Acknowledged" POs can be flipped to invoices (must acknowledge first)

### Image 6.3: PO Detail — Acknowledged PO (PO-00170) with "Create Invoice" Button
- **Page Header:** ← PO-00170 | Acknowledged (green badge) | **Create Invoice** button (teal/blue) | 5 of 8 pagination
- **Billing & Summary Section:**
  - **Billing:** PO Type: Standard PO, Purchase Type: Goods, Created by: John Doe, Supplier ID: SUP-001, Tax Identification Number: —
  - **Summary:** Business Unit: Manufacturing, PO No.: PO-00170, Currency: USD, PO Amount: $50,000.00, Payment Terms: Net 45, Shipping To: 789 Industrial Rd, Detroit, MI, Legal Entity ID: LE-001, Legal Entity: Aerospace Parkway
- **Line Items:** (1-2 of 2)
  | ID | Line ID | Item Code | Item Description | Qty Ordered | Open Qty | UoM | Unit Price | Tax Code | Tax % |
  |---|---|---|---|---|---|---|---|---|---|
  | PO-0340-L1 | 1 | ABC-100 | Laptop Pro 15 | 1 | 1 | EA | $1,200.00 | GST-18% | 18% |
  | PO-0340-L2 | 2 | XYZ-201 | Ergonomic Keyboard | 1 | 1 | EA | $150.00 | GST-18% | 18% |
- **Key Insight:** "Create Invoice" button appears ONLY on Acknowledged POs (not on Acknowledgment Pending). This is the entry point for PO-flip.

### Image 6.4: "Select Lines to Create Invoice" Modal (Empty Selection)
- **Modal Title:** "Select Lines to Create Invoice"
- **Overlay on PO Detail (PO-00170)**
- **Grid:** Same line items from PO, with checkboxes for selection
  - Pagination: 1-2 of 2
  - Columns: Checkbox, ID, Line ID, Item Code, Item Description, Qty Ordered, Open Qty, UoM, Unit Price, Tax Code
  - PO-0340-L1 (Laptop Pro 15) — unchecked
  - PO-0340-L2 (Ergonomic Keyboard) — unchecked
- **Footer Buttons:** Cancel | Create Invoice (greyed out / disabled — requires selection)
- **Key Insight:** Modal allows selective line-item picking for partial invoicing. "Create Invoice" button disabled until at least 1 line selected.

### Image 6.5: "Select Lines to Create Invoice" Modal (1 Item Selected) + Invoice Draft Created
- **Top Half — Modal with Selection:**
  - "1 Items Selected" | "Select all 2 items" link | "Clear selection" link
  - PO-0340-L1 (Laptop Pro 15) — CHECKED (highlighted blue)
  - PO-0340-L2 (Ergonomic Keyboard) — unchecked
  - **"Create Invoice" button now ACTIVE (teal/blue)**
- **Bottom Half — New Invoice Created (Draft):**
  - **Page Header:** ← New Invoice | Draft (orange badge) | Submit (greyed) | Delete | 9 of 16 pagination
  - **Success Toast:** "✓ Invoice draft created" (green banner with X dismiss)
  - **Tabs:** Details | Files
  - **Billing, Summary & Supplier Section** (with edit pencil ✏️ and collapse icons):
    - **Billing:** Bill to: MHC : Lifting Business, Legal Entity ID: 47, Bill to Address: 21, Aerospace PKY Cleveland, OH 44142, Ship to: Mazella Tennessee Sling 31702, Ship to Address: 529 4995 Outland Center Drive Suite 111 Dolomite, AI US 256061, Location: LB Memphis
    - **Summary:** Invoice No.: — (auto-generated later), Invoice Date: 08/15/2024, Payment Terms: Net 30, Type: PO, PO Number: PO-0340-L1, Currency: USD, Amount: $3,200.00, Due date: 09/15/2024
    - **Supplier:** Supplier: Apex Systems, Supplier ID: S-3245, Supplier Address: 415 Group 4300 Canton, OH US 44178, Supplier Bank Account Details: —, Supplier Tax Identification No: 27-3216794
  - **Line Items:** "+ Add Line Item" button, edit pencil, 1-2 of 2
- **Key Insights:**
  - Partial line-item selection confirmed — can create invoice from 1 of 2 PO lines
  - Invoice auto-populated from PO data (billing, supplier, line items) — this is the PO-flip
  - Invoice starts as "Draft" — not immediately submitted
  - "9 of 16" pagination — new invoice added to the invoice list (was 16, now shows as item 9)
  - Submit button is greyed initially — may require additional fields or review before submission

### Image 6.6: "Select PO Lines to add to Invoice" Modal (from Draft Invoice — Adding More Lines)
- **Context:** From the newly created Draft Invoice, supplier can add MORE PO lines
- **Top Half — Modal: "Select PO Lines to add to Invoice"**
  - "1 Items Selected" | "Select all 2 items" | "Clear selection"
  - PO-0340-L1 — CHECKED
  - PO-0340-L2 — unchecked
  - **Footer:** Cancel | **Add** (teal button — different from "Create Invoice")
- **Bottom Half — Same modal with 2 items selected:**
  - "2 Items Selected" | "Clear selection"
  - PO-0340-L1 — CHECKED
  - PO-0340-L2 — CHECKED
  - **Footer:** Cancel | **Add** (teal button)
- **Key Insights:**
  - After initial invoice creation, supplier can ADD more PO lines via "+ Add Line Item" button
  - Modal title changes from "Select Lines to Create Invoice" to "Select PO Lines to add to Invoice"
  - Button changes from "Create Invoice" to "Add" — confirms this is an additive action to existing draft
  - Supports iterative invoice building: create with partial lines → add more lines later

### Image 6.7: Invoice Draft — View Mode After Adding Lines + Success Toast
- **Page Header:** ← New Invoice | Draft (orange badge) | Submit (greyed) | Delete | 9 of 16
- **Success Toast:** "✓ Invoice lines added" (green banner with X dismiss)
- **Billing, Summary & Supplier:** Same as 6.5 — auto-populated from PO
- **Edit Pencil (✏️):** Visible at top-right of section — click to enter edit mode
- **Line Items:** "+ Add Line Item" button, edit pencil, 1-2 of 2
- **Key Insight:** Success toast confirms lines were added. Invoice is still in Draft — can continue editing.

### Image 6.8: Invoice Draft — Edit Mode (Inline Editing of Billing/Summary Fields)
- **Same invoice in EDIT MODE:**
  - "Cancel" | "Save" | side-by-side view icon buttons at top-right of section
  - **Billing fields become editable dropdowns/inputs:**
    - Bill to: dropdown (MHC : Lifting Business)
    - Legal Entity: dropdown (47)
    - Bill to Address: text input (21, Aerospace PKY Cleveland, OH 44142)
    - Ship to: dropdown (Mazella Tennessee Sling 31702)
    - Ship to Address: text input (529 4995 Outland Center Drive Suite 1...)
    - Location: dropdown (LB Memphis)
  - **Summary fields editable:**
    - Invoice No.: text input (empty — to be filled)
    - Invoice Date: date picker (08/15/2024)
    - Payment terms: dropdown (Net 30)
    - Type: dropdown (PO) — editable in this view
    - PO Number: dropdown (PO-1003)
    - Currency: text input (USD)
    - Amount: text input ($3,200.00)
    - Due Date: date picker (10/24/2024)
    - Location Code: text input (empty)
  - **Supplier section:** Read-only — Supplier: Apex Systems, Supplier ID: S-4321, Address, TIN
- **Key Insights:**
  - More fields are editable in PO-flip invoice than in Non-PO draft (Batch 5)
  - Type and PO Number are EDITABLE dropdowns — can potentially change PO reference
  - Bill-to and Ship-to are dropdowns — suggests address book lookup
  - Supplier section remains read-only — supplier identity cannot be changed on PO-linked invoice
  - Invoice No. is empty — supplier must fill in before submission

### Image 6.9: Invoice Draft — Invoice No. Filled + Save
- **Same edit mode with Invoice No. now filled: "INV-2025-003"**
- **Cancel | Save buttons visible** — about to save
- All other fields same as 6.8
- **Key Insight:** Invoice number is supplier-entered (not auto-generated) — INV-2025-003 format

### Image 6.10: Invoice Submitted — Final State
- **Top Half — Draft state with Submit button highlighted (blue/active):**
  - ← New Invoice | Draft | **Submit** (active blue) | Delete | 9 of 16
  - All fields in view mode with completed data
  - Invoice No.: INV-2025-003, Type: PO, PO Number: PO-1003, Amount: $3,200.00
- **Bottom Half — After Submit:**
  - **Page Header:** ← INV-2025-003 | **Submitted** (orange badge) | 9 of 16
  - **Success Toast:** "✓ Invoice Created Successfully" (green banner with X dismiss)
  - **All sections read-only** — no edit pencil, no Submit/Delete buttons
  - Invoice No.: INV-2025-003, Type: PO, PO Number: PO-1003
  - Supplier: Apex Systems, S-4321, TIN: 27-3216794
  - Line Items: "+ Add Line Item" still visible but likely disabled post-submit
- **Key Insights:**
  - Submit transitions invoice from "Draft" → "Submitted" status
  - After submission: read-only (consistent with Batch 5 observation for non-draft invoices)
  - Success toast confirms creation
  - Page header changes from "New Invoice" to "INV-2025-003" — invoice number becomes the title
  - Submit/Delete buttons disappear — replaced by read-only status badge
  - This completes the full PO-flip lifecycle: PO List → PO Detail → Select Lines → Draft Created → Add Lines → Edit Details → Fill Invoice No. → Save → Submit

---

## BATCH 7 — Supplier: Creating a Blank Invoice (Manual Invoice from Scratch)

### Image 7.1: Title Slide
- **Section:** Creating a Blank Invoice
- **Persona:** Supplier logged in and Creating invoice from scratch

### Image 7.2: Invoice List — Starting Point with "+ Add Invoice" Button
- Same Invoice List as previous batches — All Invoices (16)
- **Context:** Supplier clicks "+ Add Invoice" button to create a blank invoice (not from PO-flip)
- **Left Nav:** All Invoices (16), Draft (03), Submitted (02), In Progress (06), Rejected (01), Paid (04)

### Image 7.3: Blank Invoice Created — View Mode (All Fields Empty)
- **Page Header:** ← New Invoice | Draft (orange badge) | **Submit** (blue, active) | **Delete** | 9 of 16 pagination
- **Tabs:** Details | Files
- **Right Panel:** "Document Viewer" sidebar (collapsed)
- **Billing, Summary & Supplier Section** (with edit pencil ✏️):
  - **Billing:** Bill to: —, Legal Entity ID: —, Bill to Address: —, Ship to: —, Ship to Address: —, Location: LB Memphis (only Location pre-filled)
  - **Summary:** Invoice No.: —, Invoice Date: —, Payment Terms: —, Type: —, PO Number: —, Currency: —, Amount: —, Due date: —, Location Code: —
  - **Supplier:** Supplier: Apex Systems, Supplier ID: S-4321, Supplier Address: 415 Group 4300 Canton, OH US 44178, Supplier Bank Account Details: —, Supplier Tax Identification No: 27-3216794
- **Line Items Section:**
  - Actions dropdown, refresh, "+ Add" dropdown, Edit (greyed), Delete (greyed)
  - Empty grid — no line items yet
- **Key Insights:**
  - Blank invoice has almost ALL fields empty except Supplier info and Location
  - Supplier section auto-populated from logged-in supplier profile (Apex Systems, S-4321, TIN)
  - Submit button is ACTIVE even on blank invoice — different from PO-flip where it was greyed
  - Line Items has "+ Add" dropdown (not just button) — suggests multiple add methods (manual entry, from PO, etc.)
  - Edit and Delete buttons greyed in Line Items (no items to edit/delete yet)
  - "Document Viewer" sidebar visible — for viewing attached documents

### Image 7.4: Blank Invoice — Edit Mode (All Fields Empty, Editable)
- **Same invoice in EDIT MODE:**
  - Cancel | Save buttons at top-right
  - **Billing fields — ALL empty dropdowns/inputs:**
    - Bill to: empty dropdown
    - Legal Entity: empty dropdown
    - Bill to Address: empty text input
    - Ship to: empty dropdown
    - Ship to Address: empty text input
    - Location: empty dropdown
  - **Summary fields — ALL empty:**
    - Invoice No.: empty text input
    - Invoice Date: empty date picker
    - Payment terms: empty dropdown
    - Type: empty dropdown
    - PO Number: empty dropdown
    - Currency: empty text input
    - Amount: empty text input
    - Due Date: empty date picker
    - Location Code: empty text input
  - **Supplier section:** Read-only — Apex Systems, S-4321, TIN: 27-3216794
- **Line Items:** Actions dropdown, refresh, "+ Add Line Item" button, Edit (greyed)
- **Key Insights:**
  - ALL billing and summary fields are editable (blank slate)
  - Type dropdown is editable — supplier can select PO or Non-PO
  - PO Number is a dropdown — if Type=PO selected, can link to existing PO
  - This is the fully manual path vs. PO-flip (Batch 6)
  - Supplier section still read-only — consistent across all invoice creation methods

### Image 7.5: Blank Invoice — Edit Mode with Fields Filled
- **Billing fields filled:**
  - Bill to: MHC : Lifting Business (dropdown)
  - Legal Entity: 47 (dropdown)
  - Bill to Address: 21, Aerospace PKY Cleveland, OH 44142
  - Ship to: Mazella Tennessee Sling 31702 (dropdown)
  - Ship to Address: 529 4995 Outland Center Drive Suite 1...
  - Location: LB Memphis (dropdown)
- **Summary fields filled:**
  - Invoice No.: INV-2025-004
  - Invoice Date: 08/15/2024
  - Payment terms: Net 30 (dropdown)
  - Type: PO (dropdown)
  - PO Number: PO-1003 (dropdown)
  - Currency: USD
  - Amount: $3,200.00
  - Due Date: 10/24/2024
  - Location Code: empty
- **Supplier:** Read-only — Apex Systems, S-4321
- **Line Items:** Actions, refresh, "+ Add Line Item", Edit (greyed)
- **Cancel | Save** buttons visible
- **Key Insight:** Even in manual creation, supplier can link to a PO (Type: PO, PO Number: PO-1003) — this is a hybrid approach between fully manual and PO-flip

### Image 7.6: Blank Invoice — View Mode After Save, Ready to Submit
- **Bottom portion of same screen showing:**
  - ← New Invoice | Draft | **Submit** (blue, active) | Delete | 9 of 16
  - All Billing, Summary, Supplier fields populated in view mode
  - Invoice No.: INV-2025-004, Type: PO, PO Number: PO-1003, Amount: $3,200.00
  - **Submit button highlighted** — about to submit
- **Key Insight:** After saving, invoice returns to view mode with Submit active. Same flow as PO-flip: Edit → Save → Submit

### Image 7.7: Invoice Submitted — Final State (INV-2025-004, Submitted)
- **Page Header:** ← INV-2025-004 | **Submitted** (orange badge) | 9 of 16
- **No Submit/Delete buttons** — read-only after submission
- **All sections in view mode:**
  - Billing: MHC : Lifting Business, Legal Entity 47, Cleveland OH, Mazella Tennessee
  - Summary: INV-2025-004, 08/15/2024, Net 30, PO, PO-1003, USD, $3,200.00, 10/24/2024
  - Supplier: Apex Systems, S-4321, TIN: 27-3216794
- **Line Items:** Grid visible with columns (ID, Line ID, Item Code, Item Description, Qty Ordered, Open Qty, UoM, Unit Price, Tax Code)
- **Key Insights:**
  - Same final state as PO-flip submission — Draft → Submitted, read-only
  - Page header changes from "New Invoice" to "INV-2025-004"
  - Submit/Delete buttons removed post-submission
  - This completes the manual invoice creation lifecycle: Invoice List → "+ Add Invoice" → Blank Draft → Edit → Fill Fields → Save → Submit

---

## BATCH 8 — Status Variants: PO Detail & Invoice Detail (Different Statuses)

### Image 8.1: Title Slide — PO Status Variants
- **Section:** Details page for different status in PO

### Image 8.2: PO Detail — Acknowledgment Pending (PO-00181)
- **Page Header:** ← PO-00181 | Acknowledgment Pending (orange badge) | **Acknowledge** button (blue CTA) | 3-dot menu | 2 of 8 pagination
- **Billing & Summary:** Same data as Batch 4 (Standard PO, Goods, John Doe, SUP-001, Manufacturing, PO-2025-0567, USD, $15,500.00, Net 45)
- **Line Items:** Same 2 items (Laptop Pro 15 $1,200.00, Ergonomic Keyboard $150.00)
- **Key Insight:** "Acknowledge" is the primary CTA — supplier must acknowledge before any further action (e.g., Create Invoice)

### Image 8.3: PO Detail — Acknowledged (PO-00181)
- **Page Header:** ← PO-00181 | Acknowledged (green badge) | **Create Invoice** button (teal CTA) | 3-dot menu | 2 of 8 pagination
- **All other data identical to 8.2**
- **Key Insight:** After acknowledgment, the primary CTA changes from "Acknowledge" to "Create Invoice" — this is the PO-flip entry point. Status badge changes from orange to green.

### Image 8.4: PO Detail — Rejected (PO-00181) — Two Views
- **Page Header:** ← PO-00181 | Rejected (red badge) | 3-dot menu | 2 of 8 pagination
- **NO action buttons** — no Acknowledge, no Create Invoice
- **All other data identical to 8.2**
- **Key Insight:** Rejected POs are read-only — no supplier actions available. 3-dot menu may still contain options (e.g., view history, download). Two identical views shown confirming consistent rejected state.

### Image 8.5: PO Detail — Closed (PO-00181)
- **Page Header:** ← PO-00181 | Closed (green badge) | 3-dot menu | 2 of 8 pagination
- **NO action buttons** — read-only terminal state
- **All other data identical to 8.2**
- **Key Insight:** Closed is a terminal PO status — no further actions. Likely reached after all PO lines are fully invoiced and paid.

### Image 8.6: Title Slide — Invoice Status Variants
- **Section:** Details page for different status in Invoice
- **Persona:** User - Supplier

### Image 8.7: Invoice Detail — Draft (INV-2025-004)
- **Page Header:** ← INV-2025-004 | Draft (orange badge) | **Submit** (blue CTA) | **Delete** (outline) | 9 of 16 pagination
- **Tabs:** Details | Files
- **Billing:** MHC : Lifting Business, Legal Entity 47, 21 Aerospace PKY Cleveland OH 44142, Mazella Tennessee Sling 31702, 529 4995 Outland Center Drive Suite 111 Dolomite AI US 256061, LB Memphis
- **Summary:** INV-2025-004, 08/15/2024, Net 30, PO, PO-1003, USD, $3,200.00, 10/24/2024
- **Supplier:** Apex Systems, S-4321, 415 Group 4300 Canton OH US 44178, TIN: 27-3216794
- **Document Viewer** sidebar visible on right
- **Key Insight:** Draft has Submit + Delete buttons — full CRUD available. Editable state.

### Image 8.8: Invoice Detail — Submitted (INV-2025-004)
- **Page Header:** ← INV-2025-004 | Submitted (orange badge) | 9 of 16 pagination
- **NO action buttons** — read-only after submission
- **All data identical to 8.7**
- **Key Insight:** Submitted invoices are read-only — no edit, no delete. Awaiting buyer processing.

### Image 8.9: Invoice Detail — In Progress (INV-2025-004)
- **Page Header:** ← INV-2025-004 | In Progress (green badge) | 9 of 16 pagination
- **NO action buttons** — read-only
- **All data identical to 8.7**
- **Key Insight:** In Progress indicates buyer/AP system is processing the invoice. Still read-only for supplier.

### Image 8.10: Invoice Detail — Rejected (INV-2025-004)
- **Page Header:** ← INV-2025-004 | Rejected (red badge) | 9 of 16 pagination
- **NO action buttons visible** — read-only
- **All data identical to 8.7**
- **Key Insight:** Rejected invoices shown as read-only in this view. Note: no "Resubmit" or "Edit" button visible — rejection handling flow may require creating a new invoice or may be handled elsewhere.

### Image 8.11: Invoice Detail — Paid (INV-2025-004)
- **Page Header:** ← INV-2025-004 | Paid (green badge) | 9 of 16 pagination
- **NO action buttons** — read-only terminal state
- **All data identical to 8.7**
- **Key Insight:** Paid is a terminal/success state. Invoice lifecycle complete.

### Image 8.12: Invoice Detail — Void (INV-2025-004)
- **Page Header:** ← INV-2025-004 | Void (grey badge) | 9 of 16 pagination
- **NO action buttons** — read-only terminal state
- **All data identical to 8.7**
- **Key Insight:** Void is a terminal/archive state. No further actions. Not shown in Invoice List left-nav categories (confirmed in Batch 4).

### Batch 8 — Key Insights Summary
1. **PO Status Lifecycle confirmed:** Acknowledgment Pending → Acknowledged → (Rejected | Closed)
2. **PO CTA changes by status:** Acknowledgment Pending → "Acknowledge" button | Acknowledged → "Create Invoice" button | Rejected/Closed → No buttons
3. **Invoice Status Lifecycle confirmed:** Draft → Submitted → In Progress → (Rejected | Paid | Void)
4. **Invoice CTA changes by status:** Draft → "Submit" + "Delete" buttons | All other statuses → No buttons (read-only)
5. **Status badge colors:** Draft (orange), Submitted (orange), In Progress (green), Rejected (red), Paid (green), Void (grey)
6. **PO status badge colors:** Acknowledgment Pending (orange), Acknowledged (green), Rejected (red), Closed (green)
7. **No "Resubmit" on Rejected invoices** — rejection resubmission flow not shown in wireframes (identified as workflow gap in proposal)
8. **Document Viewer sidebar** visible on invoice detail across all statuses
9. **3-dot menu** on PO available across all statuses (likely contains Download, Print, etc.)
10. **Same PO/Invoice data used across all status variants** — confirms status is the only differentiator, not data changes

---

## BATCH 9 — Supplier Profile (Post-Login View)

### Image 9.1: Title Slide
- **Section:** Supplier Profile
- **Persona:** Supplier (User)

### Image 9.2: Invoice List (Navigation Context)
- Same Invoice List as previous batches (All Invoices: 16)
- Confirms left sidebar navigation: Supplier can access Profile from the same portal navigation as Invoices/POs

### Image 9.3: Supplier Information — General Supplier Information (NEW SCREEN)
- **Page Title:** Supplier Information
- **Left Navigation (vertical tabs):**
  1. **General Supplier Information** (active/highlighted — blue)
  2. Purchase Information
  3. Remittance Information
  4. Payment Information
  5. Upload Document
- **Note:** Left nav mirrors the 5-step registration wizard from Batch 2 — same structure, now as a profile view
- **Top Right Actions:** Refresh icon, Edit (pencil) icon
- **Section: "General Supplier Information"** header

#### Sub-section: Supplier Identity
| Field | Value |
|-------|-------|
| Supplier Name | James Doe |
| Doing Business As | Corporation |
| Supplier E-mail | james.doe@nike.com (clickable link) |
| Operating Unit | AOPS001 |

#### Sub-section: Tax
| Field | Value |
|-------|-------|
| TIN / Foreign TIN | 21-GHTDRT |
| Classification Type | Corporation |
| Form Type | W-8BEN |
| Form Signature Date | 01/01/2026 |

#### Sub-section: Business Profile & Certifications (NEW — not in registration)
| Field | Value |
|-------|-------|
| Description of Service/Goods | Office furniture manufacturing and installation |
| Certified by NMSDC Inc? | No (with info icon ⓘ) |
| Certified by U.S SBA? | No (with info icon ⓘ) |
| SBA Information | Large Business |

### Batch 9 Key Insights
1. **Supplier Profile is a post-registration read-only view** of the same data collected during onboarding
2. **Left nav mirrors registration stepper** — General Info, Purchase, Remittance, Payment, Upload Document (same 5 steps)
3. **Edit capability present** (pencil icon top right) — supplier can update their profile data post-registration
4. **Refresh icon** present — suggests profile data can be synced/refreshed from ERP
5. **"Business Profile & Certifications" is a NEW sub-section** not visible during registration — possibly auto-populated or added by admin post-onboarding
6. **W-8BEN form type** confirms international supplier support (W-8BEN is for foreign entities)
7. **NMSDC and SBA certification fields** — diversity/minority certification tracking (important for compliance)
8. **Operating Unit (AOPS001)** consistent with registration — confirms tenant/ERP context maintained
9. **Only "General Supplier Information" tab shown** — remaining 4 tabs (Purchase, Remittance, Payment, Upload) likely follow same read-only + edit pattern

---

## BATCH 10 — Invoice Files Tab (Attachment Management Journey)

### Image 10.1: Invoice Detail — Details Tab (Draft, Invoice "brd")
- **Invoice:** brd | Status: **In Draft** (orange badge)
- **Navigation:** 9 of 16 | ← → arrows
- **Tabs:** Details (active) | Files
- **CTAs:** Submit (blue), Delete (grey)
- **Sidebar:** "Document Viewer" collapsed on right

#### Billing Section
| Field | Value |
|-------|-------|
| Bill to | MHC |
| Legal Entity ID | 47 |
| Bill to Address | bn |
| Ship to | MHC : Indusco |
| Ship to Address | jkl |
| Location | LB Memphis |

#### Summary Section
| Field | Value |
|-------|-------|
| Invoice No. | brd |
| Invoice Date | 01/07/2025 |
| Payment Terms | DUE UPON RECEIPT |
| Type | PO |
| PO Number | - |
| Currency | USD |
| Amount | - |
| Due date | - |
| Location Code | - |

#### Supplier Section
| Field | Value |
|-------|-------|
| Supplier | ADAM FRANZ |
| Supplier ID | - |
| Supplier Address | 415 Group 4300 Canton, OH US 44178 |
| Supplier Bank Account Details | - |
| Supplier Tax Identification No | 27-3216794 |

#### Line Items
- **Actions:** Refresh, "+ Add Line Item", "Edit" buttons
- **Pagination:** 1-2 of 2

### Image 10.2: Invoice Detail — Files Tab (Empty State)
- **Same invoice:** brd | In Draft | 9 of 16
- **Tabs:** Details | **Files** (active)
- **Filter Tabs:** All (0) | Invoice (0) | Supporting (0) — all zero counts
- **Actions Bar:** Actions dropdown, **Upload** button
- **Pagination:** 1-1 of 1
- **Grid Columns:** File, Description, Tag, Type, Actions
- **Empty State:** Folder icon with "No Files Available" message, "Upload files to view here", Upload button
- **Sidebar:** "Attachments" label on right edge (collapsed)

### Image 10.3: Upload Files Modal (Empty)
- **Modal Title:** Upload Files (X close)
- **Drop Zone:** "Drag and drop files here or **Browse** your files" (Browse is a link)
- **Buttons:** Cancel | Upload (greyed out — disabled until files selected)

### Image 10.4: File Browser + Upload Modal (File Selection)
- **OS File Dialog:** Windows "Open" dialog
  - Path: This PC > Downloads
  - **3 files selected:** aqc_corp.xlsx, jan_feb.xlsx, March_april.xlsx
  - File name field shows all 3 selected
  - File type filter: All Files
- **Upload Modal behind:** Shows "our files" text in drop zone
- **Key:** Multi-file selection supported via standard OS file picker

### Image 10.5: Upload Files Modal — Upload In Progress
- **3 files uploading simultaneously:**
  - aqc_corp.xlsx — 78% Uploaded (cyan progress bar) [X to cancel]
  - jan_feb.xlsx — 78% Uploaded (cyan progress bar) [X to cancel]
  - March_april.xlsx — 78% Uploaded (cyan progress bar) [X to cancel]
- **Buttons:** Cancel | Upload (still greyed — upload in progress)

### Image 10.6: Upload Files Modal — Upload Complete
- **3 files completed:**
  - aqc_corp.xlsx — green checkmark ✓ [delete icon]
  - jan_feb.xlsx — green checkmark ✓ [delete icon]
  - March_april.xlsx — green checkmark ✓ [delete icon]
- **Buttons:** Cancel | **Upload** (now ACTIVE — blue)
- **Drop zone still visible** — can add more files
- **Key:** Upload button activates only after all files finish; delete icon to remove before confirming

### Image 10.7: Files Tab — After Successful Upload
- **Success Toast:** "Files Uploaded Successfully" (green checkmark, dismissible X)
- **Filter Tabs updated:** All (03) | Invoice (0) | Supporting (02)
- **Grid now shows 3 files (1-3 of 3):**

| File | Description | Tag | Type | Actions |
|------|-------------|-----|------|---------|
| aqc_corp.pdf | Manual | Generated (cyan) | Invoice | view, copy, 3-dot |
| jan_feb.pdf | bunt | Supporting (orange) | Invoice | view, copy, 3-dot |
| March_april.xlsx | kunt | Supporting (orange) | Others | view, copy, 3-dot |

- **Key:** .xlsx auto-converted to .pdf for Invoice-type files; "Generated" vs "Supporting" tags auto-assigned

### Image 10.8: Files Tab — 3-Dot Menu Actions
- **3-dot menu expanded on row:**
  - Edit description & type
  - Download
  - **Delete** (red text)

### Image 10.9: Edit Description and Type Modal
- **Modal Title:** Edit Description and Type (X close)
- **Fields:**
  - Attachment: March_april.xlsx (read-only)
  - Type: **GRN** (dropdown — reveals GRN as a type option)
  - Description: "kunt" (text area, editable)
- **Buttons:** Cancel | Update (greyed — activates on change)
- **Key:** Type dropdown values include: Invoice, GRN (Goods Receipt Note), Others, etc.

### Image 10.10: Files Tab — Final State
- Same grid as Image 10.7 — stable final state after upload
- **Attachments sidebar** visible on right edge (collapsed arrow)

### Image 10.11: Document Viewer — aqc_corp.pdf Preview
- **Split View:** Files grid (left) | Document Viewer (right)
- **Viewer Header:** "aqc_corp.pdf Generated" (dropdown arrow for switching files)
- **Viewer Controls:** Open in new tab, Close (X)
- **Document Rendered:** Invoice PDF showing same data as invoice detail (Invoice No: brd, ADAM FRANZ, MHC, etc.)
- **PDF Controls:** Page nav (1 of 1), Zoom (+/- 100%), Auto Zoom, Fit, Download, Print
- **Key:** "Generated" tag = system auto-generated this invoice PDF from invoice data

### Image 10.12: Document Viewer — File Switcher Dropdown
- **Dropdown from viewer header** showing all 3 files with their tags:
  - aqc_corp.pdf — Generated (cyan)
  - jan_feb.pdf — Supporting (orange)
  - March_april.xlsx — Supporting (orange)
- **Key:** Switch between attached files without closing viewer

### Image 10.13: Document Viewer — jan_feb.pdf (Supporting Document)
- **Viewer Header:** "jan_feb.pdf Supporting"
- **Document Rendered:** Real IKEA India tax invoice (sample data)
  - IKEA INDIA PRIVATE LIMITED
  - Invoice No.: S59822V000341789, Date: 18-09-2022
  - GSTIN numbers visible (Indian GST tax compliance)
  - Bill From/To, Ship From/To details
- **Key:** Supporting documents are actual uploaded files rendered in-place with full PDF viewer

### Batch 10 Key Insights
1. **Files Tab is the second tab** on Invoice Detail — dedicated to attachment management
2. **Two-step upload flow:** Select files (Browse/drag-drop) → files upload with progress → confirm Upload button
3. **Multi-file upload supported** — simultaneous upload with individual progress tracking and cancel
4. **Auto-classification:** System assigns "Generated" (system-created) vs "Supporting" (user-uploaded) tags
5. **File format conversion:** .xlsx uploads auto-converted to .pdf for Invoice-type files
6. **Type taxonomy for attachments:** Invoice, Others, GRN (Goods Receipt Note) — dropdown classification
7. **Filter tabs:** All | Invoice | Supporting — quick filtering by document category
8. **Inline Document Viewer** with full PDF rendering, zoom, download, print — no separate window
9. **File switcher dropdown** in viewer header — browse all attachments without closing viewer
10. **Full CRUD on attachments:** Upload, View (preview), Edit (description + type), Download, Delete
11. **Bulk operations** via checkbox column + Actions dropdown
12. **"Generated" invoice PDF** auto-created from invoice data — system renders invoice as downloadable PDF

---

## BATCH N — (Pending)

---

## Summary: Screens Captured So Far
| # | Screen | Persona | Module | Type |
|---|--------|---------|--------|------|
| 1 | AP Automation Dashboard | Supplier Manager | AP Automation | Dashboard |
| 2 | Supplier List / Worklist | Supplier Manager | Supplier Portal | List/Grid |
| 3 | Supplier Onboarding Invitation E-Form | Supplier Manager | Supplier Portal | Modal |
| 4 | Email Invitation (Gmail) | Supplier | Supplier Onboarding | Email |
| 5 | Registration Step 1: General Supplier Info | Supplier | Supplier Onboarding | Multi-step Form |
| 6 | Registration Step 2: Purchase Information | Supplier | Supplier Onboarding | Multi-step Form |
| 7 | Registration Step 3: Remittance Information | Supplier | Supplier Onboarding | Multi-step Form + Grid |
| 8 | Registration Step 4: Payment Information | Supplier | Supplier Onboarding | Multi-step Form |
| 9 | Registration Step 5: Upload Document | Supplier | Supplier Onboarding | Upload + Certification |
| 10 | Submission Success Toast | Supplier | Supplier Onboarding | Notification |
| 11 | Supplier Dashboard | Supplier | Supplier Portal | Dashboard |
| 12 | Invoice List | Supplier | Supplier Portal | List/Grid |
| 13 | Purchase Order List | Supplier | Supplier Portal | List/Grid |
| 14 | Purchase Order Detail (PO-00181) | Supplier | Supplier Portal | Detail View |
| 15 | PO Bulk Acknowledgment Flow | Supplier | Supplier Portal | Bulk Action Flow |
| 16 | Invoice Detail — PO-Based (INV-2025-004) | Supplier | Supplier Portal | Detail View (Read-Only) |
| 17 | Invoice Detail — Non-PO Draft (INV-2025-009) View | Supplier | Supplier Portal | Detail View (Editable) |
| 18 | Invoice Detail — Non-PO Draft Edit Mode | Supplier | Supplier Portal | Inline Edit |
| 19 | PO Detail — Acknowledged with "Create Invoice" (PO-00170) | Supplier | PO-Flip | Detail View + CTA |
| 20 | Select Lines to Create Invoice Modal | Supplier | PO-Flip | Modal (Line Selection) |
| 21 | Invoice Draft Created from PO-Flip | Supplier | PO-Flip | Detail View (Auto-populated) |
| 22 | Select PO Lines to Add to Invoice Modal | Supplier | PO-Flip | Modal (Additive Lines) |
| 23 | Invoice Draft — Edit Mode (PO-Flip) | Supplier | PO-Flip | Inline Edit |
| 24 | Invoice Submitted from PO-Flip (INV-2025-003) | Supplier | PO-Flip | Detail View (Read-Only) |
| 25 | Blank Invoice — Empty Draft (View Mode) | Supplier | Manual Invoice | Detail View (Empty) |
| 26 | Blank Invoice — Edit Mode (Empty Form) | Supplier | Manual Invoice | Inline Edit (Blank) |
| 27 | Blank Invoice — Edit Mode (Filled) | Supplier | Manual Invoice | Inline Edit (Filled) |
| 28 | Blank Invoice Submitted (INV-2025-004) | Supplier | Manual Invoice | Detail View (Read-Only) |
| 29 | PO Detail — Acknowledgment Pending (PO-00181) | Supplier | PO Status Variants | Detail View (CTA: Acknowledge) |
| 30 | PO Detail — Acknowledged (PO-00181) | Supplier | PO Status Variants | Detail View (CTA: Create Invoice) |
| 31 | PO Detail — Rejected (PO-00181) | Supplier | PO Status Variants | Detail View (Read-Only) |
| 32 | PO Detail — Closed (PO-00181) | Supplier | PO Status Variants | Detail View (Read-Only) |
| 33 | Invoice Detail — Draft (INV-2025-004) | Supplier | Invoice Status Variants | Detail View (CTA: Submit + Delete) |
| 34 | Invoice Detail — Submitted (INV-2025-004) | Supplier | Invoice Status Variants | Detail View (Read-Only) |
| 35 | Invoice Detail — In Progress (INV-2025-004) | Supplier | Invoice Status Variants | Detail View (Read-Only) |
| 36 | Invoice Detail — Rejected (INV-2025-004) | Supplier | Invoice Status Variants | Detail View (Read-Only) |
| 37 | Invoice Detail — Paid (INV-2025-004) | Supplier | Invoice Status Variants | Detail View (Read-Only) |
| 38 | Invoice Detail — Void (INV-2025-004) | Supplier | Invoice Status Variants | Detail View (Read-Only) |
| 39 | Supplier Information — General Supplier Info (Profile) | Supplier | Supplier Profile | Detail View (Read-Only + Edit) |
| 40 | Invoice Detail — Details Tab (Draft, "brd") | Supplier | Invoice Files | Detail View (Draft) |
| 41 | Invoice Detail — Files Tab (Empty State) | Supplier | Invoice Files | Tab View (Empty) |
| 42 | Upload Files Modal (Empty) | Supplier | Invoice Files | Modal (Upload) |
| 43 | Upload Files Modal — File Selection (OS Dialog) | Supplier | Invoice Files | Modal + OS Dialog |
| 44 | Upload Files Modal — Upload In Progress (78%) | Supplier | Invoice Files | Modal (Progress) |
| 45 | Upload Files Modal — Upload Complete (Ready) | Supplier | Invoice Files | Modal (Complete) |
| 46 | Files Tab — After Upload (3 files, Success Toast) | Supplier | Invoice Files | Tab View (Populated) |
| 47 | Files Tab — 3-Dot Menu (Edit/Download/Delete) | Supplier | Invoice Files | Context Menu |
| 48 | Edit Description and Type Modal | Supplier | Invoice Files | Modal (Edit Metadata) |
| 49 | Document Viewer — Generated Invoice PDF | Supplier | Invoice Files | Split View (Preview) |
| 50 | Document Viewer — File Switcher Dropdown | Supplier | Invoice Files | Split View (Switcher) |
| 51 | Document Viewer — Supporting Document (jan_feb.pdf) | Supplier | Invoice Files | Split View (Preview) |

## Key Observations
1. Supplier Portal is a separate product within Apollo platform (alongside Accounts Payable)
2. Left nav tree reveals supplier lifecycle: Invited → (TIN Check, Bank Validation, Sanctions, Need Review) → Onboarded / Inactive
3. Invitation modal captures: Name, Email (with confirmation), ERP/Company, Supplier Category
4. Multi-tenant context visible in ERP/Company dropdown (AOPS001)
5. Grid supports filtering, sorting, bulk actions, export
6. Registration form is 5-step wizard with left stepper nav: General Info → Purchase → Remittance → Payment → Upload Document
7. Supplier Name, Email, Operating Unit are pre-filled from invitation data
8. Auto-save functionality present throughout registration
9. TIN and Bank Account data collected during registration feeds directly into Screening and Bank Validation agents
10. Legal certification checkbox required before final submission
11. Confirmation email sent on successful submission
12. Remittance info uses grid-based CRUD (Add New modal → editable grid rows)
13. Document upload supports multi-file, drag-and-drop, with preview and edit/delete actions
14. Invoice List has left nav with lifecycle statuses: Draft → Submitted → In Progress → Rejected / Paid (+ Void in data)
15. Source field distinguishes "Created" (supplier) vs "Received" (ERP/buyer) invoices
16. PO List shows simple Acknowledgment Pending / Acknowledged statuses with multi-buyer support
17. PO Detail includes rich ERP metadata: PO Type, Purchase Type, Business Unit, Legal Entity, line items with Open Qty for partial invoicing
18. Bulk PO acknowledgment supported via checkbox selection + Actions dropdown with real-time status update
19. PO navigation arrows allow browsing through POs without returning to list (2 of 8 pattern)
20. Invoice Detail has 3 sections: Billing, Summary, Supplier — richer metadata than PO Detail
21. Two invoice types confirmed: PO-based (Type: PO) and manual (PO Type: Non-PO)
22. Draft invoices support full CRUD: edit (inline pencil toggle), add line items, submit, delete
23. "In Progress" invoices are read-only — no edit actions visible
24. Invoice Detail has "Details | Files" tabs — confirms document attachment on invoices
25. International addresses supported (Sydney AU, Cleveland OH) — multi-country capability
26. Some invoice fields are editable in draft (Invoice No, Date, Payment Terms) while others are read-only (PO Type, Currency)
27. PO-Flip flow: "Create Invoice" button only appears on ACKNOWLEDGED POs — must acknowledge before flipping
28. PO-Flip uses modal for selective line-item picking — enables partial invoicing (pick 1 of N lines)
29. PO-Flip auto-populates invoice from PO data: billing, supplier, line items, payment terms
30. After initial PO-flip creation, supplier can ADD more PO lines via separate "Select PO Lines to add to Invoice" modal
31. Invoice number is supplier-entered (not auto-generated) — format: INV-2025-XXX
32. Full PO-flip lifecycle: PO List → PO Detail → Select Lines → Draft → Add Lines → Edit → Save → Submit
33. Submit transitions invoice Draft → Submitted; invoice becomes read-only after submission
34. Two distinct modals: "Select Lines to Create Invoice" (initial) vs "Select PO Lines to add to Invoice" (additive)
35. Bill-to and Ship-to are dropdown selectors in edit mode — suggests address book / lookup capability
36. Supplier section is always read-only on PO-linked invoices — supplier identity inherited from PO
37. Manual invoice creation via "+ Add Invoice" creates a completely blank draft — all fields empty except Supplier info and Location
38. Blank invoice has Submit button ACTIVE immediately (unlike PO-flip where it was greyed) — suggests no mandatory pre-fill check
39. Line Items has "+ Add" DROPDOWN (not just button) in blank invoice — suggests multiple add methods (manual entry, from PO lines, etc.)
40. "Document Viewer" sidebar panel visible on blank invoice — for viewing attached documents inline
41. Even in manual creation, supplier can link to a PO via Type dropdown (PO/Non-PO) and PO Number dropdown — hybrid approach
42. Supplier section is read-only across ALL invoice creation methods (PO-flip, manual, Non-PO) — always auto-populated from supplier profile
43. Two invoice creation paths confirmed: (a) PO-Flip from PO Detail → auto-populated, (b) Manual from Invoice List → blank slate with full field editing
44. Both paths converge to same lifecycle: Draft → Edit → Save → Submit → Submitted (read-only)
45. **Full PO status lifecycle confirmed:** Acknowledgment Pending → Acknowledged → Rejected | Closed (4 statuses total)
46. **PO CTA is status-dependent:** Acknowledgment Pending → "Acknowledge" button; Acknowledged → "Create Invoice" button; Rejected/Closed → no action buttons (read-only)
47. **Full Invoice status lifecycle confirmed:** Draft → Submitted → In Progress → Rejected | Paid | Void (6 statuses total)
48. **Invoice CTA is status-dependent:** Draft → "Submit" + "Delete" buttons; all other statuses → no buttons (read-only)
49. **No "Resubmit" on Rejected invoices** — rejection resubmission flow not shown in wireframes (workflow gap confirmed)
50. **Status badge color scheme:** PO: Pending=orange, Acknowledged=green, Rejected=red, Closed=green | Invoice: Draft=orange, Submitted=orange, In Progress=green, Rejected=red, Paid=green, Void=grey
51. **Document Viewer sidebar** visible across all invoice status variants — read-only document access regardless of status
52. **3-dot menu on PO** available across all PO statuses — likely contains Download, Print, History options
53. **Supplier Profile mirrors registration structure** — same 5-tab left nav as the onboarding wizard, now as a persistent profile view
54. **Profile has edit capability** (pencil icon) — suppliers can update their information post-registration, likely triggers Master Data Change Approval agent
55. **"Business Profile & Certifications"** is a NEW section on profile not present during registration — includes NMSDC/SBA diversity certifications and service description
56. **W-8BEN form type on profile** confirms international/foreign supplier support — tax compliance tracking
57. **Profile data is read-only by default with explicit edit toggle** — consistent with the pattern seen across PO and Invoice detail views
58. **Files Tab is a dedicated second tab** on Invoice Detail for attachment management — separate from Details tab
59. **Two-step upload with progress:** Browse/drag-drop → upload with per-file progress bars → confirm Upload button
60. **Auto-classification of uploads:** System auto-tags files as "Generated" (system-created from invoice data) vs "Supporting" (user-uploaded)
61. **File format auto-conversion:** .xlsx files converted to .pdf for Invoice-type attachments — ensures consistent viewability
62. **Attachment type taxonomy:** Invoice, GRN (Goods Receipt Note), Others — dropdown-based classification via Edit modal
63. **Inline Document Viewer** renders PDFs in split-view with full controls (zoom, page nav, download, print) and file-switcher dropdown
64. **Full CRUD on attachments:** Upload, View (inline preview), Edit (description + type), Download, Delete — all available on Draft invoices
65. **"Generated" invoice PDF** = system auto-renders invoice data as a downloadable PDF document — not a user upload
66. **Attachment filter tabs** (All | Invoice | Supporting) with counts — enables quick document category filtering
