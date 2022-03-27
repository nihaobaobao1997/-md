# css盒模型
## 标准盒模型（content-box）、
1. 组成：content-padding-border-margin
2. 宽高范围：content
## IE盒模型（border-box）
1. 组成：content-padding-border-margin
2. 宽高范围：content+padding-border
## 可以通过 box-sizing 选择用哪一种
1. box-sizing: content-box ：标准盒模型（默认值）。
2. box-sizing: border-box ：IE（替代）盒模型。

# display 都有哪些属性
|值				|说明											|
|--				|--												|
|none			|此元素不会被显示。								|
|block			|此元素将显示为块级元素，此元素前后会带有换行符。		|
|inline			|默认。此元素会被显示为内联元素，元素前后没有换行符。	|
|inline-block	|行内块元素。										|
|table			|此元素会作为块级表格来显示，表格前后带有换行符。		|
|inherit		|规定应该从父元素继承 display 属性的值。			|
|flex			|弹性盒模型。										|
|grid			|网格布局										|

