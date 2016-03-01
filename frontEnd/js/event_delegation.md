# Event Delegation

## How

It allow you to avoid adding event listeners to specific nodes, instead, the
event listerner is added to the parent. So no need to add/remove if you add/delete
elements.

```html
<ul id="parent-list">
	<li id="post-1">Item 1</li>
	<li id="post-2">Item 2</li>
	<li id="post-3">Item 3</li>
	<li id="post-4">Item 4</li>
	<li id="post-5">Item 5</li>
	<li id="post-6">Item 6</li>
</ul>
```

Something needs to happen when each child element is clicked. Better solution is
to add an event listener to the parent `ul` element, children's events will bubble
up.

`e.target.nodeName` or `e.target.tagName`

```javascript
document.getElementById("parent-list").addEventListener("click", function(e){
    // e.target is the clicked element
    if (e.target && e.target.nodeName == "LI") { // capital
        console.log("List item ", e.target.id.replace("post-"), " was clicked!");
    }
});
```

We can also use `Element.matches` API.

```
if (e.target && e.target.matches("a.classA")) {
    console.log("Anchor element clicked!");
}
```

## References

- [How event delegation works](https://davidwalsh.name/event-delegate)
