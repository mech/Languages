# Functions

Large functions are where classes go to hide. The "Abstract till you drop" ask you to refactor your large functions into well-named classes.

## Function Signatures

Function argument is a liability, not an asset. Limit to 3 arguments and don't use boolean argument!

If you have a boolean argument function, you're having 2 branches of code that should be 2 functions instead.

> 2 booleans will cause a double-take

Do not use `null` as a pseudo-boolean argument. Having a `nil` argument is just as bad.

## Function Error Handling and Defensive Programming

> I hate defensive programming where my function is littered with `null` check and error check. Defensive programming just mean you don't trust your team or unit tests. However, libraries/framework code should use a lot of defensive programming because who know what consumer will do!? As for your own application code, don't bother with defensive programming. - Uncle Bob

Do you have too many error checking and guards around a function? Is it hiding the true implementation of the function?

Error handling is ok, but it cannot obscure logics.

Null value is not an error. What about NullObject pattern?

## Polymorphic Dispatch

The cure for switch and if-statement.

## Temporal Coupling

Functions that are called in order. `close()` must be called after `open()` or else there will be Side Effect.

Command Query Separation (CQS) - Command can have Side Effect. Query does not need to have.