# Data Model Documentation

## Overview
The Power BI model contains five dimension tables and eight fact tables. Dimensions provide descriptive context; facts store operational events and measurements.

## Dimension Tables

| Table | Primary key | Purpose |
|---|---|---|
| Dim_Products | Product_ID | Product, category, brand, cost, price, and stock thresholds |
| Dim_Suppliers | Supplier_ID | Supplier identity, location, status, and rating |
| Dim_Warehouses | Warehouse_ID | Warehouse location, region, and capacity |
| Dim_Customers | Customer_ID | Customer details, location, type, and segment |
| Dim_Date | Date | Calendar attributes for time analysis |

## Fact Tables

| Table | Key / grain | Purpose |
|---|---|---|
| Fact_PurchaseOrders | Purchase_ID | Purchase order header |
| Fact_PurchaseOrderDetails | Purchase_Line_ID | Products and quantities on each purchase order |
| Fact_SalesOrders | Order_ID | Customer sales order header |
| Fact_SalesOrderDetails | Sales_Line_ID | Products and quantities on each sales order |
| Fact_InventorySnapshots | Snapshot_Date + Product_ID + Warehouse_ID | Inventory position at a point in time |
| Fact_StockMovements | Movement_ID | Stock movement transactions |
| Fact_Shipments | Shipment_ID | Dispatch and delivery details |
| Fact_Returns | Return_ID | Returned sales line details |

## Main Relationships
Verify the final relationship diagram in the PBIX file before treating this list as the exact implemented model.

- Dim_Products (1) to (*) Fact_PurchaseOrderDetails
- Dim_Products (1) to (*) Fact_SalesOrderDetails
- Dim_Products (1) to (*) Fact_InventorySnapshots
- Dim_Products (1) to (*) Fact_StockMovements
- Dim_Suppliers (1) to (*) Fact_PurchaseOrders
- Dim_Warehouses (1) to (*) Fact_PurchaseOrders
- Dim_Warehouses (1) to (*) Fact_SalesOrders
- Dim_Warehouses (1) to (*) Fact_InventorySnapshots
- Dim_Warehouses (1) to (*) Fact_StockMovements
- Dim_Customers (1) to (*) Fact_SalesOrders
- Fact_PurchaseOrders (1) to (*) Fact_PurchaseOrderDetails
- Fact_SalesOrders (1) to (*) Fact_SalesOrderDetails
- Fact_SalesOrders to Fact_Shipments (one-to-one in the generated dataset)
- Fact_SalesOrderDetails (1) to (*) Fact_Returns

## Date Relationships
Dim_Date has a unique Date column. Fact tables contain different date roles, such as order, movement, snapshot, dispatch, receipt, and delivery dates. Use appropriate active/inactive relationships or role-playing date dimensions. Verify which date relationship filters each visual and measure.

## Modeling Guidelines
- Prefer one-to-many relationships from dimensions to facts.
- Prefer single-direction filtering unless a documented requirement needs otherwise.
- Avoid unnecessary fact-to-fact relationships.
- For current inventory KPIs, use the latest relevant snapshot rather than summing all snapshots.
- Validate header/detail and order/shipment relationships.
