# 10 questions every js developer should know

## original article

[medium](https://medium.com/javascript-scene/10-interview-questions-every-javascript-developer-should-know-6fa6bdf5ad95#.vtqci5wvv)

>It contains useful resources to read, please check the original page.

## questions

### Can you name 2 programming paradigms importnt for js developers?

paradigm - 范例

Javscript is a multi-paradigm language, supporting imperative/procedural
programming along with

- OOP with prototypal inheritance
- functional programming(closures, first class function, lambda)

### What is functional programming?

It produces programs by composing mathematical functions and avoids shared state
& mutable data.

It's an essential concept in JS.

Points:

- pure functions / function purity
- avoid side-effects
- simple function composition
- example languages: lisp
- first-class function, higher order functions, functions as arguments/values

## difference between classical inheritance and prototypal inheritance

- Class Inheritance

Instances inherit from classes and create sub-class relationships. Instances are
typicall instantiated via constructor functions with the `new` keyword.

- Prototypal Inheritance

simpler and more flexible

Instances inherit directly from other objects. Instances are typically instantiated
via factory functions or `Object.create()`, may be composed from many different
objects, allowing for easy selective inheritance.

points:

- classes: tight coupling, hierarchies
- protorypes: concatenative inheritance, prototype delegation, functional inheritance

## OOP vs Functional Programming

### OOP

#### pros

- easy to understand and interpret

#### cons

- typically depends on shared state
- objects and behaviors are typicall tacked together, which may be accessed at
random by any number of functions with **non-deterministic** order, which may lead
to undesirable behavior like **race conditions**

>race condition, multiple functions competing for the same resources

### FP

#### pros

- avoid shared state or side-effects
- more reusable
- pure function, easier to scale across multiple processors

#### cons

- not familar, reduce readability
- lambda, algebras...more academic
- steeper learning curves

## When is classical inheritance a good choice?

**never**

## When is prototypal inheritance a good choice?

There is more than one type of prototypal inheritance:

- Delegation (i.e. the prototype chain)
- Concatenative (i.e. mixins, `Object.assign()`)
- Functional (a function used to craete a closure)

Each type of prototypal inheritance has its own set of use-cases, but all of
them are equally useful in their ability to enable composition, which creates
`has-a` or `uses-a` or `can-do` relationships as opposed to the `is-a`
relationship created with class inheritance.

Points:

- where modules or functional programming don't provide an obvious solution
- when you need to compose objects from multiple sources
- any time you need inheritance

## What does "favor object composition over class inheritance mean"?

Code reuse should be achieved by assembling smaller units of functionality into
new objects instead of inheriting from classes and create object taxonomies.

## two-way data binding vs one-way data flow

### two-way data binding

Angular

UI fields are bound to model data dynamically such that when a UI field changes,
the model data changes with in and vice-versa.

### one-way data flow

REact

the model is the single source of truth. Changes in the UI trigger messages that
signal user intent to the model. Only model has the access to change the app's
state.

One-way data flows are deterministic, while two-way binding can cause side-effects
which are harder to follow and understand.

## monolithic vs micro-service

### Monolithic Architecture

App is written as one cohesive unit of code whose components are designed to work
together, sharing the same memory space and resources.

#### pros

The major advantage is that most apps typically have a large number of cross-cutting
concerns, like loggin, rate limiting and security features.

When everything is running through the same app, it easier to hook up components
to these cross-cutting concers. Also, shared-memory access is faster.

#### cons

- tightly coupled and entangler as the app evolves, difficult to isolate services
for purposes such as independent scaling or code maintainability
- harder to understand because of dependencies, side-effects

### Microservice Architecture

App is made up of lots of smaller, independent applications. They are capable of
running in their own memory space and scaling independently from each other.

#### pros

- better organized, each service with a very specific job
- decoupled services are also easier to recompose and reconfigure to serve other apps
- performace advantages because it's possible to isolate hot services and scale them
independently

#### cons

- cross-cutting concerns

you’ll either need to incur the overhead of separate modules for each
cross-cutting concern, or encapsulate cross-cutting concerns in another service
layer that all traffic gets routed through.

Microservices are frequently deployed on their own virtual machines or
containers, causing a proliferation of VM wrangling work.

## what is asynchronous programming, and why it's important in JS

### Synchronous programming

Code is executed sequentially from top-to-bottom, blocking on long-running tasks
such as network requests and disk I/O.

### Asynchronous programming

The engine runs in an **event loop**.

1. When a blocking operation is needed, the request is started, and the code keeps
running without blocking for the resule.

2. when the response is ready, an interrupt is fired, which causes an event handler
to be run, where the control flow continues. In this way, a single program thread
can handle many concurrent operations.

user interfaces are asynchronous by nature, and spend most of their time waiting
for user input to interrupt the event loop and trigger event handlers.

Node is asynchronous by default.


