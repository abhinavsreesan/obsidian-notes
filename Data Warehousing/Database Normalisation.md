
Database Normalization is a technique of organizing the data in the database. Normalization is a systematic approach of decomposing tables to eliminate data redundancy(repetition) and undesirable characteristics like Insertion, Update and Deletion Anomalies. 

## **First Normal Form (1NF)**

#### **Rule 1: Single Valued Attributes**

Each column of your table should be single valued which means they should not contain multiple values.

#### **Rule 2: Attribute Domain should not change**

This is more of a "Common Sense" rule. In each column the values stored must be of the same kind or type.

**For example:** If you have a column `dob` to save date of births of a set of people, then you cannot or you must not save 'names' of some of them in that column along with 'date of birth' of others in that column. It should hold only 'date of birth' for all the records/rows.

#### **Rule 3: Unique name for Attributes/Columns**

This rule expects that each column in a table should have a unique name.

![Before 1NF](_assets/f11.png)
														Before 1NF

![1NF Form by splitting the subjects to new rows](_assets/f12.png)
							1NF Form by splitting the subjects to new rows

## Second Normal Form (2NF)

#### **Rule 1:** The table should be in the First Normal Form (1NF).

#### **Rule 2:** There should be no Partial Dependency.

ref:[Second Normal Form (2NF) of Database Normalization | Studytonight](https://www.studytonight.com/dbms/second-normal-form.php)

## Third Normal Form (3NF)

#### **Rule 1:** The table should be in the Second Normal Form (2NF).

#### **Rule 2: It should not have Transitive Dependency.**

ref:[Third Normal Form (3NF)](https://www.studytonight.com/dbms/third-normal-form.php)

## Boyce and Codd Normal Form (BCNF)

#### **Rule 1:** The table should be in the Third Normal Form (3NF).

#### **Rule 2: for each functional dependency ( X → Y ), X should be a super Key**.

ref:[Boyce-Codd Normal Form (BCNF)](https://www.studytonight.com/dbms/boyce-codd-normal-form.php)

## Fourth Normal Form (4NF)

### **Rule 1:** The table should be in the Boyce and Codd Form (BCNF).

### **Rule 1: It doesn't have Multi-Valued Dependency**.

ref:[Fourth Normal Form](https://www.studytonight.com/dbms/fourth-normal-form.php)