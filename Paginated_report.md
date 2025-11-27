# **3510 Work Lot Detail (HU Listing with Sublot Sort)**
## **Project Background**

This requirement came from a **Tableau-to-Power BI migration** project.  
We built the report as a **paginated report** rather than a standard Power BI table because paginated reports can be **printed directly**. In contrast, Power BI tables must be **exported to Excel** for printing, which creates a risk of **data changes** if users modify the file.  
Building the paginated report also ensured **100% accurate data** for the **logistics team**, enabling them to verify **item deliveries** at the **plant** without Excel-related risks.

We built the report on the **semantic model** to keep the logic **centralized**, since the model is shared by other summary reports. However, this introduced a new **challenge**: the semantic model contains **M parameters** in Power Query, which function like **stored procedures**. Because no online solution existed for creating a paginated report in this setup, I had to **solve the problem independently**.

## **Contribution**

I learned how to build a paginated report on top of a **Power BI semantic model** using **M parameters** through close collaboration with **Microsoft Support**. Over two weeks, I opened **three support tickets**, worked with **five engineers**, and independently investigated the underlying concepts. Since no online solution existed, the final approach came from both **support escalation** and **independent problem-solving**, highlighting the importance of **persistence** and **deep technical investigation**.

<img width="1369" height="889" alt="image" src="https://github.com/user-attachments/assets/36e442c9-9836-4a7e-96bf-63633e0953b7" />

# **HUA Yield**
## **Project Background**

In our organization, the standard approach to developing **paginated reports** is to use **expressions**, which function similarly to a **stored procedure**. We also build paginated reports on top of a **semantic model**, which works like a database **view**.

From my previous experience at **Mingyuan**, where we developed **SSRS reports** using **stored procedures**, I was already familiar with this workflow and could adapt quickly.

<img width="1720" height="747" alt="image" src="https://github.com/user-attachments/assets/658620b4-91a1-460c-8bf4-28399bcb31d3" />

<img width="1090" height="518" alt="image" src="https://github.com/user-attachments/assets/19bd9b74-57cb-4665-a050-3a8383215735" />


