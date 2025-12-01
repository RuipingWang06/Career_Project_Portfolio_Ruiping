# **Buyer Execution Metric**
## **Power BI with Mock-up data**
<img width="1326" height="1071" alt="Cancel-showcase" src="https://github.com/user-attachments/assets/a714248e-692c-4585-b2bc-299f4d7d0f4c" />
<img width="1326" height="1071" alt="PushOut-showcase" src="https://github.com/user-attachments/assets/01b1f3eb-a44e-4c5c-bc67-0e284a5e65ed" />
<img width="1326" height="1071" alt="E O-showcase" src="https://github.com/user-attachments/assets/b8a07f57-3f0a-4355-99f1-2c43f765e4ef" />

## **Project Background**
Across 100+ Jabil plants, the lack of a **unified approach** to identify **urgent, unexecuted POs** caused **delivery delays**, **unnecessary purchases**, and recurring **multi-million-dollar losses**.

To address this, we built a **global PO lifecycle model** that integrates **PRs**, **Push-outs**, **Pull-ins**, **Cancellations**, **E&O**, and **Past-Due POs**. We also introduced a **bucketization logic** based on **MRP Delivery Date** and **lead time** to identify urgency, and defined clear **PO status stages** to provide **end-to-end visibility** across the entire process.

This solution **improved early-risk detection by 30–40%**, **reduced delays and excess spending**, **standardized workflows globally**, and strengthened **buyer accountability** through a Power App for logging un-execution reasons.

## **Tasks**
I served as the **Power BI developer** for this report, responsible for **UI/UX and layout design**, **DAX**, **data modeling**, and **Power Query** development.  

I also led **report validation**, resolved key **technical challenges**, and built a **Power App** that allows users to log the **reasons for non-execution**.

## **Challenge**
One key challenge was implementing a **clickable KPI card**, which I solved by researching and applying new Power BI features. This made the report much more **user-friendly**, allowing users to filter with a **single click** instead of relying on right-pane filters. I also created the necessary **DAX measures** to display the **selected KPI**, making it easier for users to understand what they are viewing.

## **Lesson Learned**
This project taught me the importance of combining **strong governance**, **user-centric design**, and **cross-system integration**. I learned the value of building a **standardized Power BI workflow** using **embedded data sources**, **data-limit parameters**, and **workspace pipelines** to accelerate development, improve **version control**, and avoid errors across **DEV**, **STG**, and **PRD**.

I also learned the importance of viewing the report from the **user’s perspective** and anticipating what information will help them understand it better. Beyond what users explicitly request, focusing on **usability details**,such as **data periods**, **refresh dates**, **row counts**, **clickable KPI cards**, and **built-in user guides**,can greatly improve clarity and increase **user adoption**.

Finally, integrating **Power Apps** to capture **un-execution reasons** and displaying them across report pages made the **PO execution lifecycle** far more **transparent** and **efficient**.

## **Room for Improvement**
The report includes **six 13-week summary tables** and **six current-week detail tables**, along with several **bridge tables** to connect them. Because this creates a **complex data model**, it is more efficient to use the **TREATAS** **DAX** function to link the tables rather than building complicated **model relationships**.

## **PO Status / KPI Definition**
### **PO Status**
- **Purchase Request (PR)** is the first step before creating a Purchase Order — it shows what materials or services are being requested but not yet ordered.
- **Past Due** means the PO should have been delivered already, but it’s still not received or closed.
- **Pushout PO** are orders that have been delayed to a later delivery date, usually to balance inventory or adjust to lower demand.
- **Cancel POs** are orders that are no longer needed and have been officially canceled before delivery.
- **Pull-in PO** are orders where buyers ask suppliers to deliver earlier than the original schedule.
- **E&O Reason Code** shows why certain materials became excess or obsolete, helping to identify and prevent waste.
  
### **Cancel Execution KPI**

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

## **Power Query**
<img width="885" height="372" alt="image" src="https://github.com/user-attachments/assets/273f4516-6b51-4066-9d33-ec8493b52fd8" />
<img width="1337" height="721" alt="image" src="https://github.com/user-attachments/assets/264e2a67-a3a4-4c23-8b85-ac7389cfe7de" />
<img width="1046" height="696" alt="image" src="https://github.com/user-attachments/assets/caa23336-1adf-4f49-977e-a5829b6f5d91" />











