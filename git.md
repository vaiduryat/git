# 安装

1、在腾讯软件安装中心下载

2、一直下一步

## 查看版本

```
git --version
```

## git结构

![](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200511115941510.png)

## 本地库和远程库交互的两种方式

### 团队内

![](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200511123320925.png)

### 跨团队

![](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200511123429405.png)

# 常用的git命令

## 本地仓库初始化

```
$ git init
```

.git文件默认是隐藏的，不可修改，不可删除

显示隐藏文件的命令

```
$ ll -LA
```

## 项目签名

### 系统级别

```
$ git config --global user.name "jiting"
$ git config --global user.email "1667677913@qq.com"
```

查看签名，在cd ~用户目录下的.gitconfig文件下

![](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200511134525009.png)

### 项目级别

```
$ git config user.name "jiting"
$ git config user.email "1667677913@qq.com"
```

查看签名：在当前项目的.git目录的config中

![](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200511134118470.png)

## 状态查看操作

```
$ git status
```

查看工作区/暂存区状态

## 添加操作

```
$ git add hello.txt
```

将工作区的“新建/修改”添加到暂存区

## 提交操作

```
$ git commit -m "the thist commit" hello.txt
```

将暂存区的内容提交到本地库

## 查看历史记录

```
$ git log  //只能查看当前及其之前的历史记录
```

![image-20200512104133628](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200512104133628.png)

空格：向下翻页

b:向下翻页

q:退出

```
$ git log --pretty=oneline  //只能查看当前及其之前的历史记录
```

![image-20200512104450782](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200512104450782.png)

```
$ git log --oneline //只能查看当前及其之前的历史记录
```

![image-20200512104628518](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200512104628518.png)

```
$ git reflog  //可以查看所有的历史记录
```

![image-20200512104842023](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200512104842023.png)

### 前进后退版本

基于索引值，前进后退版本

```
$ git reset --hard [部分索引值]
$ git reset --hard f55b52a
```

使用~：只能后退不能前进，HEAD~n表示后退n条记录

```
$ git reset --hard HEAD~1
```

**--soft、--mixed、--hard三者的区别**

--soft

仅仅在本地库移动HEAD指针

![image-20200512112622201](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200512112622201.png)

--mixed

在本地库移动HEAD指针

重置暂存区

![image-20200512112703501](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200512112703501.png)

--hard

在本地库移动HEAD指针

重置暂存区

重置工作区

![image-20200512113019488](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200512113019488.png)

## 删除文件并找回

前提：删除前，文件存在时的状态已经提交到了本地库

操作：git reset --hard [指针位置]

删除操作已经提交到本地库：指针位置指向历史记录

```
$ rm apple.txt
$ git add apple.txt
$ git commit apple.txt
$ git reset --hard 274d7cf
```

删除操作尚未提交到本地库：指针位置使用HEAD

```
$ rm apple.txt
$ git reset --hard HEAD
```

## 比较文件差异

git diff [文件名]：将工作区的文件和暂存区的文件进行比较

```
$ git diff apple.txt
```

git diff [本地库中的历史版本] [文件名] ：将工作区中文件和本地库历史记录比较

```
$ git diff 274d7cf apple.txt
```

不带文件名，将比较多个文件

```
$ git diff 274d7cf
```

# 分支

## 概述

![image-20200512204612786](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200512204612786.png)

## 分支操作

#### 查看分支

```
$ git branch -v
```

#### 创建分支

```
$ git branch hot_fix
```

#### 切换分支

$ git checkout hot_fix

#### 合并分支

第一步：切换到主分支

```
$ git checkout master
```

第二步：合并分支

```
$ git merge hot_fix
```

#### 解决冲突

冲突的表现

![image-20200512213015343](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200512213015343.png)

手动删除多余的内容

![image-20200512213208239](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200512213208239.png)

重新添加文件到暂存区

```
$ git add orange
```

重新添加到本地库

```
$ git commit
```

# git版本控制和分支原理

通过hash形成链表,从而形成版本链，通过改变HEAD指向，获取当前的版本

分支：在原有的master指针上，新增其他分支指针，切换分支，就是切换HEAD的指向

1、

![image-20200513095959795](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513095959795.png)

2、

![image-20200513100055853](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513100055853.png)

3

![image-20200513100145111](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513100145111.png)

4、

![image-20200513100251092](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513100251092.png)

5、

![image-20200513100343084](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513100343084.png)

# 远程仓库

## 查看远程仓库别名

```
$ git remote -v
```

![image-20200513112926200](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513112926200.png)

## 添加远程仓库别名

git remote add 仓库别名 仓库地址

```
$ git remote add origin https://github.com/vaiduryat/test.git
```

## 推送到仓库

git push 仓库别名 分支名

添加密码和账号

```
$ git push origin master
```

## 克隆仓库

git clone仓库地址

```
$ git clone https://github.com/vaiduryat/test.git
```

克隆效果：

1、完整的把远程库下载到本地

2、创建origin远程地址别名（git remote -v 查看远程库别名）

3、初始化本地库（会自动生成.git文件）

## 其他成员推送到某一账号的远程库

1、在某一账号邀请其他成员到团队

![image-20200513114618664](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513114618664.png)

2、登录其他成员账号，接收邀请

3、推送到仓库

```
$ git push origin master
```

注意：windows中的凭据管理记录用户名和密码，如果需要切换账号推送，先删除记录

![image-20200513115336200](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513115336200.png)

## 拉取

拉取相当于拉取远程仓库的某一分支加并与本地仓库合并

pull=fetch+merge

### 抓取与切换origin仓库的主分支

捉取：git fetch 仓库别名 分支名 

```
$ git fetch origin master
```

切换：$ git checkout [仓库名]/[分支名]

```
$ git checkout origin/master
```

### 把远程仓库的分支与本地库合并

$ git merge [远程仓库别名]/[远程分支名]

```
$ git merge orgin/master
```

### git pull 远程仓库别名 远程分支名

```
$ git pull origin master
```

### 解决冲突

如果不是基于GitHub远程库的最新版所做的修改，不能推送，必须先拉取。

如果拉取下来进入冲突状态，则按“分支冲突解决”，操作解决冲突再推送

# 跨团队协作

1、(先复制当前库地址发式给dfbb,dfbb登录访问这个地址)>然后Fork

![image-20200513221913478](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513221913478.png)

![image-20200513221932160](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513221932160.png)

fork 过来的仓库说明 回多下面一行(forked from at...)说明fork来源

![image-20200513222025375](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513222025375.png)

2 、dfbb(”东方不败”)本地修改，然后推送到远程 git push origin master

**3**  、dfbb在远程库中选择Pull Request

3.1 、然后点击里面的New pull requset

![image-20200513222154116](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513222154116.png)

3.2、然后点击 Create pull request

![image-20200513222216942](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513222216942.png)

3.3然后发送消息给,fork的库(ybq(岳不群))

![image-20200513223352789](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513223352789.png)

**4** ybq操作

![image-20200513223420331](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513223420331.png)

![image-20200513223431978](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513223431978.png)

5.对话 (这时还可以相互对话)

![image-20200513223510456](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513223510456.png)

![image-20200513223514837](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513223514837.png)

**6** 审核代码

![image-20200513223612755](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513223612755.png)

7、合并代码(回到对话Conversation>>合并操作如图)

![image-20200513223654049](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513223654049.png)

![image-20200513223702615](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513223702615.png)

![image-20200513223708199](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200513223708199.png)

8、上面操作完了就远程库就有合并内容>然后>将远程库修改拉取到本地

# SSh免登陆

1进入当前用户的家目录

```
$ cd ~
```

2删除.ssh 目录

```
$ rm -rvf .ssh
```

3运行命令生成.ssh 密钥目录

 

```
$ ssh-keygen -t rsa -C atguigu2018ybuq@aliyun.com
```

[注意：这里-C 这个参数是大写的 C] 

**3.2****后面直接回(使用默认)

4进入.ssh 目录查看文件列表

```
$ cd .ssh
```

```
$ ls -lF
```

**5** 查看 id_rsa.pub 文件内容

```
$ cat id_rsa.pub
```

6复制 id_rsa.pub文件内容,登录 GitHub,点击用户头像→Settings→SSH and GPG keys→**New SSH Key

然后>>key输入复制的密钥信息  Title 自定义输入标题

7回到工作区cd  > 创建远程地址别名

```
git remote add origin_ssh git@github.com:atguigu2018ybuq/huashan.git
```

8推送文件进行测试