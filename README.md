# ISO Certified Manufacturing ERP Architecture

```
Engineering
        │
        ▼
Product Master
        │
        ▼
Bill of Materials (BOM)
        │
        ▼
Routing / Process Routing
        │
        ▼
Production Planning
        │
        ▼
Material Requirement Planning (MRP)
        │
        ▼
Purchase Requisition
        │
        ▼
Purchase Order
        │
        ▼
Purchase Receive
        │
        ▼
Raw Material Inventory
        │
        ▼
Production Order / Work Order
        │
        ▼
Material Reservation
        │
        ▼
Material Issue
        │
        ▼
Production Execution
        │
        ▼
Work In Progress (WIP)
        │
        ▼
In Process QC
        │
        ▼
Production Completion
        │
        ▼
Finished Goods QC
        │
        ▼
Finished Goods Receive
        │
        ▼
Finished Goods Inventory
        │
        ▼
Sales
```

---

# ১. Standard Manufacturing Module Structure

Enterprise Manufacturing ERP-এ সাধারণত নিচের Modules থাকে।

## A. Engineering Master

এখানে Product Definition থাকে।

* Product Master
* Product Specification
* Product Version
* Formula / Recipe
* BOM
* Routing
* Operation Sequence
* Work Center
* Machine Master
* Tool Master

---

## B. Planning

এখানে Production Plan তৈরি হয়।

* Demand Planning
* Sales Forecast
* Master Production Schedule (MPS)
* Production Planning
* Capacity Planning
* Material Requirement Planning (MRP)

---

## C. Procurement Integration

MRP যদি Material Shortage দেখায় তাহলে

* Purchase Requisition
* Purchase Approval
* Purchase Order

শুরু হয়।

---

## D. Production Execution

এটি Factory Floor-এর Main Module।

* Work Order
* Batch Production
* Material Reservation
* Material Issue
* Shop Floor Execution
* Machine Allocation
* Labor Allocation
* Production Entry
* Production Completion

---

## E. Inventory Movement

* Raw Material Store
* Reserved Material
* Production Issue
* WIP
* Finished Goods
* Scrap
* Reject
* Rework
* Return Material

---

## F. Quality Management

* Incoming QC
* In Process QC
* Final QC
* Laboratory Test
* Rework
* Reject

---

## G. Costing

* Standard Cost
* Actual Cost
* Batch Cost
* Machine Cost
* Labor Cost
* Overhead
* Electricity
* Packaging
* Waste Cost

---

## H. Traceability

* Batch Management
* Lot Management
* Serial Number
* Manufacturing Date
* Expiry Date
* Recall Management

---

## I. Reports

* Production Report
* Machine Utilization
* Material Consumption
* Yield Analysis
* Waste Analysis
* OEE
* Batch History
* Traceability Report
* Cost Analysis

---

# ২. Complete Manufacturing Workflow

বাস্তব Enterprise Factory-তে Flow সাধারণত নিচের মতো হয়।

```
Customer Demand
        │
Sales Forecast
        │
Production Planning
        │
Master Production Schedule
        │
MRP Run
        │
Material Availability Check
        │
 ├───────────────┐
 │Enough Stock   │
 │               │
 ▼               ▼
Reserve Stock   Purchase Requisition
                │
                ▼
         Purchase Order
                │
                ▼
        Purchase Receive
                │
                ▼
      Raw Material Inventory
                │
                ▼
        Production Work Order
                │
                ▼
        Material Reservation
                │
                ▼
          Material Issue
                │
                ▼
      Production Execution
                │
                ▼
       Work In Progress
                │
                ▼
       In Process QC
                │
      ┌─────────┴─────────┐
      │                   │
      ▼                   ▼
    Pass                Rework
      │                   │
      └─────────┬─────────┘
                ▼
     Production Completion
                │
                ▼
       Finished Goods QC
                │
      ┌─────────┴─────────┐
      │                   │
      ▼                   ▼
    Pass               Reject
      │                   │
      ▼                   ▼
Finished Goods      Scrap/Rework
Inventory
      │
      ▼
Sales
```

---

# ৩. BOM (Bill of Materials)

BOM হলো একটি Product তৈরির Standard Recipe এবং Structure।

Biscuit-এর উদাহরণ:

```
Finished Product

Butter Biscuit 200 gm

Batch Size
1000 Packet

Yield
980 Packet

Expected Waste
2%

Ingredients

Flour
Sugar
Salt
Milk Powder
Butter
Oil
Baking Powder
Flavor

Packaging

Printed Packet
Inner Wrapper
Carton
Label
Tape
```

কিন্তু Enterprise ERP-এ BOM শুধু Raw Material List নয়।

এতে আরও থাকে—

* Version
* Effective Date
* Revision
* Alternative BOM
* UOM
* Batch Size
* Standard Yield
* Scrap %
* By Product
* Co Product

---

# ৪. Material Requirement Planning (MRP)

ধরি

১ Packet Biscuit-এর BOM অনুযায়ী লাগে

```
Flour = 250 gm

Sugar = 50 gm

Oil = 20 gm

Milk Powder = 10 gm
```

Production Plan

```
1000 Packet
```

MRP Automatically Calculate করবে

```
Flour = 250 kg

Sugar = 50 kg

Oil = 20 kg

Milk Powder =10 kg
```

তারপর Inventory Check করবে।

```
Flour Stock

200 kg

Need

250 kg

Shortage

50 kg
```

System Automatically বলবে

Purchase Required

```
Flour

50 kg
```

এরপর

Purchase Requisition তৈরি হবে।

---

# MRP-এর Business Logic

```
Production Plan

↓

BOM Explosion

↓

Material Requirement

↓

Current Stock

↓

Reserved Stock

↓

Incoming Purchase

↓

Available Stock

↓

Shortage

↓

Purchase Requisition
```

এটিকে BOM Explosion বলা হয়।

---

# ৫. Purchase Requisition

Purchase Requisition সাধারণত তিনভাবে আসে।

### Automatic

MRP থেকে

### Manual

Production Manager থেকে

### Minimum Stock Rule

Stock নিচে নেমে গেলে

এরপর Flow

```
Purchase Requisition

↓

Approval

↓

Purchase Order

↓

Receive

↓

QC

↓

Raw Material Stock
```

---

# ৬. Inventory Flow

```
Supplier

↓

Raw Material

↓

QC

↓

Raw Material Store

↓

Reserved

↓

Issue

↓

WIP

↓

QC

↓

Finished Goods

↓

Warehouse

↓

Sales
```

Stock Movement

| Stage                  | Stock                        |
| ---------------------- | ---------------------------- |
| Purchase Receive       | Raw Material +               |
| Reservation            | Available কমে Reserved বাড়ে |
| Material Issue         | Raw Material -               |
| Production Start       | WIP +                        |
| Production Complete    | WIP -                        |
| Finished Goods Receive | FG +                         |
| Reject                 | Reject +                     |
| Scrap                  | Scrap +                      |

---

# ৭. Work Order

Work Order হলো Factory-এর Production Instruction।

এতে থাকে—

* Work Order Number
* Product
* BOM Version
* Batch
* Quantity
* Machine
* Work Center
* Operator
* Planned Date
* Due Date
* Status
* QC Plan

Production Team এই Work Order অনুযায়ী কাজ করে।

---

# ৮. Quality Control

Enterprise ERP-এ QC তিনটি Stage-এ হয়।

## Incoming QC

Supplier Material

↓

Pass

↓

Raw Material Store

Fail

↓

Return

---

## In Process QC

Machine চলাকালীন

↓

Weight

↓

Moisture

↓

Dimension

↓

Temperature

↓

Quality Check

---

## Final QC

Finished Goods

↓

Pass

↓

Warehouse

Fail

↓

Reject

↓

Rework

↓

Scrap

---

# ৯. Batch / Lot Management

প্রতিটি Batch-এর নিজস্ব পরিচয় থাকে।

উদাহরণ

```
Batch

BIS250701
```

এই Batch দিয়ে আপনি জানতে পারবেন

* কোন Flour ব্যবহার হয়েছে
* কোন Supplier
* কোন Machine
* কোন Operator
* কোন QC Result
* Manufacturing Date
* Expiry Date

এটিই Traceability।

Food, Pharma, Chemical Industry-তে এটি বাধ্যতামূলক।

---

# ১০. Manufacturing Costing

Enterprise ERP Cost Formula

```
Raw Material

+

Packaging

+

Direct Labor

+

Machine Cost

+

Electricity

+

Maintenance

+

Factory Overhead

+

Quality Cost

+

Waste Cost

=

Total Production Cost
```

তারপর

```
Total Cost

/

Actual Good Quantity

=

Unit Cost
```

---

# ১১. Complete Manufacturing Module Relationship

```
Engineering
│
├── Product Master
├── Formula / Recipe
├── Bill of Materials (BOM)
├── Routing / Operations
├── Work Centers
└── Machine Master
        │
        ▼
Production Planning
        │
        ├── Sales Forecast
        ├── Customer Orders
        └── Master Production Schedule (MPS)
        │
        ▼
Material Requirement Planning (MRP)
        │
        ├── BOM Explosion
        ├── Inventory Check
        ├── Reserved Stock Check
        ├── Incoming Purchase Check
        └── Material Shortage Analysis
        │
        ▼
Purchase Requisition
        │
        ▼
Purchase Order
        │
        ▼
Purchase Receive
        │
        ▼
Incoming Quality Control
        │
        ├── Pass → Raw Material Inventory
        └── Fail → Return / Reject
                │
                ▼
Raw Material Inventory
        │
        ▼
Production Work Order
        │
        ├── Material Reservation
        ├── Material Issue
        ├── Labor Assignment
        ├── Machine Allocation
        └── Batch Allocation
                │
                ▼
Production Execution
        │
        ▼
Work In Progress (WIP)
        │
        ▼
In-Process Quality Control
        │
        ├── Pass → Continue Production
        ├── Rework → Reprocess
        └── Reject → Scrap / Reject Store
                │
                ▼
Production Completion
        │
        ▼
Finished Goods Quality Control
        │
        ├── Pass → Finished Goods Receive
        ├── Rework → Production
        └── Reject → Scrap / Reject
                │
                ▼
Finished Goods Inventory
        │
        ├── Batch / Lot Tracking
        ├── Traceability
        ├── Manufacturing Costing
        └── Inventory Valuation
                │
                ▼
Sales & Distribution
        │
        ▼
Customer
```

# Enterprise Best Practices (ISO-Aligned)

আপনার বিদ্যমান ERP-কে Enterprise Grade Manufacturing ERP-এ উন্নীত করতে Manufacturing Layer-এ নিম্নলিখিত বিষয়গুলো রাখা উচিত:

* **Engineering Change Control (ECN/ECO):** BOM বা Recipe পরিবর্তনের জন্য অনুমোদিত Revision Process।
* **BOM Versioning:** একই Product-এর একাধিক Version ও Effective Date Support।
* **Production Order Status Flow:** Draft → Planned → Released → In Progress → Completed → QC → Closed → Cancelled।
* **Material Reservation:** Work Order Release-এর আগে Material Reserve করে Stock Conflict এড়ানো।
* **Backflush বা Actual Consumption:** Standard Consumption (Backflush) অথবা Actual Consumption Entry—উভয় পদ্ধতির Support।
* **Yield & Variance Analysis:** Standard Yield বনাম Actual Yield এবং Material Variance বিশ্লেষণ।
* **Machine & Capacity Planning:** Work Center অনুযায়ী Capacity, Shift এবং Machine Load Balance।
* **Electronic Batch Record (EBR):** প্রতিটি Batch-এর সম্পূর্ণ Production History সংরক্ষণ।
* **End-to-End Traceability:** Raw Material Lot → Production Batch → Finished Goods Batch → Customer Delivery পর্যন্ত সম্পূর্ণ Traceability।
* **Complete Audit Trail:** কে, কখন, কী পরিবর্তন করেছে তার পূর্ণ ইতিহাস (ISO Audit-এর জন্য অত্যন্ত গুরুত্বপূর্ণ)।

