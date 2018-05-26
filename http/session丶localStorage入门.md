## 1. cookie和session的区别
1. cookie
- cookie是由服务器发送给浏览器的响应头里的Set-Cookie:的值构成的。
- cookie保存在客户端，并且每次都随着请求发送给server。
- 没有session之前，cookie里保存的是用户信息，由于任何人可以读写，不安全
2. session
- session是依附于cookie而存在的
- 有了session，服务器将用户的信息保存在服务器中的session表里，然后赋予相应的信息一个sessionID，于是将响应头里的Set-Cookie的值改为sessionID
- 浏览器请求时带上cookie，服务器就通过cookie里的sessionID查找session表里对应的信息
- 这样暴露给其他人的就只有sessionID，很安全。

## 2. localStorage
1. - 与cookie不同，请求的时候浏览器不会带上localStorage
   - 而且每个域名localStorage最大存储量5Mb左右，cookie只有4k左右
   - 而且localStorage理论上不会过期，除非清理缓存
   - 所以持续化存东西的时候用localStorage
2. session是服务器上的hash，localStorage是浏览器上的hash，localStorage里存的东西保存在本地。
3. 只有相同域名的网页才能互相读取localStorage。
4. API:
```
localStorage.setItem('a',1);
localStorage.getItem('a');    //1
```
5. 用来记录有没有提示过用户等信息，不能用来记录密码之类的

## 3. sessionStorage
1. sessionStorage和session没有关系
2. sessionStorage和localStorage的1、2、3点是一样的，区别是关掉浏览器后sessionStorage就会被清除