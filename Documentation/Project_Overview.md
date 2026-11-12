# Supply Chain & Inventory Analytics – Project Overview

## Project Overview
An end-to-end Business Intelligence project developed using Microsoft Power BI to analyze inventory, procurement, supplier performance, customer orders, and shipment delivery. The report contains five interactive dashboards.

## Business Problem
Supply chain teams need visibility into stock availability, purchasing activity, supplier reliability, order status, and delivery performance. This project combines operational data into a connected Power BI model to support monitoring and analysis.

## Objectives
- Monitor inventory quantities and inventory value.
- Identify low-stock, out-of-stock, and excess-stock products.
- Analyze purchase spending and purchase-order fulfillment.
- Evaluate supplier lead time, receipt timeliness, and rejected quantities.
- Analyze customer order status, cancellations, and shipment delivery.
- Present findings through interactive dashboards and recommendations.

## Five Dashboards
1. **Executive Overview** – sales, orders, inventory, procurement, and delivery indicators.
2. **Inventory Management** – stock quantity, inventory value, stock status, stock movements, and reorder requirements.
3. **Procurement Analytics** – purchase spend, purchase orders, ordered and received quantities, and receipt performance.
4. **Supplier Performance** – supplier activity, lead time, receipt timeliness, rejected quantities, and defect rate.
5. **Order Fulfillment & Delivery** – order status, delivered orders, on-time delivery, delivery duration, and cancellations.

## Dataset Summary
The synthetic dataset contains 13 CSV tables and 154,837 records.

| Table | Rows | Type |
|---|---:|---|
| Dim_Products | 300 | Dimension |
| Dim_Suppliers | 30 | Dimension |
| Dim_Warehouses | 8 | Dimension |
| Dim_Customers | 1,500 | Dimension |
| Dim_Date | 730 | Dimension |
| Fact_PurchaseOrders | 4,200 | Fact |
| Fact_PurchaseOrderDetails | 10,417 | Fact |
| Fact_SalesOrders | 11,500 | Fact |
| Fact_SalesOrderDetails | 28,621 | Fact |
| Fact_InventorySnapshots | 52,800 | Fact |
| Fact_StockMovements | 32,791 | Fact |
| Fact_Shipments | 10,830 | Fact |
| Fact_Returns | 1,138 | Fact |
| **Total** | **154,837** | |

Transaction period: January 2025–October 2026. Currency: INR. The dataset is synthetic and does not represent actual company data.

## Tools
- Microsoft Power BI Desktop
- Power Query
- DAX
- CSV
- Data cleaning, validation, modeling, and visualization

## Workflow
1. Import CSV files.
2. Inspect tables, columns, and data types.
3. Clean and transform data using Power Query.
4. Validate keys, relationships, quantities, dates, and calculated values.
5. Build the data model.
6. Create DAX measures and KPIs.
7. Design five interactive dashboards.
8. Test filters, relationships, and calculations.
9. Document insights, limitations, and recommendations.

## Data Quality Note
Shipment records were identified with date-order anomalies, including actual delivery dates earlier than dispatch dates. Delivery-duration and on-time-delivery metrics must be validated before being presented as final business conclusions. Document the treatment of anomalous records rather than silently changing them.
