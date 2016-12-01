# Code Smells and Refactoring

The easiest way to unearth smells is to make a list of the things you dislike about the code.

The truth about refactoring is that it sometimes makes things worse, in which case your efforts serve gallantly to disprove an idea. The refactoring recipes don't promise to result in code that better expresses the problem - they merely make it easy to create that new expression, and **just as easy to revert it**.

> Proper refactoring allows you to explore a problem domain safely.

One way to get better at identifying smells is to practice describing the characteristics of code. Include any patterns that you see, and things you like, hate, or don't understand.

1. Do any methods have the same shape?
2. Do any methods take an argument of the same name?
3. Do arguments of the same name always mean the same thing?
4. If you were to add the `private` keyword to this class, where would it go?
5. If you were going to break this class into 2 pieces, where's the dividing line?

> It is often better to finish horizontal refactorings before undertaking vertical tangents. - [Kent Beck](https://www.facebook.com/notes/kent-beck/dont-cross-the-beams-avoiding-interference-between-horizontal-and-vertical-refac/260531380646400/)

## Flocking Rules

## Gradual Cutover Refactoring

A strategy for keeping the code in a releasable state, gradually switching over a small number of pieces at a time. This type of refactoring can be done alongside other development work so as not to affect the release schedule.

## Conditionals

Conditionals result in multiple execution paths through the code, which add complexity and make code hard to understand.

OO mindset is deeply suspicious of conditionals.

