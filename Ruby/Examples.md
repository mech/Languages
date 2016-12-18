# Ruby Examples to Learn From

```ruby
Date._parse(string, false).values_at(:year, :mon, :mday)

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

**Builder Example**

```ruby
card(size: 'large') do |c|
  c.header 'Title here'
  c.image 'https://cdn/1.png'
  c.badges { fav: fav_count }
end

def card(options = {}, &block)
  CardBuilder.new(context, options).render(&block)
end

class CardBuilder
  def initialize(options = {})
    @size = options.fetch(:size, 'normal')
  end
  
  def render(&block)
  end
  
  def header(text)
  end
end
```

**Polyfill****

```ruby
class Hash
  unless Hash.instance_methods(false).include?(:compact)
    def compact
      select { |_, value| !value.nil? }
    end
  end
end
```

## Object Composition

```ruby
class Topologist
  attr_reader :sense_of_humor, :deliver
  
  def initialize(sense_of_humor:, deliver:)
    @sense_of_humor, @delivery = sense_of_humor, delivery
    freeze
  end
  
  def call(jokes)
    delivery.call jokes.select { |joke| sense_of_humor.call joke }.sample
  end
end

topologist = Topologist.new(
  sense_of_humor: ->(joke) { true },
  deliver:        ->(joke) { joke }
)

loud_topologist = Topologist.new(
  sense_of_humor: ->(joke) { true },
  deliver:        ->(joke) { joke.upcase + '!!!' }
)
```