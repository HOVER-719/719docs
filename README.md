# 719飞行器实验室Docs

[![](https://img.shields.io/badge/build-@719飞行器实验室-green)](https://github.com/HOVER-719/719docs)
[![](https://img.shields.io/badge/CI-ReadTheDocs-orange)](https://719hover.readthedocs.io/en/latest/)
[![](https://img.shields.io/badge/719飞行器实验室网站-blue)](https://719hover.readthedocs.io/en/latest/)

## 背景
为了让实验室拥有一个属于自己的域名，发布和共享一些信息，故构建此网站，本网站源代码由GitHub进行托管，大家可以在本地通过git拉取代码进行网站的更新，关于如何进行网站更新，其实很简单，在后面的部分我会讲解。本网站由ReadTheDocs自动化构建，这个网站会时刻监测GitHub仓库是否有新的代码提交，如果有则会进行一次构建，将构建好的html文件发布在预先定义好的域名上。

## 安装与使用
1. 注册个人Github账号
2. 安装git
#### Windows环境
去这个链接下载[Git](https://git-scm.com/)
#### Linux环境
```bash
sudo apt-get install git
```
3. 本地环境生成ssh公钥
由于后期可能出现你同时对个人仓库和实验室仓库都有提交，所以这里生成两个ssh公钥，分别导入到个人github和实验室github上。
#### Windows环境
在任意一个文件夹的空白处右键，选择“Git Bash Here”，输入以下命令：
```bash
ssh-keygen -t rsa -C "你的邮箱地址1"
```
输入完这个命令一直按回车，直到提示已完成ssh key的生成，这时在你的用户名目录下会有一个.ssh文件夹，里面就是ssh相关的私钥和公钥。

现在进行创建第二个ssh key，同样输入
```bash
ssh-keygen -t rsa -C "你的邮箱地址2"
```
不过，此时他提示你默认保存的位置需要你修改一下，例如下面的例子，就直接输入/c/Users/zhangrun/.ssh/id_rsa2，表示这时第二个ssh key，之后如果还想生成ssh key也可以按照这种方法。
```bash
$ ssh-keygen -t rsa -C "zhangrun.hit@qq.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/zhangrun/.ssh/id_rsa):
```
之后的过程也是一路回车，直到创建成功。

打开这个目录/c/Users/你的用户名/.ssh/，创建一个名字为config（没有后缀名）的文件，将下述内容写进去
```bash
#邮箱1对应账号
Host github.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa

#邮箱2对应账号
Host github2.com
HostName github.com
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa2
```

4. 将ssh key上传到github账号
分别将生成的两个ssh key上传到个人GitHub和实验室GitHub上，建议id_rsa.pub上传到个人账号上，id_rsa2.pub上传到实验室账号上。
打开git bash，输入
```bash
cat ~/.ssh/idrsa.pub
cat ~/.ssh/idrsa2.pub
```
将两串获得到的公钥复制，打开GitHub，点击右上角头像->Settings->SSH and GPG keys->New SSH key，将自己复制的ssh key粘贴到Key中，Title命名为你的名字。

5. 安装环境依赖
 - 安装python3
 - 安装pip3
 - 通过pip3安装sphinx、markdown支持、主题支持
```bash
pip3 install sphinx
pip3 install recommonmark
pip3 install sphinx_rtd_theme
```
6. 拉取代码
在git bash中找一个地方拉取本仓库代码：
```bash
git clone git@github.com:HOVER-719/719docs.git
```

7. 在代码根目录执行下面的命令，就可以进行编译，检查你的更改有没有错误
```bash
make html
```
也可以使用下面的命令生成一个本地可访问的页面，进行预览，记得把ip地址换成本机ip
```bash
sphinx-autobuild source build/html --host 192.168.31.4 --port 8080
```
上边这个例子执行后，就可以在浏览器中输入192.168.31.4:8080来看文档的更改了，这个命令会持续监测你的修改，实时编译更新，直到你手动把这个命令的执行关闭掉。

8. 文档的结构&如何添加一个文档
所有的文章内容都在source目录下，source目录下的.rst文件是整个网站的起始页，它规定了整个网站的结构、如何去向下索引细枝末节的文档
不同类型的文档可以分在不同的文件夹下，通过rst文件去索引下一级的rst，再通过rst文件来索引当前目录下的markdown文件。






### License

[GPL-3.0](LICENSE) © 719飞行器实验室