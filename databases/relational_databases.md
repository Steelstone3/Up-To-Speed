# Relational Databases

## Introduction

A relational database is a type of database management system (DBMS) that organizes and stores data in a structured manner using tables, columns, and rows. It follows the relational model, which defines relationships between tables using keys, allowing for efficient storage, retrieval, and manipulation of data.

## Concepts

Here are some key components and concepts of relational databases:

### Tables

In a relational database, data is organized into tables, which are also referred to as relations. A table consists of columns (attributes) and rows (records or tuples). Each column represents a specific type of data, such as names, dates, or numbers, while each row represents a unique record or instance of the data.

### Keys

Keys are used to establish relationships between tables. The primary key uniquely identifies each record in a table and ensures its uniqueness and integrity. Foreign keys establish relationships between tables by referencing the primary key of another table. This allows data to be connected and retrieved across related tables.

### Relationships

Relational databases allow for various types of relationships between tables. The most common relationships are one-to-one, one-to-many, and many-to-many. These relationships define how data is related or connected between different tables, enabling efficient retrieval and manipulation of related information.

### Structured Query Language (SQL)

SQL is a standard language used to interact with relational databases. It provides a set of commands and syntax for creating, modifying, and querying data in tables. SQL allows users to perform operations like retrieving specific records, inserting new data, updating existing data, and deleting records.

### Normalisation

Normalization is the process of organizing data in a database to eliminate redundancy and ensure data integrity. It involves breaking down larger tables into smaller, more manageable tables and applying rules to reduce data duplication and anomalies. Normalization helps maintain data consistency and improves database performance.

### ACID Properties

Relational databases adhere to the ACID (Atomicity, Consistency, Isolation, Durability) properties to ensure data integrity and reliability. Atomicity guarantees that database transactions are treated as a single, indivisible unit of work. Consistency ensures that only valid data is stored in the database. Isolation prevents interference between concurrent transactions. Durability guarantees that once a transaction is committed, its changes are permanently saved, even in the event of system failures.

### Indexing

Indexes are used to improve the performance of database queries by creating data structures that allow for faster data retrieval. Indexes are created on specific columns of a table, enabling quick lookups and sorting based on those columns. They help optimize query execution and enhance overall database performance.

## Normalisation Levels

Normalization is the process of organizing data in a database to eliminate redundancy, improve data integrity, and optimize data structure. It involves breaking down larger tables into smaller, more manageable tables and applying specific rules to ensure data consistency. There are different levels or forms of normalization, often referred to as normal forms, each building upon the previous one. Here are the commonly recognized normal forms:

### First Normal Form (1NF)

The first normal form requires that each column in a table contains only atomic (indivisible) values. It eliminates repeating groups or multiple values within a single cell. Each attribute or column should contain only a single value, and each table should have a primary key that uniquely identifies each record.

### Second Normal Form (2NF)

The second normal form builds upon the first normal form. It requires that each non-key attribute in a table is functionally dependent on the entire primary key. This means that attributes should depend on the whole key, not just part of it. If an attribute depends on only a subset of the primary key, it should be moved to a separate table.

### Third Normal Form (3NF)

The third normal form goes further to eliminate transitive dependencies between non-key attributes. It requires that each non-key attribute in a table is dependent only on the primary key and not on other non-key attributes. If there is a transitive dependency, where one non-key attribute depends on another non-key attribute, the dependent attribute should be moved to a separate table.

## Conclusion

Relational databases have been widely used for decades and offer a robust and efficient way to store, organize, and manage structured data. They are well-suited for a wide range of applications, from small-scale projects to enterprise-level systems, providing data consistency, reliability, and the ability to handle complex relationships between data entities.
