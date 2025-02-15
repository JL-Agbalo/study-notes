# PostgreSQL Constraints and Information Schema

## Table: `sample_table`

### Columns:

- `id` (Primary Key)
- `name` (Unique)
- `email` (Not Null)

### Constraints:

- Primary Key: `sample_table_pkey` on `id`
- Unique: `sample_table_name_key` on `name`
- Not Null: `sample_table_email_not_null` on `email`

## Information Schema Query

````sql
SELECT
    kcu.table_name,
    kcu.column_name,
    tc.constraint_name,
    tc.constraint_type
FROM
    information_schema.table_constraints AS tc
JOIN
    information_schema.key_column_usage AS kcu
ON
    tc.constraint_name = kcu.constraint_name
    information_schema.key_column_usage AS kcu
ON
    tc.constraint_name = kcu.constraint_name
WHERE
    tc.table_name = 'sample_table'; Types in PostgreSQL

### Numeric Types

- `smallint`, `integer`, `bigint`, `decimal`, `numeric`, `real`, `double precision`, `serial`, `bigserial`

### Character Types

- `varchar(n)`, `char(n)`, `text`

### Date/Time Types

- `timestamp`, `timestamp with time zone`, `date`, `time`, `time with time zone`, `interval`

### Boolean Type

- `boolean`

### JSON Types

- `json`, `jsonb`

### Arrays
### Character Types

- `character varying(n)`, `varchar(n)`: variable-length with limit
- `character(n)`, `char(n)`: fixed-length, blank padded
- `text`: variable unlimited length

### Binary Data Types

- `bytea`: binary data ("byte array")

### Date/Time Types

- `timestamp`: both date and time (without time zone)
- `timestamp with time zone`: both date and time (with time zone)
- `date`: date (no time of day)
- `time`: time of day (no date)
- `time with time zone`: time of day (with time zone)
- `interval`: time interval

### Boolean Type

- `boolean`: state of true or false

### Enumerated Types

- `enum`: static, ordered set of values

### Geometric Types

- `point`: geometric point on a plane
- `line`: infinite line
- `lseg`: line segment
- `box`: rectangular box
- `path`: geometric path
- `polygon`: closed geometric path
- `circle`: circle

### Network Address Types

- `cidr`: IPv4 or IPv6 network
- `inet`: IPv4 or IPv6 host address
- `macaddr`: MAC address

### Bit String Types

- `bit(n)`: fixed-length bit string
- `bit varying(n)`, `varbit(n)`: variable-length bit string

### Text Search Types

- `tsvector`: text search document
- `tsquery`: text search query

### UUID Type

- `uuid`: universally unique identifier

### XML Type

- `xml`: XML data

### JSON Types

- `json`: text representation of JSON data
- `jsonb`: binary representation of JSON data

### Arrays

- Arrays can be of any data type, e.g., `integer[]`, `text[]`

### Composite Types

- Custom types defined by the user

### Range Types

- `int4range`: range of `integer`
- `int8range`: range of `bigint`
- `numrange`: range of `numeric`
- `tsrange`: range of `timestamp without time zone`
- `tstzrange`: range of `timestamp with time zone`
- `daterange`: range of `date`

These data types provide flexibility and functionality to handle various types of data in PostgreSQL.

## Sample Data with Constraints

Here is an example of how to insert data into `sample_table` while respecting the constraints:

```sql
-- Insert valid data
INSERT INTO sample_table (id, name, email) VALUES (1, 'John Doe', 'john.doe@example.com');

-- Attempt to insert a duplicate primary key (will fail)
INSERT INTO sample_table (id, name, email) VALUES (1, 'Jane Smith', 'jane.smith@example.com');

-- Attempt to insert a duplicate unique key (will fail)
INSERT INTO sample_table (id, name, email) VALUES (2, 'John Doe', 'john.different@example.com');

-- Attempt to insert a null value into a not null column (will fail)
INSERT INTO sample_table (id, name, email) VALUES (3, 'Alice Johnson', NULL);
````

In this example:

- The first insert statement will succeed.
- The second insert statement will fail due to a duplicate primary key.
- The third insert statement will fail due to a duplicate unique key.
- The fourth insert statement will fail due to a null value in a not null column.

## Keys in PostgreSQL

### Primary Key

Uniquely identifies each row in a table. No duplicates or nulls allowed.

### Foreign Key

References a primary key in another table, enforcing referential integrity.

### Unique Key

Ensures all values in a column or set of columns are unique. Can contain nulls.

### Composite Key

A primary key made up of multiple columns.

### Candidate Key

A column or set of columns that can be a primary key. Only one is chosen as the primary key.

### Alternate Key

A candidate key not chosen as the primary key.

These keys ensure data integrity and efficient data retrieval in PostgreSQL.

## Indexes in PostgreSQL

Indexes are used to speed up the retrieval of rows by using a pointer. They are essential for improving the performance of database queries.

### Types of Indexes

- **B-tree Index**: The default index type, suitable for most queries.
- **Hash Index**: Used for equality comparisons.
- **GIN (Generalized Inverted Index)**: Used for full-text search.
- **GiST (Generalized Search Tree)**: Used for complex data types like geometric data.
- **SP-GiST (Space-Partitioned Generalized Search Tree)**: Used for partitioned data.
- **BRIN (Block Range INdex)**: Used for large tables with naturally ordered data.

### Creating an Index

To create an index on a table:

```sql
CREATE INDEX index_name ON table_name (column_name);
```

### Dropping an Index

To drop an index:

```sql
DROP INDEX index_name;
```

Indexes can significantly improve query performance but also add overhead to data modification operations. Use them wisely to balance read and write performance.

"""
This function implements a B-tree index, which is a self-balancing tree data structure that maintains sorted data and allows for efficient insertion, deletion, and search operations. B-trees are commonly used in databases and file systems to index large amounts of data.

Key features of B-tree index:

- Balanced tree structure: Ensures that the tree remains balanced, providing O(log n) time complexity for search, insert, and delete operations.
- Sorted order: Maintains data in sorted order, which allows for efficient range queries.
- Node capacity: Each node can contain multiple keys and children, reducing the height of the tree and improving performance.

Parameters:

- `order` (int): The maximum number of children each node can have.

Methods:

- `insert(key)`: Inserts a key into the B-tree.
- `delete(key)`: Deletes a key from the B-tree.
- `search(key)`: Searches for a key in the B-tree and returns the node containing the key, if found.
- `split_child(parent, index, child)`: Splits a full child node into two nodes and adjusts the parent node accordingly.
- `merge_children(parent, index)`: Merges two child nodes and adjusts the parent node accordingly.
  """
  https://www.codecademy.com/resources/docs/general/database/index

## Explain Analyze Example

The `EXPLAIN ANALYZE` command in PostgreSQL is used to show the execution plan of a query along with the actual run time. This helps in understanding how the query is executed and identifying performance bottlenecks.

### Example Query

```sql
EXPLAIN ANALYZE
SELECT * FROM sample_table WHERE name = 'John Doe';
```

### Output

The output of `EXPLAIN ANALYZE` provides detailed information about each step of the query execution, including:

- The type of operation (e.g., Seq Scan, Index Scan)
- The estimated and actual number of rows processed
- The estimated and actual time taken for each step
- The total execution time

Using `EXPLAIN ANALYZE` helps in optimizing queries by providing insights into the query execution process.

### Sample Explain analyze and Index

EXPLAIN ANALYZE SELECT first_name, last_name, email_address
FROM customers
WHERE last_name = 'Smith';
-- Planning time: 0.270 ms
-- Execution time: 1.741 ms

CREATE INDEX customers_last_name_first_name_email_address_idx ON customers (last_name, first_name, email_address);

EXPLAIN ANALYZE SELECT first_name, last_name, email_address
FROM customers
WHERE last_name = 'Smith';
-- Planning time: 0.139 ms
-- Execution time: 0.999 ms

## Explanation of Clustered and Non-Clustered Indexes

### Clustered Index:

A clustered index determines the physical order of data in a table. There can be only one clustered index per table because the data rows themselves can be sorted in only one order. The clustered index is typically created on the primary key column.

### Non-Clustered Index:

A non-clustered index, on the other hand, does not alter the physical order of the data in the table. Instead, it creates a separate object within the table that points back to the original table rows after searching. There can be multiple non-clustered indexes on a table, and they are typically used to improve the performance of frequently used queries.

### Example:

Consider a table `Employees` with columns `EmployeeID`, `FirstName`, and `LastName`.

- A clustered index on `EmployeeID` will sort the data rows by `EmployeeID`.
- A non-clustered index on `LastName` will create a separate structure that allows quick lookups by `LastName` without changing the order of the data rows.
