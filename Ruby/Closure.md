# Ruby Closure

* [Why Ruby is an acceptable Lisp](http://www.randomhacks.net/2005/12/03/why-ruby-is-an-acceptable-lisp/)

Minitest has good example on using closure to benchmark time. You can think of closure as an onion. Each layer of the onion is a Ruby block or method that wraps other blocks and methods inside it. Each layer builds on the on that contains it and takes you a little closer to the center.

```ruby
def run
  with_info_handler do
    time_it do
      capture_exceptions do 
        before_setup; setup; after_setup
        
        self.send self.name
      end
    end
  end
end

def with_info_handler(&block)
  t0 = Minitest.clock_time
  handler = lambda do
    warn "\nCurrent: %s#%s %.2fs" % [self.class, self.name, Minitest.clock_time - t0]
  end
  
  self.class.on_signal ::Minitest.info_signal, handler, &block
end

def time_it
  t0 = Minitest.clock_time
  
  yield
ensure
  self.time = Minitest.clock_time - t0
end

def capture_exceptions
  yield
rescue *PASSTHROUGH_EXCEPTIONS
  raise
rescue Assertion => e
  self.failures << e
rescue Exception => e
  self.failures << UnexpectedError.new(e)
end
```

## Proc

So far we've been passing anonymous blocks to the methods where they were called. While it's a very useful and simple technique, there are times where it would be more convenient to store the block in a variable and be able to reuse it later.

Ruby has a feature that allows you to do just that. You can wrap your blocks of code into Proc, making it first-class object.

```ruby
# prepare a proc first
square = Proc.new do |i|
  i ** 2
end

class Array
  def iterate(proc)
    self.each_with_index do |element, index|
      self[index] = proc.call(element)
    end
  end
end

[1, 2, 3, 4].iterate(square)
```