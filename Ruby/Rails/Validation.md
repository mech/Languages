# Rails Validation

* [dry-validation](http://dry-rb.org/gems/dry-validation/)
* [Always use the new "Sexy Validation" introduced in Rails 3](http://thelucid.com/2010/01/08/sexy-validation-in-edge-rails-rails-3/)

```ruby
class RecurringEvent < ApplicationRecord
  TIME_12H_FORMAT = /\A(1[0-2]|0?[1-9]):[0-5][0-9]\s?(am|pm)\z/i
  validates :time, presence: true, format: { with: TIME_12H_FORMAT, message: 'invalid time - use format 10:00 am' }
end
```