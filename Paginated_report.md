# **3510 Work Lot Detail (HU Listing with Sublot Sort)**

## **Background**
This requirement originated from a **Tableau-to-Power BI migration** initiative where the logistics team needed a report that could be **printed reliably** without the risk of data being altered in exported files.  
To meet this need, we implemented the solution as a **paginated report**, which supports **direct printing**, avoiding the common Excel-based workflow that can introduce **data integrity issues**.

The report had to be built on a shared **semantic model** to keep all business logic **centralized** across multiple summary reports. However, the model included **M parameters** in Power Query—functioning like **stored procedures**—and there was **no existing guidance** on how to integrate paginated reports with this architecture.  
I ultimately **designed and solved the technical approach independently**, enabling the report to run correctly without breaking model dependencies.

## **Impact**
- Ensured **100% accurate data** for the **logistics team**, eliminating risks caused by Excel modifications.  
- Enabled reliable **item-delivery verification** at the **plant**, improving operational accuracy.  
- Maintained a **centralized semantic model**, preserving consistent business logic across related reports.  
- Delivered a **scalable, supportable solution** in a setup where no online documentation existed.  
- Reduced manual work and prevented recurring **data-quality issues**, strengthening governance during the migration.

## **Lesson learned**

I learned how to build a paginated report on top of a **Power BI semantic model** using **M parameters** through close collaboration with **Microsoft Support**. Over two weeks, I opened **three support tickets**, worked with **five engineers**, and independently investigated the underlying concepts. Since no online solution existed, the final approach came from both **support escalation** and **independent problem-solving**, highlighting the importance of **persistence** and **deep technical investigation**.

<img width="1369" height="889" alt="image" src="https://github.com/user-attachments/assets/36e442c9-9836-4a7e-96bf-63633e0953b7" />

# **HUA Yield**
## **Project Background**

In our organization, the standard approach to developing **paginated reports** is to use **expressions**, which function similarly to a **stored procedure**. We also build paginated reports on top of a **semantic model**, which works like a database **view**.

From my experience at **Mingyuan**, where we developed **SSRS reports** using **stored procedures**, I was already familiar with this workflow and could adapt quickly.

<img width="1720" height="747" alt="image" src="https://github.com/user-attachments/assets/658620b4-91a1-460c-8bf4-28399bcb31d3" />

<img width="1090" height="518" alt="image" src="https://github.com/user-attachments/assets/19bd9b74-57cb-4665-a050-3a8383215735" />


