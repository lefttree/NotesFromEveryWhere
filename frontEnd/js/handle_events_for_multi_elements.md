# Handling events for many elements

1. Terrible solution

add event listeners for all the elements

2. good solution

- have a parent element
- add only one event listener to it

![pic](https://www.kirupa.com/html5/images/DOM_tree_multiple_solution_72.png)

```javascript
var theParent = document.querySelector("#theDude");
theParent.addEventListener("click", doSomething, false);
 
function doSomething(e) {
    if (e.target !== e.currentTarget) {
        var clickedItem = e.target.id;
        alert("Hello " + clickedItem);
    }
    e.stopPropagation(); // stop the propagation
}
```

## Reference

- [link](https://www.kirupa.com/html5/handling_events_for_many_elements.htm)
