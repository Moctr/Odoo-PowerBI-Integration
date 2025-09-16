
# Power BI Odoo Integration for Procurement Report

## Description

This project integrates **Power BI** with **Odoo**, a popular open-source ERP, to create a detailed procurement report. By connecting Power BI to the Odoo database, users can view and analyze procurement data directly, enabling efficient decision-making processes.

### Key Features
- Real-time connection to Odoo database.
- Seamless integration to fetch procurement data.
- Dynamic report visuals with customizable filters.
- Automated updates to procurement reports using Power BI.

---

## Table of Contents

1. [Description](#Description)
2. [Prerequisites](#prerequisites)
3. [Configuration](#configuration)
4. [Usage](#usage)
5. [Data Model](#data-model)
6. [Power BI Report Features](#power-bi-report-features)
7. [Contributing](#contributing)
8. [License](#license)

---
## Description

This project integrates **Power BI** with the **Odoo database** to provide advanced procurement, sales, inventory, and financial reporting. The integration is built on direct connections to Odoo’s PostgreSQL models, enabling real-time analysis across multiple business processes.

The following Odoo modules and models are included:

- **Purchase Module**  
  - `purchase.order` – Purchase orders header information.  
  - `purchase.order.line` – Purchase order line details.  

- **Sales Module**  
  - `sale.order` – Sales orders and quotations.  
  - `sale.order.line` – Sales order line details.  

- **Invoicing / Accounting Module**  
  - `account.move` – Invoices and vendor bills.  
  - `account.move.line` – Invoice line details.  
  - `invoicing` (custom view) – Residual and total amounts.  

- **Products & Categories**  
  - `product.product` – Product records.  
  - `product.template` – Product templates with attributes.  
  - `product.category` – Product categorization.  

- **Vendors / Partners**  
  - `res.partner` – Supplier and customer information.  

- **Inventory / Stock Module**  
  - `stock.picking` – Stock transfers and deliveries.  
  - `stock.move` – Stock movements.  
  - `stock.quant` – Current inventory quantities.  
  - `stock.location` – Warehouse and storage locations.  

This structure ensures that procurement reports are not limited to purchase orders alone, but also include **supplier performance, product-level analysis, stock movements, and invoice tracking**, providing a holistic view of operations in one Power BI dashboard.




## Prerequisites

Before running this project, ensure the following requirements are met:

### 1. System Requirements
- **Power BI Desktop** (Version 2.90 or above) installed on your local machine.  
- Access to **Power BI Service** (optional, for sharing reports online).  
- A machine with stable network access to the Odoo server.  

### 2. Odoo Environment
- **Odoo ERP** version 13 or higher.  
- Access credentials for the **PostgreSQL database** used by Odoo.  
- Activated Odoo modules:  
  - Sales  
  - Purchase  
  - Inventory  
  - Invoicing / Accounting  

### 3. Database Access
- PostgreSQL client drivers installed (e.g., **psycopg2** or ODBC driver).  
- Read access to the following Odoo tables:  
  - `purchase.order`, `purchase.order.line`  
  - `sale.order`, `sale.order.line`  
  - `account.move`, `account.move.line`  
  - `product.product`, `product.template`, `product.category`  
  - `res.partner`  
  - `stock.picking`, `stock.move`, `stock.quant`, `stock.location`  

### 4. Power BI Configuration
- Knowledge of **DirectQuery** or **Import Mode** in Power BI.  
- Configured **data gateway** (if refreshing data from Odoo in Power BI Service).  
- Basic knowledge of DAX for creating measures and KPIs.  

### 5. Security & Access
- Ensure Odoo database user has **read-only permissions** to avoid unintended changes.  
- Secure connection string or credentials stored safely.


## Configuration

Follow these steps to configure the connection between Power BI and Odoo:

### 1. Enable Database Access in Odoo
- Confirm that your Odoo instance is running on **PostgreSQL**.  
- Ensure you have a database user with **read-only privileges** for reporting.  
- If remote access is required, configure the `pg_hba.conf` and `postgresql.conf` files on the Odoo server to allow secure external connections.

### 2. Gather Database Connection Details
Collect the following Odoo PostgreSQL credentials from your system administrator:
- **Host**: Odoo database server IP or hostname  
- **Port**: PostgreSQL default is `5432`  
- **Database name**: The Odoo database to connect with (e.g., `odoo_prod`)  
- **Username**: PostgreSQL user with read access  
- **Password**: Corresponding password  

### 3. Connect Power BI to PostgreSQL
1. Open **Power BI Desktop**.  
2. Click **Get Data** → **PostgreSQL database**.  
3. Enter the **Host**, **Database**, and credentials.  
4. Choose the connection mode:  
   - **DirectQuery** – real-time queries (recommended for live monitoring).  
   - **Import** – cached data snapshots (recommended for large datasets).  

### 4. Select Required Tables
From the database navigator, select the key Odoo models needed for procurement and analysis:
- `purchase.order`, `purchase.order.line`  
- `sale.order`, `sale.order.line`  
- `account.move`, `account.move.line`  
- `product.product`, `product.template`, `product.category`  
- `res.partner`  
- `stock.picking`, `stock.move`, `stock.quant`, `stock.location`  

### 5. Create Relationships
After loading the tables, configure relationships in Power BI’s **Model View**.  
- Link purchase orders with suppliers (`purchase.order` ↔ `res.partner`).  
- Link sales orders and invoices with customers (`sale.order` / `account.move` ↔ `res.partner`).  
- Link stock movements and quantities with products (`stock.move`, `stock.quant` ↔ `product.product`).  

### 6. Define Measures and KPIs
Using **DAX (Data Analysis Expressions)** in Power BI, create calculated fields such as:  
- Total Purchase Cost  
- Procurement Savings  
- Inventory Value by Category  
- Supplier Performance Metrics  
- Invoice Status (Paid / Unpaid / Overdue)  

### 7. (Optional) Configure Power BI Service
If deploying online:
- Publish the report to **Power BI Service**.  
- Configure a **data gateway** to allow scheduled refresh from the Odoo PostgreSQL database.  
- Set refresh frequency (e.g., hourly, daily) based on reporting needs.

## Data Flow Diagram

The following diagram illustrates the data flow for the Power BI–Odoo integration:

1. **Odoo ERP System**  
   - Business transactions are recorded in Odoo modules such as **Sales**, **Purchase**, **Inventory**, and **Accounting**.  
   - Data is stored in the underlying **PostgreSQL database**.  

2. **PostgreSQL Database**  
   - Acts as the central repository for Odoo data.  
   - Power BI connects directly to PostgreSQL using either **DirectQuery** or **Import Mode**.  

3. **Power BI Desktop / Service**  
   - Extracts tables and builds relationships across **sales orders, purchase orders, invoices, products, vendors, and stock movements**.  
   - Users can create **DAX measures**, **KPIs**, and **visualizations** for procurement and performance analysis.  

4. **End Users**  
   - Managers and stakeholders interact with dashboards and reports.  
   - Data can be filtered by **time, category, supplier, product, or location**.  
   - Reports can be published to **Power BI Service** for online sharing and scheduled refresh.
  

## Data Model

The data model for this project is built around the core Odoo modules and their PostgreSQL tables. It defines how procurement, sales, inventory, and accounting data are related and can be analyzed together in Power BI.

### Key Entities

- **Purchase Module**
  - `purchase.order` – Header information for purchase orders.
  - `purchase.order.line` – Line-level details of purchased items.

- **Sales Module**
  - `sale.order` – Sales orders and quotations.
  - `sale.order.line` – Line-level details of sales orders.

- **Invoicing / Accounting Module**
  - `account.move` – Invoices and vendor bills.
  - `account.move.line` – Invoice and bill line items.

- **Products & Categories**
  - `product.product` – Individual product records.
  - `product.template` – Product templates and attributes.
  - `product.category` – Categorization of products.

- **Vendors / Partners**
  - `res.partner` – Supplier and customer information.

- **Inventory / Stock Module**
  - `stock.picking` – Stock transfers (deliveries, receipts, internal moves).
  - `stock.move` – Itemized stock movements.
  - `stock.quant` – Current stock quantities by location.
  - `stock.location` – Warehouse and storage locations.

### Relationships

- Purchase orders are linked to **vendors** (`purchase.order` ↔ `res.partner`).  
- Sales orders and invoices are linked to **customers** (`sale.order`, `account.move` ↔ `res.partner`).  
- Products and categories are linked to **orders and stock moves** (`sale.order.line`, `purchase.order.line`, `stock.move` ↔ `product.product`).  
- Stock movements and quants are tied to **warehouses and locations** (`stock.move`, `stock.quant` ↔ `stock.location`).  

### Diagram

The following diagram illustrates the overall entity relationships:  

![Odoo Power BI Data Model](https://github.com/Moctr/Odoo-PowerBI-Integration/blob/main/Data_Model_Odoo.JPG)





