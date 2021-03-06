## 1.CSS布局

##### - 什么是网页的布局方式?

​		网页的布局方式其实就是指浏览器是如何对网页中的元素进行排版的

##### - 标准流(文档流/普通流)排版方式

​		标准流(文档流/普通流)
​        	-标准流(文档流/普通流)处在网页的最底层，它表示的是一个页面中的位置，我们所创建的元素默认都处在标准流(文档流/普通流)中。
​        	-元素在标准流(文档流/普通流)中的特点
​        		块元素
​            		1.块元素在标准流(文档流/普通流)中会独占一行，块元素会自上向下排列。
​            		2.块元素在标准流(文档流/普通流)中默认宽度是父元素的100%
​            		3.块元素在标准流(文档流/普通流)中的高度默认被内容撑开
​        		内联元素
​            		1.内联元素在标准流(文档流/普通流)中只占自身的大小，会默认从左向右排列，如果一行中不足以容纳所有的内联元素，则换到下一行，继续自左向右。
​            		2.在标准流(文档流/普通流)中，内联元素的宽度和高度默认都被内容撑开

​    	1.其实浏览器默认的排版方式就是标准流的排版方式
​    	2.在CSS中将元素分为三类, 分别是块级元素/行内元素/行内块级元素
​    	3.在标准流中有两种排版方式, 一种是垂直排版, 一种是水平排版
​        	垂直排版, 如果元素是块级元素, 那么就会垂直排版
​        	水平排版, 如果元素是行内元素/行内块级元素, 那么就会水平排版
   	 4.如果希望块元素在页面中水平排列，可以使块元素脱离标准流(文档流/普通流)，使用float来使元素浮动，从而脱离标准流(文档流/普通流)
​        	可选值：
​            	none，默认值，元素默认在标准流(文档流/普通流)中排列
​            	left，元素会立即脱离标准流(文档流/普通流)，向页面的左侧浮动
​            	right，元素会立即脱离标准流(文档流/普通流)，向页面的右侧浮动



​            	当为一个元素设置浮动以后（float属性是一个非none的值），元素会立即脱离标准流(文档流/普通流)，元素脱离标准流(文档流/普通流)以后，它下边的元素会立即向上移动，那么这个时候前面一个元素就会盖住后面一个元素。

​        	    元素浮动以后，会尽量向页面的左上或者是右上漂浮，直到遇到父元素的边框或者其他的浮动元素
​            	如果浮动元素上边是一个没有浮动的块元素，则浮动元素不会超过块元素。
​            	浮动的元素不会超过他上边的兄弟元素，最多最多一边齐。

## 2.浮动流排版方式

​		1.浮动流是一种"半脱离标准流"的排版方式
​        2.浮动流只有一种排版方式, 就是水平排版. 它只能设置某个元素左对齐或者右对齐

##### - 浮动元素字围现象

​		浮动元素不会挡住没有浮动元素中的文字, 没有浮动的文字会自动给浮动的元素让位置,这个就是浮动元素字围现象

   	 -注意点:
   	    	1.浮动流中没有居中对齐, 也就是没有center这个取值
   	    	2.在浮动流中是不可以使用margin: 0 auto;

​    	-特点:
​        	1.在浮动流中是不区分块级元素/行内元素/行内块级元素的
​        	无论是块级元素/行内元素/行内块级元素都可以水平排版
​        	2.在浮动流中无论是块级元素/行内元素/行内块级元素都可以设置宽高
​        	3.综上所述, 浮动流中的元素和标准流中的行内块级元素很像

##### - 高度塌陷

​		在文档流中，父元素的高度默认是被子元素撑开的，也就是子元素多高，父元素就多高。
​    	但是当为子元素设置浮动以后，子元素会完全脱离文档流，此时将会导致子元素无法撑起父元素的高度，		导致父元素的高度塌陷。
​    	由于父元素的高度塌陷了，则父元素下的所有元素都会向上移动，这样将会导致页面布局混乱。
​    	-解决高度塌陷
​        	1.所以在开发中一定要避免出现高度塌陷的问题,我们可以将父元素的高度写死，以避免塌陷的问题出			现，但是一旦高度写死，父元素的高度将不能自动适应子元素的高度，所以这种方案是不推荐使用的。
​        	2.可以直接在高度塌陷的父元素的最后，添加一个空白的div，由于这个div并没有浮动，所以他是可以			撑开父元素的高度的，然后在对其进行清除浮动，这样可以通过这个空白的div来撑开父元素的高度，			基本没有副作用。
​        	使用这种方式虽然可以解决问题，但是会在页面中添加多余的结构。
​            		clear属性取值:
​                		none: 默认取值, 按照浮动元素的排序规则来排序(左浮动找左浮动, 右浮动找右浮动)
​                		left: 不要找前面的左浮动元素
​                		right: 不要找前面的右浮动元素
​                		both: 不要找前面的左浮动元素和右浮动元素
​        	3.通过after伪类
​        			可以通过after伪类向元素的最后添加一个空白的块元素，然后对其清除浮动，这样做和添加一个					div的原理一样，可以达到一个相同的效果，而且不会在页面中添加多余的div，这是我们最推荐使					用的方式，几乎没有副作用。
​        					.clearfix::after{
​            					/*添加一个内容*/
​            					content: "";
​           					/*转换为一个块元素*/
​            					display: block;
​           					 /*清除两侧的浮动*/
​            					clear: both;
​        					}

##### - CSS两列布局以及三列布局

##### 两列布局：左边定宽，右边自适应

```html
.left {
    float: left;
    width: 300px;
    background-color: blue;
}
.right {
    overflow: auto;
    background-color: red;
}

<div class="left">左边定宽</div>
<div class="right">右边自适应</div>
```

##### - BFC

MDN的定义：

> 块格式化上下文（Block Formatting Context，BFC） 是Web页面的可视化CSS渲染的一部分，是块盒子的布局过程发生的区域，也是浮动元素与其他元素交互的区域。

> BFC(block formatting context)块级格式化上下文，它是页面中的一块渲染区域，并且有一套属于自己的渲染规则，它决定了元素如何对齐内容进行布局，以及与其他元素的关系和相互作用。 当涉及到可视化布局的时候，BFC提供了一个环境，HTML元素在这个环境中按照一定规则进行布局

简短的总结：**BFC是一个独立的布局环境，BFC内部的元素布局与外部互不影响**

##### BFC的布局规则

1. 内部的Box会在垂直方向一个接着一个地放置。
2. Box垂直方向上的距离由margin决定。属于同一个BFC的两个相邻的Box的margin会发生重叠。
3. 每个盒子的左外边框紧挨着包含块的左边框，即使浮动元素也是如此。
4. BFC的区域不会与float box重叠。
5. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之亦然。
6. 计算BFC的高度时，浮动子元素也参与计算。

##### 哪些元素会生成BFC

1.根元素

2.float属性不为none

3.position 为absolute或fixed

4.display为inline-block table-cell table-caption flex inline-flex

5.overflow不为visible　

##### BFC的作用

- 解决浮动元素令父元素高度坍塌的问题

方法：给父元素开启BFC

原理：计算BFC的高度时，浮动子元素也参与计算

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    /* 父元素 */
    .div1 {
      width: 1000px;
      border: 10px solid red;
      /* BFC */
      overflow: hidden;
    }
    /* 子元素 */
    .div2 {
      width: 200px;
      height: 400px;
      background-color: blue;
      float: left;
    }
  </style>
</head>
<body>
  <div class="div1">
    <div class="div2"></div>
  </div>
</body>
</html>
```

- 两栏自适应布局

方法：给固定栏设置固定宽度，给不固定栏开启BFC。

原理：BFC的区域不会与float box重叠

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    .left {
      float: left;
      width: 300px;
      background-color: blue;
    }
    .right {
      /* 
        overflow:auto;(隐藏溢出的内容)利用BFC
      */
      overflow: auto;
      background-color: red;
    }
  </style>
</head>
<body>
  <div class="left">左边定宽</div>
  <div class="right">
    右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应右边自适应
  </div>
</body>
</html>
```



##### 三列布局：两边定宽，中间自适应

```html
*{
  margin: 0;
  padding: 0;
}
.left,.right {
  width: 200px;
  height: 200px;
  background-color: #999;
}
.left {
  float: left;
}
.right {
  float: right;
}
.center {
  /* 中间模块空出左右距离，设置浮动 */
  margin: 0 200px;
  height: 300px;
  background-color: #f00;
}

<div class="left">left</div>
<div class="right">right</div>
<div class="center">center</div>
```

