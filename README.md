
# Power BI Odoo Integration for Procurement Report

## Description

This project integrates **Power BI** with **Odoo**, a popular open-source ERP, to create a detailed procurement report. By connecting Power BI to the Odoo database, users can view and analyze procurement data directly, enabling efficient decision-making processes.

### Key Features
- Real-time connection to Odoo database.
- Seamless integration to fetch procurement data.
- Dynamic report visuals with customizable filters.
- Automated updates to procurement reports using Power BI.

### Procurement Dashboard

- ![Procurement Dashboard](https://github.com/Moctr/Odoo-PowerBI-Integration/blob/main/Odoo_Page1.JPG)

### Vendor Dashboard
![Vendor](https://github.com/Moctr/Odoo-PowerBI-Integration/blob/main/Odoo_P2.JPG)
---

## Table of Contents

1. [Description](#description)  
2. [Prerequisites](#prerequisites)  
3. [Configuration](#configuration)  
4. [Data Flow Diagram](#data-flow-diagram)  
5. [Data Model](#data-model)  
6. [Power Query](#power-query)  
7. [Measures Used](#measures-used)  
8. [Maintenance and Administration](#maintenance-and-administration)  
9. [Recommendations](#recommendations) 

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




## Power Query

Power Query is used in this project to extract and transform Odoo data from PostgreSQL before loading it into the Power BI data model. This ensures that tables are clean, relationships are well-defined, and KPIs can be calculated efficiently.

### Dynamic Model Loader Function

A reusable Power Query function called **`model`** has been implemented.  
- When a user provides the **Odoo model name** (e.g., `purchase_order`, `sale_order`, `account_move`),  
- The function automatically connects to the PostgreSQL database and loads the corresponding table into Power BI.  

This reduces manual effort and ensures consistent loading of Odoo models.

#### Example Usage

### Model Function
![Model Function](https://github.com/Moctr/Odoo-PowerBI-Integration/blob/main/Power%20query_Module.JPG)




Transformations Applied

Rename columns (IDs → meaningful names, e.g., partner_id → Vendor ID).

Filter states (exclude cancelled or draft records).

Merge queries (e.g., purchase orders with partners and products).

Add calculated columns:

OrderYear = Date.Year([Order Date])

OrderMonth = Date.Month([Order Date])

Date Dimension created in Power Query to enable YOY, QOQ, and time-series analysis.



## Measures Used

The following DAX measures are implemented in Power BI to calculate KPIs across Procurement, Sales, Invoicing, and Inventory. These measures enable advanced reporting, trend analysis, and decision-making.

---

###  Procurement Measures

```dax
Total Purchase Value =
SUM ( 'purchase_order_line'[price_total] )

Average Procurement Lead Time =
AVERAGEX (
    'purchase_order',
    DATEDIFF ( 'purchase_order'[date_order], 'purchase_order'[date_approve], DAY )
)

Total PO Count =
COUNTROWS ( 'purchase_order' )

Confirmed Purchase Orders =
CALCULATE (
    COUNTROWS ( 'purchase_order' ),
    'purchase_order'[state] = "purchase"
)

Supplier On-Time Delivery % =
DIVIDE (
    CALCULATE ( COUNTROWS ( 'stock_picking' ), 'stock_picking'[state] = "done" ),
    CALCULATE ( COUNTROWS ( 'stock_picking' ), 'stock_picking'[scheduled_date] <= 'stock_picking'[date_done] )
)
```
### Sales Measures

```dax
Total Sales =
SUM ( 'sale_order_line'[price_total] )

Sales Order Count =
COUNTROWS ( 'sale_order' )

Open Quotations =
CALCULATE ( COUNTROWS ( 'sale_order' ), 'sale_order'[state] = "draft" )

Confirmed Sales Orders =
CALCULATE ( COUNTROWS ( 'sale_order' ), 'sale_order'[state] = "sale" )

Sales Growth % =
DIVIDE (
    [Total Sales] - CALCULATE ( [Total Sales], DATEADD ( 'Date'[Date], -1, YEAR ) ),
    CALCULATE ( [Total Sales], DATEADD ( 'Date'[Date], -1, YEAR ) )
)

```
### Invoicing & Finance Measures
```dax
Total Invoiced =
SUM ( 'account_move_line'[price_total] )

Total Paid =
CALCULATE (
    SUM ( 'account_move'[amount_total] ),
    'account_move'[payment_state] = "paid"
)

Outstanding Amount =
SUMX (
    FILTER ( 'account_move', 'account_move'[payment_state] <> "paid" ),
    'account_move'[amount_residual]
)

Collection Rate =
DIVIDE ( [Total Paid], [Total Invoiced] )

Overdue Invoices =
CALCULATE (
    COUNTROWS ( 'account_move' ),
    'account_move'[invoice_date_due] < TODAY(),
    'account_move'[payment_state] <> "paid"
)
```
### Time Intelligence Measures
```dax
YOY Sales =
CALCULATE ( [Total Sales], DATEADD ( 'Date'[Date], -1, YEAR ) )

YOY Purchase Value =
CALCULATE ( [Total Purchase Value], DATEADD ( 'Date'[Date], -1, YEAR ) )

QOQ Purchase Value =
CALCULATE ( [Total Purchase Value], DATEADD ( 'Date'[Date], -1, QUARTER ) )

MOY Invoices =
CALCULATE ( [Total Invoiced], DATEADD ( 'Date'[Date], -1, MONTH ) )

MTD Sales =
CALCULATE ( [Total Sales], DATESMTD ( 'Date'[Date] ) )

YTD Sales =
CALCULATE ( [Total Sales], DATESYTD ( 'Date'[Date] ) )

```

### Supporting Measures
```dax
Total Vendors = DISTINCTCOUNT ( 'res_partner'[id] )

Total Customers = DISTINCTCOUNT ( 'res_partner'[id_customer] )

Total Products = DISTINCTCOUNT ( 'product_product'[id] )

Average Order Value =
DIVIDE ( [Total Sales], [Sales Order Count] )

Average Invoice Value =
DIVIDE ( [Total Invoiced], COUNTROWS ( 'account_move' ) )

```

## Maintenance and Administration

To ensure the reliability of the Power BI – Odoo integration and reporting dashboards, the following maintenance and administration practices should be applied:

### Data Refresh
- Schedule automatic refreshes in the Power BI Service (daily, weekly, or hourly depending on business needs).  
- Verify database credentials and gateway connectivity regularly.  
- If a refresh fails, check the **Manage Gateway** settings and database permissions.  

### Database Maintenance
- Monitor the Odoo PostgreSQL database size and optimize indexes for faster queries.  
- Archive old transactional data if reporting does not require it (improves performance).  
- Apply Odoo module updates carefully and validate that schema changes are reflected in Power Query.  

### Security & Access Control
- Manage access to reports via **Power BI workspaces and roles**.  
- Limit exposure of sensitive financial data to authorized managers only.  
- Use row-level security (RLS) if certain users should only see data for their business unit or hotel.  

### Administration Tasks
- Document all Power Query transformations and DAX measures.  
- Update report visuals when new KPIs or Odoo modules are introduced.  
- Maintain a change log for model updates, schema changes, and measure modifications.  

### Troubleshooting
- **REF errors in drop-down lists**: open **Data → Manage Workbook Links** in Excel or Power BI Desktop and update the data source reference.  
- **Refresh errors**: confirm the Odoo database connection is live and credentials are still valid.  
- **Performance issues**: move complex transformations to SQL views or staged tables in PostgreSQL.  

---
## Recommendations

Based on the implementation of this project, the following recommendations are suggested to maximize the value of the Odoo–Power BI integration:

1. **Automate Refreshes**  
   - Configure scheduled refresh in the Power BI Service for near real-time reporting.  
   - Use incremental refresh for large transactional tables (e.g., invoices, stock moves) to improve performance.  

2. **Enhance Data Quality**  
   - Ensure consistent use of categories, subcategories, and product codes in Odoo.  
   - Regularly audit supplier and customer master data to avoid duplicates.  
   - Validate financial entries to prevent misclassification of expenses.  

3. **Expand Reporting Scope**  
   - Add HR, Projects, or CRM modules for cross-functional insights.  
   - Incorporate budget vs. actual analysis across all business units.  
   - Enable predictive analytics (e.g., forecast sales, procurement lead times).  

4. **Improve User Adoption**  
   - Provide user training for managers and staff on navigating dashboards.  
   - Use slicers, bookmarks, and drill-through features to improve interactivity.  
   - Develop role-based dashboards (procurement, finance, operations).  

5. **Strengthen Governance & Security**  
   - Implement Row-Level Security (RLS) to restrict sensitive data by user role.  
   - Track changes to DAX measures and Power Query transformations with version control.  
   - Establish a governance team for approving new KPIs and dashboard changes.  

6. **Continuous Improvement**  
   - Gather feedback from users regularly to refine visuals and KPIs.  
   - Monitor performance metrics in Power BI and optimize queries when necessary.  
   - Plan for yearly reviews of the data model


