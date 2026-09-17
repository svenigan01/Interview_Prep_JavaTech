# Feature: Customers can view / download monthly bank statements in PDF/CSV format

## Technlogies: Java 21 + Spring Boot + Postgresql + AWS S3

## Business Requirement

Business Problem: A bank customer needs to access historical monthly account statements without contacting customer support

Functional Requirements:
1. Login to obline banking
2. Select account
3. Select available monthly statements
4. Select statement period, e.g.
     i. January 2026
     ii. February 2026
     iii. March 2026
5. View statement data
6. View/Download statement in PDF
7. Optional Download in CSV
8. Download only statements belonging to their own aacount
9. Receive appropriate error when statement doesn't exist
10. Have downloads audited

Example UI

--------------------------------------------------
              MY BANK ACCOUNT
--------------------------------------------------

Account: Checking ****1234

Available Statements

+------------+----------------+------------+
| Period     | Generated     | Actions    |
+------------+----------------+------------+
| Aug 2026   | Sep 01, 2026   | View PDF   |
| Jul 2026   | Aug 01, 2026   | View PDF   |
| Jun 2026   | Jul 01, 2026   | View PDF   |
| May 2026   | Jun 01, 2026   | View PDF   |
+------------+----------------+------------+

                 [Download CSV]


2. Non-functional requirements
This is where banking application differs from normal applications

Security:
  i. Customer can access only their own accounts
  ii. Statements must not be publicly accessible
  iii. Authentication required.
  iv. Authorization required
  iv. Encrypt data at rest
  v. Encrypt data in transit
  vi. Audit statement access/downloads
  vii. Prevent IDOR/BOLA vulnerabiliteis (Insecure Data Object reference / Broken Object Level Authorization - Access control flaw where application fails to verify user is authorized to specific object, allowing attackers to read modify data they shouldn't see)

For e.g. this blow request must NOT simply return statement 1001.


  
