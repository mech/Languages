# Hypermedia

* [REST API must be hypertext-driven](http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven)

---

* Any important resource in a RESTful system must have an identifier.
* Media type defines a processing model. For example, HTML defines a rendering process for hypertext and the browser behavior around each element.
* The interface doesn't need to be discovered. It is defined right there in the hypertext. The representation tells the client how to compose all transitions to the next application state.
* The purpose of resource modeling is to figure out what resources you have that are worth identifying, representing and manipulating. You should not be building clients that are dependent on the resource naming structure. The hypertext sends the client directly to the desired application state.