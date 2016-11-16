# CSS学习笔记
##padding

>对于块状元素设置padding 

- pading值过大，一定会影响尺寸
- width不是auto,padding影响尺寸
- width为auto,或border-size为border-box,同时padding值不过大，不影响尺寸
- 设置padding:50%可形成正方形

>对于水平inline元素

- 水平pingging影响尺寸，垂直padding不影响尺寸（但是会影响背景色占据空间）
- 百分比值相对于宽度，默认的高度宽度细节有所差异，padding会断行
- 设置padding:50%形成正方形的前提是font-size:0(因为inline的垂直padding会出现空白)

-（例子）高度可控分割线：

```css
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

##margin
##absolute
##relative
