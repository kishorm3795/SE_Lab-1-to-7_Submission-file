# Lab 1: Requirements Engineering & UML Use-Case Modelling
## Problem Statement #31: Multi-Vendor Artisan E-Commerce Marketplace

**Department of Computer Science & Engineering, PES University**  
**Course**: Software Engineering (SE) & Requirements Engineering (RE)  
**Deliverable Repository**: Complete Lab 1 Submission  

---

## 📌 Project Overview & Context

The **Multi-Vendor Artisan E-Commerce Marketplace** is an online platform tailored for independent craftspeople (Artisan Vendors) to establish digital storefronts, manage product catalogs, process customer orders, and receive automated split payouts with platform commission deductions.

### Target Stakeholders & Actors
- 🛒 **Shopper (Primary Actor)**: Individual browsing, searching, and purchasing handcrafted goods across multiple artisan vendors in a single consolidated cart.
- 🎨 **Artisan Vendor (Primary Actor)**: Independent craftsperson setting up storefront branding, managing inventory, and tracking order fulfillment.
- 💳 **Payment Gateway (External System)**: Third-party financial service authorizing payments and executing real-time split payout disbursements.
- ⚙️ **System Administrator (Secondary Actor)**: Platform operator overseeing vendor verifications, system health, security compliance, and escrow remediation.

---

## 📋 Deliverable 1: Requirements Table

The table below outlines **5 Functional Requirements (FR-001 to FR-005)** and **2 Non-Functional Requirements (NFR-001 & NFR-002)** as required by the lab specification.

| Req ID | Type | Description | Priority | Acceptance Criteria | Rationale | Comments |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **FR-001** | Functional | The system shall split customer cart payments at checkout, allocating respective item earnings to multiple independent vendor accounts after deducting a 5% platform fee. | High | **Pass**: Split payout calculations balance to total cart value.<br/>**Fail**: Payout calculation discrepancies. | Core multi-vendor financial revenue allocation functionality. *(Provided in Lab Spec)* | Requires automated escrow transaction handling and real-time ledger accounting. |
| **FR-002** | Functional | The system shall allow an Artisan Vendor to register a digital storefront, customize shop branding (logo, banner, bio), and configure verified payout banking details. | High | **Pass**: Vendor storefront profile updates save and render publicly within 2s.<br/>**Fail**: Profile save timeout > 2s or unvalidated banking details. | Essential for independent craftspeople to establish identity and receive earnings. | Must enforce micro-deposit bank account verification before activating storefront. |
| **FR-003** | Functional | The system shall enable Artisan Vendors to manage their product catalog (add, edit, delete, hide craft products) with inventory counts, pricing, and custom attributes. | High | **Pass**: Catalog changes immediately update product availability across active search sessions.<br/>**Fail**: Stock count desynchronization across concurrent orders. | Critical for maintaining accurate stock of unique, handmade inventory. | Inventory deduction must occur atomically at payment authorization. |
| **FR-004** | Functional | The system shall allow Shoppers to search, filter products by craft category, price, and location, and aggregate items from multiple vendors into a single checkout cart. | Medium | **Pass**: Multi-vendor cart displays items grouped by seller within 1s.<br/>**Fail**: Search timeout > 2s or cart state corruption. | Enhances shopper experience and enables multi-artisan single-checkout purchasing. | Cart session state must persist across device refreshes. |
| **FR-005** | Functional | The system shall generate real-time order status updates and automated dispatch/tracking notifications for both Shoppers and Artisan Vendors upon order confirmation and shipping. | High | **Pass**: Notifications (email/SMS) dispatched within 5s of status change.<br/>**Fail**: Undelivered notifications or missing tracking links. | Ensures transparency and accountability between buyers and independent vendors. | Third-party shipping API integration is required for tracking number validation. |
| **NFR-001** | Nonfunctional *(Perf & Security)* | The product catalog must support high-resolution image rendering with CDN caching delivering load times < 500 ms. | High | **Pass**: Benchmarking tests confirm target latency (< 500 ms) under peak load.<br/>**Fail**: Load time > 500 ms or CDN hit rate < 90%. | High visual quality and fast page loading are vital for conversion rates on artisan marketplaces. *(Provided)* | Automatic image compression (WebP/AVIF format) at edge CDN node. |
| **NFR-002** | Nonfunctional *(Security)* | The system must encrypt all sensitive shopper payment details and vendor bank credentials both in transit (TLS 1.3) and at rest (AES-256) per PCI-DSS standards. | High | **Pass**: Automated security audit verifies 100% encrypted fields and zero plaintext credentials.<br/>**Fail**: Plaintext payment data detected in database or logs. | Prevents financial fraud, data leaks, and ensures strict regulatory compliance. | Quarterly third-party penetration testing and tokenization service integration required. |

📄 **Submission Deliverables**: [Requirements_Table.docx](file:///Users/pavankishorm/Documents/My%20Projects/Multi-Vendor-Artisan-E-Commerce-Marketplace/Requirements_Table.docx) | [Requirements_Table.pdf](file:///Users/pavankishorm/Documents/My%20Projects/Multi-Vendor-Artisan-E-Commerce-Marketplace/Requirements_Table.pdf)

---

## 🎨 Deliverable 2: UML Use-Case Diagram

📄 **PDF Submission Deliverable**: [Use_Case_Diagram.pdf](file:///Users/pavankishorm/Documents/My%20Projects/Multi-Vendor-Artisan-E-Commerce-Marketplace/Use_Case_Diagram.pdf)

### Key Model Features & UML Syntax:
- **Actors**:
  - `Shopper` (Primary Actor - Left)
  - `Artisan Vendor` (Primary Actor - Left)
  - `Payment Gateway` (External System Actor - Right)
  - `System Admin` (Secondary Actor - Right)
- **System Boundary**: `Multi-Vendor Marketplace Platform`
- **Use Cases (`UC-01` to `UC-07`)**:
  - `UC-01`: Manage Storefront & Catalog
  - `UC-02`: Search & Filter Craft Products
  - `UC-03`: Checkout Consolidated Cart
  - `UC-04`: Process Multi-Vendor Payment & Split Payout
  - `UC-05`: Fulfill Orders & Update Tracking
  - `UC-06`: Apply Promotional Coupon
  - `UC-07`: Authenticate User Session
- **Stereotype Relationships**:
  - `UC-03 (Checkout Consolidated Cart)` ──`«include»`──► `UC-04 (Process Multi-Vendor Payment & Split Payout)`
  - `UC-01 (Manage Storefront & Catalog)` ──`«include»`──► `UC-07 (Authenticate User Session)`
  - `UC-06 (Apply Promotional Coupon)` ──`«extend»`──► `UC-03 (Checkout Consolidated Cart)`

---

## 📝 Deliverable 3: Use-Case Flow Specification

📄 **Submission Deliverables**: [Use_Case_Flow_Specification.docx](file:///Users/pavankishorm/Documents/My%20Projects/Multi-Vendor-Artisan-E-Commerce-Marketplace/Use_Case_Flow_Specification.docx) | [Use_Case_Flow_Specification.pdf](file:///Users/pavankishorm/Documents/My%20Projects/Multi-Vendor-Artisan-E-Commerce-Marketplace/Use_Case_Flow_Specification.pdf)

### Core Use Case: `UC-04 Process Multi-Vendor Cart Payment & Automated Split Payout`

#### Metadata
- **System**: Multi-Vendor Artisan E-Commerce Marketplace
- **Primary Actor**: Shopper
- **Secondary Actors**: Artisan Vendors, Payment Gateway, System Admin
- **Mapped Requirements**: `FR-001`, `FR-004`, `NFR-002`

#### Preconditions
1. **Shopper Session**: Shopper is logged in with items from at least two distinct Artisan Vendors in their cart.
2. **Vendor Bank Status**: Participating vendors have active, verified bank account credentials on file.
3. **Gateway Status**: Payment Gateway service is online and PCI-DSS tokenized.

#### Postconditions
1. Total cart payment is authorized and charged to the Shopper's payment instrument.
2. 5% platform commission fee is credited to the marketplace treasury account.
3. 95% net payout balance is allocated to corresponding vendor ledgers.
4. Individual vendor sub-orders are generated with "Paid" status and fulfillment alerts are dispatched.

#### Main Success Scenario (10 Steps)

| Step | Actor | Action |
| :--- | :--- | :--- |
| **1** | **Shopper** | Reviews multi-vendor shopping cart and clicks **"Proceed to Checkout"**. |
| **2** | **System** | Calculates itemized prices, vendor shipping rates, tax, total cart amount, and 5% platform split. |
| **3** | **Shopper** | Selects delivery address, chooses payment method, and enters payment credentials. |
| **4** | **Shopper** | Clicks **"Pay Now"** to confirm purchase. |
| **5** | **System** | Tokenizes payment details (TLS 1.3 / AES-256) and transmits request to **Payment Gateway**. |
| **6** | **Payment Gateway** | Authorizes total cart transaction amount and returns authorization success token. |
| **7** | **System** | Executes split payout engine: allocates 5% to Platform Account and 95% net earnings to **Artisan Vendor** ledgers. |
| **8** | **System** | Atomically updates inventory counts across vendor product catalogs. |
| **9** | **System** | Creates master order record and vendor sub-orders with status **"Payment Confirmed"**. |
| **10** | **System** | Displays Order Confirmation page and dispatches automated email receipts to Shopper and Vendors. |

#### Alternate Flows
- **Alternate Flow 7a: Payment Authorization Failure (Card Declined)**: Payment Gateway returns declined status. System alerts Shopper with a non-sensitive error message and prompts retry. If payment fails 3 times, checkout is cancelled and cart state is preserved.
- **Alternate Flow 8a: Vendor Account Payout Allocation Failure (Invalid Bank Account)**: If split payout to one vendor fails due to invalid bank details, Shopper payment succeeds, but affected vendor funds route into **Platform Escrow**. Admin is alerted for manual remediation, while valid vendor orders proceed without delay.

---

## 📁 Repository Directory Structure

```
Multi-Vendor-Artisan-E-Commerce-Marketplace/
├── 31_SE_Lab1_SE_Problem_Statements.pdf   # Provided Problem Statement PDF
├── Lab1_RE_student_handout.docx.pdf       # Provided Lab Handout PDF
├── LICENSE                                # MIT License File
├── README.md                              # Main Repository Documentation
├── Requirements_Table.docx                # Deliverable 1: Requirements Table DOCX
├── Requirements_Table.pdf                 # Deliverable 1: Requirements Table PDF
├── Use_Case_Diagram.pdf                   # Deliverable 2: UML Use-Case Diagram PDF
├── Use_Case_Flow_Specification.docx       # Deliverable 3: Use-Case Flow Specification DOCX
└── Use_Case_Flow_Specification.pdf        # Deliverable 3: Use-Case Flow Specification PDF
```
## PAVAN KISHOR M - PES2UG24AM111
