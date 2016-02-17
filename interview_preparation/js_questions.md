#

## Difference between call and apply

Both call and apply perform very similar functions: they execute a function in the context, or scope, of the first argument that you pass to them.

The difference is when you want to seed this call with a set of arguments.

### `call()`

`update.call(person1, 'John', 200)`

the limitation is apparent when you want to write code that doesn't know the number
of arguments to be passed in.

### `apply()`

`update.apply(persion1, ['John', 200])`

the second argument needs to be an array, then it will unpacks as arguments.
