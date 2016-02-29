# Compose Function

## functions as building blocks

Javascript treats functions as first class objects, that is they can be created
and modified dynamically and passed as data to other functions and objects.

Example

```javascript
var  alertPower = alert.compose(Math.pow);
alertPower(9,8); //alert shows 43046721

var  roundedSqRoot = Math.round.compose(Math.sqrt);
roundedSqRoot(28); //5
```

The compose function allows us to define a new function based on 2 existing(
anonymous) functions.

`myFunction = function1.compose(function2);`

when we call `myFunction(myArgs);`, function2 gets invoked with myArgs and the
result is passed to the invocation of function1.

**compose function**

```javascript
Function.prototype.compose = function(argFunction) {
    var invokingFunction = this;
    return function() { // return a function
        return invokingFunction.call(this, argFunction.apply(this, arguments));
    }
}
```


## References

- [compose function](https://javascriptweblog.wordpress.com/2010/04/14/compose-functions-as-building-blocks/)
