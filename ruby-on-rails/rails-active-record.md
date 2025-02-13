# Topics to Study in Active Record

### Migrations

Migrations are a way to alter the database schema over time in a consistent and easy way. They use Ruby to define changes to the database, making it easy to manage and version control.

To create a new migration, you can use the following command:

```bash
rails generate migration AddPriceToProducts name:string price:decimal
```

This will generate a migration file that you can edit to define the changes you want to make to the database schema.

```ruby
class CreateProducts < ActiveRecord::Migration[6.1]
    def change
        create_table :products do |t|
            t.string :name
            t.decimal :price

            t.timestamps
        end
    end
end
```

### Models

Models in Rails are used to interact with the database. Each model typically corresponds to a table in the database.
To create a new model, you can use the following command:

```bash
rails generate model Product name:string price:decimal
```

This will generate a model file, a migration file, and test files. The model file is where you can define the attributes and methods for the `Product` model.

Example:

```ruby
class Product < ApplicationRecord
end
```

The migration file will look something like this:

```ruby
class CreateProducts < ActiveRecord::Migration[6.1]
    def change
        create_table :products do |t|
            t.string :name
            t.decimal :price

            t.timestamps
        end
    end
end
```

### Associations

Associations set up relationships between different models. Rails supports several types of associations, including `belongs_to`, `has_many`, `has_one`, and `has_and_belongs_to_many`.

Example:

```ruby
class Product < ApplicationRecord
    has_many :inventories
end

class Inventory < ApplicationRecord
    belongs_to :product
end
```

In this example, a `Product` has many `Inventories`, and each `Inventory` belongs to a `Product`.

### Validations

Validations are used to ensure that only valid data is saved into your database. Rails provides several built-in validation helpers.

Example:

```ruby
class Product < ApplicationRecord
    validates :name, presence: true
    validates :price, numericality: { greater_than: 0 }
end
```

In this example, the `Product` model has two validations:

- `name` must be present.
- `price` must be a number greater than 0.

### Callbacks

Callbacks are methods that get called at certain moments of an object's lifecycle. They allow you to trigger logic before or after an alteration of an object's state.

Common callbacks include:

- `before_validation`
- `after_validation`
- `before_save`
- `around_save`
- `after_save`
- `before_create`
- `around_create`
- `after_create`
- `before_update`
- `around_update`
- `after_update`
- `before_destroy`
- `around_destroy`
- `after_destroy`
- `after_initialize`
- `after_find`
- `after_touch`

Example:

```ruby
class Product < ApplicationRecord
    before_save :normalize_name

    private

    def normalize_name
        self.name = name.downcase.titleize
    end
end
```

In this example, the `normalize_name` method is called before saving a `Product` to ensure the name is properly formatted.

### Scopes

Scopes in Rails are used to encapsulate commonly used queries, making your code more readable and reusable. They are defined in the model and can be chained with other Active Record methods.

Example:

```ruby
class Product < ApplicationRecord
    scope :available, -> { where(available: true) }
    scope :priced_above, ->(amount) { where("price > ?", amount) }
end
```

In this example, two scopes are defined:

- `available`: Returns products that are available.
- `priced_above(amount)`: Returns products with a price greater than the specified amount.

You can use these scopes in your queries like this:

```ruby
Product.available
Product.priced_above(100)
Product.available.priced_above(100)
```

Scopes help keep your code DRY (Don't Repeat Yourself) and make complex queries easier to manage.

### Query Interface

### Active Record Relations

### Eager Loading

### Polymorphic Associations

### Single Table Inheritance

### Database Transactions

### Custom Validations

### Performance Optimization

### Rails Scaffold Command

The command `rails generate scaffold ModelName field1:type field2:type` creates a model, migration, controller, views, and routes for `ModelName` with fields `field1` and `field2`.

```bash
rails generate scaffold ModelName field1:type field2:type
```
