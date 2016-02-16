# Javascript Interview Questions

### pitfall with using `typeof bar === "object"`

`null` is also considered an object in Javascript!

`(bar !== null) && (typeof bar === "object")`

`function` is not `object`
`array` is `object`

### variable hoist

```javascript
(function(){
    var a = b = 3;
})();
// a
// b
```

In fact, `var a = b = 3` is actually shorthand for 

```
b = 3;
var a = b;
```

b is a global variable

### Use strict mode

- makes debugging easier
- prevents accidental globals
    + without this, assigning a value to an undefined variable would create a
    global varilable
- eliminates `this` coercion
    + in strict mode, treferencing a `this` value of `null` or `undefined` throws
    an error
- disallows duplicate property names or parameters
- makes `eval()` safer
- throws error on invalid usage of `delete`

### NaN

unreliable, ES6 offers a new `Number.isNaN()` function

### Number are all treated with floating point precision

so `0.1 + 0.2 == 0.3` may not be true

### events and timing

```javascript
(function(){
    console.log(1);
    setTimeout(function(){console.log(2)}, 1000);
    setTimeout(function(){console.log(3)}, 0);
    console.log(4);
})();
```

Results would be

```
1
4
3
2
```

The browser has an event loop which checks the event queue and processes pending
events. If an event happens in the background while the browser is busy(processing
an `onClick`), the event **gets appended to the queue**.

`setTimeout` put referenced function into the event queue if the browser if busy.
`setTimeout(func, 0)` would try to execute the function **asap**.

>setTimeout(.., 0) is applied to execute the action after browser processing and other handlers.

### DOM mutation events are synchronous

### arguments

```
function sum(x) {
  if (arguments.length == 2) {
    return arguments[0] + arguments[1];
  } else {
    return function(y) { return x + y; };
  }
}
```

or

```
function sum(x, y) {
  if (y !== undefined) {
    return x + y;
  } else {
    return function(y) { return x + y; };
  }
}
```

### infamous loop event listener

```javascript
for (var i = 0; i < 5; i++) {
  var btn = document.createElement('button');
  btn.appendChild(document.createTextNode('Button ' + i));
  btn.addEventListener('click', (function(i) {
    return function() { console.log(i); };
  })(i));
  document.body.appendChild(btn);
}
```

```javascript
for (var i = 0; i < 5; i++) {
  var btn = document.createElement('button');
  btn.appendChild(document.createTextNode('Button ' + i));
  (function (i) {
    btn.addEventListener('click', function() { console.log(i); });
  })(i);
  document.body.appendChild(btn);
}
```

```javascript
['a', 'b', 'c', 'd', 'e'].forEach(function (value, i) {
  var btn = document.createElement('button');
  btn.appendChild(document.createTextNode('Button ' + i));
  btn.addEventListener('click', function() { console.log(i); });
  document.body.appendChild(btn);
});
```

### Prevent stack overflow

```javascript
var list = readHugeList();

var nextListItem = function() {
    var item = list.pop();

    if (item) {
        // process the list item...
        nextListItem();
    }
};
```

change to

```javascript
    if (item) {
        setTimeout( nextListItem, 0);
    }
```

It's because the event loop handles the recursion, not the call stack, so the call
stack remains clear.

### Closure

A closure is an inner function that has access to the variables in the outer
functions's scope chain. The closure has access to variables in 3 scopes

1. variable in its own scope
2. variables in the enclosing function's scope
3. global variables

### `1 && 2 = 2`

 The interesting thing with the `&&` operator is that when an expression is
 evaluated as “true”, then the expression itself is returned.

### key stringify

```javascript
var a = {},
    b = {key:'b'},
    c = {key:'c'};

a[b] = 123;
a[c] = 456;

console.log(a[b]);
```

result would be `456` not `123`.

Because javascript will implicitly `stringify` the key, `b` and `c` are both objects,
they will both be converted to `"[object Object]"`.

### Javascript execution and rendering

In most browsers, rendering and js use single event queue, which means that while
Javascript is running, no rendering occurs.

### Javascript events and timing

Most browsers use single thread for UI and JavaScript, which is blocked by synchronous calls. So, JavaScript execution blocks the rendering.

Events are processed asynchronously with the exception of DOM events.

The `setTimeout(..,0)` trick is very useful. It allows to:

- Let the browser render current changes.
- Evade the “script is running too long” warning.
- Change the execution flow.

### Drawback of true private methods in javascript

They are very memory-inefficient, a new copy of the method would be created for
each instance.

### How to check if an object is an array or not?

```javascript
Object.prototype.toString.call(arrayList) === '[object Array]'
```

### `delete` from array

```javascript
var trees = ["xyz","xxxx","test","ryan","apple"];
delete trees[3];

console.log(trees.length);
```

output would be 5

### addition operators

- Number + Number -> Addition
- Boolean + Number -> Addition
- Boolean + Boolean -> Addition
- Number + String -> Concatenation
- String + Boolean -> Concatenation
- String + String -> Concatenation

### Javascript Hoisting

variable and function are `hoisted`.

```javascript
foo();
var foo = function foo(){ 
     return 12; 
 }; 
```

is actually like this

```
var foo = undefined;
foo();
foo = function() {
    //
};
```

```javascript
var salary = "1000$";

 (function () {
     console.log("Original salary was " + salary);

     var salary = "5000$";

     console.log("My New Salary " + salary);
 })();
```

is actually

```javascript
 var salary = "1000$";

 (function () {
     var salary = undefined;
     console.log("Original salary was " + salary);

     salary = "5000$";

     console.log("My New Salary " + salary);
 })();
```

### typeof

```javascript
function func(x) {
    console.log(typeof x, arguments.length);
}
```

### Cookie

read a cookie

`document.cookie`

create a cookie

```javascript
document.cookie = "key1 = value1; key2 = value2; expires = date";
```

delete a cookie

just set the expiration date to a time in the past

### 
