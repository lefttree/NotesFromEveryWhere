# Critical rendering path

## Concepts

- DOM: Document Obejct Model
- CSSOM: CSS Object Model
- DOM和CSSOM都是以Bytes -> characters -> tokens -> nodes -> object model
    + DOM tree的构建过程是一个DFS的过程
- Render Tree
    + DOM, CSSOM combined

> display:none node won't be added into Render Tree, but visibility: hidden will

## Rendering Process

1. Create/Update DOM And request css/image/js：浏览器请求到HTML代码后，在生成DOM的最开始阶段（应该是 Bytes → characters 后），并行发起css、图片、js的请求，无论他们是否在HEAD里。
注意：发起 js 文件的下载 request 并不需要 DOM 处理到那个 script 节点，比如：简单的正则匹配就能做到这一点，虽然实际上并不一定是通过正则：）。这是很多人在理解渲染机制的时候存在的误区。
2. Create/Update Render CSSOM：CSS文件下载完成，开始构建CSSOM
3. Create/Update Render Tree：所有CSS文件下载完成，CSSOM构建结束后，和 DOM 一起生成 Render Tree。
4. Layout：有了Render Tree，浏览器已经能知道网页中有哪些节点、各个节点的CSS定义以及他们的从属关系。下一步操作称之为Layout，顾名思义就是计算出每个节点在屏幕中的位置。
5. Painting：Layout后，浏览器已经知道了哪些节点要显示（which nodes are visible）、每个节点的CSS属性是什么（their computed styles）、每个节点在屏幕中的位置是哪里（geometry）。就进入了最后一步：Painting，按照算出来的规则，通过显卡，把内容画到屏幕上。

Timeline:

- 首屏时间和DomContentLoad事件没有必然的先后关系
- 所有CSS尽早加载是减少首屏时间的最关键
- js的下载和执行会阻塞Dom树的构建（严谨地说是中断了Dom树的更新），所以script标签放在首屏范围内的HTML代码段里会截断首屏的内容。
- 普通script标签放在body底部，做与不做async或者defer处理，都不会影响首屏时间，但影响DomContentLoad和load的时间，进而影响依赖他们的代码的执行的开始时间。

## script position

Q: script tag的位置会影响首屏时间吗？

A: 不影响（如果这里里的首屏指的是页面从白板变成网页画面——也就是第一次Painting），但有可能截断首屏的内容，使其只显示上面一部分。
