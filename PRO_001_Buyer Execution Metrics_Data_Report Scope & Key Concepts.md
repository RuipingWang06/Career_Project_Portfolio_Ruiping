# **Cancel Execution KPI**

**Total Cancel Actions**
- **Definition:**  
The total number of **MRP delivery lines (PO schedule lines)** identified on **Monday’s baseline** that require cancellation.  
These are lines where:  
`MRP Exception Message = 20 (Cancel process)` or `21 (Cancel: demand beyond lead time)`
Excludes deleted PO line items and lines with `Open Quantity = 0`
- **Purpose:**  
Represents the total population of cancel opportunities for the week.

**Executable Demand Beyond LT**
- **Definition:**  
MRP lines where:  
MRP Delivery Date > Current Date + Cancel LT + 8 days
AND Exception Message = 21
- **Purpose:**  
Captures orders where demand exists **beyond the lead time window** — cancellation is technically possible but not urgent.

**Week 1 Priority**
- **Definition:**  
Displayed together on the dashboard card but split in tables and trends.
MRP Delivery Date between (Current Date + Cancel LT)
and (Current Date + Cancel LT + 8 days)
- **Executable Cancel No Demand**  
Exception Message = 20
- **Purpose:**  
Identifies short-term or immediate cancellation actions that should be prioritized by buyers.

**Inside Cancel LT**
- **Definition:**  
MRP Delivery Date < Current Date + Cancel LT
AND Cancel LT < Order LT
- **Purpose:**  
Represents orders **inside the cancellation lead time**, where suppliers may already have started production or shipment.

**NCNR (Non-Cancelable / Non-Returnable)**
- **Definition:**  
MRP Delivery Date < Current Date + Cancel LT
AND Cancel LT ≥ Order LT
- **Purpose:**  
Captures items marked as **non-cancelable and non-returnable** per supplier agreements. Usually excluded from performance metrics.

**Un-Executed**
- **Definition:**  
Cancel actions still pending at the end of the week (**Sunday**), where:  
Exception Message = 20 or 21
AND none of the other result conditions (Received, Partial Received, Cancelled, Cancel Not Allowed, Not Needed) are met
- **Purpose:**  
Indicates cancellation requests that remain **unexecuted** or **pending buyer action**.
