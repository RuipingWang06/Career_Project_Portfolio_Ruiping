# **Business Impact**
This project gave Arista clear visibility into how their **materials** were used and where **defects** occurred, enabling them to analyze failures and improve their **supply strategy**.

# **Contribution**
The main **challenge** in this project was analyzing the **requirements** and clarifying the actual **data logic**. Initially, I was given several tables and asked to create the **SQL scripts** myself, but after examining the tables and trying to join them, I realized they did not contain the necessary **low-granularity** data to meet the requirements.

I scheduled a meeting with the team to **clarify the data sources** based on the **system screens** and asked the **BA** to provide the **SQL** triggered when a **WIP SN** is selected. After analyzing that script, I reconstructed the correct **business logic**, and we essentially **rebuilt the BRD**. This alignment ensured that all parties had a **clear understanding** and agreed on the final approach.

a) Acted as both a **Power BI developer** and **data engineer**, collaborating with site BAs, outsourced developers, the QA manager, the project manager, and the global SQL Server admin.  
b) Reviewed the **BRD** and identified conflicts between business requirements and available **data sources**.  
c) Clarified the correct **business logic** and redesigned the end-to-end **data flow**.  
d) Developed **stored procedures** to extract, transform, and load **daily data** into clean result tables.  
e) Built an internal **Power BI dashboard** for stakeholders to monitor performance.  
f) Created an external **paginated report** for Arista to support **traceability**.

# **Lesson Learned**
I learned the importance of validating **requirements** early and adjusting the reporting approach based on **data volume** using **daily summary tables** instead of aggregating directly from detailed data.  
I also realized that in a large organization, identifying the right people with the necessary **server permissions** is essential.  
Clear **communication** and early **alignment** help prevent rework and ensure a reliable end-to-end solution.

# **Pagined Report & Power BI report**
<img width="1845" height="1230" alt="image" src="https://github.com/user-attachments/assets/5e9bad8f-cb9e-415e-8813-360920d22bd6" />
<img width="704" height="1029" alt="image" src="https://github.com/user-attachments/assets/215ab968-9eac-4516-b6ca-dcd683862c46" />

# **Detail link**
[https://github.com/RuipingWang06/Legacy_MES_Arista_DPPM/blob/main/README.md](https://github.com/RuipingWang06/Legacy_MES_Arista_DPPM/tree/main)
