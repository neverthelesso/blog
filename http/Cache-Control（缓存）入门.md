## 1. 性能优化
想让哪个文件被缓存（如js文件、css文件等），就在服务器里的路由里写上

`response.setHeader('Cache-Control', 'max-age=30')`
这样每次浏览器请求完这个url后的30s内，都不会再请求这个文件，提升了速度。
但只要改变url，文件就会被再请求一次

## 2. html不要设置Cache-Control
因为html若设置了缓存，浏览器就不会向服务器发送任何请求，这样用户无法获取到任何更新后的版本。
若是css、js这类文件更新了，可以通过改变url来使用户获取到更新，例如
```
<script src="main.js"></script>  //第一个版本

<script src="main.js?v=2"></script>    //第二个版本，改变url，加了个查询参数，于是浏览器就会重新请求文件了

<script src="main.js?v=3"></script>   //第三个版本

<script src="main.js?随机数"></script>   //以后的版本
```

## 3. 旧版本的缓存(Expires)
`response.setHeader('Expirse', 'Feb 2018 14:04:04.....')`
区别：Expires设置的是日期，而且是根据本地时间判断的，若是用户的本地时间有误，就会有bug，所以现在都用Cache-Control，若两个都设置了会优先使用Cache-Control，因为这是新版的