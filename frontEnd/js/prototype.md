# Understanding Prototype

## 2 concepts

2 concepts with `prototype` in javascript:

1. Every javscript `function` has a `prototype property`, and you attach properties
and methods on this prototype property when you want to implement *inheritance*.

**inheritance**, add methods and properties to make them available to instances
of that function.

2. `prototype attribute`, think of this as a characteristic of the `object`, it
tells the object's "parent".

It refers to the prototype object, and is auto set when you create a new object.

```javascript
function PrintStuff(myDocuments) {
    this.documents = myDocuments;
}

// add the print() method to PrintStuff prototype property
PrintStuff.prototype.print = function() {
    console.log(this.documents);
}

// create a new object with the PrintStuff() constructor
var newObj = new PrintStuff("I am a new Object and I can print.");

// new
newObj.print();

console.log(PrintStuff.prototype) // PrintStuff{}
console.log(newObj.prototype) // undefined
console.log(newOBj.__proto__) // PrintStuff{}
console.log(PrintStuff.__proto__) // function (){}
```

Also note that the `__proto__` “pseudo” property contains an object’s prototype 
object (the parent object it inherited its methods and properties from).

## constructor

A function used for initializing new objects, and use the `new` keyword to call
the constructor.

```javascript
function Account() {};
var userAccount = new Account();
userAccount.constructor; // Account()
```

## Object creation

### Created with `new Object()` or Object Literal

inherits from `Object.prototype`

### Created with a Constructor function

`var userAccount = new Account();`

Inherits from that constructor, prototype attribute is `Account.prototype`

### In ECMAScript 5, you can use Object.create()

It allows you to set the new object's prototype object.

## Why prototype important, when to use?

1. Prototype-based inheritance

In javascript, you implement inheritance with the prototype preperty.

```javascript
function Plant() {
    this.country = "Mexico";
    this.isOrganic = true;
}

Plant.prototype.showNameAndColor =  function () {
    console.log("I am a " + this.name + " and my color is " + this.color);
}

function Fruit(fruitName, fruitColor) {
    this.name = fruitName;
    this.color = fruitColor;
}

// set the Fruit's prototype to Plant's constructor, thus inheriting all of
// Plant.prototype methods and properties
Fruit.prototype = new Plant();
```

2. Prototype Attribute: Accessing Properties on Objects

prototype chain

## References

- [js prototype in plain lang](http://javascriptissexy.com/javascript-prototype-in-plain-detailed-language/)
