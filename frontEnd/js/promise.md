# Promise

The Promise object is used for deferred and asynchronous computations. A Promise
represents an operation that hasn't completed yet, but is expected in the future.

`new Promise(function(resolve, reject){ ... });`

A Promise is in one of these states:

    - pending: initial state, not fulfilled or rejected.
    - fulfilled: meaning that the operation completed successfully.
    - rejected: meaning that the operation failed.

## how to create a promise

```javascript
var promise = new Promise(function(resolve, reject) {
  // do a thing, possibly async, then…

  if (/* everything turned out fine */) {
    resolve("Stuff worked!");
  }
  else {
    reject(Error("It broke"));
  }
});
```

## how to use that promise

```javascript
promise.then(function(result) {
  console.log(result); // "Stuff worked!"
}).catch(function(err) {
  console.log(err); // Error: "It broke"
});
```

## References

- [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [promises on html5 rocks](http://www.html5rocks.com/en/tutorials/es6/promises/)
- [promises with exmaples](https://www.toptal.com/javascript/javascript-promises)
