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

The message-based perspective yields more flexible applications than does the class-based perspective.

Changing from fundamental design question from "I know I need this class, what should it do?" to "I need to send this message, who should respond to it?" is the first "ah-ha" moment you can have of OOD.

## Duck Typing

* Inheritance - is-a
* Composition - has-a
* Duck Type - behaves-like-a

It's not what an object **is** that matters, it's what it **does**.

> Code like this gets written when programmers are blinded by existing classes and neglect to notice that they have overlooked important messages; this dependent-laden code is a natural outgrowth of a class-based perspective.

The concreteness of class-type makes it simple to understand buy dangerous to extend. The duck-type alternative is more abstract; it places slightly greater demands on your understanding but in return offers ease of extension.

This tension between the costs of concretion and the costs of abstraction is fundamental to object-oriented design.

The ability to tolerate ambiguity about the class of an object is the hallmark of a confident designer. Once you begin to treat your objects as if they are defined by their behavior rather than by their class, you enter into a new realm of expressive flexible design.

`case` statement, `kind_of?`, `is_a?` and `responds_to?` all point to a missing duck type.

> Place trust in your ducks

The decision to create a new duck type relies on judgment. The purpose of design is to lower costs; bring this measuring tick to every situation. If creating a duck type would reduce unstable dependencies, do so. Use your best judgement.

Duck typing create virtual types that are defined by what they do instead of who they are.