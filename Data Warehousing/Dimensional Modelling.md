
Dimension modelling describes the following:

1.  **Subject areas** that are involved in building a warehouse.
2.  The **level of detail(GRAIN)** of data which is termed granularity.
3.  The **time span of database**. This is calculated by determining how much of archived data needs to be stored in a warehouse [1].

Data warehouse models can be built using three different schemas:

-   **Star Schema**: Here, the fact table, which consists of measure, and facts, is arranged **surrounded by dimensions** which resemble a star.
-   **Snowflake Schem**a: This schema is very similar to star schema except that the **dimensions are normalized**.
-   **Fact constellation Schema**: This schema is not used as it contains multiple fact and dimension tables that are shared amongst each other.

Fact tables can be classified based on the level of data that is stored:

**Detailed fact table**: This store detail information about the facts.

**Summarized fact table**: This are also called as aggregated fact table as they contain aggregated data.