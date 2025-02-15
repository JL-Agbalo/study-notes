# Indexes in Ruby on Rails

## Introduction

Indexes are database objects that improve the speed of data retrieval operations on a table at the cost of additional storage and maintenance overhead. In Ruby on Rails, indexes can be added to database tables using migrations.

## Creating Indexes

### Adding a Single Column Index

To add an index to a single column, you can use the `add_index` method in a migration:

```ruby
class AddIndexToUsersEmail < ActiveRecord::Migration[6.1]
    def change
        add_index :users, :email
    end
end
```

### Adding a Multi-Column Index

To add an index to multiple columns, you can pass an array of column names to the `add_index` method:

```ruby
class AddIndexToUsersFirstAndLastName < ActiveRecord::Migration[6.1]
    def change
        add_index :users, [:first_name, :last_name]
    end
end
```

### Adding a Unique Index

To ensure that all values in a column are unique, you can add a unique index:

```ruby
class AddUniqueIndexToUsersUsername < ActiveRecord::Migration[6.1]
    def change
        add_index :users, :username, unique: true
    end
end
```

## Discussion

Indexes are crucial for optimizing database performance, especially for large datasets. They allow the database to find and retrieve specific rows much faster than scanning the entire table. However, indexes come with trade-offs:

- **Storage Overhead**: Indexes consume additional disk space.
- **Maintenance Overhead**: Indexes need to be updated whenever the data in the indexed columns is modified, which can slow down write operations.

When designing indexes, it's important to consider the queries your application will run most frequently and create indexes that support those queries. Over-indexing can lead to unnecessary overhead, while under-indexing can result in slow query performance.

## Conclusion

Indexes are a powerful tool for improving database performance in Ruby on Rails applications. By carefully designing and implementing indexes, you can ensure that your application runs efficiently even as your data grows.

TODO: Study

- https://www.youtube.com/watch?v=F5AOseNUAk0

### Clustered Index

A clustered index determines the physical order of data in a table. There can be only one clustered index per table because the data rows themselves can be sorted in only one order. In most databases, the primary key is often used as the clustered index.

#### Example

To create a clustered index in a Rails migration, you can use the `execute` method to run raw SQL:

```ruby
class AddClusteredIndexToUsers < ActiveRecord::Migration[6.1]
    def change
        execute <<-SQL
            CREATE CLUSTERED INDEX index_users_on_id ON users(id)
        SQL
    end
end
```

In this example, a clustered index is created on the `id` column of the `users` table. This ensures that the data in the `users` table is physically ordered by the `id` column, which can improve the performance of queries that search by `id`.

### Considerations

- **Single Clustered Index**: Each table can have only one clustered index.
- **Performance**: Clustered indexes can significantly improve the performance of read operations but may slow down write operations due to the need to maintain the physical order of rows.
- **Primary Key**: By default, the primary key of a table is often used as the clustered index.

Clustered indexes are particularly useful for range queries, where you need to retrieve a range of rows based on a specific column value.
