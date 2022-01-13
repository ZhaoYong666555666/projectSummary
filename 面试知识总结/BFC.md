## BFC的理解

> 块级格式化上下文，它是指一个独立的块级渲染区域，至于Block-level BOX参与，
>该区域拥有一套渲染规则来约束块级盒子的布局，且与外部区域无关

@ 理解成以下三点即可
- 1 块级盒子上下文
- 2 它有一套独立的块级渲染区域 
- 3 与区域外部无关

## 从一个现象说起
- 一个盒子不设置height，当内容子元素都浮动的时候，无法撑起自身
- 这个盒子没有形成BFC

## 如何创建BFC
- 方法一：float的值不是none
- 方法二：position的值不是static或者relative
- 方法三：display的值是inline-block,flex,inline-flex
- 方法四：overflow:hidden;  // 最优方案

## BFC的其他作用
- BFC可以取消盒子margin塌陷，使得父元素盒子形成BFC
- BFC可以阻止元素被浮动元素覆盖
