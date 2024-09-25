# Relational Database

A relational database organizes data into tables, where each table is a collection of related data entries. This structure allows for easy management, retrieval, and manipulation of data.

A table consists of multiple **rows** and **columns**

- Rows (Records): Each row in a table represents a single, unique record. It holds all the information for a particular entry in the table.

- Columns (Fields): Each column represents a specific attribute of the entity. Columns have a defined data type and contain atomic values.

**Atomic fields**: An atomic field refers to a field that holds the smallest possible data unit, ensuring that the data in each column is indivisible. Like a PhoneNumber field should not hold multiple phone numbers; instead, it should store only one phone number per record.

For example, we can have a a teachers table, each associated with a department and their own salary

![image](https://github.com/user-attachments/assets/4eccee84-ed75-40d6-a21c-bc25f7e6a452)

this is called a **schema**

We can define relationships between tables, which is why it's called a **relational database**

- One-to-One (1:1):

A row in Table A is related to one and only one row in Table B, and vice versa.
Example: Each person has one passport, and each passport is assigned to one person.

- One-to-Many (1:M):
  
A row in Table A can be related to multiple rows in Table B, but a row in Table B can relate to only one row in Table A.
Example: One customer can have multiple orders, but each order belongs to only one customer.

- Many-to-Many (M:M):

Rows in Table A can relate to multiple rows in Table B, and rows in Table B can relate to multiple rows in Table A.
Example: Students can enroll in multiple courses, and each course can have multiple students. This requires an intermediary table (junction table).

## Keys 

Keys are special fields (or combinations of fields) used to identify rows in a table and establish relationships between tables.

- SuperKey:

A superkey is a set of one or more columns that can uniquely identify a row in a table. It may contain unnecessary columns, i.e., not every column in a superkey is necessary for unique identification.

- Primary Key:

The primary key is a candidate key that is chosen to uniquely identify rows in a table. It cannot contain NULL values and must be unique across the table.
Example: CustomerID in a Customer table could be a primary key, ensuring each customer has a unique ID.

- Candidate Key:

A candidate key is a minimal set of columns in a table that uniquely identifies each row in that table. They are fields that can be chosen as a **primary key**, making them a **candidate**

- Foreign Key:

A foreign key is a column (or set of columns) in one table that references the primary key in another table. It is used to establish and enforce a link between the data in the two tables.
Example: CustomerID in an Orders table can be a foreign key referencing the CustomerID in the Customer table.

## Schema diagrams

A database schema, along with primary key and foreign-key constraints, can be depicted by **schema diagrams**

Primary-key attributes are shown underlined. Foreign-key constraints appear as arrows from the foreign-key attributes of the referencing relation to the primary key of the referenced relation

![image](https://github.com/user-attachments/assets/d56a36c3-7ee6-49fb-9161-ac18219cafed)
