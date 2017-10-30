#### 盒子模型

width 和 height 设置的是内容的宽高

块级元素默认的宽度为父元素的宽度,其内容不会超出父元素的宽度,但是内容过多会溢出父元素

修改padding属性会影响盒子的大小,其设置具有对称关系 padding只设置两个值,那么其余两个值
与这两个值是对称的.

margin 指的是两个盒子的外边距 当两个盒子上下外边距合并时,取其中最大的值作为上下间距。

对于两个嵌套关系的块元素,如果父元素没有上内边距及边框,则父元素的上外边距会与子元素的上外
边距发生合并,合并后的外边距为两者中的较大者,即使父元素的上外边距为0,也会发生合并.

嵌套元素的上外边距合并，此时影响的为父元素的样式。

当两个行内元素并列时 设置左右边距两者会叠加不会出现重叠现象。

解决嵌套关系的外边距合并(2种办法)
1.为父元素设置(border)边框 或者 (border-top)上边框
2.为复元素设置一个padding-top:1px;

使用padding让子元素居中:
对置元素添加 background-clip: content-box;
background-clip 属性规定背景的绘制区域
border-box	背景被裁剪到边框盒。
padding-box	背景被裁剪到内边距框。
content-box	背景被裁剪到内容框。

border属性
border-style: solid(实线) dashed(虚线) dotted(小点);

float浮动
设置浮动主要目的是为了让元素同行排列，设置浮动会使元素脱离标准流，在脱离标准流的
同时获得行内块元素的特点。

clearfix清除浮动的办法主引入了伪元素after与before,(引入伪元素必须设置content属性)；
```
.clearfix::after, .clearfix::before{
   content:"";
   line-height:0;
   clear:both;
   display:block;
   visibility:didden;
}
.clearfix{
  z-index:1 //兼容ie
}
```

display属性 (display属性可以让块元素和行内元素任意转换)
display:inline-block属性可以把块元素变成行内块元素不独占一行，但具有块元素的特点
display:bloack 可以把行内元素转换为块元素

visibility与display (隐藏显示属性)
visibility:hidden; 当前元素隐藏，但仍占据页面位置
visibility:visible; 隐藏元素显示

display:none; 当前元素隐藏，但不占据页面位置
display:block; 隐藏元素显示

overflow属性
overflow:hidden; 超出部分隐藏
overflow:scroll; 超出部分会以滚动条形式出现，但是未超出扔出现滚动条
overflow:auto; 根据当前内容多少判断是否出现滚动条(比较智能)。

position属性
当前元素设置了absolute，但是除了body并没有其余的祖先元素，那么其绝对定位
是相对于body的。

当前元素设置了absolute，但是其父元素(祖先元素)都没有设置过position，那么
其绝对定位是相对于body的。

当前元素设置了absolute，但是其父元素(某一个祖先元素)设置了
position:(absolute, relative都可以)，那么其绝对定位是相对
于最近设置的position的祖先元素。

position:fixed; 相对于浏览器的可视窗口进行固定。

嵌套关系的父子元素，让子元素居中显示在父元素内的方法：
1.在知道父元素宽高的条件下，对子元素设置margin-top与margin-left调整，可以使
子元素居中。
2.在知道父元素宽高的条件下，对父元素设置padding-top与padding-left，但是在设
置的同时，要对父元素的宽高进行更改，padding会填充父元素大小，设置的数值要在其本
身的宽高里减去。
3.在知道父元素宽高的条件下，使用定位的办法对父元素设置position:relative，子元
素设置position:absolute或relative都可以，调节top与left值就可以使子元素居中。
4.在知道父元素宽高的条件下，对子元素设置一个backgrounf-clip：content-box的属性，
然后调节padding就可以。
5.如果在不知道父元素宽高的情况下的时候，使用定位的办法对父元素设置position:relative,
子元素设置绝对定位(position:absolute);调节top:50%与left:50%,这个百分比%是相对父
元素的位置，这之后在调节margin-top与margin-left减去自身的宽高的一半。

position的层级问题(z-index);
z-index只对设置了position的元素起作用。
在默认的情况下，设置定位的元素层级都比普通的元素层级要高，都是 ≥ 0，≤1的数，z-index
可以设置负值。

设置了position的元素，默认情况下，元素的层级也是逐渐增大的，从0开始无限接近1
浮动在一行的所有元素，默认情况下，元素的层级从左到右逐渐增大，从0开始无限接近1

li标签可以直接background添加图片，在background-position位置调 left center
就可以使图片位于开头位置

使用 i 标签添加小图片的时候要先将 i 标签转换为行内块元素 然后在进行设置

outline:none;可以直接写在样式内。对于input的标签来说

css Hack
不同的浏览器对css的解析结果是不同的，因此会导致相同的的css输出页面效果不同，这就需要css
Hack 来解决浏览器的兼容性问题。而这个针对不同的浏览器写不同的css代码的过程，就叫CSS Hack。

CSS Hack常见的有三种模式：CSS属性Hack、CSS选择符Hack以及IE条件注释，Hack主要针对IE浏览器。

CSS 三栏布局的几种方法:

1.左右两边设置浮动(左浮和右浮动)，然后中间部分设置width:100%即可。

2.左右两边设置绝对定位(左边为left:0;右边为right:0)，中间部分width:100%;需要设置一个box-sizing:border-box;然后在设置一个与左右宽度相符
的padding就可以。

3.写一个大的div(box),对box设置display:flex;然后box里面左右两边设置flex-shrink:0;中间部分设置width:100%即可。

