# bfc

## bfc有什么特征

### 两个独立的bfc，样式互不影响。
浮动会形成bfc，两个浮动的元素，样式互不影响，比如margin不会共用，而非bfc的元素，margin会共用。

### bfc作用范围内，浮动的元素也会被计算高度
一个bfc作用范围，浮动的元素的高度，能够撑起父元素。而没有形成bfc的元素，高度会坍塌。

### bfc区域的元素，不会被浮动的元素覆盖
BFC的区域不会与float box重叠，而非bfc区域的，会被浮动的元素覆盖。

## 如何形成bfc
 - 根元素，即HTML标签
 - 浮动元素：float值为left、right
 - overflow值不为 visible，为 auto、scroll、hidden
 - display值为 inline-block、table-cell、table-caption、table、inline-table、flex、inline-flex、grid、inline-grid
 - 定位元素：position值为 absolute、fixed
