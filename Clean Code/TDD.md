# Test-Driven Development

> Testable == Decoupled

Under pressure, teams give up the wrong things. They don't test enough; they leave the code in poor condition.

Under pressure, teams test less and therefore put more defects in.

Good tests weather code refactorings with aplomb; they are written such that changes to the code do not force rewrites of the tests.

## Pains of Tests

If a test require painful setup, the code expects too much context.

If testing one object drags a bunch of others into the mix, the code has too many dependencies.

Testing, done well, speeds development and lowers costs. It's also true that flawed tests slow you down and cost you money.

## Fear of Tests

The way to deal with errors is by building curiosity, not fear. "Why is this thing breaking?" rather than "How can I make this problem go away!".

## Green Bar Patterns

1. Fake it ('til you make it)
2. Obvious implementation
3. Triangulate

Developing the habit of writing just enough code to pass the tests forces you to write better tests.

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

* [The Transformation Priority Premise](https://8thlight.com/blog/uncle-bob/2013/05/27/TheTransformationPriorityPremise.html)

> As the tests get more specific, the code gets more generic.

Your test code cannot be generic because it is not true production  code. It must be very specific and full of constraints.

> The difference between the solution that adds a conditional and the solution that interpolates a variable into a string is that in the first, **as the tests get more specific, the code stays equally specific**. Every verse has its own personal test and its own individual code; there will never be a time when the code can do anything which is not explicitly tested.

Code becomes more generic by becoming more abstract.

> If you're in the middle of writing test, better information is as close as the next test. Squeezing all duplication out at the end of every test is not necessary. It's perfectly reasonable to tolerate a bit of duplication across several tests, hoping that coding up a number of slightly duplicative examples will reveal the correct abstraction. It's better to tolerate duplication than to anticipate the wrong abstraction.

Writing Shameless Green means optimizing for understandability, not changeability, and patiently tolerating duplication if doing so will help reveal the underlying abstraction. **Subsequent tests, or future requirements**, will provide the exact information necessary to improve the code.

The Shameless Green solution is optimized to be straightforward and intentional-revealing, and doesn't much concern itself with changeability or future maintenance. The goal is to use green to maximize your understanding of the problem and to unearth all available information before committing to abstractions.

> Quick green excuses all sins.

**Test-to-code coupling**

A great deal of pain originates with tests that are tied too closely to code. Every improvement to the code breaks the tests. Therefore, the first step is to understand how to write tests that confirm what your code does without any knowledge of how your code does it.

> Tests are not the place for abstractions - they are the place for concretions. Abstractions belong in code.

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

* [Thoughts on Mocking](http://practicingruby.com/articles/thoughts-on-mocking-1)

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

Use Extract Method to make mocks easier to write:

```ruby
# test/test_helper.rb
def mock_filemaker_with_response(response)
  fm_server = Minitest::Mock.new
  FMS::ConnectionPool.stub(:connect) do
    fm_server.expect(:get, response)
    yield
  end
  fm_server.verify
end
```

Use Extract Method to write custom assertions.


## Videos

* [Budgeting Reality: a New Approach to Mock Objects - Justin Searls](https://vimeo.com/53276460)
* [RailsConf 2016 - Get a Whiff of This by Sandi Metz](https://www.youtube.com/watch?v=PJjHfa5yxlU)