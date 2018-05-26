## 1. Sass和SCSS的区别
SCSS是Sass推出的一个全新的语法，更加贴近css，所以一般都是用SCSS。
请注意 Sass 从来没有大写过，无论你指的是语法或者这个语言。同时， SCSS 一直是大写的！

## 2. 安装（mac）
我安装的是node-sass
在命令行里进入~目录，输入：

  - npm config set registry https://registry.npm.taobao.org/
 - echo 'export SASS_BINARY_SITE="https://npm.taobao.org/mirrors/node-sass"'>> ~/.bashrc(若是用的zshrc则改为~/.zshrc)
- source ~/.bashrc(同上)
- sudo cnpm i -g node-sass（需要先安装cnpm）
- mkdir ~/Desktop/scss-demo
- cd ~/Desktop/scss-demo
- mkdir scss css
- touch scss/style.scss
- node-sass style.scss style.css -w style.scss（开始监听style.scss）
## 3. 使用
终端进入含css和scss文件的目录，执行
`node-sass style.scss style.css -w style.scss`（开始监听main.scss）
直接编辑main.scss，node-scss就会自动给main.css实时更新。
在 scss 文件里添加以下内容
```
@function px( $px ){
  @return $px/$designWidth*10 + rem;  //js里获取innerWidth的时候除以了10，这里就要乘以10
}

$designWidth : 640; // 640是设计稿的宽度，设计师给的。这样好像就不能动态的随着屏幕大小变化而变了

.child{
  width: px(320);
  height: px(160);
  margin: px(40) px(40);
  border: 1px solid red;
  float: left;
  font-size: 1.2em;
}
```
可看到css变化，SCSS将px变成了rem放入了css中。
若不使用SCSS的话，我们每次将px转化为rem都要自己去算，使用SCSS可以帮我们算

## 4. 语法
```
.topNavBar{
  nav{
    background: red;
  }
}
```