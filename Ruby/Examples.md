# Ruby Examples to Learn From

```ruby
puts 'foo', 'bar'

# class TooManyTimesheetError < TreyError; end
TooManyTimesheetError = Class.new(TreyError)

result =
  if some_cond
    calc1
  else
    calc2
  end
  
user
  .posts
  .includes(:comments)
  .where(published: true)
  .where.not(category: 'Private')
  .each do |post|
  end
  
# Splat
s = *'Hello' # => ["Hello"]
a = *(1..3)  # => [1, 2, 3]

# Will change the value only if it exists
balance &&= balance.increase

# Underscore for unused variable
result = hash.map { |_, v| v + 1 }

# Use warn instead of $stderr.puts

# Or sprintf
format('%{first} %{second}', first: 20, second: 10)
email_with_name = format('%s <%s>', user.name, user.email)

do_something if x.between?(1000, 2000)

rand(1..6)

email, username = options.values_at(:email, :nickname)
```