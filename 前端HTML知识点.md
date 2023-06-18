# HTML介绍
HTTP 请求 HTTP 协议 超文本传输协议 (http://)

Html5: 全称: Hyper Text Markup Language  超文本标记语言

W3C 组织: 是万维网的主要国际标准组织 成立于 1994 年 负责制定 Web 标准 主要是 HTMl+CSS

# 转义字符:

  &lt;  小于号

  &gt; 大于号

  &nbsp;  空格(不会被折叠)

  &copy;  版权符号@ 

class(类名): 页头 header ,  logo logo ,  导航条 nav , 横幅 banner , 内容区域 content , 页脚 footer, 功能区 tool.

# HTML 骨架:

1.第一行 DTD

2.第二行 html 标签对 header 标签对是网页配置 body 标签对是 网页内容

# DTD：

文档类型申请/文档类型定义 <!DOCTYPE html>

        <dt>HTML</dt>

        <dd>超文本标记语言</dd>

        <dt>css</dt>

        <dd>层叠式样式表</dd>

        <dt>javascript</dt>

        <dd>js 脚本程序</dd>

用什么标签 要看 html 的语义  div 标签是分割的语义


# 网页的字符集

 UTF-8(一个文字占三个字节 文字很全) gb2312(gbk)(一个文字占两个字节 文字不全)

# SEO:

搜索引擎优化 遵守的规则有 书写好网页 title  两个 meta 标签 name="Keywords"  name="Deacription"  h1 不可使用多次 

<meta name="Keywords" content="小魏医生,有责任心 ,踏实肯干">

 <meta name="Deacription" content="内科,外科,口腔科,皮肤科">

# Http 请求：

浏览器发出 HTTP 请求 服务器发回 HTTP 响应 将做好的网页上传到服务器上 才能被用户看见

# 
# 简单属性以及标签
&emsp; 代表一个空格符

box-sizing:border-box 属性 ：加了 box-sizing:border-box 属性，padding 和 border 的值就不会在影响元素的宽高，相当于把 padding 和 border 的值都算在 content 里

盒子模型会自动根据 padding 和 border 的值来调整 content 的值，就不需要手动调整

# HTML标签
# html 列表 

## ul 为无序列表 

有小圆点

![图片](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAh4AAABZCAMAAABG392FAAAAIGNIUk0AAHomAACAhAAA+gAAAIDoAAB1MAAA6mAAADqYAAAXcJy6UTwAAADbUExURSgsNElRYklJSiwsNCgsOzZJYklCQyg2U0lRWzYxNDs2NEJRYjs2O0I8OzEsNCgsQztRYigxSkJRU0lRU3tLa+BsdeBsYJksNChAYChsoKuyoGcsNCgsd46yv45sNEqBsquysn1QNCgsScJsdcJANChQjp+yv5+BWCgsWH2lv6uljkosNKuVd6uyv2eVvygsPrBiddRLPtRsdZk2U9RsYOBsa7A2NDg9RZlXdeBiU3ssNDFCYp+yoI6yskJRW9Rsa5+ysuBXSbA2ScJsaywxPFKL/6ulsmdQjv///6EUcuMAAAABYktHREjwAtTqAAAACXBIWXMAAA7DAAAOwwHHb6hkAAAAB3RJTUUH5wUUCAAZunY3WgAAAAFvck5UAc+id5oAAAMuSURBVHja7d1rc9JAGIbhjYJRq21RQqEFsQcQtNAWpaJW69n//48km2yCkASaTbtJvK8vTDuB2Uyf2QP7diMEAAAAAOSede++6SYgvyrVB6abgByzHz4y3QTkVqVqPTbdBuTW1pPqU9NtQG5tV6r0Hoi1s0s8EKv2bNt0E5BbLGyRwCIdAAAAAAAAAABs5nmWG3J1x2nsmb4jZCjTeAjRJB6lohuP1v7B4o9ePNqdF6bvC5nQjEf35aEQR8cnKhh+79HrvzJ9Y8iCVjwGQ9l3rMZj3n+8fmP61qBPJx7tzql8jYiHSg6KTSce3VF8PMR4xPhSfAwuSJDF1PTs/ELYE6amJWRZev9EKRe2TcdpvH23d3buzE0vWdgCAAAAyI33phuAPCMeSEA8kIB4IAHxKD8r/cliN4hHWITadE7iLpJfxc8c58NH+eOMukTzalupz466Ue/RXB+PlrfJWyceOfIp9fkvm8VjMJSbt0s1yt2F/f7x6eKFQTz+eTsMueV4qIoyLx72xPF7j7EqJhsM/aT0rrzfePEIhiP1ATDhlgeXlqoZU72HLB1ydUdy07/XV399vxMJeg/1DsoSDaqmP3J/g3jIaiFpJR5eclojVRnS/uxfuhyPeXCCT8Ed06gWWx+PdichHr3+/sFgGMSjq3qR1XiomlbcOY1awkwHl8FQ5YTBpRxSTE3DeCxPTVvBUmYpHkxNTdKoNd18YRsUodbdV+ciYmE79nqZo2P3gkZYtsrCtqiy/FJdrWpRGlnGY8wIUjZsySEB8UAC4gEAAADgjmT2sLDFr8nDqh8UW1bPKQ13XKVw3x5FVtF8CLY613TpfFM/Hl2OkCq22hetw4GCcjB3x9U9RErY15ciYt8ehWTpjC1hpU7v62FkPFTVD4pJ5zHHC5U6shQwKh5hvRiKyE5fbRrWgHp1xJHxcEtKTd8jUrPTl6qHg4tXCsjgUjo7u1orF29qqla1s2/zXEyZmpaH1tRU+AtaVQpoT5zp9x8xJaX4X42ZfSKWXNUCAABo+bnOr7VXoOCIBxIQDyQgHkhAPJBAdGI3Rda+l3iUnvh9RTwQR/whHoj1F6t6n0O0CDC+AAAAJXRFWHRkYXRlOmNyZWF0ZQAyMDIzLTA1LTIwVDA4OjAwOjI1KzAwOjAwlUwteAAAACV0RVh0ZGF0ZTptb2RpZnkAMjAyMy0wNS0yMFQwODowMDoyNSswMDowMOQRlcQAAAAodEVYdGRhdGU6dGltZXN0YW1wADIwMjMtMDUtMjBUMDg6MDA6MjUrMDA6MDCzBLQbAAAAAElFTkSuQmCC)


## ol 为有序列表 

orderde  list 有序列表  list item 列表项

<ol>

                    <li>

                        <dl>

                            <dt>《养身唐》</dt>

                            <dd>11111111</dd>

                        </dl>

                    </li>

                </ol>

## dl 为定义列表

 dt 数据项 dd 数据定义    dl>dt>dd

只要语义上有"解释说明" 含义的文字 且为列表形态 应该使用定义列表

ol 标签的 type 属性 a  表示小写英文字母编号  A 表示 大写英文字母编号 i 表示小写罗马数字编号 I 表示大写罗马数字编号 1 表示数字编号

ol 标签的 start 属性 必须为阿拉伯数字 必须是整数 指定了列表编号的起始值

ol 标签的 reversed 的属性不需要值  指定列表中的条目是否是倒序排列的

li 不能散着放  ul 的字标签只能是 li  li 里面可以放任何东西

无序列表的 type 属性 可以定义前导符号的样式   disc  默认值 空心圆  circle 空心圆 square 实心方块

ul 的子标签只能是 li  绝对不能出现其他任何标签

li 标签内部可以放任何其他标签

## list-style属性 

去掉ul小圆点

list-style:none 去掉列表的符号.


# 

# 图片 音频 与视频标签

## 音频 <audio>标签

    <audio src="音频地址">

        您的浏览器不支持 audio 标签 请升级浏览器

    </audio>

音频  controls 属性 显示播放控件

音频  autoplay 属性 音频会自动播放

音频  loop 属性 会循环播放

## 视频 <video> 标签

视频  controls 属性 显示播放控件

视频  autoplay 属性 音频会自动播放

视频  loop 属性 会循环播放

## 图片<img>标签

<img src="./01.jpeg" alt="景色">

相对路径就是 从网页出发找到图片 绝对路径就是本地图片 ../表示上一级

img 是 images 的缩写 src 是 source 的缩写 

alt 属性 对图像的描述  使用 alt 的原因 1.由于某种原因无法加载图片 浏览器会显示 alt 属性中的文本 2.供视力不方便的朋友使用网页朗读器 也会朗读 alt 中的文本

# 超链接a标签

超链接 a 标签对 target="_blank" 说明 要在新的网页窗口打开

# span 标签

对 是文本中的“区块” 标签 没有啥特殊的显示效果 可以结合 css 添加不同的显示效果

 <p>

        <span>北京</span>的区号是<span>010</span>

    </p>

    <p>

        <span>北京</span>的区号是<span>021</span>

    </p>

# 文字加粗倾斜下划线标签

<b>标签  被加粗的文字

<u>标签 加下划线的文字

<i>标签 倾斜的文字

<br>标签对是换行 <hr>标签对是下划线 

 <p>

            <b>小魏同学</b>

            <br>

            <u>小苟同学</u>

            <hr>

            <i>苟老师</i>

            <hr>

        </p>

<strong> 代表特别重要的文字

<em> 代表强调文字

<mark> 代表一段需要被高亮的文字

<figure> 代表一段独立的内容 与说明 <figcaption>配合使用

# HTML5 众多区块标签

section 标签对  文档的区域 语义比 div 大

article 标签对 文档的核心文章内容 会被搜索引擎主要抓取

aside 标签对  文档的非必要相关内容 比如广告等

nav 导航条

header 页头

main  网页核心部分

footer 页脚


## 表格标签 table

table  表格整体 可用于包裹多个 tr       

tr     表格每行 可用于包裹多个 td

td    表格单元格 可用于包裹多个表格内容

<table>

 <tr>

            <td>姓名</td>

            <td>成绩</td>

            <td>评语</td>

        </tr>

        

        <tr>

            <td>小哥哥</td>

            <td>100 分</td>

            <td>小哥哥真帅气</td>

        </tr>

</table>

tabled 标签对的属性

border  边框宽度

width 表格宽度

height  表格高度

表格标题和表头单元格标签

caption  表格大标题 表示表格整体大标题 默认在表格整体顶部居中位置显示

th 表头单元格 表示一列小标题 通常用于表格第一行 默认内部文字加粗并居中显示

 

表格的结构：thead  表格头部  tbody 表格主体  tfoot  表格底部   

合并单元格 将水平或者垂直多个单元格合并为一个单元格

合并单元格步骤：

1.明确合并那几个单元格

2。通过左上原则 确定保存谁删除谁

    1.上下合并 只保留最上的 删除其他

    1.左右合并 只保留最左的 删除其他

3.给保留的单元格设置：跨行合并（rowspan） 或者跨列合并（colspan）

!注意事项：只有同一个结构标签中的大单元格才可以合并 不能跨结构标签合并 （不能跨：thead tbody tfoot


## 表单标签：

input 系列标签

button 按钮标签

select 下拉菜单标签

textarea 文本域标签

label 标签

input 系列标签 type 属性值：

标签名  type 属性   说明

input    text       文本框 用于输入单行文本 常见属性:placeholder 占位符 提示用户输入内容的文本

input    password    密码框 用于输入密码

input   radio        单选框 用于多选一 name 分组 相同 name 属性值的单选框为一组 checked 默认选中

input  checkbox     多选框 用于多选多   name 分组 相同 name 属性值的单选框为一组 checked 默认选中

input   submit     提交按钮 用于提交

input   reset      重置按钮 用于重置

input   button    普通按钮 配置 js 添加功能

 

## 表单 input 种类

color  颜色选择控件

data time 日期时间选择控件

email 电子邮件输入控件

file 文件选择控件   多文件选择 属性为 multiple

number 数字输入控件 限制最大和最小数 最小 min 最大 max

range  拖拽条    限制最大和最小数 最小 min 最大 max

search  搜索框

url   网址输入控件

submit  提交按钮 (value 里面写的是按钮上出现的文本)

<input type="submit" value="提交表单">

required 必填

<input type="text" required>

datalist 控件  可以为输入框提供一些备选项 当用户输入的内容与备选项文字相同时 将会显示智能感应

<input type="text" list="lis">

            <datalist id="lis">

                <option value="米饭"></option>

                <option value="面条"></option>

                <option value="烤肠"></option>

                <option value="麻辣烫"></option>

                <option value="火锅"></option>

                <option value="虾尾"></option>

                <option value="烤鱼"></option>

            </datalist>

## button 按钮标签

标签名    type 属性值       说明

button   submit      提交按钮

button    reset      重置按钮

button    button     普通按钮

## select 下拉菜单标签  

selected 为默认选中

select 标签 表示下拉菜单的整体

option 标签 表示下拉菜单的每一项

# 	**HTML 网页设计**
**1.**

**<!DOCTYPE HTML>：**doc 为文档，type 为类型，即 DOCTYPE 为文档类型，为了声明只是一个网页类型。

**<!-- -->:**注释说明作用，里面的内容不会显现在网页上面。

**meta:**主要用来声明重要的一些信息，比如：设置网页的编码字符集。

常用语法：<Meta charset=”utf-8” /> 

Html 的全称为 HYPER TEXT MARKUP LANGUAGE

整体代码框架：

<!DOCTYPE HTML>

<html>

	<head>

	<title>

	</title>

	</head>

	<body>      

	</body>

</html>

# **2.** **网页设计的常用标签：**

标签分为**行级和块级**标签，行级标签不会自动换行(例如文字、音频、图片、视频等标签)块级标签可以自动换行（例如<div></div>）。

**（****1****）字体标签：**

<u></u>下划线             <b></b>加粗                    <sub></sub>下角标  <sup></sup>上角标      <hr/>水平线（特例）          

<a></a>超链接------固定使用格式为<a href=”” target=”_blank”>超链接名称</a> ，“ ”中要输入跳转的文件具体位置名称或者网页名称，非电脑自带的网站要加上前缀“http”,“href”表示属性,target 表示目标，该句表示目标网址需新建一个窗口打开。

例子：<a href=”http//:www.baidu.com”>百度</a>

**（2）****图片标签：**

<img src=””/>----””中输入图片的名称，src:属性  设置长宽高在引号后输入空格，再输入相应的要设置的参数即可。

**（3）****音频标签：**

<audio src=” ” controls  autoplay></audio>:中输入音频名称，路径，controls 表示显示音频控件，autoplay 表示自动播放

如果浏览器不支持“audio”，则换用另外一种格式：

<audio controls>

<source src=” ”/>

</audio>

**（****4****）视频标签：**

<video src=” ” poster=” ”  controls autoplay>

</video>

poster 指设置视频封面或者插入广告

**（5）列表标签：**

A. **无序列表：<ul type=””> </ul>** (type 为设置列表项前符号属性，circle 为空心圆环，square 为正方形)

    <li> </li>(列表项，默认列表项开始的符号为实心圆点)

B. **有序列表：<ol type=””></ol>**(type 为设置列表项前序号属性,数字则为 1，字母则为 a,区分大小写)，默认为 1，2，3

C.**自定义列表：<dl>**

	<dt>标题</dt>

	<dd>内容</dd>

	</dl>

***列表标签在嵌套时只能在<li></li>中嵌套，不可直接在<ul></ul>或者<ol></ol>中嵌套。**

**（6）表格标签：**

A、规则性表格即为无合并单元格

B、不规则性表格即为有合并单元格，分为行合并和列合并。

**行合并**：合并内容不在同一组 tr 中，**rowspan=“”**

**列合并**：合并内容在同一组 tr 中,**colspan=“”**

**框架如下：**

<table>

	<tr>      **表示行数，例如一行只有一对<tr></tr>**

	<td>     **表示列数，同上**

	</td>

	</tr>

</table>

**设置单元格的属性**：

1、border:设置边框线条粗细

2、cellsapcing:设置单元格与单元格之间的边距

3、bgcolor:设置表格背景颜色

4、background:设置背景图片(凡是设置了背景图都会有平铺)

5、width:设置表格的宽度

6、cellpadding:设置单元格与内容之间的距离

7、height:设置单元格的高度（通常只设置宽度，高度自动撑开）

8、align:设置表格内内容对齐方式

9、如果要**加粗内容**，只需将 **td 变为 th**即可

***注：以上属性中 tr 中不能设置宽度，可以设置高度；td 中不能设置高度，可以设置宽度。**

**（7）标题标签：**

<h1> </h1>

......

<hn></hn>(n 为标题数量，标题大小会随着 n 的增大而减小)

**（8）段落标签：**

<p> </p>

**（9）分割线标签：**

<hr color=”” size=””>   

	线的粗细大小

**（10）表单标签：**

**例如：**

<form action=”” method=”post/get”>

	  

|   [无法识别的内容]   <br> |    |
|:----|:----|
|    |    |

用户名：<input type=”text” name=”username” placeholder=”请输入用户名”/>

	密码：<input type=”password” name=”pass”>

	性别：男<input type=”radio” name=”a” value=“男”>

	女<input type=”radio” name=”a” value=”女”>

	爱好：

	<input type=”checkbox” name=”aihao” value=”打游戏”>打游戏

	<input type=”checkbox” name=”aihao” value=”看书”>看书

	<input type=”checkbox” name=”aihao” value=”听音乐”>听音乐

	<input type=”checkbox” name=”aihao” value=”绘画”>绘画

	民族；<select name=”民族”>

	<option value=”汉族”>汉族</option>

	<option value=”苗族”>苗族</option>

	<option value=”其他民族”>其他民族</option>

	</select>

	<br>

	<input type=”submit”>

</form>

***<input type=””>中的“”中写的是输入的内容的属性，添加空格使用的标签为：****&nbsp；****,换行使用的标签为****<br>****，checked 表示默认选项或默认值。**

  

|    |    |
|:----|:----|
|    |    |

 

disabled:按钮失效，无法点击，数据不能修改，数据无法上传

readonly:只读属性，数据不能修改，但是数据可以上传

hidden:数据隐藏属性，但是数据可以上传

网址：<input type=”**url**”>

日期；<input type=”**date**”>

年龄：<input type=”**number**” max=”100” min=”1” step=”1”>

滑动块：<input type=”**range**”>

多行文本：<textarea style=”resize:none;”></textarea>

