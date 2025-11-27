# **Buyer Execution Metric**
## **Power BI with Mock-up data**
<img width="1326" height="1071" alt="Cancel-showcase" src="https://github.com/user-attachments/assets/a714248e-692c-4585-b2bc-299f4d7d0f4c" />
<img width="1326" height="1071" alt="PushOut-showcase" src="https://github.com/user-attachments/assets/01b1f3eb-a44e-4c5c-bc67-0e284a5e65ed" />
<img width="1326" height="1071" alt="E O-showcase" src="https://github.com/user-attachments/assets/b8a07f57-3f0a-4355-99f1-2c43f765e4ef" />

## **Business Impact**

Across 100+ Jabil plants, the lack of a **unified approach** to identify **urgent, unexecuted POs** caused **delivery delays**, **unnecessary purchases**, and recurring **multi-million-dollar losses**.

To address this, we built a **global PO lifecycle model** that integrates **PRs**, **Push-outs**, **Pull-ins**, **Cancellations**, **E&O classifications**, and **Past-Due POs**, providing **end-to-end visibility** across the entire process.

This solution **improved early-risk detection by 30–40%**, **reduced delays and excess spending**, **standardized workflows globally**, and strengthened **buyer accountability** through a Power App for logging un-execution reasons.

## **Contribution**
I served as the **Power BI developer** for this report. One key challenge was implementing a **clickable KPI card**, which I solved by researching and applying new Power BI features. This made the report much more **user-friendly**, allowing users to filter with a **single click** instead of relying on right-pane filters. I also created the necessary **DAX measures** to display the **selected KPI**, making it easier for users to understand what they are viewing.

## **Lesson Learned**

This project taught me the importance of combining **strong governance**, **user-centric design**, and **cross-system integration**. I learned the value of building a **standardized Power BI workflow** using **embedded data sources**, **data-limit parameters**, and **workspace pipelines** to accelerate development, improve **version control**, and avoid errors across **DEV**, **STG**, and **PRD**.

I also learned the importance of viewing the report from the **user’s perspective** and anticipating what information will help them understand it better. Beyond what users explicitly request, focusing on **usability details**,such as **data periods**, **refresh dates**, **row counts**, **clickable KPI cards**, and **built-in user guides**,can greatly improve clarity and increase **user adoption**.

Finally, integrating **Power Apps** to capture **un-execution reasons** and displaying them across report pages made the **PO execution lifecycle** far more **transparent** and **efficient**.

## **Room for Improvement**
The report includes **six 13-week summary tables** and **six current-week detail tables**, along with several **bridge tables** to connect them. Because this creates a **complex data model**, it is more efficient to use the **TREATAS** **DAX** function to link the tables rather than building complicated **model relationships**.
## **Power Query**
<img width="885" height="372" alt="image" src="https://github.com/user-attachments/assets/273f4516-6b51-4066-9d33-ec8493b52fd8" />
<img width="1337" height="721" alt="image" src="https://github.com/user-attachments/assets/264e2a67-a3a4-4c23-8b85-ac7389cfe7de" />
<img width="1046" height="696" alt="image" src="https://github.com/user-attachments/assets/caa23336-1adf-4f49-977e-a5829b6f5d91" />











