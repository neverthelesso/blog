## 1. CSS简介
css2.1是目前世界上应用最广泛的版本，2011年开始css被分为多个模块单独升级，统称为CSS3，现在已经有很多模块升级到了CSS4。[CSS文档 ](https://www.w3.org/Style/CSS/specs.en.html)

## 2. 编写CSS的第一步
给你要写的css标签加上border
`border:1px solid red;`
让你知道它在哪、它的大小、形状

## 3. 使导航栏横着在同一行
给所有li加上`cssfloat:left;`，然后给ul加上`class:clearfix`,下面是clearfix的css
```
.clearfix::after{
  content: "";
  display: block;
  clear: both;
}
```
方法二：给ul加上`display:flex`
若想让li在同一行里平均分布，见下面6.5

## 4. 高度
div（块级元素）：高度是由内部文档流元素高度的总和决定的。文档流：文档内元素的流动方向，内联元素是从左往右，块级元素是从上往下
span（内联元素）：高度是由其中文字高度决定的，内联元素设置width和height是无效的，上下的margin和padding也无效，要将它们设为display:inline-block才有效。

## 5. 小提醒
尽量不写height和width，这两个属性会引出很多bug，要宽高的时候可以用padding，但img最好先写width，因为可以先占位，因为引用图片时浏览器不知道图片大小，所有等图片下载完成，它后面的元素又要重新排位置，若先写好width，则不用重排，知道height也可以先写好height。
另外span元素设置padding的时候要将它设为display:inline-block，因为内联元素不能设置宽高，inline-block具有inline的同行特性，也具有block的高度特性。
对于display:inline(内联元素)的元素，设置width/height/上下margin和padding都是无效的

## 6. 居中
 ### 1. 垂直居中
1. 若父元素没有写height，则直接在父元素写
`padding: 10px 0;`
子元素就可以居中，所以尽量避免父亲高度确定
2.让一个元素在父级元素中绝对居中
 方法一：
 给父级元素加:
 ```
 position:relative;   //若父级元素是body可以不用
 加
 ```
再给自己加：
```
div{
 position: absolute;
 top: 0;
 left: 0;
 bottom: 0;
 right: 0;
 margin: auto;
}
```
方法二：（若不兼容IE，工作中只要用这一种方法即可，最简单，Chrome，移动端都可以用）
给父元素加：
```
display: flex;               //让它变成一个弹性盒
justify-content: center;     //水平居中
align-items: center;         //垂直居中
```
3. table自带居中（兼容IE）
```
<html>
<style>
.parent{
  border: 1px solid red;
  height: 600px;
}
.child{
  border: 1px solid green;
}
</style>
<body>
<table class="parent">
  <tr>
    <td class="child">
      文字
    </td>
  </tr>
</table>
</body>
</html>
```
文字会居中
4. 用div假扮table（兼容IE）
```
<html>
<style>
div.table{
  display: table;
  border: 1px solid red;
  height: 600px;
}

div.tr{
  display: table-row;
  border: 1px solid green;
}

div.td{
  display: table-cell;
  border: 1px solid blue;
  vertical-align: middle;
}

</style>
<body>
<div class="table">
    <div class="tr">
      <div class="td">
        文字
      </div>
    </div>
  </div>
</body>
</html>
```
5. 用100%高度的before和after
```
.parent{
  border: 3px solid red;
  height: 600px;
  text-align: center;
}

.child{
  border: 3px solid black;
  display: inline-block;
  width: 300px;
  vertical-align: middle;
}

.parent:before{
  content:'';
  display: inline-block;
  height: 100%;
  vertical-align: middle;
}
.parent:after{
  content:'';
  display: inline-block;
  height: 100%;
  vertical-align: middle;
}
```
6. 绝对定位加上margin-top: -自身height的50%
```
<html>
<style>
.parent{
  height: 600px;
  border: 1px solid red;
  position: relative;
}
.child{
  border: 1px solid green;
  width: 300px;
  position: absolute;
  top: 50%;
  left: 50%;
  margin-left: -150px;
  height: 20px;
  margin-top: -10px;
  text-align: center;
}
</style>
<body>
<div class="parent">
  <div class="child">
    文字
  </div>
</div>
</body>
</html>
```
7. 让一个背景图居中，并且让它自适应屏幕
```
background: url("wallhaven-w-min.jpg") no-repeat center center ;
background-size: cover;
```
### 2. 水平居中
1. 块级元素水平居中
```
margin-left:auto;
margin-right:auto;
```
2. 内联元素水平居中，给它们的父元素加上
`text-align:center;`
若不是内联元素想让它居中，可加display:inline-block，加了之后一般还要加下面这句，不然可能会有bug（下面可能会空出一行）
`vertical-align: top;`
3. 让导航栏横过来，并在同一行里均匀分布
给ul加css
```
ul{
  display:flex;  
  justyfy-content:space-between;
}
```
去掉li的`float:left`
去掉ul的`clearfix`

## 7. 用css做三角形
1. 等腰三角形：
```
div{
  border:50px solid transparent;
  width:0;
  height:0;
  border-bottom-color:red;
}
```
2. 增高三角形
```
div{
  border: 50px solid transparent;
  width: 0;
  height: 0;
  border-bottom: 100px solid red;  //只需增加这个border的厚度
}
```
3. 直角三角形：
```
div{
  border:50px solid transparent;
  width:0;
  height:0;
  border-top-width:0;
  border-left-color:red;
}
```
4. 不规则三角形
```
//还有这种操作！
div{
  width: 0;
  height: 0;
  border-top: 30px solid black;
  border-left: 30px solid transparent;
  border-right: 40px solid transparent;
}
```

## 8. 梯形
```
div{
  width:50px;
  height: 42px;
  border: 18px solid transparent;
  border-top: 18px solid black;
}
```
## 9. 怎样脱离文档流
1. 相对于窗口定位：
`position:fixed`
2. 相对于父级元素定位：
在父级元素加上：`position:relative`
给自己加上：`position:absolute`（绝对定位后元素会变成`display:block`）

## 10. 使用::before和::after时
要加上这两行的代码，才会显示内容
```
content: "";
display:block;  //如果是绝对定位就不用加，因为绝对定位是display:block;
```
而且before和after是不受*管束的，例如
```
*{
  box-sizing: border-box;
}
//设置了这个，但是对before和after无效，给它们加border它们还是会变化大小

//除非这样
*::after{
    box-sizing: border-box;
}
*::before{
    box-sizing: border-box;
}
```

## 11. 图片的轮播
\<html>
```
<div class="window">
    <div class="images" id=images>
        <img1>
        <img2>
        <img3>
    </div>
</div>
```
\<css>
要给window的div和每个img都定好宽高！并给window加上overflow:hidden
```
.images{
    display: flex;    //给image的div加上这个图片才能横这放！
}
.images > img{
    width: 100%;
}
```
## 12. box-shadow
`box-shadow: -16px 0 16px 1px rgba(102,102,102,0.4);`
第一个值代表阴影左右偏移，正数往右，负数往左
第二个值代表上下偏移，正往下，负往上
第三个值越大，模糊面积越大越淡
第四个值取正值时，阴影扩大，取负值时，阴影收缩

## 13. calc
`//css3新属性，绝对定位的时候
left: calc(50% - 8px)  //元素的左边在父元素的中间偏左8px`
## 14. 消除默认样式
```
*{
  margin: 0;
  padding: 0;
}

*,
*::before,
*::after{
  box-sizing: border-box;
}

a{
    text-decoration: none;  //  去掉下划线
}

ul,ol{
    list-style: none;
}

button{
    outline: none;
}
```
## 15. img 等比例自动缩放
```
img{  
    width: auto;  
    height: auto;  
    max-width: 100%;  
    max-height: 100%;     
}
```