# ActiveRecord Queries

## 1. `find`

The `find` method is used to retrieve a single record by its primary key.

### Example:

```ruby
User.find(1)
```

---

## 2. `find_by`

The `find_by` method is used to find a record by any given attribute.

### Example:

```ruby
User.find_by(email: 'example@example.com')
```

---

## 3. `take`

The `take` method retrieves a single record (not necessarily the first one).

### Example:

```ruby
User.take
```

---

## 4. `order`

The `order` method is used to sort records by one or more attributes.

### Example:

```ruby
User.order(:name)
```

---

## 5. `select`

The `select` method allows you to select specific columns from a table.

### Example:

```ruby
User.select(:name, :email)
```

---

## 6. `limit`

The `limit` method restricts the number of records returned.

### Example:

```ruby
User.limit(5)
```

---

## 7. `count`

The `count` method returns the number of records that match the given condition.

### Example:

```ruby
User.count
```

---

## 8. `joins`

The `joins` method is used to perform an SQL join operation between tables.

### Example:

```ruby
User.joins(:posts)
```

---

## 9. `group`

The `group` method groups records by a specific attribute.

### Example:

```ruby
User.group(:age).count
```

---

## 10. `having`

The `having` method adds a `HAVING` clause for use with `group`.

### Example:

```ruby
User.group(:age).having('count(*) > 1')
```

---

## 11. `distinct`

The `distinct` method ensures that only unique records are returned.

### Example:

```ruby
User.select(:name).distinct
```

---

## 12. `pluck`

The `pluck` method retrieves an array of values for a specific column.

### Example:

```ruby
User.pluck(:name)
```

---

## 13. `where`

The `where` method filters records based on a condition.

### Example:

```ruby
User.where(age: 30)
```

---

## 14. `or`

The `or` method combines `WHERE` conditions with an `OR` operator.

### Example:

```ruby
User.where(age: 30).or(User.where(name: 'John'))
```

---

## 15. `includes`

The `includes` method eager loads associated records to avoid N+1 query problems.

### Example:

```ruby
User.includes(:posts)
```

---

## 16. `preload`

The `preload` method eager loads associations but does not use SQL `JOIN`.

### Example:

```ruby
User.preload(:posts)
```

---

## 17. `references`

The `references` method is used with `includes` to force a SQL `JOIN`.

### Example:

```ruby
User.includes(:posts).references(:posts)
```

---

## 18. `exists?`

The `exists?` method checks if any records exist that match a condition.

### Example:

```ruby
User.exists?(name: 'John')
```

---

## 19. `find_or_create_by`

The `find_or_create_by` method finds a record or creates a new one if it doesn't exist.

### Example:

```ruby
User.find_or_create_by(name: 'John', age: 30)
```

---

## 20. `find_or_initialize_by`

The `find_or_initialize_by` method finds a record or initializes a new one (doesn't save).

### Example:

```ruby
User.find_or_initialize_by(name: 'John')
```

---

## 21. `update_all`

The `update_all` method updates multiple records in one query.

### Example:

```ruby
User.where(age: 30).update_all(age: 31)
```

---

## 22. `destroy_all`

The `destroy_all` method deletes multiple records in one query.

### Example:

```ruby
User.where(age: 30).destroy_all
```

---

## 23. `update`

The `update` method updates a single record's attributes and saves it.

### Example:

```ruby
user = User.find(1)
user.update(name: 'John')
```

---

## 24. `destroy`

The `destroy` method deletes a record from the database.

### Example:

```ruby
user = User.find(1)
user.destroy
```

---

## 25. `new`

The `new` method instantiates a new object but does not save it.

### Example:

```ruby
user = User.new(name: 'John')
```

---

## 26. `create`

The `create` method instantiates a new object and saves it to the database.

### Example:

```ruby
User.create(name: 'John', age: 30)
```

---

## 27. `create!`

The `create!` method instantiates and saves a new object; raises an exception if validation fails.

### Example:

```ruby
User.create!(name: 'John', age: 30)
```

---

## 28. `reload`

The `reload` method reloads the record from the database.

### Example:

```ruby
user.reload
```

---

## 29. `merge`

The `merge` method combines two ActiveRecord relations.

### Example:

```ruby
User.where(active: true).merge(User.where(admin: true))
```

---

## 30. `reverse_order`

The `reverse_order` method reverses the order of a query.

### Example:

```ruby
User.order(:name).reverse_order
```

---

## 31. `scoping`

The `scoping` method defines and applies custom scopes.

### Example:

```ruby
class User < ApplicationRecord
  scope :active, -> { where(active: true) }
end

User.active
```

---

## 32. `save`

The `save` method saves a record to the database (without creating a new one).

### Example:

```ruby
user = User.find(1)
user.name = 'John'
user.save
```
