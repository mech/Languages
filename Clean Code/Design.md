# Object Oriented Design

Good code not only works, but is also simple, understandable, expressive and changeable.

## Lack of Design

Failure of OOD might look like failures of coding technique but they are actually failures of perspective.

## Cost of Change

Something always change. It always does. The customers didn't know what they wanted, they didn't say what they meant. You didn't understand their needs, you've learned how to do something better, etc.

It is the need for change that makes design matter.

Dependencies stand in the way of change.

You must combine an overall understanding of your application's requirements with knowledge of costs and benefits of design alternatives and then devise an arrangement of code that is cost effective in the present and will continue to be so in the future.

Design that anticipate specific future requirements almost always end badly. Practical design does not anticipate what will happen to your application, it merely accepts that something will and that, in the present, you cannot know what.

## Principles and Patterns

OO designer has tools - principles and patterns.

## Overdesign

A little bit of knowledge is dangerous; as their knowledge increases, they design relentlessly. In an excess of enthusiasm they apply principles inappropriately and see patterns where none exist.

## Iterative

The iterative nature of Agile development allows design to adjust regularly and to evolve naturally.

You customers can't define the software they want before seeing it, so it's best to show them sooner rather than later. Thus software should be build in tiny increments, gradually iterating your way into an application that meets the customer's true need.

> If lack of a feature will force you out of business today it doesn't matter how much it will cost to deal with the code tomorrow.

## Abstraction

> Your code is less concrete but more abstract - you've made it initially harder to understand in hopes that it will ultimately be easier to maintain.

OOD isn't free!

DRY is a great idea, but that doesn't mean it's free. The price you pay for DRYing out code is that the invoker of the new method no longer knows the implementation, only the message it should send. If you're willing to pay this price (i.e. being willingly ignorant of the actual behavior), the reward your reap is that when the behavior changes, you need alter your code in only one place.

Did you divid one large class into many small ones? You can now reuse the new classes independently of one another, but it's no longer obvious how they fit together for the original case.

Increasing the level of abstraction is not free!

Each of these design choices has costs, and it only makes sense to pay these costs if you also accrue some offsetting benefits. Design is thus about picking the right abstraction. If you choose well, your code will be expressive, understandable and flexible. If you get the abstraction wrong, your code will be convoluted, confusing and costly.

> Even with the best of intentions, abstractions are easy to get wrong.

Well-meaning programmers tend to over anticipate abstractions, inferring them prematurely from incomplete information. Early abstractions are often not quite right and therefore they create a catch-22. You can't create the right abstraction until you fully understand the code, but the existence of the wrong abstraction may prevent you from ever doing so. **This suggests that you should not reach for abstractions, but instead, you should resist them until they absolutely insist upon being created**.

> The code you write should meet 2 conflicting goals: It must remain concrete enough to be understood while simultaneously being abstract enough to allow for change.

There is a sweet spot that represents the perfect compromise between comprehension and changeability, and it's your job as a programmer to find it.

> This code is hard to understand because it is inconsistent and duplicative, and because it contains **hidden concepts that it does not name**.

Duplication of logic suggests that there are concepts hidden in the code that are not yet visible because they haven't been isolated and named.

> Code clarity is built upon names.

---

> The code gives the impression that its author feared that the logic for selecting or invoking a template would someday need to change, and so added levels of indirection in a misguided attempt to protect against that day. They did not succeed.

---

> Insufficient patience can hurt your chances of revealing the right abstractions.

---

> Shameless Green is clearly the best solution, yet almost no one writes it. It feels embarrassingly easy, and is missing many qualities that you expect in good code. It duplicates strings and contains **few named abstractions**.

---

> Clean code is ... full of crisp abstractions ...

It is cheaper to manage temporary duplication than to recover from incorrect abstractions. The resulting code might just be "good enough". The challenge comes when a change request arrives. Code that's good enough when nothing ever changes may well be code that's not good enough when things do.

## Relationship of Different Pieces

Change ripple through the system.

## Event Flow Confusing

Object may be well-designed, but the event flow and message passing is confusing.

## Locality

Dependencies locality.

## Compositionality

> The meaning of a compound expression is a function of the meanings of its parts and the syntactic rule by which they are combined. - [Building on SOLID foundations - Steve Freeman & Nat Pryce](https://www.youtube.com/watch?v=6Bia81dI-JE)

DSL can be composable.

```java
Scenario bankingCrisis = ScenarioDefinition.create()
  .yieldCurveShifts(
    when(currency,
      is(EUR, proportionalShift(-0.1)),
      is(GBP, proportionalShift(-0.05)),
      is(USD, proportionalShift(+0.1)),
      otherwise(proportionalShift(+0.005))))
  .stockPriceShifts(
    when(sector, is(BANKING)))
```

```java
List<Employee> newEmployees = employees.hired(TODAY);

assertThat(newEmployees).hasSize(6).contains("frodo", "sam");
```