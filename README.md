
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
