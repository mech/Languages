# Designing Flexible Interfaces

Classes implement methods, some of those methods are intended to be used by others and these methods make up its public interface.

Let the customer order **what (interfaces)** they want without knowing **how (implementations)** it is being made.

Design experts notice domain objects without concentrating on them; they focus not on these objects but on the messages that pass between them. These messages are guides that lead you to discover other objects, ones that are just as necessary but far less obvious.

## Event Flow Confusing

Object may be well-designed, but the event flow and message passing is confusing.

OO application is more than just *classes*. It is *made up of classes* but *defined* by messages. Design, therefore, must be concerned with the messages that pass between objects. It deals not only with what objects know (their responsibilities) and who they know (their dependencies), but how they talk to one another. The conversation between objects takes place using their *interfaces*.

> The roots of this problem lie not in what each class *does* but with what it *reveals*.

## Public Interfaces

* Reveal its primary responsibility
* Will not change on a whim
* Are safe for others to depend on

Public methods should read like a description of responsibilities. The public interface is a **contract** that articulates the responsibilities of your class.

## Sequence Diagrams

Notice now that you have drawn a sequence diagram, this design conversation has been inverted. The previous design emphasis was on classes and who and what they knew. Suddenly, the conversation has changed; it is now revolving around messages. Instead of deciding on a class and then figuring out its responsibilities, you are now deciding on a message and figuring out where to send it.