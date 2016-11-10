# SOLID

## SRP

> "Should these 2 responsibilities be separated? That depends upon how the application is changing."
> If, on the other hand, the application is not changing in ways that cause the two responsibilities to change at different times, then there is no need to separate them.

"Reason to change" is an estimation.

Because the class you're reusing is confused about what it does and contains several tangled up responsibilities, it has many reasons to change. You increase your application's chance of breaking unexpectedly if you depend on classes that do too much.

* [Rules, Laws, and Gentle Guidelines ](https://www.youtube.com/watch?v=BDXQ4pcbEBA)

### Determining if a class has a single responsibility

1. Interrogate it. Ask questions for each method.
2. Attempt to describe it in one sentence. If you have "and" or "or", then the class likely has more than one responsibility.

When everything in a class is related to its central purpose, the class is said to be *highly cohesive* or to have a single responsibility.

SRP doesn't require that a class do only one narrow thing or that it change for only a single nitpicky reason, instead SRP requires that a class be cohesive - that everything the class does be highly related to its purpose.

### Depend on behavior, not data

```ruby
attr_reader :cog

# We want to hide data behind behavior instead of using @cog all over the place
def cog
  @cog * complex_adjustment_factor
end
```

Hide @ivar from yourself. Doing so protects the code from unexpected changes. Data very often has behavior that you don't yet know about.

> To manage this complexity, we divvy the system's behaviors into objects that play well-defined roles.

For any desired behavior, an object either knows it personally, inherits it, or knows another object who knows it.

### Postponing decisions

Because you are writing changeable code, you are best served by postponing decisions until you are absolutely forced to make them.

> If circumstances allow you to create a separate class, perhaps you should. For now, imagine that you choose not to create a new, permanent, publicly available class at this moment. Perhaps some design restriction has been imposed upon you, or perhaps you are so uncertain about where you're going that you don't want to create a new class that others might start depending on.

### Parts, Roles, Responsibilities, Behaviors, Contracts

> Look at an object and ask: What role does it play?

An objet embodies a set of roles with a designated set of responsibilities.

Every object is held responsible. Each contributes its knowledge (Information Holder) and services (Service Provider).

We reinvent the object roles and shift responsibilities among them until they "fit".

An object contract (conditions-of-use) describes the conditions under which it guarantees its work and the effects it leaves behind when its work is complete.

> It's none of your business how I do my job, as long as I do it according to our agreement!

### Group collaborators into subsystems

