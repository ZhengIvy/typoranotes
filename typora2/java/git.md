# 1. 为什么要用版本控制

1. 有后悔药可以吃
2. 利于团队开发
3. 而且git是用分布式来开发的，因此的话可以各机子互相传数据，而不是集中式的那样，在服务器上管理，那如果服务器坏了就麻烦了

# 2. git的优势

1. 大部分操作在本地完成，不需要联网
2. 完整性保证
3. 尽可能添加数据而不是删除或修改数据
4. 分支操作非常快捷流畅
5. 与linux命令全面兼容

# 3. git的结构



<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309110736.png" alt="image-20210309110735986" style="zoom:67%;" />

# 4. Git和代码托管中心

1. 局域网环境下

   GitLab服务器

2. 外网环境下

   - GitHub
   - 码云

代码托管中心的任务：维护远程库

## 1. 团队间合作

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104722.png" alt="image-20210310104722558" style="zoom: 33%;" />

1. 小明创建了远程库并把本地库的代码push到远程库中
2. 在一个团队的小红把该项目克隆到本地
3. 小红添加了些代码之后把该项目又push到远程库中
4. 小明使用pull更新本地库的项目

## 2. 跨团队的合作

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104800.png" alt="image-20210310104800445" style="zoom: 50%;" />

1. 跨团队合作不需要外援加入你的团队的仓库，而是先fork一份到远程库中
2. B克隆到本地后添加代码后再push到远程库
3. 完事之后B发起pull request，表示写完代码想要合并到你的仓库中去
4. A便接收到了请求并进行审核
5. 如果审核成功的话就进行merge操作，也就是A仓库中就会有B写好的代码了

# 5. Git命令操作

## 1. 本地库初始化

命令： `git init`

效果：

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104834.png" alt="image-20210310104834101" style="zoom:50%;" />

注意：.git目录中存放的是本地库相关的子目录和文件，不要删除，也不要胡乱修改

## 2. 设置签名

1. 形式

   用户名：Ivy

   Email地址: ivymartin07@gmail.com(随便一个邮箱都可以，并不需要发邮件)

2. 作用：区分不同开发人员的身份

3. 辨析：这里设置的签名和登录远程库(代码托管中心)的账号密码没有任何相关

4. 命令

   - 项目级别/仓库级别：仅在当前本地库范围内有效

     - git config  user.name Ivy

     - git config user.email  ivymartin07@gmail.com

     - 信息保存位置： `./.git/config`

       <img src="https://raw.githubusercontent.com/Ivy0700/Figurebed/main/img/20210307113222.png?token=AMVITW4GTOL4Z4TN2OTMHO3AIREYG" style="zoom:67%;" />

   - 系统用户级别：登录当前操作系统的用户范围

     - git config --global user.name Ivy
     - git config --global user.email  ivymartin07@gmail.com

     - `cd ~`进入系统用户的家目录，相当于windows的`c/user/用户名`
     - 信息保存位置： `~/.gitconfig 文件`

     <img src="https://raw.githubusercontent.com/Ivy0700/Figurebed/main/img/20210307113249.png?token=AMVITW426RILNKJPD3253VLAIREZ6" style="zoom:67%;" />

   - 级别优先级

     - 就近原则：项目级别优先于系统用户级别，二者都有时采用项目级别
     - 如果只有系统用户级别的签名，就以系统用户级别为准
     - 二者都没有不允许

其实一般的话我们设置全局的签名就可以了，除非有特殊情况哈

## 3. 基本操作

### 1. 状态查看操作

`git status`

查看工作区、暂存区的状态

### 2. 添加操作

`git add [file name]`

将工作区的新建/修改添加到暂存区

### 3. 提交操作

`git commit -m "commit message" [file name]`

将暂存区的内容提交到本地库,如果不加`-m`的话要在编辑器文本里面改，麻烦，所以一般就直接这样最好

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104927.png" alt="image-20210310104927432" style="zoom:50%;" />



对文件有修改之后的操作

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104953.png" alt="image-20210310104952998" style="zoom: 67%;" />

### 4. 查看历史记录

最完整的形式`git log`

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310105032.png" alt="image-20210310105032285" style="zoom:50%;" />

显示提交的历史记录

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310105109.png" alt="image-20210310105108884" style="zoom: 50%;" />

还有两个观赏性更好的操作

多屏显示控制方式：

​	空格向下翻页

​	b向上翻页

​	q退出

`git log --pretty=oneline`

`git log --oneline`

`git reflog` HEAD@{移动到当前版本需要多少步}

![image-20210310105151849](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310105152.png)

可以移动版本欸，那还是有后悔药可以吃的噢

### 5. 前进后退

本质

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310105248.png" alt="image-20210310105248471" style="zoom:67%;" />

- 基于索引值操作【推荐】

  `git reset --hard 【索引值】`

  <img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310105320.png" alt="image-20210310105320514" style="zoom:50%;" />

- 使用`^`符号：只能后退

  `git reset --hard HEAD^`

  注：一个`^`表示后退一步，n个表示后退n步

- 使用`~`符号：只能后退

  `git reset --hard HEAD~n`

  注：表示后退n步

- 然后呢`git log --oneline`是只显示之前的版本，意思是你退到以前的版本之后你就显示不了以前的未来版本啦

### 6. reset命令的三个参数对比

- soft

  - 仅仅在本地库移动HEAD指针

    <img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310105357.png" alt="image-20210310105357735" style="zoom:50%;" />

- mixed

  - 在本地库移动HEAD指针
  - 重置暂存区

  <img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310105417.png" alt="image-20210310105417843" style="zoom:50%;" />

- hard

  - 在本地库移动HEAD指针
  - 重置暂存区
  - 重置工作区

这些个参数到底啥意思呢？举出几个参数出来是为了理解hard参数，首先呢等级是由`soft->mixed->hard`逐级升高的，soft就只改本地库，然后暂存区和工作区还是老样子，所以看似是工作区和暂存区改了然后没有同步到本地库里去。

而mixed的话本地库和暂存区都改了，工作区没改，所以显示的文件内容是没改的，这样就相当于你改了文件内容，然后还没由提交到暂存区里面去。

而hard的话是三者都改，所以就是一个很同步的结果

### 7. 删除文件找回

其实你要删除文件，可以在工作区删除，然后可以把这个指令 add 和commit表示本地库也删除文件，那你想恢复的话就像上面一样，用一个索引就可以恢复到之前的状态了

- 前提：删除前，文件存在时的状态提交到了本地库
- 操作： `git reset --hard 【指针位置】`
  - 删除操作已经提交到本地库：指针位置：历史记录
  - 删除操作尚未提交到本地库：指针位置指向HEAD

### 8. 比较文件

`git diff [文件名]`

- 将工作区中的文件和暂存区进行比较

`git diff [本地库中历史版本] [文件名]`

- 将工作区中的文件和本地库历史版本记录比较

不带文件名可以比较多个文件，不指定文件名的时候可以和工作区的多个文件名进行比较哈

### 9. 分支管理

#### 1. 什么是分支？

在版本控制过程中，使用多条线同时推进多个任务

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310105441.png" alt="image-20210310105441675" style="zoom:67%;" />

讲下上面这个图，可以说有些就是命名的规范，首先master就是一个主分支(现在github已经把主分支改名为main)，然后feature之类的都是分支，而且实际上是复制一个一样的出来，然后在此基础上开发新的功能，开发完毕后就可以返回master进行合并，如果发现有bug的话，要修复bug，一般开辟的分支叫hot_fix,这个是假设你项目已经跑起来的情况下的bug修改，修改完再合并回去就可以了

#### 2. 分支的好处

- 同时并行推进多个功能开发，提高开发效率
- 各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任何影响，失败的分支删除重新开始即可。

#### 3. 分支的操作

- 创建分支

  `git branch [分支名]`

- 查看分支

  `git branch -v`

- 切换分支

  `git checkout [分支名]`

- 合并分支

  - 第一步：切换到接收修改的分支(被合并，增加新内容)上

    ​	`git checkout [被合并的分支名]`

  - 第二步： 执行merge命令

    ​	`git merge [有新内容分支名]`

  其实这个合并是根据版本号来的，所以的话你合并之后为什么还能同步是因为相当于在同一个版本下，而如果你加到本地库之后相当于两个分支在不同的版本了，那就不会同步了。看下下面这个链接把。

  https://blog.csdn.net/qq_42780289/article/details/97945300

- 解决冲突

  - 冲突的表现

    <img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310105518.png" alt="image-20210310105517939" style="zoom:67%;" />

  - 冲突的解决

    - 第一步：编辑文件，删除特殊符号
    - 第二步：把文件修改到满意的程度，保存退出
    - 第三步：git add [文件名]
    - 第四步：`git commit -m "日志信息"`
      - 注意：此时commit一定不能带具体的文件名

  - 冲突的理解: 这是基于版本号的理解，冲突发生在你对同一个地方的修改，那你merge的时候就会有错误，而且要去解决他，让你去手动解决，那你就找到和你的提交发生冲突的人，然后出来一个解决方案，接着就把你的提交就可以了，最后解决了冲突

  

### 10. Hash函数简介

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310105533.png" alt="image-20210310105533847" style="zoom:67%;" />

之前还没有想到是这样子的呃，其实是用哈希算出来的版本号，然后不同的哈希算法有不同的特点，因此他还有一个作用就是校验文件的完整性，因为你改变一下你的哈希值就不同了，那么就可以通过哈希值来校验你的文件的完整性哈

### 11. Git保存版本的机制

#### 1. 集中式版本控制工具的文件管理机制

![image-20210228111024154](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210228111024154.png)

是一种增量式，每次只保存修改的部分，最后你要那个版本的时候再拼接起来可以了，比较节约空间哈

#### 2. Git文件管理机制

![image-20210228131557971](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210228131557971.png)

快照是文件的一种状态。

`Snapshot is to a repository as screenshot is to a video,It's the content(files and folders) of a repository at some point in time, a state of a repository, if you will.`当你commit的时候，就等于保存了一次快照，instead of 存的是差异的version，git保存的是整个文件把，所以有些占空间，但不同的是如果是相同的文件的话，会删掉重复的文件，而是保留一个链接哈。

[what is snapshot](https://stackoverflow.com/questions/4964099/what-is-a-git-snapshot)

#### 3. Git文件管理机制细节

![image-20210228130208598](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210228130208598.png)

### 12.  Git分支管理的本质

![image-20210228162806929](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210228162806929.png)

![image-20210228162851562](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210228162851562.png)

![image-20210228163206340](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210228163206340.png)

这个还是知道的，之前有搞过哈

## 6. GitHub

## 4. 推送

git push [别名] [分支名]

![image-20210228211435690](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210228211435690.png)

## 5. 克隆

`git clone [远程地址]`

![image-20210228211638266](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210228211638266.png)

1. 完整地把远程库下载到本地
2. 创建origin 远程地址别名
3. 初始化本地库

## 6. 拉取

![image-20210228213008598](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210228213008598.png)

pull = fetch + merge

`git fetch [远程库地址别名][远程分支名]`

`git merge [远程库地址别名/远程分支名]`,注意这里的/不是或者的意思，而是`git merge origin/master`，就是觉得有点怪怪的把啊。

这样做的好处是fetch下来不会改变你原有的文件，而是先看看它里面写的是什么，`git checkout origin/master`,是你要的内容话你合并就好了哈。

## 7. 解决冲突

要点

- 如果不是基于GitHub远程库的最新版所做的修改，不能推送，必须先拉取。
- 拉取下来后如果进入冲突状态，则按照"分支冲突解决"操作解决即可。

怎么理解要拉取的这个点，因为github不帮你这样去检查的话，那你有可能push上去的时候就把原先的版本给覆盖掉了，而别人又在那个版本上写了东西，而你clone下来的时候他还没写，那这样就会造成比较大的麻烦，所以这个pull操作时非常好的！

而发生冲突就时另外一回事了，那你就要自己去商量解决下然后重新提交！

## 8. 跨团队协作操作

1. Fork

   ![image-20210301181421919](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210301181421919.png)

   也就是外援来点

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210301181618027.png)

 2. 本地修改，然后推送到远程

 3. Pull Request

    ![image-20210301181909092](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210301181909092.png)

## 9. SSH登录

## 10. Git工作流

![image-20210301211655906](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210301211655906.png)

不错不错，能懂。