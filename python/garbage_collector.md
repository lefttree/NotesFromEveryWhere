# Garbage Collector

>CPython

## Main Ideas

1. Maintain reference count

2. Periodically detect reference cycles

Consider 2 objects A and B, where A holds a reference to B and B holds a reference
to A. This is a reference cycle.

3. Performance is enhanced with heuristics

CPython introduces the concept of **generation** to accoutn for the relative
age of an object. By default CPython has 3 generations.

## References

- [quora](https://www.quora.com/How-does-garbage-collection-in-Python-work)
- [python垃圾回收机制](http://foofish.net/blog/94/python-gc)
