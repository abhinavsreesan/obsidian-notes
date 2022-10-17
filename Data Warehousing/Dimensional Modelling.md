
Dimension modelling describes the following:

1.  **Subject areas** that are involved in building a warehouse.
2.  The **level of detail(GRAIN)** of data which is termed granularity.
3.  The **time span of database**. This is calculated by determining how much of archived data needs to be stored in a warehouse [1].


``` Text
**Dimension** : A category of information. For example, the time dimension.
**Attribute** : A unique level within a dimension. For example, Month is an attribute in 
the Time Dimension.
**Hierarchy**: The specification of levels that represents relationship between different attributes within a dimension. For example, one possible hierarchy in the Time dimension is Year → Quarter → Month → Day.
```

- **[Fact Table](https://www.1keydata.com/datawarehousing/fact-table-granularity.html)**: A fact table is a table that contains the measures of interest. For example, sales amount would be such a measure. This measure is stored in the fact table with the appropriate granularity. For example, it can be sales amount by store by day. In this case, the fact table would contain three columns: A date column, a store column, and a sales amount column.

- **Lookup Table**: The lookup table provides the detailed information about the attributes. For example, the lookup table for the Quarter attribute would include a list of all of the quarters available in the data warehouse. Each row (each quarter) may have several fields, one for the unique ID that identifies the quarter, and one or more additional fields that specifies how that particular quarter is represented on a report (for example, first quarter of 2001 may be represented as "Q1 2001" or "2001 Q1").

Data warehouse models can be built using three different schemas:

- **Star Schema**: Here, the fact table, which consists of measure, and facts, is arranged surrounded by dimensions which resemble a star.
- **Snowflake Schema**: This schema is very similar to star schema except that the dimensions are normalized.
- **Fact constellation Schema**: This schema is not used as it contains multiple fact and dimension tables that are shared amongst each other.

Fact tables can be classified based on the level of data that is stored:
	- **Detailed fact table**: This store detail information about the facts.
	- **Summarized fact table**: This are also called as aggregated fact table as they contain aggregated data.