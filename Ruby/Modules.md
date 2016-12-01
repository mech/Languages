# Ruby Modules

Module can be used for namespacing. But it's most important function is to share behaviors.

Module can be used for sharing code through automatic delegation of messages similar to classical inheritance.

* [In Ruby, how can I apply an attr_accessor from a module that is being extended?](http://stackoverflow.com/questions/32901178/in-ruby-how-can-i-apply-an-attr-accessor-from-a-module-that-is-being-extended)
* [Good Module, Bad Module](https://blog.codeship.com/good-module-bad-module/)

## Constants

```ruby
# KEY is in lexical scope. Physically located together will work.
module SimpleCrypto
  KEY = 'secret'
  
  class Encrypt
    def initialize(key = KEY) # Key works here
    end
  end
end

# Not in enclosing lexical scope and thus KEY will not work
module SimpleCrypto
  KEY = 'secret'
end

class SimpleCrypto::Encrypt
  def initialize(key = KEY) # raises NameError for KEY
  end
end
```

All global constants are kept at `Object` class. See `Object.constants`. That's why Ruby look up constant in 2 places: current lexical scope and the inheritance hierarchy.

This is also why if you want to use a fully qualified constant name like `Array`, you can use `Object::Array` or simply `::Array`.

## Extend

If you class mixin a module, it is the same as extending an instance of the same class. But this is 1 time only.

```ruby
module Greetable
  def greet
    print 'Hi'
  end
end

greetable = Object.new
greetable.extend(Greetable)

# Use it like it has been included all along
greetable.greet

# But actually it is a singleton method for this specific object only
def agreetable.greet
end
```

## Class Utility Methods

Favor the use of `module_function` over `extend self` when you want class methods.

```ruby
# This is bad
module Utilities
  extend self
  
  def parse(string)
  end
end
```

## Module attribute accessors

Rails extends Ruby with module accessor `mattr_accessor` and `cattr_accessor`. Just as Ruby's `attr_accessor` generates getter/setter methods for instances, module accessor provide getter/setter methods at the class or module level.

```ruby
module Config
  mattr_accessor :hostname
end

# Same as this
module Config
  def self.hostname
    @@hostname
  end
  
  def self.hostname=(hostname)
    @@hostname = hostname
  end
end
```

In Minitest, we can see module accessor also:

```ruby
module Minitest
  mc = (class << self; self; end) # Eigenclass, metaclass, singleton class
  
  mc.send :attr_accessor, :info_signal
  self.info_signal = 'INFO'
end
```

In Rails 5, there are also [thread-level module and class level variables](http://blog.bigbinary.com/2016/09/05/rails-5-adds-ability-to-create-module-and-class-level-variables-on-per-thread-basis.html) with `thread_mattr_accessor`.

## Singleton Class, Metaclass, Eigenclass

* [My Meta Moments](https://www.youtube.com/watch?v=0OAgZBNIixU)
* [Writing DSL in Ruby](https://robots.thoughtbot.com/writing-a-domain-specific-language-in-ruby)

Not to be confused with Singleton Pattern. The Singleton Class is just the idea that a Class is actually an Object.

## Delegation

```ruby
require 'forwardable'

module Rollbar
  PUBLIC_NOTIFIER_METHODS = %w(debug info warn warning error critical log).freeze
  
  class << self
    extend Forwardable
    def_delegators :notifier, *PUBLIC_NOTIFIER_METHODS
    
    def notifier
      Thread.current[:_rollbar_notifier] ||= Notifier.new(@root_notifier)
    end
  end
end
```

```ruby
require 'forwardable'

class Parts
  extend Forwardable
  def_delegators :@parts, :size, :each
  include Enumerable
  
  def initialize(parts)
    @parts = parts
  end
  
  def spares
    select { |part| parts.needs_spare }
  end
end
```