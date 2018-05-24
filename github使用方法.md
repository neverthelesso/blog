一. 配置GitHub
点击New SSH key
title随便写
终端运行ssh-keygen -t rsa -b 4096 -C "邮箱"
运行 cat ~/.ssh/id_rsa.pub，得到一串东西，复制粘贴到key里，点击 Add SSH key
运行 ssh -T git@github.com
二. 配置git
依次运行
git config --global user.name “英文名”
git config --global user.email “邮箱”
git config --global push.default matching
git config --global core.quotepath false
git config --global core.editor "vim"

三. 使用git的三种方法
1. 建立本地仓库
a. 在桌面创建git-demo目录mkdir git-demo
b. cd git-demo
c. git init
d. 在git-demo目录里运行touch index.html
e. 运行 git status -sb 可以看到文件前面有 ??
f. 运行git add .
g. git commit -m "第一次提交"
h. git pull先把github上的文件拉下来（一般可忽略）
i. git push推上去

2. 将本地仓库上传到github
a. 先确保有本地仓库，再在github上创建一个仓库
b. name和电脑上的目录名一样，其他东西不动，创建
c. 点击SSH地址！然后复制页面上这行代码运行git remote add origin git@github.com:xxxxxxxxx/git-demo-1.git
d. 复制第二行 git push -u origin master运行

3. 在github上创建仓库并下载
a. 创建时勾选initialize this … ，Add .gitignore 选node，Add a license 选MIT License
b. 进入仓库点右上角绿色clone or download
c. 点 use SSH，并复制下面的地址
d. 终端进入桌面运行git clone 地址，于是将仓库下到了电脑上
e. 进入文件夹git init，初始化本地仓库

四.上传更新
1.git add .
2.git commi -m “第一次更新”
3.git pull（将网上更新的文件拉到电脑上）
4.git push（上传）