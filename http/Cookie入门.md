## 1. 看一遍注册登陆的代码
- [注册登录 ](https://github.com/neverthelesso/sign-up-in-demo)
- Cookie 默认在用户关闭页面后就失效，后台代码可以任意设置 Cookie 的过期时间
- 大小大概在 4kb 以内

## 2. 以注册登陆为例
1. 你注册账号时，服务器把你的用户名、密码存入数据库。
2. 登陆的时候，浏览器发送post请求，服务器把你的账号密码和数据库里的匹配，若匹配成功，则发送一个响应头给浏览器，如：
`Set-Cookie: sign_in_email=xxx@xxx.com`
这就是cookie，里面记录着你的登陆信息，浏览器会在一段时间内保存cookie
3. 当你再访问相同域名的网页时，浏览器会带着这个cookie发送GET请求，服务器会将cookie里的信息和数据库匹配，若匹配上了，则直接发送给你已经登陆上的页面
4. cookie默认在关闭页面后被清除，而后台可以 设置cookie的过期时间

## 3. 前端永远不要读写cookie
前端用localStorage

## 4. 设置cookie过期时间
1. setMaxAge
```
cookie.setMaxAge(0);//不记录cookie
cookie.setMaxAge(-1);//会话级cookie，关闭浏览器失效
cookie.setMaxAge(60*60);//过期时间为1小时
```
2. 过时了的expires

`Set-Cookie: name=Nicholas; expires=Sat, 02 May 2009 23:38:25 GMT
//星期六 5月2号 2009年 23:38:25时过期`