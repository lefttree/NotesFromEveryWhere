# A Guide to Javascript Engines

A 'Javascript Engine' is often termed a type of **Virtual Machine**. A "Virtual
Machine" refers to the software-driven emulation of a given computer system.

- 'System Virtual Machine'
- 'Process Virtual Machine'

> Javascript engine is different from the layout engines taht power a browser by
> laying our web pages. Read [this](http://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)

## What is JS Engines

Is to take the Javascript code that a develope writes and converts it to fat, 
optimized code that can be interpreted by a browser or even embedded into an
application.

## How does it work?

Covers 2 here

1. WebKit's JavaScriptCore
2. Google's V8 engine

analyze, interpret, optimize, and garbage collect JavaScript code

### JavaScriptCore

1. It performs a lexical analysis, breaking down the source into a series of
tokens, or strings with an identified meaning.
2. The tokens are then analyzed by the parser for syntax and built into a syntax
tree.
3. Four JIT (just in time) processes then kick in, analyzing and executing the
bytecode produced by the parser.

### V8

1. Full-codegen: a fast compiler that produces unoptimized code

It can generate good code for any js but not JIT code. doesn't do any type analysis
and doesn't know anything about types.

2. Crankshaft: a slower compiler that produces fast, optimized code.

It comes later and re-compiles hot functions. The crankshaft compiler takes types
from the inline cache and make decisions about how to optimize the code better.

## How V8 works

### Hidden Class

JS is prototype-based and dynamically typed.

V8 creates hidden classes, at runtime, in order to have an internal representation
of the type system and to improve the property access time.

n fact, V8 creates a new hidden class everytime the constructor function declares a property and keeps track of the changement in the hidden class.

## Why should we care?

The goal of a JavaScript engine's code parsing and execution process is to
generate the most optimized code in the shortest possible time.

## References

- [A guide to js engines for idiots](http://developer.telerik.com/featured/a-guide-to-javascript-engines-for-idiots/)
- [how browser works](http://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)
- [how v8 engine works](http://thibaultlaurens.github.io/javascript/2013/04/29/how-the-v8-engine-works/)

