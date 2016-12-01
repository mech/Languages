# Hypermedia

> REST is the architectural style of the Web.

* [REST API must be hypertext-driven](http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven)
* [Chapter 5: Representation State Transfer (REST)](http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)

---

* Any important resource in a RESTful system must have an identifier.
* Media type defines a processing model. For example, HTML defines a rendering process for hypertext and the browser behavior around each element.
* The interface doesn't need to be discovered. It is defined right there in the hypertext. The representation tells the client how to compose all transitions to the next application state.
* The purpose of resource modeling is to figure out what resources you have that are worth identifying, representing and manipulating. You should not be building clients that are dependent on the resource naming structure. The hypertext sends the client directly to the desired application state.

Components of REST:

* HTTP - Transport protocol
* HTML - Hypermedia format
* Links - Controls, Actions, Operations
* Media Types - Used to represent resources

## Shared Resources

> Resource is an abstraction that can be named. Documents, images, temporal services (e.g. "today's weather in Tampines"), etc.

Or should we focus on representations and state transitions rather than resources.

A resource is modified by manipulating its representation. The representation contains the actual resource state, and this is what is exchanged between client and server. This means that users interact with a particular resource through representations of its state.

> You need to think about "doing", don't think about "being"

```
Being = entity = noun = resource-oriented = object-oriented
Doing = behavior = verb = verb-oriented = affordances
```

**Affordances**

Give conscious thought to the signs you see, the way that you relate objects in your environment.

A noun-oriented design doesn't allow for affordances because affordances are verbs, not nouns. A good way to think about hypermedia APIs is including affordances to indicate what you can do next. In other words, it's using hypermedia as the means of driving application state forward.

Algorithms are a series of steps. Algorithms are made of verbs, not nouns. Algorithms are a series of state changes in your application's state. A slightly different way of thinking about hypermedia APIs is the usage of affordances to communicate an algorithm to a client.

> Thinking in terms of explorable resources is easier if we concentrate on the application flow we want our users to follow.

## Architectural Constraints

1. Null Style
2. Client-Server
3. Stateless
4. Cache
5. Uniform Interface
6. Layered System
7. Code-on-Demand

---

The 4 interface constraints:

1. Identification of resources
2. Manipulation of resources through representations
3. Self-descriptive messages
4. HATEOAS

While REST is totally stateless, using hypermedia resource representations allow the client to manage state transitions.

## Links

> Follow links, don't calculate the URL.

## Videos

* [Hypermedia APIs - Jon Moore](https://vimeo.com/20781278)