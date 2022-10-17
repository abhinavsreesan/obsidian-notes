
Ref:

[Data Analyst's Primer to Slowly Changing Dimensions](https://towardsdatascience.com/data-analysts-primer-to-slowly-changing-dimensions-d087c8327e08)

**SCD Type 0**

The first type is referred to as Type 0. This refers to attributes that **never change** and will not be updated in the data warehouse.

### **SCD Type 1**

A Slowly Changing Dimension Type 1 refers to an instance where the **latest snapshot** of a record is maintained in the data warehouse, without any historical records.

### **SCD Type 2**

With SCD Type 2, every time there is a change in the source system, **a new row will be added** to the data warehouse table. In the resulting table, there will be more records, but the prior history is retained and query able.

### **SCD Type 3**

In Slowly Changing Dimensions is Type 3 Instead of adding new rows to the table to reflect each record change, an **additional column is added**.


### **SCD Type 4**

Here, the concept of a **history table** is introduced. Historical data will be maintained as in SCD Type 2 but the distinction here is that the history will be maintained on a **separate table within the data warehouse. The current record will be included in the primary table.**
