# Database Normalization

## Introduction

Database normalization is a process used to organize a database into tables and columns. The main goal is to reduce data redundancy and improve data integrity.

## Normal Forms

There are several normal forms, each with specific rules:

### First Normal Form (1NF)

- Ensure each table has a primary key.
- Eliminate repeating groups in individual tables.
- Create separate tables for each group of related data.

### Second Normal Form (2NF)

- Meet all requirements of the first normal form.
- Remove subsets of data that apply to multiple rows of a table and place them in separate tables.
- Create relationships between these new tables and their predecessors using foreign keys.

### Third Normal Form (3NF)

- Meet all requirements of the second normal form.
- Remove columns that are not dependent upon the primary key.

### Boyce-Codd Normal Form (BCNF)

- Meet all requirements of the third normal form.
- Every determinant must be a candidate key.

## Benefits of Normalization

- Reduces data redundancy.
- Improves data integrity.
- Simplifies the database structure.
- Makes maintenance easier.

## Example

Consider a table storing student information and their courses:

### Unnormalized Table

| StudentID | StudentName | Course1 | Course2 |
| --------- | ----------- | ------- | ------- |
| 1         | John Doe    | Math    | Science |
| 2         | Jane Smith  | Math    | English |

### First Normal Form (1NF)

| StudentID | StudentName | Course  |
| --------- | ----------- | ------- |
| 1         | John Doe    | Math    |
| 1         | John Doe    | Science |
| 2         | Jane Smith  | Math    |
| 2         | Jane Smith  | English |

### Second Normal Form (2NF)

| StudentID | StudentName |
| --------- | ----------- |
| 1         | John Doe    |
| 2         | Jane Smith  |

| CourseID | StudentID | Course  |
| -------- | --------- | ------- |
| 1        | 1         | Math    |
| 2        | 1         | Science |
| 3        | 2         | Math    |
| 4        | 2         | English |

### Third Normal Form (3NF)

Already in 3NF as there are no transitive dependencies.

## Conclusion

Normalization is a crucial process in designing a database that is efficient, reliable, and easy to maintain. By following the rules of normalization, you can ensure that your database is well-structured and free of unnecessary redundancy.
