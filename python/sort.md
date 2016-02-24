# Sort

## sort vs sorted

`sort()` is a method of list.  As explained, it sorts the list **in place**
and it does not return the list as a reminder of that fact.

`sorted()` is a builtin function, not a method on list, because it's
more general taking any iterator as its first argument (for example an
open file), not just a list.  It of course does return a list.

## How to sort

Default is **ascending**

```python
a = [5, 2, 3, 1, 4]
b = sorted(a)
a.sort()
```

### key functions

`sort()` and `sorted()` can have a key parameter to specify a **function** to be
called on each list element prior to making comparisons.

```python
>>> sorted("This is a test string from Andrew".split(), key=str.lower)
['a', 'Andrew', 'from', 'is', 'string', 'test', 'This']

>>> student_tuples = [
        ('john', 'A', 15),
        ('jane', 'B', 12),
        ('dave', 'B', 10),
]
>>> sorted(student_tuples, key=lambda student: student[2])   # sort by age
[('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
```

### Operator Module Functions

Convenient functions to make accessor functions easier and faster

`from operator import itemgetter, attrgetter, methodcaller`

```python
sorted(student_tuples, key=itemgetter(2))
sorted(student_objects, key=attrgetter('age'))
```

The operator module functions allow **multiple level of sorting**.

```python
sorted(student_tuples, key=itemgetter(1,2))
```

### Ascending and Descending

`reverse` parameter

`sorted(student_tuples, key=itemgetter(2), reverse=True)`

## old way

- Decorate-sort-undercorate
- cmp
