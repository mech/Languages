# Introduction

* [Java Design Patterns Usage](http://stackoverflow.com/questions/1673841/examples-of-gof-design-patterns-in-javas-core-libraries/2707195#2707195)

## Decorator

Wrapper class. Higher-order functions.

Decorator allows you to build up complex behaviors by composing objects at runtime.

Decorator allows us to add behavior to objects without affecting other objects of the same class. It is a useful alternative to sub-classing.

Decorator is a nice pattern, but use it sparingly. Too much of it makes your eyes bleed.

* [File I/O is using Decorator](http://www.javaworld.com/article/2075920/core-java/decorate-your-java-code.html)

```java
// First you create an abstract class that defines the set of operations
// you need to support.
// Then you create the subclass that inherits from that abstract class,
// accepts an instance of the class in its constructor
abstract class ToolControllerDecorator extends ToolController {
  protected ToolController controller;

  public ToolControllerDecorator(ToolController controller) {
    this.controller = controller;
  }

  public void raise() {
    controller.raise();
  }

  public void lower() {
    controller.lower();
  }
  
  public void step() {
    controller.step();
  }
}

public class StepNotifyingController extends ToolControllerDecorator {
  private List notifiers;

  public StepNotifyingController(ToolController controller, List notifiers) {
    super(controller);
    this.notifiers = notifiers;
  }

  public void step() {
    controller.step();
  }
}

// We can nest
ToolController controller = new StepNotifyingController(
  new AlarmingController(new ACMEController()),
  notifiers
)
```