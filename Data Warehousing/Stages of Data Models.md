There are three main stages of Data Models:

###  **Conceptual Data Model**

A conceptual data model identifies the highest-level relationships between the different entities. Features of conceptual data model include:

-   Includes the important entities and the relationships among them.
-   No attribute is specified.
-   No primary key is specified.

The figure below is an example of a conceptual data model.

### Conceptual Data Model
A conceptual data model identifies the highest-level relationships between the different entities. Features of conceptual data model include:

-   Includes the important entities and the relationships among them.
-   No attribute is specified.
-   No primary key is specified.

![Conceptual Data Model](https://www.1keydata.com/datawarehousing/conceptual-data-model.jpg)

### **Logical Data Model**
A logical data model describes the data in as much detail as possible, without regard to how they will be physical implemented in the database. Features of a logical data model include:

-   Includes all entities and relationships among them.
-   All attributes for each entity are specified.
-   The primary key for each entity is specified.
-   Foreign keys (keys identifying the relationship between different entities) are specified.
-   Normalization occurs at this level.

The steps for designing the logical data model are as follows:

1.  Specify primary keys for all entities.
2.  Find the relationships between different entities.
3.  Find all attributes for each entity.
4.  Resolve many-to-many relationships.
5.  Normalization.

The figure below is an example of a logical data model.

### Logical Data Model

![Logical Data Model](https://www.1keydata.com/datawarehousing/logical-data-model.jpg)

### Physical Data Model

Physical data model represents how the model will be built in the database. A physical database model shows all table structures, including column name, column data type, column constraints, primary key, foreign key, and relationships between tables. Features of a physical data model include:

-   Specification all tables and columns.
-   Foreign keys are used to identify relationships between tables.
-   Denormalization may occur based on user requirements.
-   Physical considerations may cause the physical data model to be quite different from the logical data model.
-   Physical data model will be different for different RDBMS. For example, data type for a column may be different between MySQL and SQL Server.

The steps for physical data model design are as follows:

1.  Convert entities into tables.
2.  Convert relationships into foreign keys.
3.  Convert attributes into columns.
4.  Modify the physical data model based on physical constraints / requirements.

The figure below is an example of a physical data model.

### Physical Data Model

![Physical Data Model](https://www.1keydata.com/datawarehousing/physical-data-model.jpg)

