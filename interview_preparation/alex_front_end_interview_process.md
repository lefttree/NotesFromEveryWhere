## Alex's process

### object prototypes

1. define a `spacify` function which taks a string as an argument and returns the
same string but with each character separated by a space.

```javascript
function spacify(str) {
    return str.split("").join(" ");
}
```

2. to place the `spacify` function directly on the `String` object, like `'hello world'.spacify()`

get a idea of function prototypes.

```javascript
String.prototype.spacify = function() {
    return this.split("").join(" ");
};
```

3. function declaration vs function expression

declaration

```javascript
function bar() {
    return 3;
}
```

expression: defines a function as a part of a larger expression syntax, can be
named or anonymous.

```javascript
var a = function() {
    return 3;
}

// self invoking function expression
(function sayHello(){
    alert("hello");
})();
```

Function declaration hoisting causes some confusion. Should use function expression.

1. In javascript functions are living objects with values, but in java methods are
just metadata storage.

function expression shows that we are creating an object.

2. function expression are more versatile. functional programming!

never put a function declaration in an `if` statement

### Arguments

1. write a `log()` function to proxies its string argument to `console.log()`

Better candidates will often skip directly to using `apply`, `apply` takes `arguments`
directly.

```javascript
function log(){
    console.log.apply(console, arguments);
}
```

2. next ask to prefix all logged messages with `(app)`, "(app) hello world"

Good candidates know that `arguments` is a *pseudo array*, and to manipulate it
we need to **convert it into a standard array first**. The common pattern for this
is using `Array.prototype.slice`.

```javascript
function log() {
    var args = Array.prototype.slice.call(arguments);
    args.unshift("(app)"); // insert in the front
    console.log.apply(console, args);
}
```

### Context

1.

```javascript
var User = {
    count: 1,
    getCount: function() {
        return this.count;
    }
}

console.log(User.getCount());
var func = User.getCount;
console.log(func());
```

result should be `1` and `undefined`, the `func` is called in the context of `window`.

2. Use `bind` to make sure it's always bound to `User`.

```javascript
var func = User.getCount.bind(User);
```

3. Older browsers don't have `bind`, shim it.

Use `apply`.

```javascript
// use native if avaialble in the or statement
Function.prototype.bind = Function.prototype.bind || function(context) {
    var self = this;

    return function() {
        return self.apply(context, arguments);
    };
}
```

4. **currying function** & **compose function**


### Overlay Library

1. use `position:fixed`, which will ensure the overlay encompasses the entire
window even if it's scrolled.

```css
.overlay {
    position: fixed;
    left: 0;
    right: 0;
    bottom: 0;
    top: 0;
    background: rgba(0,0,0,.8);
}
```

2. how they choose to center content inside.

- some may choose to use css and absolute positioning, which is possible if content
is a fixed width and height.
- otherwise use javascript for positioning

```css
.overlay article {
  position: absolute;
  left: 50%;
  top: 50%;
  margin: -200px 0 0 -200px;
  width: 400px;
  height: 400px;
}
```

3. add a eventlistener so overlay is closed if it's clicked.

`$(".overlay").click(closeOverlay);` would not work correctly, cause click on the
overlay's children will all close the overlay. Should check the event's **target**,
and make sure the event **wasn't propagated**.

- `e.target`: identifies the element on which the event **occured**
- `e.currentTarget`: always refers to the element the event handler has been **attached to**

```javascript
$(".overlay").click(function(e)) {
    if (e.target == e.currentTarget) {
        closeOverlay();
    }
}
```

## References

- [alex frontend interview](http://blog.sourcing.io/interview-questions)
