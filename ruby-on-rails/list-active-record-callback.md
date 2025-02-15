# ActiveRecord Callbacks

## 1. `before_validation`

Triggered **before** validations are run on the model. It’s used for preprocessing data before checking validity.

### Example:

```ruby
class User < ApplicationRecord
before_validation :normalize_name

private
def normalize_name
self.name = name.strip.titleize
end
end
```

---

## 2. `after_validation`

Triggered **after** validations are run on the model. It’s useful for actions that depend on the result of validation.

### Example:

```ruby
class User < ApplicationRecord
after_validation :send_welcome_email

private
def send_welcome_email
UserMailer.welcome(self).deliver_later if self.valid?
end
end
```

---

## 3. `before_save`

Triggered **before** saving a record, whether it's being created or updated. This is useful for modifying attributes before the data is saved to the database.

### Example:

```ruby
class User < ApplicationRecord
before_save :downcase_email

private
def downcase_email
self.email = email.downcase
end
end
```

---

## 4. `after_save`

Triggered **after** saving a record, whether it's being created or updated. This can be used for actions that should occur after the record is saved.

### Example:

```ruby
class User < ApplicationRecord
after_save :log_user_creation

private
def log_user_creation
Rails.logger.info "User #{self.id} was created or updated."
end
end
```

---

## 5. `before_create`

Triggered **before** a new record is created. It's often used to prepare data right before it's persisted.

### Example:

```ruby
class User < ApplicationRecord
before_create :generate_unique_token

private
def generate_unique_token
self.token = SecureRandom.hex(10)
end
end
```

---

## 6. `after_create`

Triggered **after** a new record is created. You can perform actions that should happen once the record is saved for the first time.

### Example:

```ruby
class User < ApplicationRecord
after_create :send_account_activation_email

private
def send_account_activation_email
UserMailer.activation(self).deliver_later
end
end
```

---

## 7. `before_update`

Triggered **before** an existing record is updated. This is helpful for checks or modifications before persisting the changes.

### Example:

```ruby
class User < ApplicationRecord
before_update :check_for_changes

private
def check_for_changes
if self.email_changed?
self.email_verified = false
end
end
end
```

---

## 8. `after_update`

Triggered **after** an existing record is updated. You can use this to perform actions after a record has been updated in the database.

### Example:

```ruby
class User < ApplicationRecord
after_update :send_email_update_notification

private
def send_email_update_notification
UserMailer.email_update(self).deliver_later
end
end
```

---

## 9. `before_destroy`

Triggered **before** a record is destroyed. You can use this callback to prevent a record from being deleted or to perform checks before destruction.

### Example:

```ruby
class User < ApplicationRecord
before_destroy :check_if_admin

private
def check_if_admin
if self.admin?
throw(:abort)
end
end
end
```

---

## 10. `after_destroy`

Triggered **after** a record is destroyed. It's useful for actions that need to occur after a record has been removed from the database.

### Example:

```ruby
class User < ApplicationRecord
after_destroy :log_deletion

private
def log_deletion
Rails.logger.info "User #{self.id} was destroyed."
end
end
```

---

## 11. `around_save`

Triggered **around** saving a record (before and after). This is useful for wrapping a save action with custom logic before and after saving.

### Example:

```ruby
class User < ApplicationRecord
around_save :track_save_time

private
def track_save_time
start_time = Time.now
yield
Rails.logger.info "User saved in #{Time.now - start_time} seconds."
end
end
```

---

## 12. `around_create`

Triggered **around** creating a record (before and after). Similar to `around_save`, but specifically for create operations.

### Example:

```ruby
class User < ApplicationRecord
around_create :track_creation_time

private
def track_creation_time
start_time = Time.now
yield
Rails.logger.info "User created in #{Time.now - start_time} seconds."
end
end
```

---

## 13. `around_update`

Triggered **around** updating a record (before and after). This allows custom behavior during update operations.

### Example:

```ruby
class User < ApplicationRecord
around_update :track_update_time

private
def track_update_time
start_time = Time.now
yield
Rails.logger.info "User updated in #{Time.now - start_time} seconds."
end
end
```

---

## 14. `around_destroy`

Triggered **around** destroying a record (before and after). This allows custom behavior during destruction operations.

### Example:

```ruby
class User < ApplicationRecord
around_destroy :track_destroy_time

private
def track_destroy_time
start_time = Time.now
yield
Rails.logger.info "User destroyed in #{Time.now - start_time} seconds."
end
end
```

---

## 15. `before_validation_on_create`

Triggered **before validation when creating a new record**. Useful for preparing data or checking conditions before validation during creation.

### Example:

```ruby
class User < ApplicationRecord
before_validation_on_create :check_email_format

private
def check_email_format
unless email.match?(/\A[^@\s]+@[^@\s]+\z/)
errors.add(:email, "is invalid")
end
end
end
```

---

## 16. `after_validation_on_create`

Triggered **after validation when creating a new record**. You can perform actions once the validation has passed during creation.

### Example:

```ruby
class User < ApplicationRecord
after_validation_on_create :notify_user_creation

private
def notify_user_creation
Rails.logger.info "New user created with email: #{self.email}"
end
end
```

---

## 17. `before_validation_on_update`

Triggered **before validation when updating an existing record**. This allows you to check or modify the data before updating it.

### Example:

```ruby
class User < ApplicationRecord
before_validation_on_update :check_if_email_changed

private
def check_if_email_changed
if email_changed?
errors.add(:email, "can't be blank after update") if email.blank?
end
end
end
```

---

## 18. `after_validation_on_update`

Triggered **after validation when updating an existing record**. You can perform actions after validation when updating a record.

### Example:

```ruby
class User < ApplicationRecord
after_validation_on_update :log_update_changes

private
def log_update_changes
Rails.logger.info "User #{self.id} updated email."
end
end
```

---

## 19. `before_commit`

Triggered **before a transaction is committed** to the database. It’s useful for performing actions that need to happen before the transaction is final.

### Example:

```ruby
class User < ApplicationRecord
before_commit :send_email_notifications

private
def send_email_notifications
UserMailer.notify_changes(self).deliver_later
end
end
```

---

## 20. `after_commit`

Triggered **after a transaction has been committed** to the database. This is often used for operations that should occur only after a successful database commit.

### Example:

```ruby
class User < ApplicationRecord
after_commit :update_audit_log

private
def update_audit_log
AuditLog.create(action: "User created", user_id: self.id)
end
end
```

---

## 21. `before_rollback`

Triggered **before a transaction is rolled back**. You can perform actions just before the database transaction is undone.

### Example:

```ruby
class User < ApplicationRecord
before_rollback :log_rollback

private
def log_rollback
Rails.logger.info "Rolling back user changes for user: #{self.id}"
end
end
```

---

## 22. `after_rollback`

Triggered **after a transaction has been rolled back**. Useful for cleanup or notifications when a transaction fails.

### Example:

```ruby
class User < ApplicationRecord
after_rollback :notify_rollback

private
def notify_rollback
Rails.logger.info "Rollback complete for user: #{self.id}"
end
end
```

---

## 23. `after_touch`

Triggered when the `touch` method is called, usually to update the `updated_at` timestamp. It’s a lightweight callback for tracking changes without modifying the record itself.

### Example:

```ruby
class Post < ApplicationRecord
after_touch :log_touch

private
def log_touch
Rails.logger.info "Post touched: #{self.id}"
end
end
```

---

## 24. `on_destroy`

Custom callback triggered by custom destroy actions (less commonly used).

### Example:

```ruby
class User < ApplicationRecord
on_destroy :custom_destroy

private
def custom_destroy
Rails.logger.info "Custom destroy logic for user: #{self.id}"
end
end
```

---

## 25. `on_create`

A more custom callback mechanism (usually for creating records within a specific context).

### Example:

```ruby
class User < ApplicationRecord
on_create :custom_create

private
def custom_create
Rails.logger.info "Custom create logic for user: #{self.id}"
end
end
```
