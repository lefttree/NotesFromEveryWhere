# Currying Function

Currying allows you to easily create custom functions by **partially invoking**
an existing function.

Generally, curry returns a copy of the invoking function, with its **first n
arguments pre-assigned** with the arguments passed by the curry invocation.

example

```javascript
var add = function(a, b) {
    return a + b;
}
var addTen = add.curry(10);
addTen(20); // 30
```

## Code

Curry function doesn't exist in native javascript, but it's easy to write one.

>function `arguments` is not a true array, so we need to convert it into array.

```javascript
function toArray(enum) {
    // convert enum to array
    return Array.prototype.slice.call(enum);
}

Function.prototype.curry = function() {
    if(arguments.length < 1) {
        return this;
    }

    var __method = this;
    var args = toArray(arguments); // arguments for curry invocation
    return function() {
        return __method.apply(this, args.concat(toArray(arguments)));
    };
}
```

As the logic gets complicated, it's more useful.

```javascript
var converter = function(ratio, symbol, input) {
    return [(input*ratio).toFixed(1),symbol].join(" ");
}
 
var kilosToPounds = converter.curry(2.2,"lbs");
var litersToUKPints = converter.curry(1.75, "imperial pints");
var litersToUSPints = converter.curry(1.98, "US pints");
var milesToKilometers = converter.curry(1.62, "km");
 
kilosToPounds(4); //8.8 lbs
litersToUKPints(2.4); //4.2 imperial pints
litersToUSPints(2.4); //4.8 US pints
milesToKilometers(34); //55.1 km
```

## References

- [currying function](https://javascriptweblog.wordpress.com/2010/04/05/curry-cooking-up-tastier-functions/)
