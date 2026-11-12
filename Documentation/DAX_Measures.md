# DAX Measures Documentation

## Purpose
This document records the DAX measures used in the report. The measure register below is a working list based on project discussions, not a verified export of every measure. Confirm exact names and formulas in the final PBIX.

## Working Measure Register

| Area | Measure | Business meaning |
|---|---|---|
| Executive | Total Sales Revenue | Revenue across sales order details |
| Executive | Total Orders | Distinct customer orders |
| Inventory | Latest Inventory Snapshot Date | Latest snapshot date in context |
| Inventory | Latest Stock Quantity | On-hand units at latest snapshot |
| Inventory | Latest Inventory Value | Inventory value at latest snapshot |
| Inventory | Latest Available Stock Quantity | Available units at latest snapshot |
| Inventory | Low Stock Products | Products with positive available stock at/below reorder level |
| Inventory | Out-of-Stock Products | Products with zero available stock |
| Inventory | Excess Stock Products | Products above target stock |
| Inventory | Stock In Quantity | Sum of stock received/in quantities |
| Inventory | Stock Out Quantity | Sum of stock issued/out quantities |
| Inventory | Reorder Quantity | Quantity needed to reach target stock for qualifying products |
| Procurement | Total Purchase Spend | Ordered quantity multiplied by unit purchase cost |
| Procurement | Total Purchase Orders | Distinct purchase order count |
| Procurement | Total Purchase Quantity | Sum of ordered quantity |
| Procurement | Total Received Quantity | Sum of received quantity |
| Procurement | Purchase Order Fulfillment % | Received quantity divided by ordered quantity |
| Procurement | On-Time Receipt % | Eligible receipt lines received on/before expected date |
| Supplier | Total Suppliers | Distinct supplier count |
| Supplier | Active Suppliers | Suppliers whose status is Active |
| Supplier | Average Lead Time | Average days from purchase order date to actual receipt date |
| Supplier | Total Rejected Quantity | Sum of rejected quantity |
| Supplier | Defect Rate % | Rejected quantity divided by received quantity |
| Delivery | Delivered Orders | Distinct orders with an actual delivery date |
| Delivery | On-Time Delivery % | Eligible shipments delivered on/before promised date |
| Delivery | Average Delivery Days | Average days from dispatch to actual delivery |
| Delivery | Cancellation Rate % | Cancelled distinct orders divided by all distinct orders |
| Delivery | Order Fulfillment % | Delivered orders divided by total orders |

## Example Formulas

### Defect Rate %
```dax
Defect Rate % =
DIVIDE(
    [Total Rejected Quantity],
    [Total Received Quantity],
    0
)
```

### Average Lead Time
```dax
Average Lead Time =
AVERAGEX(
    FILTER(
        Fact_PurchaseOrderDetails,
        NOT ISBLANK(Fact_PurchaseOrderDetails[Actual_Receipt_Date])
            && NOT ISBLANK(RELATED(Fact_PurchaseOrders[Order_Date]))
    ),
    DATEDIFF(
        RELATED(Fact_PurchaseOrders[Order_Date]),
        Fact_PurchaseOrderDetails[Actual_Receipt_Date],
        DAY
    )
)
```

### On-Time Delivery %
```dax
On-Time Delivery % =
VAR ValidDeliveries =
    FILTER(
        Fact_Shipments,
        NOT ISBLANK(Fact_Shipments[Actual_Delivery_Date])
            && NOT ISBLANK(Fact_Shipments[Promised_Delivery_Date])
    )
VAR OnTimeDeliveries =
    FILTER(
        ValidDeliveries,
        Fact_Shipments[Actual_Delivery_Date]
            <= Fact_Shipments[Promised_Delivery_Date]
    )
RETURN
    DIVIDE(COUNTROWS(OnTimeDeliveries), COUNTROWS(ValidDeliveries), 0)
```

### Average Delivery Days
```dax
Average Delivery Days =
AVERAGEX(
    FILTER(
        Fact_Shipments,
        NOT ISBLANK(Fact_Shipments[Dispatch_Date])
            && NOT ISBLANK(Fact_Shipments[Actual_Delivery_Date])
    ),
    DATEDIFF(
        Fact_Shipments[Dispatch_Date],
        Fact_Shipments[Actual_Delivery_Date],
        DAY
    )
)
```

### Cancellation Rate %
```dax
Cancellation Rate % =
DIVIDE(
    CALCULATE(
        DISTINCTCOUNT(Fact_SalesOrders[Order_ID]),
        Fact_SalesOrders[Order_Status] = "Cancelled"
    ),
    DISTINCTCOUNT(Fact_SalesOrders[Order_ID]),
    0
)
```

### Order Fulfillment %
```dax
Order Fulfillment % =
DIVIDE([Delivered Orders], [Total Orders], 0)
```

## Formatting and Validation
- Counts and quantities: whole number.
- Currency: INR with suitable display units.
- Rates: percentage format, normally 2 decimal places.
- Durations: days, normally 1–2 decimal places.
- Confirm percentage denominators and purchase-spend definition.
- Validate shipment date anomalies before trusting delivery-duration metrics.
- Ensure latest inventory measures use the correct snapshot date.
