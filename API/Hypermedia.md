# Hypermedia

> REST is the architectural style of the Web.

* [History of REST APIs](https://blog.readme.io/the-history-of-rest-apis/)
* [REST API must be hypertext-driven](http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven)
* [Chapter 5: Representation State Transfer (REST)](http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)
* [A Hypermedia API Reading List - Steve Klabnik](http://blog.steveklabnik.com/posts/2012-02-27-hypermedia-api-reading-list)
* [Just Because Github Has a GraphQL API Doesn't Mean You Should Too](http://www.programmableweb.com/news/just-because-github-has-graphql-api-doesn%E2%80%99t-mean-you-should-too/analysis/2016/09/21)
* [REST-API-Multiple-Request-Chaining](https://github.com/mikestowe/REST-API-Multiple-Request-Chaining)
* [HTTP Made Simple](https://www.pandastrike.com/posts/20140128-http-made-simple-part-3)
* [Nobody Understands REST or HTTP](http://blog.steveklabnik.com/posts/2011-07-03-nobody-understands-rest-or-http)
* [Design Patterns in HTTP](https://www.pandastrike.com/posts/20160726-design-patterns-in-http)

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

> You can strip away certain architectural constraints of REST, but if you strip away the wrote ones for the wrong reasons, you demonstrate a misunderstanding of the problem REST is supposed to solve and how the architectural constraints apply.
Your link demonstrates common misunderstandings of REST, leading to this whole REST vs GraphQL debate.

> It starts with level 0, which proposes to use HTTP as RPC. Already, we're on the wrong foot.

> Then level 1, which proposes to identify URIs to resources. Which invariably leads people to associate URIs to objects (in the OOP sense), and now we're completely off track.

> Level 2 and level 3 build on this foundation. URIs as they are used in REST define state transitions. Given the representation you hold now (say HTML), the URIs point to the next states that you can proceed to. More importantly, the representation you hold provides the server the necessary context to process the request. The server does not have to remember its conversation with you. This implements the most important design feature of REST, fault tolerance and scalability.

> By using hyperlinks as the engine of application state, allows the sever to control the URI space, and leads to another feature of REST, which is API longevity.

> Other features, such as MIME type, give the client information about how to interact with the server. HTML being the best example, because the specification tells the client exactly what to send the server, with only "in band" information. This leads to another feature of REST, which is allowing a wide range of clients to interact with the application on the server.
TL;DR - if you want to implement the design goals of the architectural pattern called REST, go to the source, Roy Fielding's thesis. Articles like the one you link start from the wrong conceptual foundation and inevitably lead to the wrong conclusions. - [RESTful APIs vs GraphQL APIs by Example](https://www.reddit.com/r/programming/comments/4a1idd/restful_apis_vs_graphql_apis_by_example/)