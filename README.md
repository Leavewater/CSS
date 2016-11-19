# CSS学习笔记
##float
> 特性

- 包裹性
  - 元素block水平化
- 破坏性
  - 去除button之间的空格

> IE7兼容性

1. 含clear的浮动元素包裹不正确的问题；
2. 浮动元素倒数2个莫名垂直间距问题；
3. 浮动元素最后一个字符重复问题；
4. 浮动元素楼梯排列问题；
5. 浮动元素和文本不在同一行的问题；

- 清除浮动

```
.clearfix:after { content: ''; display: table; clear: both; }
.clearfix { *zoom: 1; }
```
##padding

>对于块状元素设置padding 

- pading值过大，一定会影响尺寸
- width不是auto,padding影响尺寸
- width为auto,或border-size为border-box,同时padding值不过大，不影响尺寸
- 设置padding:50%可形成正方形

>对于水平inline元素

- 水平padding影响尺寸，垂直padding不影响尺寸（但是会影响背景色占据空间）
- 百分比值相对于宽度，默认的高度宽度细节有所差异，padding会断行
- 设置padding:50%形成正方形的前提是font-size:0(因为inline的垂直padding会出现空白)

- （例子）高度可控分割线：

```
登陆<span></span>注册
span{
			padding: 16px 6px 2px;
			margin-left: 12px;
			border-left: 2px solid;
			font-size: 0;
		}
```
> padding没有负值

- padding百分比是相对于宽度计算的

>padding值

- 所有浏览器input/textarea输入内置padding
- 所有浏览器button按钮内置padding
- 部分浏览器select下拉内置padding,如firefox、IE8+可以设置padding
- 所有浏览器radio/checkbox单选复选框没有内置padding
- button按钮的padding设置  
 在firefox设置为0时仍然有padding  
 解决方案：button::-moz-focus-inner {padding:0; }
 在IE7下，文字越多，左右padding越大
 解决方案：overflow:visible;
- padding与高度计算不兼容  
 在IE7、firefox下，高度计算不一样，所以一般用a标签模拟button  
 如果要用来提交，则
 
 ```
 <button id="btn"></button>
 <label for="btn">按钮</label>
 label{
  display: inline-block;
  line-height:20px;
  padding:10px;
 }
 button:z-index:-1或者绝对定位外
 ```

##margin
> 元素尺寸

-  可视尺寸(clientWidth)
  - 适用于没有设定width/height的普通block水平元素（不包括浮动、绝对定位元素、inline、table-cell...）；
  - 只适用于水平方向尺寸
-  占据尺寸(outerWidth)
  - block水平和inline-block水平元素均适用
  - 与有没有设定width/height值无关
  - 适用于水平方向和垂直方向

> 定宽高居中

`
  .father{
	height: 200px;
	position: relative;
}
.son{
	position: absolute;
	top: 0;
	bottom: 0;
	left: 0;
	right: 0;
	width: 500px;
	height: 100px;
	margin: auto;
}
`

> 百分比值

- 普通元素margin的百分比值都是相对于容器的宽度计算的
- 绝对定位元素margin的百分比值是相对于第一个定位祖先元素的宽度计算的

> margin重叠通常特性

1. block水平元素（不包括float和absolute元素）
2. 不考虑writing-mode,只发生在垂直方向

>重叠3种情形

1. 相邻的兄弟元素
2. 父级第一个/最后一个子元素（重叠条件）
  1. margin-top重叠
    - 父元素非块状格式化上下文元素（overflow:hidden等）
    - 父元素没有border-top值
    - 父元素没有padding-top值
    - 父元素与第一个元素间没有inline元素分割（&nbsp）
  2. margin-bottom重叠
    - 父元素非块状格式化上下文元素
    - 父元素没有border-bottom值
    - 父元素没有padding-bottom值
    - 父元素与最后一个元素间没有inline元素分割
    - 父元素没有height、min-height、max-height限制
3. 空block元素margin重叠条件
  - 元素没有border设置
  - 元素没有padding设置
  - 里面没有inline元素
  - 没有height或min-height
4. 重叠的计算规则
  - 正正取大值
  - 正负值相加
  - 负负取最负
  

> margin负值

- 如果浮动元素有margin负值，会重叠到上一个浮动元素上面。
  
> margin失效情形

- inline水平元素的垂直margin无效
  - 前提是inline是非替换元素
  - 正常书写模式（不是writing-mode或者direction）
  - margin重叠
- display:table-cell与margin
  - table-cell与table-row等声明的margin无效
- 绝对定位与margin
  - 绝对定位元素非定位的margin值“无效”-----指的是绝对定位的margin值一直是有效的  
    只是不像普通元素那样，可以和兄弟元素作用（父元素设置relative，就能体现出来）
- 鞭长莫及导致的margin无效
- 内联特性导致的margin无效
  margin负值小到一定程度就失效了，（如img）原因是内联元素的排版，要与文字对齐特性限制了
- margin-start
  - 正常流情况下margin-start与margin-left作用相等，两者重叠不累加；
  - 如果水平流是从右向左的，margin-start相当于margin-right;
  - 垂直流情况下margin-start相当于margin-top

##absolute
>特性

- 包裹性
- 破坏性
- 越独立越强大
  - 没有relative的情况下可以超越overflow的限制
  - absolute与float类似，relative与clear类似
  
>在不使用具体定位值的情况下（包括auto）

- 脱离文档流
- 去浮动（浮动不起效）
- 位置跟随（原来什么位置绝对定位后就是什么位置）
  - ！！绝对定位元素与前面的同辈元素之间不能有空格（可以用<!---->&nbsp代替），否则会错位
  - 例子：1.图片、图标覆盖。2.下拉框提示
  - chrome浏览器下绝对定位后再改变display就不会再渲染（一次渲染？）
  - ie7浏览器下永远display:inline-block化（解决：套一个div）
- !配合margin精确定位（可用负值）兼容ie6

>技巧

- left,right等对立出现时会拉伸
- 如height:100%;width:100%;相当于absolute;top:0;left:0;right:0;bottom:0;(ie7+)
- 容器无需固定 width/height值，内部元素亦可拉伸；
  容器拉伸，内部元素支持百分比width/height值；
- 如果拉伸和width/height尺寸同时存在  
  width/height设置的尺寸> left/top/right/bottom拉伸的尺寸
 
>与z-index的关系

-  如果只有一个绝对定位元素，自然不需要z-index，自动覆盖普通元素；
- 如果两个绝对定位，控制DOM流的前后顺序达到需要的覆盖效果，依然无z-index；
- 如果多个绝对定位交错，非常非常少见，z-index：1控制；
- 如果非弹框类的绝对定位元素z-index>2, 必定z-index冗余，请优化！


##z-index
>特性

- 一般较大的会覆盖较小的
- 支持负值
- 支持CSS3 animation动画
- CSS2.1中需要和定位元素配合使用

##relative
>部分特性

- 相对自身
- 无侵入
- 实现拖拽
- left、right、top、bottom对立时，取left、top

>计算规则

- 后面覆盖前面的
- 值大的在上面

>限制定位

- 限制top、left、right、bottom

>限制层级

- 当相对定位设置具体的z-index值后  
  绝对定位的z-index值不起作用且和相对定位的z-index值相等
  
- 当z-index发生嵌套时：  
  祖先优先原则（前提z-index的值必须为数值）

>层叠上下文

- 优先级别：用户 > 层叠上下文 > 嵌套
- 页面根元素
- z-index为数值的定位元素
- 其它属性。。。

>层叠上下文特性

- 层叠上下文可以嵌套，组成一个可以分层次的层叠上下文
- 每个层叠上下文和兄弟元素独立：当进行层叠变化或渲染时，只考虑后代元素
- 每个层叠上下文是自成体系的：当元素的内容被层叠后，整个元素被认为是在父层的层叠顺序中
  
> 层叠水平

- 发生在层叠上下文中

- 后面覆盖前面
- 值大的覆盖值小的

>限制超越overflow

- 在没有设置relative的情况下设置overflow:hidden对绝对定位元素不起作用 

>与fixed的关系

- 只能限制fixed的层级

>提高元素的层叠上下文 "Madoko reference manual"

##overflow

- overflow-x和overflow-y(IE8+);
  - overflow-x和overflow-y值相等，则等同于overflow
  - overflow-x和overflow-y值不相等，其中一个设置了hidden、auto、scroll,另一个是visible，则另一个重置为auto
  
> 起作用的前提

- 非display:inlnie水平
- 对应方位的尺寸限制width/height/max-width/max/height/absolute限制  
- 对应单元格td等，还需要table为table-layout:fixed状态才行
- ie7下button元素文字越多左右padding越大（解决方案只要加上overflow:visible就行）

> 各个浏览器滚动条长度、外表不一样

> ie7子元素100%会出现滚动条

> 出现条件：

- 值为auto/scroll，html(!!非body)、textarea天生自带滚动条
- ie7默认html(overflow-y:hidden),ie8默认html(overflow:auto)

> js与滚动高度

- chrome浏览器下：document.body.scrollTop;
- 其它浏览器下：document.documentElement.scrollTop;
- 因此滚动高度=document.body.scrollTop||document.documentElement.scrollTop

> padding-bottom缺失

- chrome浏览器下，容器的padding-bottom不会缺失，其它浏览器下会缺失

> 滚动条会占用浏览器的宽度和高度

- 一般各浏览器的滚动条宽度均为17px

> 水平居中跳动问题修复

1. html(overflow:scroll)ie8以下
2. container(padding-left:calc(100vw-100%))

>触发bfc:

- auto、scroll、hidden
- 清除浮动的影响（ie7+）
- 避免margin穿透问题
- 两栏自适应布局（可以给浮动的加margin）
  ```
    .cell{
      display:table-cell;width:2000px;
      *display:inline-block;*width:auto;(IE7伪特性)
    }
    ```
- overflow:hidden;自适应，但溢出不可见，限制应用场景
- float+float,包裹性+破坏性，无法自适应，块状浮动布局
- absolute，脱离文档流
- display:inline-block,包裹性，无法自适应；ie6,ie7不识别
- table-cell，包裹性，但天生无溢出特性，绝对宽度也能自适应

> 失效

- 当overflow在绝对定位元素及其包含块（含position:absolute/fixed/relative声明的父级元素,没有则默认body）之间的时候

> 避免失效方法

- overflow元素自身为包含块
- overflow元素的子元素为包含块（子元素自身加一个div，relative）
- 任意合法transform声明当做包含块
  - overflow元素自身transform,只有ie9+/firefox支持
  - overflow子元素transform,都支持
  

> resize属性

- 元素的overflow属性不能是visible
- 拖拽区域大小17px*17px

> ellipsis文字溢出省略
- white-space:nowrap;overflow:hidden;

> 锚点、锚链接

- 容器可滚动
- 锚元素在容器内

>锚点定位的本质
- 改变容器的滚动高度

> 锚点定位的触发

1. url地址中的锚链与锚点元素；
2. 可focus的元素处于focus状态

> 选项卡技术（适用于单页应用）

