# repaint & reflow

- repaint: 如果某些操作影响了DOM元素的可见性，但没有影响布局，就会repaint
- reflow: 让browser重新计算位置和尺寸大小。

触发reflow:

- 添加、删除和修改可见的 DOM 元素
- 添加、删除和修改部分 CSS 样式，比如修改元素的宽度，会影响其相邻元素的布局位置
- CSS3 动画和过渡效果
- 使用 offsetWidth 和 offsetHeight。这种情境很诡异，读取一个元素的 offsetWidth 和 offsetHeight 属性会触发回流
- 用户行为，比如鼠标悬停、输入文本、调整窗口大小、修改字体样式等等

## Best Practices

## References

- [提高web性能的技巧](http://web.jobbole.com/84999/)
