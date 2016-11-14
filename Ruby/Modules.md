# Ruby Modules

Module can be used for namespacing. But it's most important function is to share behaviors.

* [In Ruby, how can I apply an attr_accessor from a module that is being extended?](http://stackoverflow.com/questions/32901178/in-ruby-how-can-i-apply-an-attr-accessor-from-a-module-that-is-being-extended)
* [Good Module, Bad Module](https://blog.codeship.com/good-module-bad-module/)

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