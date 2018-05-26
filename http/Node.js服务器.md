## 自制一个服务器

### 用 Node.js 在你的电脑创建第一个服务器

1. 在桌面创建一个目录，目录里面有个 server.js 这个文件就是服务器，向服务器写如下代码，写完下面的代码就已经创建了一个服务器，只不过你还没有开启而已。

   ```
   var http = require('http')
   var fs = require('fs')
   var url = require('url')
   var port = process.argv[2]

   if(!port){
     console.log('请指定端口号好不啦？\nnode server.js 8888 这样不会吗？')
     process.exit(1)
   }

   var server = http.createServer(function(request, response){
     var parsedUrl = url.parse(request.url, true)
     var path = request.url 
     var query = ''
     if(path.indexOf('?') >= 0){ query = path.substring(path.indexOf('?')) }
     var pathNoQuery = parsedUrl.pathname
     var queryObject = parsedUrl.query
     var method = request.method

     /******** 从这里开始看，上面不要看 ************/
     console.log('方方说：得到 HTTP 路径\n' + path)
     console.log('方方说：查询字符串为\n' + query)
     console.log('方方说：不含查询字符串的路径为\n' + pathNoQuery)
     /******** 代码结束，下面不要看 ************/
   })

   server.listen(port)
   console.log('监听 ' + port + ' 成功\n请用在空中转体720度然后用电饭煲打开 http://localhost:' + port)
   ```

2. 打开终端，在server.js文件路径下输入`node server.js`按照提示报错即可开启服务器，如果你想停止 server 服务，按`Ctrl + C`即可 

   ​

### 发送第一条请求内容给 server.js 服务器

1. 在另一个终端输入`curl -s -v -- localhost:8888/thisispath?thisisstr`可以看到你发送了第一条请求内容给 server.js 服务器。内容如下：

   ![第一条请求内容](https://ooo.0o0.ooo/2017/10/14/59e19221c6079.bmp)

   ​


### 发送第一条响应内容给客户端

1. 只需在 server.js 文件方方老师叫你看的区域末尾中，添加` response.write('Hi') response.end()`，并且在终端服务器中断开再开启服务器`node server.js 8888`即可产生第一条响应内容，并且发送给客户端。

2. 此时命令行的响应内容为：

   ![](https://ooo.0o0.ooo/2017/10/14/59e195aaaf160.bmp)




### 模拟一个网站的HTTP请求

完成以下需求：
仿照（或抄袭）课程文章《一个简易 Server》中的代码，写出一个 server.js 文件，满足以下功能

1. 用户请求 / 时，返回 html 内容
2. 该 html 内容里面由一个 css link 和一个 script
3. css link 会请求 /style.css，返回 css 内容
4. script 会请求 /main.js，返回 js 内容
5. 请求 `/` `/style.css` `/main.js` 以外的路径，则一律返回 404 状态码

步骤：

1. `cd ~/桌面/;mkdir mockServer-demo;cd mockServer-demo;touch server.js;gedit server.js`

2. 在打开的文档粘贴

   ```
   var http = require('http')
   var fs = require('fs')
   var url = require('url')
   var port = process.argv[2]

   if(!port){
     console.log('请指定端口号好不啦？\nnode server.js 8888 这样不会吗？')
     process.exit(1)
   }

   var server = http.createServer(function(request, response){
     var parsedUrl = url.parse(request.url, true)
     var path = request.url 
     var query = ''
     if(path.indexOf('?') >= 0){ query = path.substring(path.indexOf('?')) }
     var pathNoQuery = parsedUrl.pathname
     var queryObject = parsedUrl.query
     var method = request.method

     /******** 从这里开始看，上面不要看 ************/
   	把我删除，在这里添加需求代码
     /******** 代码结束，下面不要看 ************/
   })

   server.listen(port)
   console.log('监听 ' + port + ' 成功\n请用在空中转体720度然后用电饭煲打开 http://localhost:' + port)
   ```

3. 在方方老师指定的代码区域内，写代码

   ```
   if(path=="/"){
       response.setHeader('Content-Type', 'text/html; charset=utf-8')
       response.write('<!DOCTYPE>\n<html>'  + 
       '<head><link rel="stylesheet" href="/style.css">' +
       '</head><body>'  +
       '<h1>你好</h1>' +
       '<script src="/main.js"></script>' +
       '</body></html>')
   } else if(path=="/style.css") {
     	response.setHeader('Content-Type', 'text/css; charset=utf-8')
       response.write('body{background-color: #ddd;}h1{color: red;}')
       response.end()
   } else if(path=="/main.js") {
       response.setHeader('Content-Type', 'text/javascript; charset=utf-8')
       response.write('alert("这是JS执行的")')
       response.end()
   } else {
     	response.statusCode = 404
       response.end()
   }
   ```

   ​

4. 在 Chrome 输入`localhost:8888/`

5. 当我输入`localhost:8888/`的时候发生了什么？

   1. 将localhost转化为IP地址，在host记录为127.0.0.1，并且127.0.0.1表示本机

   2. :8888表示客户端（chrome）连接服务器的8888号端口，使用8888号服务。

   3. 上面两个合在一起的意思是：**使用本机作为服务器，且使用8888端口**。

   4. 当你输入`localhost:8888/`的时候，就发送了请求内容给服务器

   5. 服务器根据你发送的请求内容，主要是path的内容，来给客户端返回你if提前设置好的响应内容，在这里，响应的是

      ```
      response.setHeader('Content-Type', 'text/html; charset=utf-8')
      response.write('<!DOCTYPE>\n<html>'  + 
      '<head><link rel="stylesheet" href="/style.css">' +
      '</head><body>'  +
      '<h1>你好</h1>' +
      '<script src="/main.js"></script>' +
      '</body></html>')
      ```

   6. 客户端根据服务器返回的第二部分，发现了第四部分是html格式，因此在客户端在获得第四部分的时候会把他们（第四部分）当成html来渲染。

   7. 在渲染的时候，发现`<link rel="stylesheet" href="/style.css">`标签，那么客户端会再次发起请求，向服务器要path=/style.css的响应内容。内容是：

      ```
      response.setHeader('Content-Type', 'text/css; charset=utf-8')
      response.write('body{background-color: #ddd;}h1{color: red;}')
      response.end()
      ```

   8. 客户端根据服务器返回的第二部分，发现了第四部分是css格式，因此在客户端在获得第四部分的时候会把他们（第四部分）当成css来渲染。

   9. 在渲染的时候，发现`<script src="/main.js"></script>`标签，那么客户端会再次发起请求，向服务器要path=/mian.js的响应内容。内容是：

      ```
      response.setHeader('Content-Type', 'text/javascript; charset=utf-8')
      response.write('alert("这是JS执行的")')
      response.end()
      ```

   10. 至此，全部请求与响应结束。




## 细节

### HTTP，TCP，IP分别是什么意思？关系是什么？

1. 我想用信鸽把A信息发送给B人。而信鸽是通过地磁来感知B人的地理位置。

2. 意思：

   1. HTTP表示A信息
   2. TCP表示我是用信鸽的方法发送信息的
   3. IP表示信鸽是通过地磁方式来获得B人的地理位置

3. 关系：

   HTTP协议的底层是通过TCP/IP协议来实现的，这样理解：我们使用HTTP，HTTP使用TCP，而TCP需要指定IP和端口。

   ​

###  TCP

1. TCP 和 UDP 的区别是什么
简答：TCP 可靠、面向连接、慢一点，但注重安全性，适应于网页、邮件；
UDP 不可靠，无连接、较快，安全性低一点，适应于视频、语音。

2. TCP 的三次握手指的是什么
简答：每次建立连接前，客户端和服务端之前都要先进行三次对话才开始正式传输内容，三次对话大概是这样的：

   1\. 客户端：我要连接你了，可以吗
   2\. 服务端：嗯，我准备好了，连接我吧
   3\. 客户端：那我连接你咯。
   4\. 开始后面步骤

### 内网和外网是什么？内网和外网是通过什么通信的？

![](https://i.loli.net/2017/10/14/59e1c5b3eb205.bmp)

解释：

1. 内外网的圈的IP都可以互相访问。

2. 你是怎么用电脑访问qq.com的呢？过程如下：

   1. 电脑IP访问路由器的内网IP

   2. **路由器的内网IP访问路由器的外网IP**

   3. 路由器的外网IP访问qq的外网IP

      ​



### 记忆IP

1. `127.0.0.1`表示机器自己

2. `0.0.0.0`不表示任何设备

3. `192.168.x.x`表示内网的设备

4. 255是IP最大数字

   ​

### 端口怎么理解？

1. **一个端口等于一个服务**

2. 如果没有端口的概念，那么会是这样的，无论你做什么服务，都要按顺序排队![菜单_024.bmp](https://i.loli.net/2017/10/14/59e1cb1fc7998.bmp)

   ​

3. 如果有个端口，那么会这样，你做什么服务就在哪里服务窗口排队![菜单_023.bmp](https://i.loli.net/2017/10/14/59e1cac883b03.bmp)





### 路径怎么理解？

1. 我们要知道，路径到底在什么地方被提及？
   1. 输入网站为`localhost:8888/thisispath?thisisstr`，`/thisispath？thisisstr`就是路径。
   2. 请求内容的第一部分的路径指的是斜杠之后的东西，不包括锚点
   3. 在服务器中，根据路径（第一部分）和if通道来返回不同的响应内容。
2. HTTP的路径的作用不是用来指示电脑文件的路径，而是用来与服务器（比如前面的Node.js做成的服务器）if路径作对比，如果if路径和HTTP路径相同，则在响应消息返回该if路径下的内容。





### HTTP响应的页面中看到乱码，可能什么原因？