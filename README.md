# CSS学习笔记
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

>提高元素的层叠上下文
