## 1. MD5
摘要算法，任何相同文件的MD5值都一样，只要改变了这个文件里的内容，它的MD5值就会变

##  2. ETag
在服务器里设置响应头
```
let string = fs.readFileSync('./main.js', 'utf8')
let fileMd5 = md5(string);
response.setHeader('ETag', fileMd5)
```
这样响应头的ETag中就会有该文件的md5值，浏览器会在请求头里设置if-None-Match，并附上这个md5值。
于是在请求的时候，如果这个md5值和你文件的md5值一样，说明文件没有更新，不需要下载
```
if(request.header['if-None-Match'] === fileMd5){
  response.statusCode = 304;
}
```

## 3. 和缓存的区别
缓存根本就不会发请求，而ETag会发请求，并比较md5值是否一样。
所以还是缓存好

