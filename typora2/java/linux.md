# Linux 课程内容

![image-20201009192535136](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009192535136.png)

![image-20201009192558525](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009192558525.png)

Linux的学习方向

1. Linux运维工程师
2. Linux嵌入式开发工程师
3. 在linux下做各种程序开发

Linux的应用领域

1. 个人桌面应用领域

2. 服务器应用领域

   java等项目部署到linux上进行

3. 嵌入式应用领域

## Linux基础篇

Linux介绍

1. Linux时一款操作系统，免费，开源，安全，高效，稳定，处理高并发非常强悍，现在很多的企业级项目都部署到Linux/unix服务器运行

2. Linux创始人

3. Linux的吉祥物 企鹅，tux，燕尾服

4. Linux的主要发行版 

   ![image-20201009201853603](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009201853603.png)

   > 咋有这么多版本呢，像我们去饭店吃饭，点菜的时候不能说我要一盘菜把，而是我要xxx菜，因为每个版本具体的东西时不一样的

5. 目前主要的操作系统:windows,android,车载系统,linux等

unix怎么来的

![image-20201009212930272](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009212930272.png)

> 一开始时那个蓝色格子的人搞出来了,然后很多大企业嗅到了赚钱的气息,纷纷在unix的基础上搞了自己的,但是收费很贵,这时候richard就说应该免费啊

Linux怎么来的

![image-20201009212152743](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009212152743.png)

> 这是基本的操作原理,用户对浏览器操作,然后进入shell阶实层把浏览器传过来的操作解释成linux懂的东西,然后传给操作系统,然后操作系统再去操作硬件

![image-20201009212424040](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009212424040.png)

> Richard就发到了GNU计划,这个计划的基本架构时这样子,就是上面的模式,然后linux就是响应这个计划而生的.

Linux和Unix的关系

![image-20201009212830911](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009212830911.png)

> 那这两个之间又有什么关系呢?因为一开始是unix,unix的基础上搞了AT&T,又搞了Minix,然后在这基础上就是用的linux的了哈

# Linux VM 和 Centos的安装

学习Linux需要一个环境,我们需要创建一个虚拟机,然后在虚拟机上安装一个Centos系统来学习

1. 先安装virtual machine vm12
2. 再安装Linux(CentOS 6.8)
3. 原理示意图,这里我们画图说明一下VM和CentOS的关系

![image-20201009221732941](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009221732941.png)

**几种连接方式**

![image-20201010170241510](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201010170241510.png)

![image-20201010170225368](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201010170225368.png)

> 这个就像是一座桥，只要你能通往一个对面，那对面的其他东西你也能访问得到

![image-20201010171632248](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201010171632248.png)

> 你又是怎么理解的NAT模式的呢？额，不知道怎么就蹦出了个母机哈，我首先是这么理解的，这个应该是在一个局域网内，才有一个相应的ip地址，然后自己的主机也是有一个对应的ip地址的，但是NAT模式呢就会用母机的地址而不是局域网的地址，这样的话基本每个主机的地址都不大相同，所以不会有ip冲突，虽然说同个局域网年内的访问不了linux，但是linux可以访问外网，因为可以使用代理进行，所以非常好，没有桥连接的缺点了，一般都用这个



## Centos的终端使用和联网

### 1. 终端的使用

点击鼠标右键，即可选择打开终端

![image-20201011102917940](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011102917940.png)

### 2.配置网络，可以上网

点击上面右侧的两个计算机的图标，选择启用 eth0,即可成功连接到网络

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011103333078.png" alt="image-20201011103333078" style="zoom:67%;" />

![image-20201011103346949](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011103346949.png)

### 3. vmtools的安装

#### 安装的需求

> 其实就是我在windows系统中粘贴了一些东西，想放在linux的系统中，但是发现不可行
>
> 其次是我想在两个系统之间创建一个共享的文件夹，大家可以共享一些数据，但是目前也是不可行的，所以我就需要一个vmtools的工具

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011103515625.png" alt="image-20201011103515625" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011103701748.png" alt="image-20201011103701748" style="zoom:67%;" />

#### 安装的步骤

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011103931977.png" alt="image-20201011103931977" style="zoom:67%;" />

#### 设置共享文件夹

![image-20201011110219670](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011110219670.png)

**ctrl+ 空格**可以在linux中输入中文



# Linux的目录结构介绍

## 基本介绍

linux的文件系统是采用级层式的树状目录结构，在此结构中的最上层是根目录"/",然后在此目录下再创建其他的目录。就像我们在windows一样最起码有两个根目录`c: d:`,但是呢linux就一个哈，就是root

**在Linux世界里，一切皆文件**

![image-20201011112328035](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011112328035.png)

系统帮你创建了默认的目录，是有讲究的，通过文件来管理设备

![image-20201011112826580](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011112826580.png)

![image-20201011113258709](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011113258709.png)

![image-20201011113426958](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011113426958.png)

![image-20201011113521903](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011113521903.png)

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011114241461.png)



**linux目录总结**：

1. linux的目录中有且只有一个根目录 /
2. linux的各个目录存放的内容是规划好的，不要乱放文件
3. linux是以文件的形式管理我们的设备，因此linux系统，一切皆为文件
4. linux的各个文件目录下存放什么内容，大家必须有一个认识
5. 学习后，你脑海中应该有一颗linux目录树



> /boot分区？ 就是你linux启动的时候需要些引导文件，默认就会放在boot分区下面
>
> swap分区的话就是交换分区，当你其他不够用的时候暂时会来这里？所以这里普遍也不需要太多，2个g就足够哈

# Linux实操篇 远程登录Linux系统

## 为什么要远程登录Linux系统

![image-20201011161211027](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011161211027.png)

> 你看这个，一般linux操作系统是不在我们的电脑上的，都是在公司的一个机房里，所以的话是需要你远程登录的，那那款软件呢就是`XShell5`,还有一款上传和下载的文件的软件是`Xftp5`

![image-20201011161412383](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011161412383.png)

![image-20201011164336403](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011164336403.png)

需要额外说下你这linux的sshd服务是需要打开的，就是专门为远程服务的？不然的话你远程登录连不上哈

**特别说明，如果希望安装好XShell 5就可以远程访问Linux系统的话，需要有一个前提，就是Linux启动了SSHD服务，该服务会监听22号端口**



## 安装XShell5 并使用

看老师的视频演示即可,基本是下一步即可

## XShell5 的关键配置

首先你是要获得机房linux的ip地址的，那怎么获得呢，那就是要linux联网之后会分配一个ip地址给你

![image-20201011201029808](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011201029808.png)

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011195441234.png)

XShell5 远程登录到Linux后，就可以使用指令来操作Linux系统

![image-20201011195957273](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011195957273.png)

然后就远程连上了linux啦

## 远程上传下载文件Xftp5

![image-20201011201229134](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011201229134.png)

### Xftp5 的安装配置和使用

安装就看老师的演示即可

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011202432952.png" alt="image-20201011202432952" style="zoom:50%;" />

连接到Linux的界面如下![image-20201011202822899](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011202822899.png)

## 如何解决XFTP5中文乱码的问题	

![image-20201011203010852](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011203010852.png)

点击确定刷新即可就可以解决中文乱码

# Linux实操vi和vim编辑器

## 介绍



![image-20201011205639480](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011205639480.png)

## vi和vim的三种常见模式

![image-20201011210021271](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011210021271.png)

### 正常模式

在正常模式下可以使用快捷键。

### 插入模式/编辑模式

在模式下，程序员可以输入内容

### 命令行模式

如上哈，我这里就不说了

### 快速入门案例

要通过vim保存一个Hello.java的文件，

1. ![image-20201011213350162](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011213350162.png)

   先创建一个这样的文件出来哈，然后你就可以写入程序

2. 在写之前你会发现诶，怎么按不动嘚？因为现在默认的是正常模式，不可插入，所以就按个`i`就可以了

![image-20201011213139487](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011213139487.png)

	3.  这时候写完了怎么退啊？按一个`Esc`，退出键，再`:wq`，这个意思是写入并退出，就是保存，然后就完成啦

----------------------------------2020.10.18 anki到此一游--------------------------------------------------------------

### 三种模式的相互转换(重要！！！)

![image-20201011212540434](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011212540434.png)

> 其实这个很简单哈，实际上上面写这个Hello.java的文件的过程就用了这些步骤，首先可以了解到的是要想进入一般模式都是直接按`esc`，但是命令模式多一种选择，可以输入命令行进入，然后呢一般模式进入编辑模式也很简单咯，也就`i`或者`a`,一般模式进入命令模式后，有三个命令，我一一解释哈，`:wq`,写入并退出也就是保存并退出的意思，`:q`，就是单纯退出的意思，适合你在看一个文件内容，然后啥也不动退出的情况，`:q!`的意思是写了但是不想保存直接退出，也就是强制退出的意思

### vi和vim快捷键

![image-20201011215636768](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011215636768.png)

p是粘贴

到最末行和最首行都是在正常模式下进行的

![image-20201011223231662](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201011223231662.png)

![image-20201012192529824](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012192529824.png)

# 开机、重启和用户登录注销

## 关机&重启命令

- `shutdown`
- `shutdown -h now`:表示立即关机
- `shutdown -h 1`:表示1分钟后关机
- `shutdown -r now`:立即重启
- `halt`：直接使用，效果等效于关机
- `reboot`：重启系统
- `syn`：把内存的数据同步到磁盘上

## 注意细节

当我们关机或者重启时，都应该先执行一下`sync`指令，把内存的数据写入磁盘，防止数据丢失，就可以帮我们保存未保存的东西，比较重要哈，要养成这个习惯

### 用户的登录和注销

![image-20201012193444012](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012193444012.png)

> 这个切换的意思是让你最好要干嘛的时候用普通用户操作，如果遇到权限不够的话再切换成root管理员

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012193930185.png" alt="image-20201012193930185" style="zoom:67%;" />

> 那看来还是我不是很行哈，我一直理解错意思了哈，注销的话还是那种logout，而不是真的销号，那种也是蛮危险的，你直接logout就好了哈，这个注销，是用户注销哈，就是root退出，实际上就是远程登录的账户可以退出，上面的图形运行级别的话指的直接在vm上退出无效，因为说实话也没必要退出啊，在本机上面，要么就关机好了，远程登录的才有必要退出把

# 用户管理

基本介绍：

![image-20201012200813535](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012200813535.png)

>  linux如何管理用户的？
>
> 他是一个分组的概念，一个人是可以在不同的组的，那我就觉得这个有点像朋友圈分组，可能会有限制什么功能把？现在还没怎么讲到，然后呢有一个用户家目录的概念，每个用户都有自己专属的家目录，这个要区别一下`user`目录，这个像是`program file`的目录，我觉得是一些应用程序啊什么的就会默认下载到这里，但具体每个用户是否都有一个这个文件夹呢？我觉得是有的把。

![image-20201012201748209](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012201748209.png)

## 添加用户

### 基本语法

`useradd[选项] 用户名`

### 实际案例

添加一个用户xm

![image-20201012202233875](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012202233875.png)

![image-20201012202219249](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012202219249.png)

创建xm用户后，home里面有小明的目录，同时会给小明分个组，就是取的小明的本名，并把小明放在这个组里面

特别地说明一下，`cd`表示切换文件目录

![image-20201012202545516](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012202545516.png)

看看，有小明的目录诶

给小明设置密码的时候使用![image-20201012204437119](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012204437119.png)

注意当你输密码的时候你会以为你啥都没输进去，实际上有的，然后你就按确认就可以了

## 细节说明

1. 当创建用户成功后，会自动地创建和用户同名的家目录

2. 也可以通过`useradd -d` 指定目录 新的用户名，给新创建的用户指定家目录

   ![image-20201012204543235](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012204543235.png)

## 用户设置或修改密码

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012205157119.png)

## 删除用户

![image-20201012205242545](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012205242545.png)

1. 删除用户xm，但是要保留家目录

   ![image-20201012205556385](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012205556385.png)

2. 删除用户xh以及用户主目录

   ![image-20201012205905395](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012205905395.png)

### 思考题

是否应当保留家目录？

再删除用户时，我们一般不会将家目录删除掉

## 

## 查询用户信息

![image-20201012211732990](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012211732990.png)

![image-20201012212054485](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012212054485.png)

![image-20201012212139867](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012212139867.png)

> 这里说一下哈，为什么你看id，名字那里组的和用户的都相同呢？之前说实话说的只是名字会相同没有想到id也相同哈

## 切换用户

![image-20201012212411123](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012212411123.png)

![image-20201012212848297](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012212848297.png)

---------------------------------------------------anki 2020.10.18-----------------------------------------------------

## 用户组

![image-20201012215703120](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012215703120.png)

## 介绍

类似于角色，系统可以对有共性的多个用户进行统一的管理

## 增加组

`groupadd 组名`

## 案例

![image-20201012220606973](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012220606973.png)

删除组的指令

![image-20201012221058270](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201012221058270.png)

### 增加用户时直接加上组

增加一个用户zwj，直接将他指定到wudang

![image-20201013103649369](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013103649369.png)

### 修改用户组

`usermod -g 用户组 用户名`

创建一个shaolin组，让将zwj用户修改到shaolin

![image-20201013104055812](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013104055812.png)

## 用户和组的配置文件

![image-20201013105041142](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013105041142.png)

> 对啊，你总得去瞧瞧你这个用户的配置在哪吧？你的组配置在哪吧？

![image-20201013105756134](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013105756134.png)

### `/etc/passwd`查看用户配置文件

![image-20201013110157824](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013110157824.png)



> 如果你看不到这些用户的话，那你就一直空格往下面找就可以看到了

### /etc/shadow 文件

口令配置文件

每行的含义：登录名；加密口令:最后一次修改时间，最小时间间隔，最大时间间隔，警告时间：不活动时间，失效时间，标志

![image-20201013110701946](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013110701946.png)你看诶，之前删掉的用户这些的信息都没有删掉

### /etc/group文件

![image-20201013110853840](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013110853840.png)

> 然后你对应小组的用户你是看不到的

# 实用指令

## 指定运行级别

![image-20201013112203444](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013112203444.png)

有七个级别

![image-20201013112215075](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013112215075.png)

![image-20201013112629045](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013112629045.png)

## 切换指定运行级别的指令

### 基本语法	

`init [012356]`

### 应用示例

通过init来切换不同的运行级别，比如从5->3，然后关机

![image-20201013113730959](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013113730959.png)

### 面试题

如何找回root的密码,如果我们不小心忘记root密码，怎么找回？

思路：进入到单用户模式，然后修改root密码就可以了，因为进入单用户模式，root不需要密码就可以登录

![image-20201013114037077](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013114037077.png)

总结

开机->在引导时输入 回车键-> 看到一个界面输入一个 e->看到一个新的界面，高亮到选中第二行(编辑内核)再输入一个e->在这行的最后输入 1 ->再输入 回车键 -> 再次输入b，这是就会进入到单用户模式，使用passwd root 来修改root密码 

然后你有疑问这不是谁都可以改密码吗？不是的，这个有个硬性要求，你必须进入机房，不能远程操作，必须是你在linux本机上操作才是可以的。

### 课堂练习：

请设置我们的运行级别，linux运行后，直接进入到命令行界面，即进入到3运行级别

`vim /etc/inittab`

将`/etc/inittab的id:5:initdefault`这一行的数字

命令:`init[012356]`

**如果有人故意把你的模式设置成了1的话，就是你一开机就关机的话，那怎么办？**

同样还是进入单用户模式，直接改就可以了哈

## 帮助指令

### 介绍

当我们对某个指令不熟悉时，我们可以使用Linux提供的帮助指令来了解这个指令的使用方法

![image-20201013190555248](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013190555248.png)

**提示下：在linux中以`.`打头的文件是隐藏文件**

![image-20201013191041738](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013191041738.png)

![image-20201013191445831](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013191445831.png)

所以有两个指令，你可以用help或者man(stands for manual)

## 文件目录类

![image-20201013192910908](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013192910908.png)

`pwd`:present working directory

![image-20201013194809126](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013194809126.png)

### ls指令

![image-20201013195125624](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013195125624.png)

感觉就是查看属性的作用，不过是以list的形式

### ls

![image-20201013201516349](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013201516349.png)

感觉一般不会用这个把，因为这个是横着排的，影响可读性

### ls -l

![image-20201013201503254](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013201503254.png)

这样的话就相当于`ll`了

### ls -la

![image-20201013201744889](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013201744889.png)

这个就把隐藏的文件给显示出来了

### cd指令

![image-20201013201933528](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013201933528.png)

#### 相对路径和绝对路径

我感觉我终于在这里懂了？![image-20201013202925278](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013202925278.png)

这个相对路径啊，看`..`的意思是返回上一路径，在该路径下有一个home，那的确是啦

> 很有趣哈，那`../../root`又是什么意思？返回两个上级然后去root目录
>
> 不过说实话的话这好像和我们之前在html里面不是很一样？sorry 是一样的哈

### mkdir

![image-20201015160449172](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015160449172.png)

创建目录的(make directory)

#### 创建一个目录

![image-20201015162342885](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015162342885.png)

#### 创建多级目录

![image-20201015185808412](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015185808412.png)

### rmdir

![image-20201015185902572](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015185902572.png)

![image-20201015190040486](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015190040486.png)

#### 删除空目录和非空目录的操作

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015190458197.png)

`-rf`:应该是remove force 的意思，就是强制删除

### touch

![image-20201015191404246](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015191404246.png)

![image-20201015191559732](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015191559732.png)

#### 一次性创建多个文件

![image-20201015192228476](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015192228476.png)

也是ok的

#### 与vim的区别

1. vim是直接进入编辑页面，相当于打开一个word文档写完好后保存，而touch是直接右键新建不仅如此编辑页面
2. vim一次性就创建一个文件，而touch可以一次性创造多个文件

### cp[重要]

![image-20201015192257454](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015192257454.png)

`copy`
`-r`:r代表recursion，就是不断复制，所以的话就可以复制整个文件夹

![image-20201015193405256](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015193405256.png)

#### 案例

将`/home/test`整个目录拷贝到`/home/zwj`目录

![image-20201015194406621](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015194406621.png)

##### 强制覆盖

![image-20201015194721347](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015194721347.png)

#### 小细节 上下箭头

可以通过上下箭头的键，调出原来使用过的指令

### rm

![image-20201015195203902](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015195203902.png)

![image-20201015201155372](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015201155372.png)

> 感觉这个就是以文件为单位搞的，所以删目录的时候，首先会进入目录，然后再删掉一个个文件哈。因此的话，和前面的`rmdir`比较的话那个就是纯粹用来删空文件夹的，作用很明确哈

![image-20201015201803648](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015201803648.png)

![image-20201015201854434](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015201854434.png)

### mv指令

![image-20201015201911488](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015201911488.png)

> 这个可以其实这么理解哈，重命名可以看做是在同一目录下的移动，所以就没什么特别的，还是依照move处理也很好理解，当你进入这个目录下，发现已经有这个名字了，那你就把这个按照他说的移动到目标文件下就可以啦，本质是一样的哈。当你想要重命名的时候，你也就可以很容易地想到这个了

![image-20201015203620854](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015203620854.png)

#### 小细节点

![image-20201015204053454](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015204053454.png)

![image-20201015204205753](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015204205753.png)

> 其实呢，你看上面这两种移动的方法，一个是移后保持原来的名字，另外一个则修改了名字。那老师上面说的原理就感觉不是很成立的感觉了，我觉得还是，流嘛，这玩意是通过流来完成的，那就是创造一个文件粘贴过去，然后给他起名，如果你没有给他起名的话，他就默认按照原来的名字

### cat指令

![image-20201015204529015](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015204529015.png)

> 以只读的方式，不能修改

![image-20201015210503269](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015210503269.png)

### more指令

![image-20201015204822812](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015204822812.png)

额，所以怎么不直接用more代替cat呢，md，真的是太多指令了

### less指令

![image-20201015211310624](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015211310624.png)

> 适合查看大型文件，因为是一页一页加载的



### > 指令和>>指令

![image-20201015213000778](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015213000778.png)

> `>`：会将原来的文件内容进行覆盖
>
> `>>`:追加，不会覆盖原来文件的内容，而是追加到文件的尾部

![image-20201015214148685](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015214148685.png)

说明：`ls -l > a.txt`，将`ls -l`显示的内容覆盖写入到`a.txt`文件，如果该文件不存在，就创建该文件

![image-20201015214541203](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015214541203.png)

![image-20201015214734008](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201015214734008.png)

> 这个一开始想的是怎么cat不是只读吗，怎么还能把文件复制过去呢？然后想想做到这个功能的不是cat而是`>`，它这个指令就和前面一样，把你当前显示出来的东西，写入到某文件里了，这个就相当于复制粘贴文本内容了，没想到这些指令也可以实现哈，之前都是通过`cp`实现的

### echo指令

![image-20201016084330196](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201016084330196.png)

![image-20201016084521632](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201016084521632.png)

那我大概明白了上面的`echo "内容" > aaa.txt`，就是先输出到控制台，然后copy过去

### head

![image-20201016084653197](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201016084653197.png)

咋感觉和less好像呢，但还是不一样吧，使用起来的感觉

![image-20201016085242347](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201016085242347.png)

显示前5行，但和less不同的是就是没less那么多功能，翻页之类的，只是单纯显示多少行然后任务就结束退出了，

### tail

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201016085342938.png)

![image-20201016085537631](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201016085537631.png)

显示最后5行	

![image-20201016090326522](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201016090326522.png)

就是如果你在其他地方追加了一些或者是修改了一些东西的话，你用tail就可以实时监测到，而且有意思的是tail这个单词本身也就有追踪的意思

#### 细节

你发现退不出来了？

`ctrl+c`就可以解决哈

### ln

![image-20201016090712441](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201016090712441.png)

![image-20201016092610275](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201016092610275.png)

![image-20201016093816192](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201016093816192.png)

首先去看了下，链接那里，实际上就是一道任意门，通往root的文件夹，所以本质`linkToRoot`是一个文件夹，所以从删除的话也是删除一个文件夹，呃呃呃呃呃，但是呢，为什么不能加一个`\`在`linkToRoot`后面我就不知道为什么了。所以删除的操作都是按照删除文件夹的操作来的，但至于不能加那个我就疑惑了，听说会把整个root文件给删掉哈

### history

![image-20201016093858625](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201016093858625.png)

#### 显示所有的历史指令

![image-20201016095924863](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201016095924863.png)

![image-20201016095951186](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201016095951186.png)

显示10个

![image-20201016100052569](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201016100052569.png)

执行有序号的指令

## 时间日期类

![image-20201016100245669](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201016100245669.png)

### date指令，显示当前日期

![image-20201016100338082](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201016100338082.png)

#### 自己自定义格式的

![image-20201017144422704](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017144422704.png)

![image-20201017151101872](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017151101872.png)

#### 设置日期

![image-20201017152148707](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017152148707.png)

### cal指令

![image-20201017152322383](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017152322383.png)

## 搜索查找类

### find指令

![image-20201017153146547](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017153146547.png)

![image-20201017153328654](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017153328654.png)

#### 通过名字查找文件

![image-20201017153814224](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017153814224.png)

#### 通过用户查找文件

![image-20201017153929491](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017153929491.png)

#### 通过文件大小查找文件(+n 大于 -n 小于 n等于)

![image-20201017154628898](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017154628898.png)

#### 查找所有的txt文件

![image-20201017155234382](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017155234382.png)

### locate指令

![image-20201017155226246](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017155226246.png)

![image-20201017155937217](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017155937217.png)

### grep指令和管道符号

![image-20201017160345109](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017160345109.png)

#### 案例：在hello.txt文件夹中，查找`yes`所在行，并且显示行号

![image-20201017160910438](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017160910438.png)

> 讲下这个管道的理解，你可以理解为一个`|`，长得很像一个管道把，上面的把拿到的结果 传给下面的，作为输入，所以的话就很简单了吧

## 解压缩和压缩类

### gzip/gunzip 指令

![image-20201017163704073](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017163704073.png)

![image-20201017164357182](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017164357182.png)

> 细节说明：
>
> 当我们使用`gzip`对文件进行压缩后，不会保留原来的文件

#### 解压

![image-20201017164803652](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017164803652.png)

### zip/unzip指令

### 

![image-20201017165040592](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017165040592.png)

#### 案例

#### 1. 将/home下的所有文件进行压缩成`mypackage.zip`

![image-20201017171114963](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017171114963.png)

![image-20201017171150665](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017171150665.png)

#### 2.`mypackage.zip`解压到`/opt/tmp`目录下

![image-20201017171752402](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017171752402.png)

### tar指令

![image-20201017172540151](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017172540151.png)

#### 案例1：压缩多个文件，将`/home/a1.txt`和`/home/a2.txt`压缩成`a.tar.gz`

![image-20201017174428984](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017174428984.png)

#### 案例2:将`/home`的文件夹压缩成`myhome.tar.gz`

![image-20201017174825295](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017174825295.png)

#### 案例3：将`a.tar.gz`解压到当前目录

![image-20201017175327513](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017175327513.png)

-z  ：透过 gzip  的支持进行压缩/解压缩：此时档名最好为 *.tar.gz

> 这里就是有一个问题哈，为什么我们要用`z`?，然后呢看了一下，他不止有压缩的功能,
>
> emem就相当于一个技术支持把，然后x就去用这个技术实现，v就是看你操作了啥，f就是指定文件名？



#### 案例4：将`myhome.tar.gz`解压到`/opt/tmp2`目录下

![image-20201017175720371](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017175720371.png)

指定解压到的那个目录，事先要存在才能成功，否则会报错

> 这里就是注意一个`-C`,就是这样写的，应该就是代表`change`的意思。

> ~~无语哈，你说看操作就懂了，然后我完全没有明白意思哈~~

# 组管理和权限管理

![image-20201017205626173](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017205626173.png)

![image-20201017205719110](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017205719110.png)

## 查看所有者

![image-20201017205856337](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017205856337.png)

![image-20201017210715191](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017210715191.png)

![image-20201017210915239](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017210915239.png)

> 哈，原来human readable是显示在这里啊，果然用google就是好，你上百度完全找不到
>
> 而且这个指令就是原来的那个查看文件的指令哈，就只是多加了选项而已

### 案例

创建一个组police,再创建一个用户tom,将tom放在police组，然后使用tom来创建一个文件`ok.txt`,看看情况如何

![image-20201017211628416](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017211628416.png)

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017211949229.png)

## 修改文件的所有者

![image-20201017212418495](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017212418495.png)

> 这个一般默认你用户在哪个组，那就默认你是属于哪个组的，但是呢可以改哈。
>
> 就像你的东西给了别人一样。

### 案例

要求使用root创建一个文件`apple.txt`,然后将其所有者修改成`tom`

![image-20201017212950509](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017212950509.png)

> 这个呢，你会发现所有者改变了，但他对应的组是没有改变的哈，你可以这里理解，root是一个甲方，然后police组是乙方，然后root把工作给乙方一个人，但是呢这个各种要求和改动都是属于甲方这边操作的，所以呢他还是属于root这个组的

## 组的创建

![image-20201017213301118](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017213301118.png)

## 文件/目录所在组

![image-20201017213509061](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017213509061.png)

### 案例

使用root用户创建文件orange.txt，看看当前这个文件属于哪个组，然后将这个文件所在组，修改到police组

![image-20201017214305596](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017214305596.png)

## 其他组

除文件的所有者和所在组的用户外，系统的其他用户都是文件的其他组

> 还是之前的公司举例子，甲方乙方这样子的，我们在接手一个任务，那肯定是除了这两个之外的公司都不掺和啦

## 改变用户所在组

![image-20201017214637616](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017214637616.png)

![image-20201017215409119](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201017215409119.png)

## 权限的基本介绍

![image-20201018091824850](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201018091824850.png)

![image-20201018091936785](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201018091936785.png)

### rwx权限详解

![image-20201018092019619](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201018092019619.png)

![image-20201018093138251](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201018093138251.png)

#### 说明下隐藏目录`.` ,`..`是什么意思

这个实际上代表的就是当前目录和上一级目录哈，不然你想想你是怎么回去上一级目录的，他这里也是有一个传送门的。

## 修改权限-chmod

![image-20201018095110722](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201018095110722.png)

### 案例1

给abc文件的所有者读写执行的权限，给所在组读执行权限，其他组读执行权限

![image-20201018100324146](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201018100324146.png)

### 案例2

给abc文件的所有者除去执行的权限。增加组写的权限

![image-20201018100523785](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201018100523785.png)

### 案例3

给abc文件的所有用户添加读的权限

![image-20201018100737057](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201018100737057.png)

### 用数字变更权限

![image-20201018101027493](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201018101027493.png)

#### 要求

将`/home/abc.txt`文件的权限修改成`rwxr-xr-x`，使用给数字的方式实现

这里我就不演示了哈，很简单，因为就是二进制而已哈

## 修改文件所有者-chown(增强版)

![image-20201018102004173](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201018102004173.png)

注意哈，这个`R`是大写的？ 之前见到的都是小写的诶

### 案例

将`/home/kkk`目录下所有的文件和目录的所有者都修改成tom

![image-20201018103542898](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201018103542898.png)

## 修改文件所在组-chgrp 增强版

![image-20201018103652942](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201018103652942.png)

![image-20201018103838487](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201018103838487.png)

## 最佳实践-警察和土匪游戏

![image-20201020112751423](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020112751423.png)

### 创建用户

![image-20201020113259667](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020113259667.png)

### jack创建文件，修改权限

![image-20201020113642810](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020113642810.png)

![image-20201020113918300](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020113918300.png)

### xh投靠警察，看看是否可以读写

先用root修改xh的组：

![image-20201020115750196](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020115750196.png)

使用jack给他的家目录 `/home/jack`所在组一个rx的权限，

![image-20201020115846701](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020115846701.png)

这时xh需要重新注销再到jack目录就可以操作jack的文件

![image-20201020120205905](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020120205905.png)

### 课后练习1

![image-20201020120412656](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020120412656.png)

我做完了，很简单，跟上面的差不多

### 课后练习2

晚上再练把，有一点点忘了哈

![image-20201020121705534](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020121705534.png)

# crond任务调度

![image-20201020121829616](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020121829616.png)

![image-20201020122354137](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020122354137.png)

![image-20201020213505189](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020213505189.png)

## 常用选项

![image-20201020212226288](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020212226288.png)

## 案例

![image-20201020212306415](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020212306415.png)

### 步骤如下：

1. crontab -e
2. `*/l * * * * ls -l /etc/ > /tmp/to.txt`
3. 当保存退出后就启动程序
4. 在每一分钟都会自动地调用`ls -l /etc >> /tmp/to.txt`

### 参数说明

![image-20201020214501069](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020214501069.png)

![image-20201020214625855](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020214625855.png)

## 任务调度的几个应用示例

![image-20201020215039103](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020215039103.png)

还有几个相关的指令也很好用哈

### 案例1

1. 先编写一个文件/home/mytask1.sh

   `date>> /tmp/mydate`

2. 给mytask1.sh 一个可以执行权限

   `chmod 744 /home/mytask.sh`

3. crontab -e

4. `*/1 * * * * ` /home/mytask1.sh

5. 成功

### 案例3

![image-20201021204748923](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201021204748923.png)

额，学了mysql也不知道这是什么

# Linux磁盘分区、挂载

![image-20201021205350020](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201021205350020.png)

是`gpt`哈，分区的话就是`c`,`d`，这种吧

第二个比较优越，了解就好，容量增加，分区变多了

## windows的分区

![image-20201021211158350](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201021211158350.png)

## linux分区

![image-20201021211442145](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201021211442145.png)

![image-20201021213317019](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201021213317019.png)

![image-20201021213417754](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201021213417754.png)

这个呢，`x`表示的是哪块盘，`~`表示的是哪个区，像主分区，扩展分区这样的，`IDE`的话就是hxd嘛，那就是hd

### 使用`lsblk(老师不离开)`指令查看当前系统的分区情况

![image-20201021215225488](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201021215225488.png)

![image-20201021215650208](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201021215650208.png)

> 我理解的是本身这里有几块磁盘，然后这些磁盘分出去作为文件等让他去存东西，像给c盘，d盘分空间一样

## 挂载的经典案例

需求是给我们的linux系统增加一个新的硬盘，并且挂载到`/home/newdisk`

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201021222326599.png)

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201021222343750.png)

![image-20201021223652033](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201021223652033.png)

### 如何增加一块硬盘

1. 虚拟机添加磁盘

2. 分区 `fdisk /dev/sdb`

3. 格式化 `mkfs -t ext4 /dev/sdb1`(mkfs 是 make file system)

4. 挂载  先创建一个 `/home/newdisk`,挂载`mount /dev/sdb1 /home/newdisk`(但有一个问题是这个挂载之后就没有了，是临时挂载的，所以就有了下一步)

5. 设置可以自动挂载(永久挂载，当你重启系统后，仍然可以挂载到`/home/newdisk`上)

   `vim /etc/fstab`

   `/dev/sdb1                                 /home/newdisk                       ext4    defaults        0 0`

看 老师的演示

分了区没有格式化，买了房子没有装修没法住人

### 具体操作步骤整理

1. ![image-20201022205443789](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022205443789.png)

2. ![image-20201022205528597](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022205528597.png)

3. ![image-20201022205628540](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022205628540.png)

4. ![image-20201022205909328](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022205909328.png)

5. 永久挂载

   ![image-20201022210419823](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022210419823.png)

   感觉有点像脚本诶

## 磁盘情况查询

### 1. 查询系统整体磁盘使用情况

`df -lh`

![image-20201022212016259](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022212016259.png)

### 2.查询指定目录的磁盘占用情况

`directory usage`

![image-20201022212201678](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022212201678.png)

![image-20201022212517402](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022212517402.png)

## 磁盘情况-工作实用指令

1. 统计/home文件夹下文件的个数

   ![image-20201022214231424](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022214231424.png)

2. 统计/home文件夹下目录的个数

   ![image-20201022214313229](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022214313229.png)

3. 统计/home文件夹下文件的个数，包括子文件夹里的

   ![image-20201022215016392](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022215016392.png)

4. 统计文件夹下目录的个数，包括子文件夹里的

   ![image-20201022215116165](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022215116165.png)

5. 以树状显示目录结构

   ![image-20201022220255469](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022220255469.png)



# 网络配置

## Linux网络配置原理图(含虚拟机)

目前我们的网络配置采用的是NAT

![image-20201022224435315](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022224435315.png)

> 然后这个ip地址不是固定的，所以需要联网
>
> 解释下这个虚拟网卡，其实很像唐顿庄园，外面给你连了个电话，外界的，但是内部也有电话，就管家和各个房间可以打电话，各个房间可以通过与管家的接触来和外面接触，但是问题是这个每天过后，每个房间都会改变，所以你需要打电话确定哪个房间是那个人，这样远程登录的时候才知道你要找的人是哪个房间的

Linux现在的ip地址：`192.168.100.128`

## 查看网络和IP网关

### 查看虚拟网络编辑器

![image-20201023084935340](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201023084935340.png)

### 修改虚拟网卡的ip地址

![image-20201023085022578](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201023085022578.png)

### 查看网关

![image-20201023085251182](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201023085251182.png)

### 查看windows环境中的VMnet8网络配置(ipconfig)命令

![image-20201023085321639](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201023085321639.png)

1. 使用ipconfig查看

   `192.168.100.1`

   ![image-20201023191737113](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201023191737113.png)

2. 界面查看

   <img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201023194525696.png" alt="image-20201023194525696" style="zoom:50%;" />

   俺这里是自动获取的诶，不知道为啥子

### ping测试主机之间的连通性

![image-20201023085707332](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201023085707332.png)

## linux网络环境配置

### 第一种方法(自动获取)

![image-20201023085947494](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201023085947494.png)

估计就是联网把，自动联网，你不用手动连了，但是缺点就是ip地址每次可能会不一样

缺点：linux启动后会自动获取IP，每次可能会不一样，这个不适用于做服务器，因为我们服务器的ip是需要固定的

### 第二种方法(指定固定的ip)

![image-20201023202824975](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201023202824975.png)

![image-20201023094044764](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201023094044764.png)

![image-20201023095422406](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201023095422406.png)

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201023095827438.png)

修改 后，一定要重启服务

1. `service network restart`
2. reboot 重启系统

> 但是这里说明一点，我联网各种都没有问题，就是有一个地方是有问题的，linux连windows连不上哈，windows ping linux是完全没有问题的，但i don't know 
>
> ![image-20201023203649982](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201023203649982.png)
>
> 啥都没动哈

#  进程管理

![image-20201023205034752](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201023205034752.png)

> 像排队一样哈，有人在小程序点单，有人在现场排队，一个是后台，一个是前台

![image-20201023205228912](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201023205228912.png)

## 显示系统执行的进程

说明：查看进行使用的指令是`ps(进程)`:一般来说使用的参数是`ps -aux`(奥克斯空调)

![image-20201024085716506](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024085716506.png)

### ps指令详解

`PID:Process id`

`PPID:parents process id`

![image-20201024090655587](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024090655587.png)

**要求：以全格式显示当前的所有进程**

![image-20201024091432797](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024091432797.png)

![image-20201024091036617](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024091036617.png)

这里用到了全格式，因为之前没用的时候是显示不出父进程的

## 终止进程kill和killall

![image-20201024092517609](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024092517609.png)

![image-20201024093116242](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024093116242.png)

### 案例2：终止远程登录服务sshd，在适当时候再次重启sshd服务

![image-20201024093555238](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024093555238.png)

### 案例3：终止多个gedit编辑器(killall,通过进程名称来终止进程)

![image-20201024094213899](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024094213899.png)

> 为什么说这种可以杀死多个进程呢？我是这么觉得呢，kill+进程号那摆明就是只能杀死一个进程了，但是killall+名称的话就像是你打开一个软件，然后你再在软件上进行各种操作，那就是有很多的子进程，所以的话就完美啦，你killall+名称是完全有理的

### 案例4：强制杀掉一个终端

![image-20201024101516799](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024101516799.png)

这个终端必须要强制删掉，你不加 -9 的话你是删不掉的，然后有`bin`就代表是终端哈拉

### pstree指令

以树状的形式展现

![image-20201024101739054](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024101739054.png)

## 服务(service)管理

![image-20201024114501855](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024114501855.png)

![image-20201024114556001](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024114556001.png)

### 使用电脑检查是否启动监听

![image-20201024114819140](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024114819140.png)

需要在windows服务与管理中打开`telnet`

### 一个问题：这种方式只是临时生效，重启系统后，还是回归以前对服务的设置



### 一共有多少服务呢？

![image-20201024115311560](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024115311560.png)

#### 方式1：

![image-20201024115821136](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024115821136.png)

#### 方式2：

![image-20201024115912787](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024115912787.png)

### 运行级别(重要哈)

![image-20201024120004367](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024120004367.png)

![image-20201024120202804](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024120202804.png)

![image-20201024120857959](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024120857959.png)

![image-20201024120921067](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024120921067.png)

> 在这里讲下为什么从服务讲到了运行级别，因为你这个运行级别啊，在每个不同的运行级别下面是不一定每个服务是开的，有些服务是按照运行级别自动开启关闭的。

### 1. chkconfig --list 查看服务

![image-20201024121338919](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024121338919.png)

### 2. grep 过滤

![image-20201024121408870](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024121408870.png)

### 3. 和grep同样效果

![image-20201024121453642](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024121453642.png)

### 4. 修改运行级别

![image-20201024121602126](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024121602126.png)

ssh实际上就是远程登录连接

### 案例

![image-20201024180604183](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024180604183.png)

## 动态监控

![image-20201024202451195](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024202451195.png)

> 站在山顶就可以动态看进程

![image-20201024202609584](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024202609584.png)

![image-20201024203620352](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024203620352.png)

### 杀死进程

![image-20201024203739140](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024203739140.png)

## 监控网络状态

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024204509148.png)

![image-20201024205147232](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024205147232.png)

### 查看sshd的连接状态

![image-20201024205517359](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201024205517359.png)

# RPM和YUM

## RPM

![image-20201025112338402](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025112338402.png)

> 个人理解的话就是一种文件格式，然后可以用来管理软件？？ 但是`setup.exe`也就起了个安装程序的作用罢了

![image-20201025112814340](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025112814340.png)

`qa:query all`

### 案例

请查询看一下，当前的linux是否安装了firefox

![image-20201025113608672](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025113608672.png)

emm所以呢基本上是又可以作为执行文件，又可以进行查询，嗯，看起来还是蛮有趣的哈

![image-20201025113753443](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025113753443.png)

### rpm的其他查询指令

![image-20201025114213833](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025114213833.png)

#### 查询rpm软件包信息

`rpm -qi file`

![image-20201025114632229](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025114632229.png)

#### 查询rpm安装了哪些文件，安装到了哪里去了

![image-20201025115155901](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025115155901.png)

#### 通过文件全路径名 查询文件所属的软件包

![image-20201025115416338](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025115416338.png)

#### 删除软件包

![image-20201025115952973](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025115952973.png)

![image-20201025115919803](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025115919803.png)

像依赖一样，idea中也有这个。带上`--nodeps`就是强制删除

#### 安装rpm包

![image-20201025120054281](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025120054281.png)

##### 安装firefox浏览器

步骤：先找到firefox的安装rpm包，你需要挂载上我们安装centos的iso文件，然后到`/media/`下去找rpm

` cp firefox-45.0.1-1.el6.centos.x86_64.rpm /opt/`

![image-20201025121540480](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025121540480.png)

> 实际上呢就是从镜像文件拿到一个安装包，但我们一般不在光驱里面装，所以的话就复制到`/opt`里面去，这个文件夹一般都是用来装安装程序的，大致思路就是这样，然后你就进行安装指令就可以了

## YUM

![image-20201025122346940](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025122346940.png)

管理rpm的，类似于maven？

**使用yum的前提是联网**

![image-20201025194058281](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025194058281.png)

## yum的应用示例

请使用yum的方式来安装firefox

### 先查看一下 firefox rpm 在yum服务器有没有

![image-20201025194655100](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025194655100.png)

### 安装

`yum install firefox`,默认安装最新的版本