```sql
-- 1
SELECT * FROM customers LIMIT 10;
SELECT * FROM books LIMIT 10;
SELECT * FROM orders LIMIT 10;

-- 2
SELECT *
FROM pg_indexes
WHERE tablename IN ('customers', 'orders', 'books');

CREATE UNIQUE INDEX books_pkey ON cc_user.books USING btree (book_id);
CREATE UNIQUE INDEX orders_pkey ON cc_user.orders USING btree (order_id);
CREATE INDEX books_author_idx ON cc_user.books USING btree (author);
CREATE INDEX books_title_idx ON cc_user.books USING btree (title);

-- Partial Index
-- 3
EXPLAIN ANALYZE
SELECT customer_id, quantity
FROM orders
WHERE quantity > 18;
-- Planning time: 0.024 ms
-- Execution time: 11.416 ms

-- 4
CREATE INDEX orders_quantity_idx ON orders (quantity);

-- 5
EXPLAIN ANALYZE
SELECT customer_id, quantity
FROM orders
WHERE quantity > 18;
-- Planning time: 0.142 ms
-- Execution time: 4.096 ms

-- Primary Key
-- 6
EXPLAIN ANALYZE
SELECT *
FROM customers
WHERE customer_id = 123;
-- Planning time: 0.166 ms
-- Execution time: 11.554 ms

ALTER TABLE customers
ADD PRIMARY KEY (customer_id);

EXPLAIN ANALYZE
SELECT *
FROM customers
WHERE customer_id = 123;
-- Planning time: 0.155 ms
-- Execution time: 0.046 ms

-- 7
CLUSTER customers USING customers_pkey;
SELECT *
FROM customers
LIMIT 10;

-- No secondary lookup
-- 8
EXPLAIN ANALYZE
SELECT customer_id, book_id, quantity
FROM orders
WHERE customer_id = 1234 AND book_id = 5678 AND quantity > 10;
-- Planning time: 0.251 ms
-- Execution time: 11.503 ms

CREATE INDEX orders_customer_id_book_id_idx
ON orders (customer_id, book_id);

-- 9
-- Drop the old index
DROP INDEX IF EXISTS orders_customer_id_book_id_idx;

-- Create the new index with the quantity column
CREATE INDEX orders_customer_id_book_id_quantity_idx
ON orders (customer_id, book_id, quantity);

EXPLAIN ANALYZE
SELECT customer_id, book_id, quantity
FROM orders
WHERE customer_id = 1234 AND book_id = 5678 AND quantity > 10;
-- Planning time: 0.188 ms
-- Execution time: 0.051 ms

-- Combining Indexes
-- 10
CREATE INDEX books_author_title_idx
ON books (author, title);

EXPLAIN ANALYZE
SELECT * FROM books
WHERE author = 'Some Author' AND title = 'Some Title';
-- Planning time: 0.279 ms
-- Execution time: 0.034 ms

-- An Ounce of Prevention is worth a Pound of Cure
-- 11
EXPLAIN ANALYZE
SELECT order_id, customer_id, quantity, price_base, (quantity * price_base) AS total_price
FROM orders
WHERE (quantity * price_base) > 100;
-- Planning time: 0.226 ms
-- Execution time: 58.174 ms

-- 12
CREATE INDEX orders_total_price_idx
ON orders ((quantity * price_base));

-- 13
EXPLAIN ANALYZE
SELECT *
FROM orders
WHERE quantity * price_base > 100;
-- Planning time: 0.198 ms
-- Execution time: 16.137 ms

-- 14
-- Examine Existing Indexes
SELECT *
FROM pg_indexes
WHERE tablename IN ('customers', 'books', 'orders')
ORDER BY tablename, indexname;

-- Removing Redundant Indexes
DROP INDEX IF EXISTS books_author_idx;
-- DROP INDEX IF EXISTS orders_customer_id_quantity;

-- Add New Useful Indexes
-- Customer
CREATE INDEX customers_last_name_first_name_email_address
ON customers (last_name, first_name, email_address);

-- Orders
CREATE INDEX orders_customer_id_book_id_quantity_idx
ON orders (customer_id, book_id, quantity);

-- Books
CREATE INDEX books_author_title_idx
ON books (author, title);

-- Test
EXPLAIN ANALYZE
SELECT * FROM customers WHERE last_name = 'Smith' AND first_name = 'John';

EXPLAIN ANALYZE
SELECT * FROM orders WHERE customer_id = 123 AND quantity > 10;

EXPLAIN ANALYZE
SELECT * FROM orders WHERE customer_id = 123 AND quantity > 10;
```
