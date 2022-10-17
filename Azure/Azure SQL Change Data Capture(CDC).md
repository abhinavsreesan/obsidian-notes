## What is Change Data Capture (CDC)?

Change Data Capture (CDC) **records** insert, delete and update activity on a database table using SQL Server Agent. It creates a mirror table from the source table with additional columns to record the changes performed on the database.

-   It writes one record into the mirror table for each INSERT and DELETE statement
-   It writes two records into the mirror table for each UPDATE statement. These two records contain data before and after the change.

The additional columns include:

-   **__\$start_lsn** and **__\$end_lsn** that show the commit log sequence number (LSN) assigned by the SQL Server Engine to the recorded change
-   **__\$seqval** that shows the order of that change related to other changes in the same transaction, **__\$operation** that shows the operation type of the change, where 1 = delete, 2 = insert, 3 = update (before change), and 4 = update (after change)
-   **__\$update_mask** that is a bit mask defined for each captured column, identifying the updating columns

## Steps to enable CDC:

1. Enable CDC on database level:
```SQL 

EXEC sys.sp_cdc_enable_db
GO
```
2. Enable CDC on Table level:
```SQL
EXEC sys.sp_cdc_enable_table  
@source_schema = N'Schema_Name',  
@source_name   = N'TableName',  
@role_name     = NULL,  
@filegroup_name = NULL,  
@supports_net_changes = 0

GO
```

``` 
Note:
Once CDC is enabled on the table, a number of system tables will be created under the CDC schema of the database to store the CDC related information. These tables include the following

-   **Schema_Name.captured_columns** table that contains the list of captured column
-   **Schema_Name.change_tables** table that contains the list of tables that are enabled for capture
-   **Schema_Name.ddl_history** table that records the history of all the DDL changes since capture data enabled
-   **Schema_Name.index_columns** table that contains all the indexes that are associated with change table
-   **Schema_Name.lsn_time_mapping** table that is used to map the LSN number with the time and finally one change table for each CDC enabled table that is used to capture the 
```

3. To see the CDC Data for a table you can query the table 'Schema_Name.Table_Name_CT'

## Using CDC to get incremental Data

1. First you can get the count of records modified using the below query on a CDC enable Database:
```SQL
DECLARE @from_lsn binary(10), @to_lsn binary(10); 
SET @from_lsn =sys.fn_cdc_get_min_lsn('dbo_customers'); 
SET @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', GETDATE()); SELECT count(1) changecount FROM cdc.fn_cdc_get_net_changes_dbo_customers(@from_lsn, @to_lsn, 'all')
```
2. If the change count is not zero then use the below query to get changed rows:
```SQL
DECLARE @from_lsn binary(10), @to_lsn binary(10); 
SET @from_lsn =sys.fn_cdc_get_min_lsn('dbo_customers'); 
SET @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', GETDATE());
SELECT * FROM cdc.fn_cdc_get_net_changes_dbo_customers(@from_lsn, @to_lsn, 'all')
```

- The above logic can be incorporated into Data Factory to get incremental data from a CDC enabled SQL DB table ref [Incremental Data in Data Factory using CDC](https://learn.microsoft.com/en-us/azure/data-factory/tutorial-incremental-copy-change-data-capture-feature-portal)
