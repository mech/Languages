# Test-Driven Development

> Testable == Decoupled

Under pressure, teams give up the wrong things. They don't test enough; they leave the code in poor condition.

Under pressure, teams test less and therefore put more defects in.

Good tests weather code refactorings with aplomb; they are written such that changes to the code do not force rewrites of the tests.

## Pains of Tests

If a test require painful setup, the code expects too much context.

If testing one object drags a bunch of others into the mix, the code has too many dependencies.

## Incoming and Outgoing Messages

The incoming messages make up the public interface of the receiving object.

The outgoing messages, by definition, are incoming into other objects and so are part of some other object's interface.

For incoming messages, you make assertions about the results that these messages return. These are *test of state*.

For outgoing messages, you should not test these outgoing messages for state. You don't own it.

There are 2 outgoing messages:

1. Queries - No need to test as it will be tested at other side
2. Commands - Side effects

For outgoing command messages, we need to "prove" that they are properly sent. Proving that a message gets sent is a test of behavior, not state, and involves assertions about the number of times, and with what arguments, the message is sent.

When you test outgoing command messages only to prove they get sent, your loosely coupled tests can tolerate application changes without being forced to change in turn.

## Generic Code and Transformations

> As the tests get more specific, the code gets more generic.

Your test code cannot be generic because it is not true production  code. It must be very specific and full of constraints.

## Prevent Code Rot

## Stubs - Object#stub

Stub replaces real implementation and delivers a desired response when called. This comes in handy when testing code that depends on resources outside your control like external services, the date and time, and so on.

For simple test doubles it's fine to use plain old Ruby objects:

```ruby
# This test double stubs `diameter`
# The fact that it always returns 10 is perfect for predictability in test
class DiameterDouble
  def diameter
    10
  end
end
```

But this fake is after all a fake. If the `diameter` interface name changes, the test won't know it and still passes.

```ruby
array.stub(:length, 10) do
  assert_equal 10, array.length
end
```

This may be obvious, but still, never ever stub the object under test. More often than not, you'll end up testing the stub and not the object itself.

## Mocks

Mocks are tests of behavior, as opposed to tests of state. Instead of making assertions about what a message returns, mocks define an expectation that a message will get sent.

Easy to do if you have dependency injection. In scenarios where it's not possible to change your code to support injection, you can also resort to a stub to inject dependencies indirectly.

```ruby
# 1. Create a mock
@observer = Minitest::Mock.new
# 2. Inject it
@gear = Gear.new(cog: 11, observer: @observer)
# 3. Set expectation
@observer.expect(:changed, true, [42, 11])
# 4. Perform action
@gear.set_cog(12)
# 5. Finally verify that it has been called
@observer.verify

# OR new in v5
assert_mock @observer
```

The more collaborators you mock, the greater the risk of false positives.

## Shared Helpers/Examples



## Videos

* [Budgeting Reality: a New Approach to Mock Objects - Justin Searls](https://vimeo.com/53276460)
* [RailsConf 2016 - Get a Whiff of This by Sandi Metz](https://www.youtube.com/watch?v=PJjHfa5yxlU)