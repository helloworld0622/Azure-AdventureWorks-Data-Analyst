# Load these tables into the **Bronze Layer** as-is for initial ingestion

## 1. Sales Analysis
### Tables and Relevant Columns
- **`SalesLT.SalesOrderDetail`**:
  - **Columns**: `SalesOrderID`, `ProductID`, `UnitPrice`, `OrderQty`, `LineTotal`.
  - **Purpose**: Provides item-level sales details.
- **`SalesLT.SalesOrderHeader`**:
  - **Columns**: `SalesOrderID`, `OrderDate`, `CustomerID`, `TotalDue`, `ShipToAddressID`.
  - **Purpose**: Includes order-level sales metadata, such as dates and total amounts.

### For Enrichment
- **`SalesLT.Product`**:
  - **Columns**: `ProductID`, `Name`, `ListPrice`.
  - **Purpose**: Maps `ProductID` to product details like `Name` and `ListPrice`.

---

## 2. Customer Analysis
### Tables and Relevant Columns
- **`SalesLT.Customer`**:
  - **Columns**: `CustomerID`, `FirstName`, `LastName`, `EmailAddress`, `Phone`.
  - **Purpose**: Provides customer details for building RFM models.
- **`SalesLT.SalesOrderHeader`**:
  - **Columns**: `CustomerID`, `OrderDate`, `TotalDue`.
  - **Purpose**: Provides transaction history for RFM metrics.
- **`SalesLT.CustomerAddress`**:
  - **Columns**: `CustomerID`, `AddressID`.
  - **Purpose**: Links customers to geographical details.
- **`SalesLT.Address`**:
  - **Columns**: `City`, `StateProvince`, `CountryRegion`.
  - **Purpose**: Enriches customer data with location information.

---

## 3. Financial Analysis
### Tables and Relevant Columns
- **`SalesLT.SalesOrderHeader`**:
  - **Columns**: `TotalDue`, `Freight`, `TaxAmt`.
  - **Purpose**: Helps compute revenue, cost, and tax-related metrics.

### Optional
- Financial-specific tables are not explicitly present in the dataset. If needed, you can treat sales data (`TotalDue`) as revenue for simplicity.

---

## 4. Supply Chain Analysis
### Tables and Relevant Columns
- **`SalesLT.Product`**:
  - **Columns**: `ProductID`, `StandardCost`, `ListPrice`, `SellStartDate`, `SellEndDate`.
  - **Purpose**: Includes product-related details like pricing and lifecycle.
- **`SalesLT.SalesOrderDetail`**:
  - **Columns**: `ProductID`, `OrderQty`.
  - **Purpose**: Tracks product demand.
- **`SalesLT.ProductCategory`**:
  - **Columns**: `ProductCategoryID`, `Name`.
  - **Purpose**: Categorizes products.

---
