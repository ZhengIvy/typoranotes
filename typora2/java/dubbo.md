## 为什么要使用dubbo

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200913154851564.png" alt="image-20200913154851564" style="zoom:80%;" />

> 首先，单一的应用架构比如说小型 的项目，超市收银那种，把一个项目涵盖所有功能部署到一个服务器上面，如果流量大的话可以为了引流，把一个项目部署到两个服务器上面，但是现在如果你想扩展功能的话就需要在一个项目里面改改改，而且扩展之后文件变得超大，服务器承担不了，性能得不了提升

所以接下来介绍了垂直应用架构

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200913154220248.png" alt="image-20200913154220248" style="zoom:67%;" />

> 可以把一个项目分成几个小的项目去跑，扩展也比较容易
>
> 缺点
>
> 1. 界面 + 业务逻辑不能实现分离(原话说界面的要求经常在改，难道改一次就要重新部署一次嘛？(我以为就是这样子的。。))
> 2. 应用之间不可能完全独立，大量应用之间需要交互(原来独立还真是完全独立啊，我以为就算垂直的 还有一些联系呢)

### 分布式服务架构

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200913155941114.png" alt="image-20200913155941114" style="zoom:67%;" />

> 好处就是解决了上述的垂直结构的缺点
>
> 1. 界面与业务分开
> 2. 能够不同的项目进行调用
>
> 所以这里就依靠了一种技术：`RPC,远程过程调用`，他举了个例子，我有些懵逼，一般情况下再用户web中调用别的方法啊啥的就直接创建实例对象，再调方法属性就行了，但是这里的话不行，需要依靠`RPC`技术才能成功(但我有个问题，他的用户web里面有后台的业务逻辑？不然他为什么这样举例？后面看看吧)
>
> 缺点就在于不能灵活地调度服务器的使用，比如说用户业务的流量大，但是只有10台服务器，商品web流量小，却有100台，这就很不合理，不能灵活地进行调用

#### 来啦来啦，更高级的来啦

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200913160707667.png" alt="image-20200913160707667" style="zoom:67%;" />

> 调度中心可以提高利用率

### RPC 的基本原理

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200913161017325.png" alt="image-20200913161017325" style="zoom:67%;" />

> 使用了网络编程诶
>
> 首先是client那边需要什么，就找client的小助手通过网络编程告诉给目标服务器上的项目，然后对方的小助手收到之后就从项目那里拿到数据再通过网络编程返回

![image-20200913161825516](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200913161825516.png)

> 所以`RPC`主要有几个注意的点，通信和序列化反序列化的速度。这是决定`RPC`效率的关键因素

**最后，回到dubbo，RPC的框架有很多，dubbo就是其中一个**





### dubbo的好处

1. 完善了上面分布式讲的缺点，智能负载均衡，不会让一台服务器过于闲置，也不会让一台过于繁忙

2. 服务自动注册与发现，我一直以为框架已经解决好了，不用说了，但正是因为解决好了，才要拿出来说哈

   <img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200913165818874.png" alt="image-20200913165818874" style="zoom:67%;" />

   比如说用户业务是1,2,3号服务器，支付业务是7,8,9,服务器，但你怎么知道呢？而且当有一个服务器坏了的时候，但你不知道，你访问了不就gg了吗，所以这时候有一个注册中心来管理这件事情，就像是一个管理狗的领养情况中心，每一只狗与每一个主人对应上，如果有一个人所养的狗的情况发生了变化，那就在名单上增删查改。可以及时获取消息

## 



## dubbo的设计

![image-20200913174206801](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200913174206801.png)

> 这玩意就是订阅者模式啦，provider的话打比方可以是service服务，consumer是前端的web服务，当前端想调service的时候就要根据注册中心给的名单去调用，那基本上就是这样子吧

### 直连式

#### 提供者

1. 创建一个maven web工程：服务的提供者
2. 创建一个实体bean查询的结果
3. 提供一个服务接口：xxx
4. 实现这个服务接口:xxxImpl
5. 配置dubbo服务提供者的核心配置文件
   1. 声明dubbo服务提供者的名称：保证唯一
   2. 声明dubbo使用的协议和端口号
   3. 暴露服务，使用直连方式
6. 添加监听器

#### 消费者

1. 创建一个`maven web `工程：服务的消费者
2. 配置pom文件：添加需要的依赖(spring,dubbo)
3. 设置dubbo的核心配置文件
4. 编写`controller`
5. 配置中央调度器(就是一个servlet:`DispatcherServlet`)
6.  



> 1. dubbo官方推荐必须有一个接口工程，他就是一个maven java工程
> 2. 要求接口工程里存放到内容如下
>    1. 对外暴露的服务接口(service接口)
>    2. 实体bean对象
>
> 

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200916223152690.png" alt="image-20200916223152690" style="zoom:67%;" />