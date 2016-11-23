# Accessors

Instance variables are private by default. Without accessors they're only accessible from within instance methods.

```ruby
class Person
  attr_reader :first_name, :last_name
  
  def initialize(first_name, last_name)
    @first_name = first_name
    @last_name = last_name
  end
end

# Or just use Struct
Person = Struct.new(:first_name, :last_name) do
end
```

When you do `self.value = 1`, you are calling a method, so the following will lead to stack too deep. It may look like assignment, but it is actually invoking setter method.

```ruby
# Wrong! Stack too deep
def value=(x)
  self.value = x
end

# Correct!
def value=(x)
  @value = x
end
```

## Protected Methods

Use protected method if you want the variables to remain private but want to access it outside. However protected methods can only be accessed if it is called from objects of the same class or inherit from common superclass.

```ruby
class Widget
  def overlapping?(other)
    x1, y1 = screen_coordinates
    x2, y2 = other.screen_coordinates # other must be same class in order to use protected method
  end
  
  protected
  
  def screen_coordinates
    # Private variables
    [@screen_x, @screen_y]
  end
end
```

## Class Instance Variables and Class Variables

* `@instance_variable`
* `@@class_variable` - attached to a class and visible to all instances of that class. Avoid it due to their nasty behavior in inheritance.

The problem with `@@class_variable` is that once set, it will affect all subclasses also. Any instance of one of these subclasses can access the shared class variables and modify them.

To prevent this global-like shared behavior, we can use "class instance variable" which is an `@instance_variable` for the class:

```ruby
# It is easy to confuse class instance variable as normal instance variable
def self.instance
  @single ||= new
end
```

If you think about it, class methods are just instance methods for the class object, then it makes sense that we also have "class instance variables".


