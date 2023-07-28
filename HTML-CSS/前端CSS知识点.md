# 前端CSS知识点
# CSS语法规则

# CSS：层叠样式表

CSS写在style标签中 一般写在head标签里面 title标签下面

CSS作用 对HTML标签进行美化

        /* 变文字颜色 */

            color: antiquewhite;

            /* 文字变大 */

            font-size: 30px;

            /* 背景颜色 */

            background-color: yellowgreen;

            /* 宽度 */

            width: 400px;

            /* 高度 */

            height: 50px;

# CSS的引入方式

1. style标签放到head标签 -- 内嵌式(适合小案例使用)

2. CSS写在一个单独的.css文件当中 --外联式(适合写项目的时候)  需要在head标签里引入link

3. CSS写在标签里 --行内式(配合js使用)

#  基础选择器：

1.标签选择器(通过标签名去写)

    通过标签名 找到页面中所有这类标签 设置样式  选中所有的这个标签都生效

2.类选择器 .类名{CSS属性名: 属性值；}

    通过类名 找到页面中所有带有这个类名的标签 设置样式 

    所有标签上都有class属性 class的属性值称为类名

    类名可以由数字 字母 下划线 中划线组成但不可以以数字或者中划线开头

    一个标签可以同时有多个类名 类名之前以空格隔开

    类名可以重复 一个类选择器可以同时选中多个标签

3.id选择器 #id属性{CSS属性名:属性值；} 将来配合js使用 一般不做网页美化

    通过id属性值 找到页面中带有这个id属性的标签 设置样式

    所有标签上都有id属性

    id属性值类似于身份证号码 在一个页面是唯一

    一个标签上只能有一个id属性值

    一个id选择器只能选中一个标签

4.通配符选择器 *{CSS属性名:属性值；}

    开发中极少会用到 只有特殊情况下才能用到

    在基础班小页面可能会用去除标签默认样式的margin和padding

# 文字和文本的样式

字体大小  属性名 font-size  取值是 数字+px

文字粗细  属性名font-weight 取值是 100-900的整百数  关键字 nomal(正常)  bold(加粗)

文字是否倾斜  属性名font-style 取值 nomal默认  倾斜 italic

font 符合属性中 倾斜和加粗可以省略

行高  line-height 取值 数字+px  倍数 font-size的倍数 行高是50px  (上间距+文本高度+下间距)=50px

行高也可以在font符合属性中  font:style weight size/line-height family

   Chrome调试工具

浏览器页面按F12 进入调试模式

   颜色常见取值

关键词                                 red green blue

rgb表示法   红绿蓝三原色 每项取值：0-255     rgb(0,0,0) rgb(255,255,255)

！！！！rgba表示法     红绿蓝三原色+a透明度 取值范围为1  rgba(255,255,255,0.5)

！！！！十六进制表示法  #开头，将数字转换为十六进制表示  #000000 ,#ff0000  简写 #000 #f00

        标签水平居中方法

如果让div p h1 标签居中  可以通过margin (0 auto)来实现 ---复合属性  0为上下 auto左右

         选择器的进阶

复合选择器-后代选择器:  选择器父级 选择器子级{css}  子级包括儿子 孙子 重孙子

复合选择器-子代选择器:  选择器父级>选择器子级{css}  子级只包括儿子

复合选择器-并集选择器:  同时选择多组标签 设置相同的样式  选择器1,选择器2{css}

复合选择器-交集选择器:  选中页面中 同时满足多个选择器的标签  选择器1选择器2{css}

复合选择器-hover伪类选择器: 选择器:hover{css}  任何一个标签都可以添加伪类 任何一个标签都可以鼠标悬停

# Emment语法

简写 快速生成大量代码

# 背景相关属性

background-color 背景颜色  默认值为 rgba(0,0,0,0)

背景图片 background-img:url('图片的路径') 


背景图片平铺 background-repeat

repeat     水平和垂直方向都平铺

no-repeat   不平铺

repeat-x    沿着x轴平铺

repeat-y    沿着轴平铺

背景位置  background-position

水平方向位置 垂直方向位置

background-position(left/center/right     top/bottom/center)

background-position(50px/-50px     100px/-100px)


# img与背景图片的区别

img是个标签 不设置宽高默认会以原尺寸显示

div+背景图 需要设置div的宽高 因为背景图片只是装饰Css样式 不能撑开div标签


# 元素的显示模式

## 块级元素：

div为块级标签

独占一行 一行只能显示一个 宽度默认为父元素的宽度 高度默认有内容撑开

## 行内元素

一行可以显示多个 宽度高度由内容撑开 不可以设置宽高 

a span b u i strong em del.....


## 行内块元素

一行可以显示多个 可以设置宽高

input textarea  button select img

# 元素的显示模式转换

display：block   转换成块级特点   使用较多

display：inline-block 转换为行内块元素  使用较多

display：inline  转换为行内元素      使用极少


# CSS的三大特性

## 1.继承性

文字的可以继承

## 2.层叠性 

## 3.优先性  

选择器谁的范围越广 谁的优先级越低

如果一个标签使用了多个选择器

继承<通配符选择器<标签选择器<类选择器<id选择器<行内样式<!important

优先级的叠加计算方式

复合选择器中  行内样式的个数  id选择器的个数 类选择器的个数 标签选择器的个数

PxCook (像素大厨)基本使用

# 盒子模型（布局）

padding  内边距  padding：20px 10px 20px 10px  顺序: 上右下左

margin  外边距   margin：20px 10px 20px 10px  顺序 上右下左

content   内容区域  width 宽度 height 高度

border  边框   border（复合属性）: 10px solid red;  solid 实线 dashed 虚线  dotted点线

border-top上    border-right右边  border-bottom下边  border-left 左边 

border-width  边框粗细   border-style 线条样式  border-color  边框颜色

  css3盒模型( 自动内减) 好处:给盒子加了border和padding 不需要手动做减法

box-sizing:border-box

#  清除默认内外边距

 *{

    padding:0;

    margin:0;

 }

#  版心居中:网页的有效内容

 

#  外边距 margin 的折叠现象-塌陷现象

1.给父元素加border-top   或者加padding-top

2.或者给父元素加overflow:hidden

3.转化为行内块元素

# 设置浮动

行内标签的margin-top 和 bottom不生效

行内标签的padding-top 和 bottom不生效

加行高 line-height就可以


# 结构伪类选择器：

通过HTML中的结构关系查找元素

E:first-child  匹配父元素下的第一个子元素

E:last-child   匹配父元素下的最后一个子元素

E:nth-child(n) 匹配父元素下的第n个子元素

E:nth-last-child(n)  匹配父元素中倒数第n个子元素

n可以填公式

n 从0开始

偶数    2n、even

奇数    2n+1、2n-1、odd

找到前五个   -n+5

找到从第五个往后 n+5

# 伪元素

由CSS模拟出的标签效果

:before  在父元素内容的最前添加一个伪元素

:after  在父元素内容的最后一个添加一个伪元素

！必须设置content属性才能生效

! 伪元素默认是行内元素

# 标准流

又称文档流 是浏览器在渲染网页内容时默认采用的一套排版方式


# 浮动

浮动早期的作用：图文环绕

浮动现在的作用：网页布局 块标签完美的在一横排

# 浮动的特点

  浮动后的标签具备行内块特点

1.浮动的标签会脱离标准流 

2.浮动找浮动 第二个浮动会在上一个浮动元素后面左右浮动

3.浮动元素有特殊的显示

   可以设置宽高

   一行可以显示多个

# 清除浮动

含义 清除浮动带来的影响

 

## 清除浮动方法

### 1.给父级加高度

### 2.额外标签法(在父元素内容的最后添加一个块级元素 给块级元素添加clear:both)

### 3.单伪元素清除法

 基本写法：                       

    .clearfix::after{               

      content:'';

      display：block;

      clear:both;

    }

 补充写法:

 .clearfix::after{               

      content:'';

      display：block;

      clear:both;

      height:0;

      visibility:hidden;

    }

4.双伪元素清除法

  .clearfix::before,

  .clearfix::after{               

      content:'';

      display：table;

  }

  .clearfix::after{   

      clear:both;

    }

### 5.给父元素设置overflow：hidden


# 定位

可以让元素自由的摆放在网页的任意位置

一般用于 盒子之间的层叠情况

可以让盒子始终固定在屏幕中的某个位置 

  实现定位的步骤

## 1.设置定位方式

 属性名 position   属性值     静态定位 static

                             相对定位 relative

                             绝对定位 absolute

                             固定定位  fixed

                            

## 2.设置偏移值

  偏移值设置分为两个方向，水平和垂直方向各选一个使用即可

  选取的原则一般是就近原则(离那边近用那个)

水平   left  数字+px      距离左边的距离

水平   right  数字+px     距离右边的距离

垂直   top     数字+px    距离上边的距离

垂直   bottom   数字+px   距离下边的距离


## 相对定位  

相对于自己之前的位置进行移动

position:relative  

特点：

1.占有原来的位置

2.仍然具备标签原有的显示模式特点

3.改变位置是参照自己原来的位置


## 绝对定位 

 相对于非静态定位的父元素进行定位  

  绝对定位: 先找已经定位的父级 如果有这样的父级就以这个父级为参照物进行定位；

  有父级 可能没有定位，以浏览器窗口为参照物进行定位

position:absolute

特点:

 1.不占位

 2.改变标签原有的显示模式特点：具备了行内块的特点（在一行共存 宽高生效）

 子绝父相  父级相对定位 子级绝对定位

 绝对定位查找父级的方式：就近找定位的父级，如果逐层找不到这样的父级 那就以浏览器窗口为参照物进行定位

自己宽度高度的一半

 transform:translate(-50%,-50%)

# **2.** **CSS的介绍和使用**
# （1）**css用来美化html框架，固定语法为**：

<head>

<title></title>

	**①　内嵌式：<style type=”text/css”>**

	**需要修饰的标签名：{需要修饰的属性：属性值；}**

	**</style>**

	**②　外部引用式：<link rel=”stylesheet” href=”css的路径”/>**

</head>

（2）**css基本选择器：**

	①　标签选择器：标签名{}

	②　类选择器：标签中:**class**=”类名”

	Css中：**.**类名{}

	③　Id选择器：标签中:**id**=”名称”

	css中：**#**名称{}

***在css中设置属性时，类名可以重复，属性可以复用，但id最好不要重复使用，id相当于ip地址，不能重复。****内部嵌套式中三种选择器的优先级为：id>class>标签。所有类型中的优先级为：行内样式>id>class**

**（3）css扩展选择器：**

	**①　组合选择器：**

	将不同的标签设置成相同的属性：需要设置的标签1**，**标签2**，**标签3{相同的属性}，例子：.a,.b,.c{}

	**②　包含选择器**

需要将父标签里所有的元素设置为一个属性：

a.  父标签名称 子元素{}（父标签里所有包含的元素均为一个属性）,例子：ul li{}

b.  父标签名称>子元素{}（只有父标签里的子元素为所设的属性，后代元素不被其改变）,例子：ul>li{}

	**③　交集选择器**

例子：p.a,span.a{}（只设置了p和span标签的属性）

	**④　伪类选择器**

**常用的a标签伪类选择器用法：**

a:link:未单击访问时的超链接样式

a:visited:单击访问时的超链接样式

a:hover:鼠标悬浮在超链接上的样式

a:active:鼠标单击未释放的超链接样式

常用的p标签伪类选择器用法：

1)  p:after{

	content:’’;

}

2)  p:before{

	content:’’;

}

 

# **css常用样式+案例**

## **(1)**    **font:设置字体的所有样式属性**

	①　font-family:定义字体类型

	②　font-size:定义字体大小

	③　font-weight：定义字体的粗细

	④　color：字体颜色

## **(2)**    **文本属性：**

	①　line-height:设置行高（即行间距），常用取值为25px、28px，**其值要和文本所在的块标签的高度保持一致**;

	②　text-align:设置对齐方式，常用的取值为left、right以及

center，justify(两端对齐);

	③　letter-spacing:设置字符间距，常用的取值为3px、8px;

	④　text-decoration:设置文本修饰，常用的取值为：加下划线(underline)、中划线等(line-through)、none(去掉下划线)。

## (3)      **边距属性：**

外边距：margin(内容外边框与页面边框的距离)

内边距：padding（内容与内容外边框的距离）

***盒子模型的宽度计算方法：宽度+左右边框宽度+左右内边距+左右外边距**

 

例如：如右图所示盒子模型宽度为：

400+10*2+1*2+10*2=442px

 

## **（4）边框属性：**

border-width:边框粗细

border-color:边框颜色

border-style:边框的样式

border:none (表示为去掉块标签自带的边框线)

border-radius:设置块标签或者按钮的圆角样式,取值为具体的数值

outline:none(去掉按钮点击时的外边框)

## **（5）列表属性：**

	①　list-style-type:用于设定表项的符号，取值：none(无)、disc(实心圆)、circle(空心圆)、square(实心方块)；

	②　list-style-image:用于设定图像作为列表项目符号，其值为图像对应的url；

	③　list-style-position:用于设定项目符号在列表项的位置，取值为：inside、outside；

list-style:将三个统一设定，其顺序必须按照1、2、3，不得乱序。

## **（6）背景属性：**

	①　background-color:设置元素的背景颜色

	②　background-image:设置元素的背景图片，取值为：url

	③　background-repeat:设置元素的背景图片平铺方式：repeat-x（x轴平铺），repeat-y（y轴平铺）,no-repeat（不平铺）

	④　background-position:设置元素背景图片位置

	⑤　background-size:设置元素背景图片大小

	⑥　Background-attachment:设置元素的背景图片是否跟随元素的移动而移动，取值可为fixed(固定图片)

	⑦　background:复合属性

**（7）hover{**

	background-color:

}(设置鼠标滑过时元素的背景颜色)

**（8）**.类名：nth-child()-------**表示只设置括号里序号所在的元素属性**

## **（9）背景颜色的渐变：**

	①　线性渐变：

a.  background:linear-gradient(<angle>||<direction>,<color_stop>,<color_stop>...);

  

|    |    |
|:----|:----|
|    |    |

 

 

 

 

 

 

 

 

 

b.  重复线性渐变：background:repeating-linear-gradient(<angle>||<direction>,<color_stop>,<color_stop>...);

	②　径向渐变：

a.  background:radial-gradient(<shape>||<size> at <position>,<color_stop>,...);

  

|    |    |
|:----|:----|
|    |    |

 

 

 

 

 

 

 

 

b.  重复性径向渐变：

background:repeating-radial-gradient(<shape>||<size> at <position>,<color_stop>,...);

## **（10）阴影属性：**

a.  文本阴影：text-shadow:5px 6px 7px red;

 

b.  盒子阴影：box-shadow:5px 6px 7px red;经常与hover连用，即经常运用于鼠标经过盒子时增加阴影，还与transition(用来设置延迟时间)连用。

# **5、盒子模型：**

l  **margin的值可以设置为负数，但是border和padding只能取正数。**

  

|    |    |
|:----|:----|
|    |    |

 


# l  **display**

 

 

l  visibility:hidden(将元素隐藏，但元素所在位置依然存在，占据位置)

l  transform:translateX()/translateY()/translate( ，)-----变形，控制盒子水平/垂直/水平和垂直方向的移动

l  transform:rotateX()/rotateY()/rotate( )-----旋转，控制盒子水平/垂直/水平和垂直方向的旋转角度，括号里填具体的度数，单位为deg

l  transform-origin:top left/top center/top right/center center/bottom left.....(表示盒子旋转时的基准点位置，共有八个基准点)

  

|    |    |    |    |
|:----|:----|:----|:----|
|    |    |    |    |
|    |    |    |    |
|    |    |    |    |

 

# 

# l  动画的运用

 

 

	**.动画盒子类名：hover{animation-play-state:paused}**表示鼠标经过动画区域时，动画界面停止，鼠标离开时，动画继续。

 

# **6、盒子浮动：**

float:浮动。（只要使用浮动就会脱离文档流）

清除浮动的方法：

(1)      在设置了浮动的盒子下方重新创建一个盒子并设置属性：clear:both

(2)      给浮动的父元素设置高度

(3)      给父元素after追加一个元素，content=’’,设置为clear:both

(4)      给父元素设置样式overflow:auto

# **7、****盒子定位：**

position

(1)      静态定位：position:static（默认）

(2)      相对定位：position:relative(移动时，是从原来默认的位置开始移动，移动后并未脱离文档流，原来占据的位置依然在)

(3)      绝对定位：position:absoulte(移动后脱离文档流，不会占位置。移动时先看父元素有无定位，父元素没有定位时就一直往上找，直到body，这时元素则会从body的左上角开始移动；如果父元素有定位，元素则会从父元素的左上角开始移动)

(4)      固定定位：position:fixed（每次移动只看body，浏览器左上角）

z-index:具体的数值（数值越大越优先显示，前提是元素必须有定位属性）

# **8、弹性盒子**

（1）在盒子属性中加：

display:flex(表示该盒子为弹性盒子)

（2）弹性盒子的属性：

l  flex-direction:row/column(表示弹性盒子中的子元素排列方式为行或列，一般默认为列)

l  flex-wrap:wrap(表示子元素超出盒子后会自动折行)

l  align-content:stretch/flex-end/flex-start(表示子元素纵向排列方式为每一行间距为默认间距/子元素全部从盒子底部开始排列，并每一行紧密排列，行距为0/子元素全部从盒子顶部开始排列，并每一行紧密排列，行距为0)

l  justify-content:flex-end/flex-start/space-between/space-around(表示子元素横向排列方式为紧贴右边/紧贴左边/左右两个子元素分别紧贴盒子左右，中间的子元素居中排列/左右两个子元素均匀排列于左右，但不紧贴盒子边框，中间子元素居中排列)

l  align-items：center（表示盒子中的子元素纵向居中排列）

（3）弹性盒子的子元素的属性：

l  order：具体数值(数值越小，排列越前，设置子元素的排列顺序，可以为负值)

l  flow-grow：默认值为0（表示该元素相对于其他灵活的元素扩展的量）

l  flow-shrink：默认值为1（表示该元素相对于其他灵活的元素收缩的量）

