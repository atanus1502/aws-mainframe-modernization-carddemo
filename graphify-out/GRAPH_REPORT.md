# Graph Report - aws-mainframe-modernization-carddemo  (2026-09-05)

## Corpus Check
- 36 files · ~150,685 words
- Verdict: corpus is large enough that graph structure adds value.

## Summary
- 365 nodes · 471 edges · 33 communities (23 shown, 10 thin omitted)
- Extraction: 89% EXTRACTED · 10% INFERRED · 1% AMBIGUOUS · INFERRED: 45 edges (avg confidence: 0.79)
- Token cost: 374,249 input · 0 output

## Community Hubs (Navigation)
- VSAM Dataset Catalog
- CardDemo Base Application Overview
- Authorization Extension (IMS/DB2/MQ)
- Transaction Type Management (DB2)
- User Application Flow
- Authorization Flow Architecture
- Main Menu Navigation
- Contributing & Governance
- Account Extraction via MQ
- Optional Features & JCL Utilities
- Admin Application Flow
- Sample Data Entity Model
- Admin Menu & User Security
- Pending Authorization Extension
- Authorization Details Screen
- Authorization Summary Inquiry
- IMS Pending Authorization Model
- Base App Technical Stack
- Fraud Detection Screen
- Code of Conduct
- Account Extraction MQ Transactions
- Sign-on & CICS Session
- Batch Utility Programs
- DB2 Fraud Data Model
- Git Version Info Script
- Local Compile Script
- Remote Compile Script
- Remote Refresh Script
- Remote Submit Script
- Full Batch Run Script
- Interest Calc Run Script
- Posting Run Script
- Module Upload Script

## God Nodes (most connected - your core abstractions)
1. `CardDemo - Mainframe Credit Card Management Application` - 82 edges
2. `CardDemo VSAM Catalog Listing (LISTCAT)` - 52 edges
3. `CardDemo Extension: Credit Card Authorizations (IMS/DB2/MQ) README` - 42 edges
4. `Transaction Type Management with DB2 README` - 24 edges
5. `Authorization Flow Diagram` - 17 edges
6. `Main Menu Screen` - 14 edges
7. `Credit Card Authorizations with IMS, DB2, and MQ` - 10 edges
8. `Transaction Type Management with DB2` - 9 edges
9. `DB2` - 9 edges
10. `Admin Menu Screen (CA00 / COADM01C)` - 8 edges

## Surprising Connections (you probably didn't know these)
- `Discount Group Record` --shares_data_with--> `Account Record`  [AMBIGUOUS]
  app/data/ASCII/discgrp.txt → app/data/ASCII/acctdata.txt
- `Card Record` --shares_data_with--> `Account Record`  [INFERRED]
  app/data/ASCII/carddata.txt → app/data/ASCII/acctdata.txt
- `Transaction Category Balance Record` --shares_data_with--> `Account Record`  [INFERRED]
  app/data/ASCII/tcatbal.txt → app/data/ASCII/acctdata.txt
- `Daily Transaction Record` --shares_data_with--> `Card Record`  [INFERRED]
  app/data/ASCII/dailytran.txt → app/data/ASCII/carddata.txt
- `Daily Transaction Record` --shares_data_with--> `Transaction Category Record`  [INFERRED]
  app/data/ASCII/dailytran.txt → app/data/ASCII/trancatg.txt

## Import Cycles
- None detected.

## Communities (33 total, 10 thin omitted)

### Community 0 - "VSAM Dataset Catalog"
Cohesion: 0.04
Nodes (53): ACCTDATA.PS (Sequential Dataset), ACCTDATA.VSAM.KSDS (VSAM KSDS Cluster), BIND (PDS Library), BMS (PDS Library), CARDDATA.PS (Sequential Dataset), CARDDATA.VSAM.AIX (Alternate Index), CARDDATA.VSAM.AIX.PATH (AIX Path), CARDDATA.VSAM.KSDS (VSAM KSDS Cluster) (+45 more)

### Community 1 - "CardDemo Base Application Overview"
Cohesion: 0.04
Nodes (53): ACCTFILE (Load Account Database), Additional Dataset Types (VSAM ESDS/RRDS, GDG, PDS), Admin Menu Diagram, Advanced Data Formats (COMP, COMP-3, Zoned Decimal, Signed, Unsigned), Apache 2.0 License, Application Flow - Admin Diagram, Application Flow - User Diagram, CardDemo - Mainframe Credit Card Management Application (+45 more)

### Community 2 - "Authorization Extension (IMS/DB2/MQ)"
Cohesion: 0.08
Nodes (43): CardDemo Extension: Credit Card Authorizations (IMS/DB2/MQ) README, Authorization Details Screen Image, Authorization Flow Diagram, Mark Authorization Fraud Screen Image, Authorization Summary Screen Image, AUTHFRDS (DB2 Fraud Tracking Table), CardDemo (base application), CBPAUP0C (Expired Authorization Purge Batch) (+35 more)

### Community 3 - "Transaction Type Management (DB2)"
Cohesion: 0.17
Nodes (25): Admin Menu (CA00), CardDemo, CICS, COBTUPDT, COTRTLI (BMS Map), COTRTLIC, COTRTUP (BMS Map), COTRTUPC (+17 more)

### Community 4 - "User Application Flow"
Cohesion: 0.10
Nodes (21): Account Management, Add Transaction (Add a transaction), Authorization Details (View), Authorization Summary (List), Authorizations (Optional), Authorizations Mark Fraud, Bill Pay (Pay Balance), Card Management (+13 more)

### Community 5 - "Authorization Flow Architecture"
Cohesion: 0.23
Nodes (18): Authorization Flow Diagram, Account DB (VSAM), API Gateway, Authorization (CICS COBOL Application) [A.0], Authorization Details COBOL Green Screen [S.1], Authorization Summary COBOL Green Screen [S.0], Call Center Agent Workstation, Cardholder (Payment Initiator) (+10 more)

### Community 6 - "Main Menu Navigation"
Cohesion: 0.14
Nodes (15): Menu Option: Account Update, Menu Option: Account View, Menu Option: Bill Payment, AWS Mainframe Modernization CardDemo Application, COMEN01C Program, Menu Option: Credit Card List, Menu Option: Credit Card Update, Menu Option: Credit Card View (+7 more)

### Community 7 - "Contributing & Governance"
Cohesion: 0.16
Nodes (14): Reporting Bugs/Feature Requests, Amazon Open Source Code of Conduct, Code of Conduct FAQ, Creating a Pull Request (GitHub Docs), Contributing Guidelines, Finding Contributions to Work On, Forking a Repository (GitHub Docs), Default GitHub Issue Labels (+6 more)

### Community 8 - "Account Extraction via MQ"
Cohesion: 0.24
Nodes (13): Account Extractions Module, CardDemo, cbl/ Directory, CDRA Transaction, CDRD Transaction, CICS, COACCT01 Program, CODATE01 Program (+5 more)

### Community 9 - "Optional Features & JCL Utilities"
Cohesion: 0.17
Nodes (13): Additional JCL Utilities (Optional Feature), CA00 Admin Menu (COADM01C), CREADB21 (Create CardDemo Db2 Database), CTLI Tran Type List/Update/Delete (COTRTLIC), CTTU Tran Type Add/Edit (COTRTUPC), Db2, DB2 Rewards (Roadmap), Fraud (Domain Feature) (+5 more)

### Community 10 - "Admin Application Flow"
Cohesion: 0.18
Nodes (12): Add User, Admin (Actor), Delete User, Application Flow - Admin (Diagram), List Users, Login (Login Screen), Menu (Admin Menu), Transaction Type Management (+4 more)

### Community 11 - "Sample Data Entity Model"
Cohesion: 0.36
Nodes (9): Account Record, Card Record, Card Cross-Reference Record, Customer Record, Daily Transaction Record, Discount Group Record, Transaction Category Balance Record, Transaction Category Record (+1 more)

### Community 12 - "Admin Menu & User Security"
Cohesion: 0.33
Nodes (9): Admin Menu Screen (CA00 / COADM01C), CA00 (Admin Menu Transaction), COADM01C (Admin Menu Program), List/Update Transaction Types (Db2), Maintain Transaction Types (Db2), User Add (Security), User Delete (Security), User List (Security) (+1 more)

### Community 13 - "Pending Authorization Extension"
Cohesion: 0.25
Nodes (8): Pending Authorization Extension (app-authorization-ims-db2-mq), CBPAUP0J (Purge Expired Authorizations, CBPAUP0C), CP00 Process Authorization Requests (COPAUA0C), CPVD Pending Authorization Details (COPAUS1C), CPVS Pending Authorization Summary (COPAUS0C), Credit Card Authorizations with IMS, DB2, and MQ, IMS DB, IMS DC Implementation (Roadmap)

### Community 14 - "Authorization Details Screen"
Cohesion: 0.47
Nodes (6): Authorization Details Record (card, auth resp, amount, merchant), COPAUS1C Program, CPVD Transaction, Mark/Remove Fraud Function (F5), Merchant Details (Name, Merchant ID, City, State, Zip), View Authorization Details Screen

### Community 15 - "Authorization Summary Inquiry"
Cohesion: 0.60
Nodes (5): Account Authorization Inquiry Feature, Authorization Summary Screen (CPVS), CardDemo Application, COPAUS0C Program, CPVS Transaction

### Community 16 - "IMS Pending Authorization Model"
Cohesion: 0.50
Nodes (5): account, customer, customer_card_xref, PEND AUTH DETAILS, PEND AUTH ROOT

### Community 17 - "Base App Technical Stack"
Cohesion: 0.40
Nodes (5): Base Application (Technical Highlights), CICS, COBOL, JCL, VSAM (KSDS with AIX)

### Community 18 - "Fraud Detection Screen"
Cohesion: 0.67
Nodes (4): COPAUS1C Program, Auth Fraud Screenshot (View Authorization Details), Fraud Detection / Fraud Status Marking, CPVD View Authorization Details Transaction

### Community 19 - "Code of Conduct"
Cohesion: 0.67
Nodes (4): Code of Conduct, Amazon Open Source Code of Conduct, Code of Conduct FAQ, opensource-codeofconduct@amazon.com

### Community 20 - "Account Extraction MQ Transactions"
Cohesion: 0.83
Nodes (4): Account Extractions using MQ and VSAM, CDRA Inquire Account Details via MQ (COACCT01), CDRD Inquire System Date via MQ (CODATE01), MQ

### Community 21 - "Sign-on & CICS Session"
Cohesion: 0.67
Nodes (3): CardDemo Application, CC00 Transaction ID, Sign-on Screen (CICS 3270 UI)

### Community 22 - "Batch Utility Programs"
Cohesion: 0.67
Nodes (3): ASSEMBLER, COBDATFT, MVSWAIT

## Ambiguous Edges - Review These
- `Account Record` → `Discount Group Record`  [AMBIGUOUS]
  app/data/ASCII/discgrp.txt · relation: shares_data_with
- `User Management` → `Transaction Type Management`  [AMBIGUOUS]
  diagrams/Application-Flow-Admin.png · relation: conceptually_related_to
- `Authorization (CICS COBOL Application) [A.0]` → `Account DB (VSAM)`  [AMBIGUOUS]
  diagrams/auth_flow.png · relation: shares_data_with
- `Authorization (CICS COBOL Application) [A.0]` → `Customer DB (VSAM)`  [AMBIGUOUS]
  diagrams/auth_flow.png · relation: shares_data_with
- `Authorization (CICS COBOL Application) [A.0]` → `Xref DB (VSAM)`  [AMBIGUOUS]
  diagrams/auth_flow.png · relation: shares_data_with

## Knowledge Gaps
- **178 isolated node(s):** `git-addSrcVersionInfo.sh script`, `local_compile.sh script`, `remote_compile.sh script`, `remote_refresh.sh script`, `remote_submit.sh script` (+173 more)
  These have ≤1 connection - possible missing edges or undocumented components. (Counts symbols only; 187 node(s) total have ≤1 connection when file, concept and rationale nodes are included.)
- **10 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **What is the exact relationship between `Account Record` and `Discount Group Record`?**
  _Edge tagged AMBIGUOUS (relation: shares_data_with) - confidence is low._
- **What is the exact relationship between `User Management` and `Transaction Type Management`?**
  _Edge tagged AMBIGUOUS (relation: conceptually_related_to) - confidence is low._
- **What is the exact relationship between `Authorization (CICS COBOL Application) [A.0]` and `Account DB (VSAM)`?**
  _Edge tagged AMBIGUOUS (relation: shares_data_with) - confidence is low._
- **What is the exact relationship between `Authorization (CICS COBOL Application) [A.0]` and `Customer DB (VSAM)`?**
  _Edge tagged AMBIGUOUS (relation: shares_data_with) - confidence is low._
- **What is the exact relationship between `Authorization (CICS COBOL Application) [A.0]` and `Xref DB (VSAM)`?**
  _Edge tagged AMBIGUOUS (relation: shares_data_with) - confidence is low._
- **Why does `CardDemo - Mainframe Credit Card Management Application` connect `CardDemo Base Application Overview` to `Optional Features & JCL Utilities`, `Pending Authorization Extension`, `Base App Technical Stack`, `Account Extraction MQ Transactions`, `Batch Utility Programs`?**
  _High betweenness centrality (0.053) - this node is a cross-community bridge._
- **What connects `git-addSrcVersionInfo.sh script`, `local_compile.sh script`, `remote_compile.sh script` to the rest of the system?**
  _178 weakly-connected nodes found - possible documentation gaps or missing edges._