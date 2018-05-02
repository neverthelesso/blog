## 1.引用
- 在 head 中或在 body 中添加 script 标签，src 指向 jquery.js 或 jquery.min.js 文件的地址
- [jquery下载页面](https://jquery.com/download/)，下载为js文件，在html中引用即可

## 2. 基础
jQuery的原型为jQuery.prototype
```
var div = document.getElementById('x')  //dom对象
var $div = $('#x')  //jquery对象
```
div和$div的联系：`$div[0] === div`
`$div === $(div)`
区别：div是id为x的元素
&div是对象

## 3. 常用API
```
$nodes.addClass('red');
$nodes.addClass(function(index,currentClass){
      return 'sd-'+index;    //这样nodes里每一项会依次添加sd-0 sd-1 sd-2 sd-3 ......的class
    });  
var classes = ['red','blue','black'];
$nodes.addClass(function(index,currentClass){
      return classes[index];    //前三项就会添加red、blue、black的class
    });  

$nodes.removeClass('red');

$(x).on('click', function(){    //建一个button并给它id为x
    $nodes.toggleClass('red');  //每点一次button，nodes就增加或删除'red'class
})
```
## 4. jQuery对象和DOM对象的转换
jquery转dom

`var div = $div[0]  //这样jquery就转换成了DOM对象，或div = $div.get(0)`
dom转jquery

`var $div = $(div);  //这样dom对象div，就转换成了jquery对象`
## 5.题目
### 1.请说出 div 和 $div 的联系和区别。
```
<div id=x></div>
var div = document.getElementById('x');
var $div = $('#x');
```
答案:
```
div 和 $div 的联系是:
$(div) 可以将 div 封装成一个 jQuery 对象，就跟 $div 一样
$div[0] === div ，$div 的第一项就是 div

div 和 $div 的区别是：
div 的属性和方法有 childNodes firstChid nodeType 等
$div 的 属性和方法有 addClass removeClass toggleClass 等
```
### 2.题目:
```
window.jQuery = ???
window.$ = jQuery

var $div = $('div')
$div.addClass('red') // 可将所有 div 的 class 添加一个 red
$div.setText('hi') // 可将所有 div 的 textContent 变为 hi
```
答案
```
window.jQuery = function(node1){
  var node = {}
  
  if(typeof node1 === "string"){
    var temp = document.querySelectorAll(node1)
    for(var j = 0; j < temp.length; j++){
      node[j] = temp[j]
    }
    node["length"] = j
  }else{
    node = {}
    node[0] = node
    node["length"] = 1
  }
  
  node.addClass = function(className){
  	for(var i = 0; i < node.length; i++){
      node[i].classList.add(className)
  	}
  }
  
  node.setText = function(value){
    for(var i = 0; i < node.length; i++){
    	node[i].innerText = value
    }
  }
  
  return node
}
```