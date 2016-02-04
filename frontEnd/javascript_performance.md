# Javascript Performance

## Reduce Activity in Loops

`for (i = 0; i < arr.length; i++){}`

move `arr.length` out of the loop

## Reduce DOM Access

Accessing the HTML DOM is very slow. If you expect to access a DOM element
several times, access it once, and use it as a `local variable`.

## Reduce DOM Size

## Avoid Unnecessary Variables

```javascript
var fullName = firstName + " " + lastName;
document.getElementById('demo').innerHTML = fullName;
```

can be replaced with:

```javascript
document.getElementById("demo").innerHTML = firstName + " " + lastName
```

## Delay Javascript Loading

Putting scripts at the bottom of page body.

Can also add by code:

```javascript
<script>
window.onload = downScripts;

function downScripts() {
    var element = document.createElement("script");
    element.src = "myScript.js";
    document.body.appendChild(element);
}
</script>
```

## Avoid Using `with`

--------------------

# Google Optimizing Javascript Code

https://developers.google.com/speed/articles/optimizing-javascript

## Working with Strings

String concatenation causes major problems with IE 6 and 7 garbage collection
performance. Use `join()` instead.

## Building strings with portions coming from helper functions

Build up long strings by passing string builders(either an array or a helper class)
into functions, to avoid temporary result strings.

## Defining Class methods

This is inefficient:

```javacript
baz.Bar = function() {
  // constructor body
  this.foo = function() {
    // method body
  };
}
```

Preferred:

```javascript
baz.Bar = function() {
  // constructor body
};

baz.Bar.prototype.foo = function() {
  // method body
};
```

## Initializing instance variables

Place instance variable declaration/initialization on the `prototype` for instance
variables with `value type` (rather than `reference type`) initialization values.

```javascript
foo.Bar = function() {
  this.prop3_ = [];
};

foo.Bar.prototype.prop1_ = 4;

foo.Bar.prototype.prop2_ = true;

foo.Bar.prototype.prop4_ = 'blah';
```

## Avoiding pitfalls with closures

```javascript
function setupAlertTimeout() {
  var msg = 'Message to alert';
  window.setTimeout(function() { alert(msg); }, 100);
}
```

is slower than:

```javascript
function setupAlertTimeout() {
  window.setTimeout(function() {
    var msg = 'Message to alert';
    alert(msg);
  }, 100);
}
```

which is slower than:

```javascript
function alertMsg() {
  var msg = 'Message to alert';
  alert(msg);
}

function setupAlertTimeout() {
  window.setTimeout(alertMsg, 100);
}
```

