# Business Insights & Recommendations

## Purpose
This document summarizes findings from the five dashboards and translates them into potential business actions. Recheck all findings against the final refreshed PBIX before publication.

## Inventory Management
### Observed dashboard indicators
- Latest inventory value: approximately ₹471M.
- Available stock: approximately 46K units.
- Low-stock products: 83.
- Out-of-stock products: 0.
- Excess-stock products: 7.

### Interpretation
The latest snapshot indicates that some products are below their reorder thresholds while a smaller group is above target stock.

### Recommendations
1. Review low-stock products and prioritize replenishment based on demand and lead time.
2. Review excess-stock products before placing additional purchase orders.
3. Monitor inventory value and available stock by warehouse and category.
4. Use consistent snapshot dates when comparing inventory KPIs.

## Procurement Analytics
### Observed dashboard indicators
- Purchase spend: approximately ₹17.67bn.
- Purchase orders: approximately 4.2K.
- Ordered quantity: approximately 2M units.
- Received quantity: approximately 1M units.
- Purchase order fulfillment: approximately 75%.
- On-time receipt: approximately 55%.

### Recommendations
1. Investigate purchase orders with incomplete receipts.
2. Review suppliers and products associated with late receipts.
3. Monitor ordered versus received quantities by supplier and category.
4. Review high-value purchase orders and purchasing trends.

## Supplier Performance
### Observed dashboard indicators
- Total suppliers: 30.
- Active suppliers: 28.
- Average lead time: approximately 9.44 days.
- Defect rate: approximately 2%.
- Rejected quantity: approximately 23K units.

### Recommendations
1. Review suppliers with longer-than-average lead times.
2. Investigate rejected quantities and recurring quality issues.
3. Compare supplier performance using consistent receipt and quality definitions.
4. Work with suppliers to improve delivery reliability and product quality.

## Order Fulfillment & Delivery
Analyze total and delivered orders, order status distribution, cancellation rate, on-time delivery, average delivery days, and carrier/region performance.

### Data quality caution
Shipment data contains records where actual delivery dates may precede dispatch dates. These can produce negative delivery durations. Investigate the underlying records and document the treatment before publishing average delivery days.

Validate on-time delivery if it displays 100% across all months. Check the eligible shipment population, date relationships, and filter context.

### Recommendations
1. Investigate shipment records with inconsistent dispatch and delivery dates.
2. Monitor late shipments by carrier and region.
3. Analyze cancellation reasons and order status patterns.
4. Reconcile delivered-order counts against shipment records.

## Executive Recommendations
- Monitor inventory, procurement, supplier, and delivery KPIs regularly.
- Prioritize low-stock products and investigate excess stock.
- Improve supplier receipt timeliness and purchase order completion.
- Track rejected quantities and address quality issues.
- Validate operational dates and KPI definitions before decisions are made.

## Limitations
- The dataset is synthetic and does not represent a real company's operations.
- Dashboard figures depend on selected filters and snapshot dates.
- Some shipment date anomalies require investigation.
- KPI definitions and exact DAX formulas should be verified against the final report.

## Conclusion
The project demonstrates an integrated approach to supply chain reporting using Power BI, combining data preparation, relational modeling, DAX measures, interactive visualizations, and business recommendations across five operational areas.
