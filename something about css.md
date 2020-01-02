#### 1.弹性盒子布局（Flexible Box）

注意设置flex布局后，子元素的float，clear，vertical-align属性将失效，所有子元素自动成为容器的成员，称为flex item。

**总共六个属性设置在容器上：**

- **flex-direction**：决定主轴的方向（即项目的排列方向）
	- `row`：主轴为水平方向，起点在左端
	- `row-reverse`：主轴为水平方向起点在右端
	- `column`：主轴为垂直方向，起点在上沿
	- `column-reverse`：主轴为垂直方向，起点在下沿

<!--more-->

- **flex-wrap**：如果一条轴线排不下，如何换行
	- `nowrap`：不换行（默认）
	- `wrap`：换行，第一行在上方
	- `wrap-reverse`：换行，第一行在下方
- **flex-flow**：是flex-direction和flex-wrap的简写形式，默认值为row nowrap
- **justify-content**：定义了主轴上的对齐方式
	- `flex-start`：左对齐（默认值）
	- `flex-end`：右对齐
	- `center`：居中
	- `space-between`：两端对齐，项目之间的间隔都相等
	- `space-around`：每个项目两端之间的间隔相等。所以项目之间的间隔比项目与边框的间隔大一倍
- **align-items**：定义项目在交叉轴上如何对齐
	- `flex-start`：交叉轴的起点对齐
	- `flex-end`：交叉轴的中点对齐
	- `center`：交叉轴的中点对齐
	- `baseline`：项目第一行文字的基线对齐
	- `stretch`：如果项目未设置高度或设为auto，将占满整个容器的高度
- **align-content**：定义了多根轴线的对齐方式，如果只有一根轴线则不起作用
	- `flex-start`：与交叉轴的起点对齐。
	- `flex-end`：与交叉轴的终点对齐。
	- `center`：与交叉轴的中点对齐。
	- `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布。
	- `space-around`：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
	- `stretch`（默认值）：轴线占满整个交叉轴。

**设置在项目的属性：**

- `order`：属性定义项目的排列顺序，数值越小，排列越靠前
- `flex-grow`：属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大
- `flex-shrink`：属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小
- `flex-basis`：属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为`auto`，即项目的本来大小
- `flex`：属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选
- `align-self`：属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch











### 四种快捷居中div的方法

1. 利用display：flex设置弹性盒子布局(在容器中)

```css
.parent-div{
            display: flex;
            justify-content: center;
            align-items: center;
        }
```

  2.设置margin; o auto

  3.设置text-align And inline-block

```css
.parent-div{
    text-align:center;
}
.example-div{
    display:inline-block;
}
```

  4.2D的transform

```css
.example-div{
    position:absolute;
    top:50%;
    left:50%;
    transform:translate(-50%,-50%);
}
```

