# Javascript Garden

## Objects

### usage and properties

Everything in JS acts like an object, with only 2 exceptions `null` and `undefined`.

>number literals is different because js parser tries to parse the dot as floating
point

### objects as data type

1. hashmap `var foo = {};`

2. accessing: dot notation or the square bracket notation

3. deleting properties

`delete obj.baz;`

4. notation of keys: can be both notated as plain characters and as strings.

## Prototype

Prototypal inheritance. inheritance in JS uses *prototype chains*.

```javascript
function Foo() {
    this.value = 42;
}
Foo.prototype = {
    method: function() {}
}

function Bar() {}

// set Bar's prototype to a new instance of Foo
// all Bar instances share the same Foo instance
Bar.prototype = new Foo();
Bar.prototype.foo = "Hello";

Bar.prototype.constructor = Bar; // list Bar as the actual constructor

var test = new Bar();
```

### Property Lookup

`protytype.chain`

### Prototype property

The prototype property is used by js to build the prototype chians.

### hashOwnProperty

To check whether an object has a property defined on `itself`.

use in `for in` loops

### for-in loop

```javascript
var foo = {moo: 2};
for(var i in foo) {
    console.log(i); // prints both bar and moo
}

// still the foo from above
for(var i in foo) {
    if (foo.hasOwnProperty(i)) {
        console.log(i);
    }
}
```

## Functions

Declaration vs Expression

### this

call, apply, bind to explicitly set `this`

#### common pitfalls

```javascript
Foo.method = function() {
    function test() {
        // this is set to the global object
    }
    test();
}
```

`that`, `self` trick

```javascript
Foo.method = function() {
    var self = this;
    function test() {
        // Use self instead of this here
    }
    test();
}
```

can also use `bind()`

```
Foo.method = function() {
    var test = function() {
        // this now refers to Foo
    }.bind(this);
    test();
}
```

## Closures and References

only function scope.

### common mistake: closures inside loops

```javascript
for(var i = 0; i < 10; i++) {
    setTimeout(function() {
        console.log(i);  
    }, 1000);
}
```

The anonymous function keeps a reference to `i`. At the time `console.log` gets
called, the `for loop` has already finished, and the value of `i` has been set
to 10.

### avoiding the reference problem

```javascript
for(var i = 0; i < 10; i++) {
    (function(e) {
        setTimeout(function() {
            console.log(e);  
        }, 1000);
    })(i);
}


for(var i = 0; i < 10; i++) {
    setTimeout((function(e) {
        return function() {
            console.log(e);
        }
    })(i), 1000)
}

for(var i = 0; i < 10; i++) {
    setTimeout(console.log.bind(console, i), 1000);
}
```

anonymous wrapper, it gets called immediately with `i`

## The `arguments` Object

It's **not** an array, is an `Object`. It's important to convert it to a real
`Array` in order to use the standard `Array` methods on it.

### Converting to an Array

`Array.prototype.slice.call(arguments);`

Better to use arguments using `apply()`

### Don't use arguments.callee

## Constructors

Any function call that is preceded by the `new` keyword acts as an constructor.

In case of an `return`, the function returns the value only if the return value
is an `Object`

```javascript
function Car() {
    return 'ford';
}
new Car(); // a new object, not 'ford'

function Person() {
    this.someValue = 2;

    return {
        name: 'Charles'
    };
}
new Person(); // the returned object ({name:'Charles'}), not including someValue
```

### Factories

In order to omit the `new` keyword, the constructor has to explicitly return a
value.

```javascript
function Robot() {
    var color = 'gray';
    return {
        getColor: function() {
            return color;
        }
    }
}
```

```javascript
function CarFactory() {
    var car = {};
    car.owner = 'nobody';

    var milesPerGallon = 2;

    car.setOwner = function(newOwner) {
        this.owner = newOwner;
    }

    car.getMPG = function() {
        return milesPerGallon;
    }

    return car;
}
```

Drawbacks:

- uses more memory since the created objects do **not** share the methos on a prototype
- In order to inherit, the factory needs to copy all the methods from another object
or put the object on the prototype.

## Scopes and Namespaces

It is recommended to always use an anonymous wrapper to encapsulate code in its
own namespace. This does not only protect code against name clashes, but it also
allows for better modularization of programs.
