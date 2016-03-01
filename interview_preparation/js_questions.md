# JS Questions

## Hoisting

`Function declarations` and `function variables` are always moved (‘hoisted’) to
the top of `their JavaScript scope` by the JavaScript interpreter

variable `declarations` get hoisted but their `assignment` expression **don't**.

## Difference between call, apply and bind

Both call and apply perform very similar functions: they execute a function in the context, or scope, of the first argument that you pass to them.

The difference is when you want to seed this call with a set of arguments.

### `call()`

`update.call(person1, 'John', 200)`

need to pass in positional arguments as a sequence.

the limitation is apparent when you want to write code that doesn't know the number
of arguments to be passed in.

### `apply()`

`update.apply(persion1, ['John', 200])`

the second argument **needs to be an array**, then it will unpacks as arguments.

### `bind()`

`bind()` creates a new function that, when called, has its `this` keyword



## References

- [front-end interview question github](https://github.com/h5bp/Front-end-Developer-Interview-Questions)
- [Javascript Garden](http://bonsaiden.github.io/JavaScript-Garden/)
- [Frontend Handbook](http://www.frontendhandbook.com/practice/interview-q.html)

- [alex frontend interview questions](http://blog.sourcing.io/interview-questions)
- [Function declaration vs expression](https://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/)
