# CSS Animation

An animation lets an element gradually change from one style to another. To use
CSS3 animation, you must first specify some keyframes for the animation. Keyframes
hold what styles the element will have at certain times.

To get an animation to work, you must bind the animation to an element.

**Example**

```css
@keyframes example {
    from {background-color:red;}
    to {background-color: yellow;}
}

div {
    width: 100px;
    height: 100px;
    background-color: red;
    animation-name: example;
    animation-duration: 4s;
}
```

without `animation-duration`, it will have no effect.

Can also use percentage

```css
@keyframes example {
    0%   {background-color: red; left:0px; top:0px;}
    25%  {background-color: yellow; left:200px; top:0px;}
    50%  {background-color: blue; left:200px; top:200px;}
    75%  {background-color: green; left:0px; top:200px;}
    100% {background-color: red; left:0px; top:0px;}
}
```

## Properties

- animation-delay
- animation-direction
- animation-duration
- animation-iteration-count
- animation-name
- animation-play-state
- animation-timing-function
- animation-fill-mode


### Delay an Animation

`animation-delay: 2s;`

### how many times

`animation-iteration-count: 3;`

### direction

- `animation-direction:reverse`
- `animation-direction:alternate`

## Advantages over traditional script-driven animation techniques:

1. They're easy to use for simple animations
2. The animations run well, even under moderate system load. The rendering engine
can use **frame-skipping** and other techniques to keep the preformance as smooth
as possible
3. Letting the browser control the animation sequence lets the browser optimize
performace and efficiency by, for exmaple, reducing the update frequency of animations
running in tabs that aren't currently visible.

## References

- [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations/Using_CSS_animations)
- [w3c](http://www.w3schools.com/css/css3_animations.asp)
- [Introduction to CSS Animation](http://webdesign.tutsplus.com/tutorials/a-beginners-introduction-to-css-animation--cms-21068)

... `check out w3school`
