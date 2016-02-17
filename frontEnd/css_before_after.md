# CSS before after

- `::before` can insert pseudo-element before an element
- `::after` can insert pseudo-element after an element

```html
<style>
    p:before{
        content: "H"  /*:before和:after必带技能，重要性为满5颗星*/
    }
    p:after{
        content: "d"  /*:before和:after必带技能，重要性为满5颗星*/
    }
</style>
<p>ello Worl</p>
```

## Example with message box

### Triangle

```html
.triangle{
      width: 0;
      height: 0;
      border:50px transparent solid; /*这里我们将元素的边框宽度设置为50px，transparent表示边框颜色是透明的，solid表示边框是实线的*/
      border-top-color: black;  /*这里我们仅将上边框的颜色设置为黑色，众所周知，css后面的样式代码会覆盖之前的相同的样式代码，至于其他三边的还是透明色*/
      /*border-bottom-color: black; /*这里设置底部边框色为黑色*/
      border-left-color: black;  /*这里设置左边边框色为黑色*/
      border-right-color:black*/ /*这里设置右边边框色为黑色*/
}
<div class="triangle"></div>
```

我们就会看到一个在底部的方向向上的三角形

### message box

```css
.test-div{
    position: relative;  /*日常相对定位*/
    width:150px;
    height: 36px;
    border:black 1px solid;
    border-radius:5px;
    background: rgba(245,245,245,1)
}
/* before and after at the same position */
.test-div:before,.test-div:after{
    content: "";  /*:before和:after必带技能，重要性为满5颗星*/
    display: block;
    position: absolute;  /*日常绝对定位*/
    top:8px;
    width: 0;
    height: 0;
    border:6px transparent solid;
}
/* before is moved to left 11px, and z-index is 1, will cover after*/
.test-div:before{
    left:-11px;
    border-right-color: rgba(245,245,245,1);
    z-index:1
}
/* after is moved to right 12px, z-index is 0*/
.test-div:after{
    left:-12px;
    border-right-color: rgba(0,0,0,1);
    z-index: 0
}
```

## Beautiful hover effect

- [hover effect ideas](http://tympanus.net/Development/HoverEffectIdeas/index.html)
