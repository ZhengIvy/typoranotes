# 1. Basic Characteristics of Computer Networks

1. Fault Tolerance
2. Scalability(扩展性)
3. Quality if Service(QoS)
4. Security

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310103553.png" alt="image-20210310103552568" style="zoom:67%;" />

## 1. Fault Tolerance

1. Continue working despite failures
2. Ensure no loss of Service

例子就是当你回家时，有一个障碍物阻挡了你平常的道路，你会选择不回家吗？不会，而是另外选择一条道路

## 2. Quality of Service

1. set priorities(有优先级别，比如一个打电话，一个发短信，打电话的级别更高的，所以不会有延时，而发短信可能会有点延时)
2. Manage data traffic to reduce data loss,delay etc.

然后另外几个性质就不讲了，应该很好理解的

# 2. Network Protocols & Communications

## 1. Data Flow

### 1. Simplex (单工)

> Communication is always unidirectional(单向的) .
>
> One device can transmit and the other device will receive.
>
> Example : Keyboards, Traditional monitors

### 2. Half Duplex(半双工)

> Communication is in both directions but not at the same time.
>
> If one device is sending, the other can only receive, and vice versa.
>
> Example: Walkie-Talkies(对讲机) 很生动形象了

### 3. Duplex or Full Duplex(双工)

> Communication is in both directions simultaneously
>
> Device can send and receive at the same time.
>
> Example: Telephone line.

## 2. Protocols(协议)

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310103631.png" alt="image-20210310103630571" style="zoom:67%;" />

就是一些规定，交流是需要规定的，比如一个在说英语，一个在说中文，那肯定是听不懂的

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310103715.png" alt="image-20210310103715170" style="zoom:67%;" />

其实理解起来挺简单，就是先确定好和谁说话，然后问他愿不愿意交谈，再者看是否交谈的是同种语言，接下来看语速，语速太快的话那我就听不懂啦

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310103749.png" alt="image-20210310103748613" style="zoom:67%;" />

这要记的吗，无语啊！解释下最后一个什么意思吧，看你是单个发还是群发的这种

### 1. message encoding

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310103822.png" alt="image-20210310103822358" style="zoom:67%;" />

咋去理解这个呀，其实也不是没遇到过把，反正我们都知道信息都是要进行编码之后才能传输的。

### 2.  message formatting and encapsulation

![image-20210310103855551](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310103855.png)

其实就像我们寄快递一样，你要寄的东西要符合一定的格式包装起来，然后上面写着收件人和寄件人的信息。

### 3. message size

![image-20210310103926986](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310103927.png)

这个倒是不知道把，不过又好像知道的样子。而且break into small segments的话会给每个segment标号，这样就可以identify哪些missing，可能这样就可以找回来把。

### 4. message timing

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104017.png" alt="image-20210310104016822" style="zoom:67%;" />

解释一下flow control，可以理解为一段车流，控制车流的交警，如果没有控制就会不断有人涌进来，但是你个口就出去那么点人，秩序不太好，所以flow control的话可以保证传输的速度。

而response timeout指的是当你的receiver接收到之后会传个信息回去告诉他我收到了，那如果没收到的话，sender会等一段时间，过了那段时候后就再发送一次

### 5. message delivery options

![image-20210310104046072](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104046.png)

1. unicast(单播)，一对一传输，只有一个接收者
2. multicast(多播)，一个sender，多个receiver，但不是全部的receiver
3. broadcast(广播)，传输给all the network

看到这里不禁去比较和data flow的区别，虽然两者都看起来是有 多种选项，但本质是不一样的，那种其实是在unicast的情况下进行的data flow，也就是在一对一情况下是可以只能接收，还是不能同一时间接收发送，还是可以同一时间接收发送这种。

这些概念可能容易搞混吧

## 3. network types

### 1. P2P network(Peer-to-Peer network)  

原来p2p是这个意思，记得之前一直有一个p2p诈骗。

实际上是对等互联网络技术。

![image-20210310104109609](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104109.png)

1. 没有中心的主机控制

   不像 Client / Server network，有专门的server，而且基本上就是一个，可以获取所有client的数据，这个的话隐私性就不好，但是呢p2p就不存在这种问题，自己的数据自己控制把

2. 每个都是对等的

3. 适用于小型的应用(这个我倒是不咋知道为啥)

4. 扩展性不强(扩展性指的是网络上可以加设备，而peer to peer的话端口有限？？？呃)

### 2. Client Server Network

![image-20210310104128104](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104128.png)

1. 是有中心的主机的，交流就是在client 和 server之间。而且基本是master-slave的模式，话说不知道要不要改名噢。
2. 而且request-response model 表示你需要什么东西你首先要和server请求，然后server才会response，多少带点主从关系的把。
3. 扩展性好，毕竟可以连多台设备
4. 但是服务器可能overloaded，如果设备过多的话那就有可能把

## 4. Components of a computer network

![image-20210310104149565](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104149.png)

对应的是节点，介质，服务？ 不是很好用中文说出来啊

### 1. nodes

![image-20210310104205788](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104205.png)

终端和中间结点把，

![image-20210310104223968](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104224.png)

终端可以是电脑，打印机，等等。可以是 starting point of the communication or the ending point of the communication

![image-20210310104243765](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104243.png)

ok，终于是明白了intermediary node是啥了，因为之前想怎么样才是intermediary呢，看来的确没错，是介质

### 2. media

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104316.png" alt="image-20210310104316696" style="zoom:67%;" />

其实也就是link罢了

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104346.png" alt="image-20210310104345784" style="zoom:67%;" />

![image-20210310104415401](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104415.png)

### 3. services

![image-20210310104548310](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310104548.png)

就是一些服务把，跟网上搜的组成不同，除了介质和结点，还有软件和操作系统，这里的话算归在一起了吧

## 5. Classification of Computer Networks

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309111532.png" alt="image-20210309111532344" style="zoom:67%;" />

其实就是广域网，局域网和城域网。不过之前只知道局域网而已，而且也不是很懂局域网的具体意思

![image-20210308232559359](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210308232559.png)

![image-20210308232618857](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210308232618.png)

### 1.  局域网

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309111523.png" alt="image-20210309111522664" style="zoom:67%;" />

这个就是局域网啦！是局部地区的网络，可以让局部地区内的电脑进行交流沟通，不过有分为有线和无线的，有线的话就是以太网的那些，无线的就是wifi

### 2.  城域网

![image-20210309111935792](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309111936.png)

城域网，其实就是允许多个局域网进行交流，比如学校A有一个局域网，学校B也有一个局域网，那么A和B之间的交流就是通过城域网进行交流的。

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309112136.png" alt="image-20210309112135370" style="zoom:67%;" />

城域网的就是连起一个城市里面的局域网，然后例子的话其实我感觉我不是很懂

### 3. 广域网

![image-20210309112232437](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309112233.png)

然后你想想城市与城市之间怎么交流呢，那就是通过广域网，广域网还可以实现国家与国家之间的交流

![image-20210309112245884](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309112246.png)

这个例子挺好的，一看就明白。

### 4. Storage  Area Network(SAN)

好像是现在的新技术，新发展方向，特别是云计算把

![image-20210309112647439](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309112648.png)

比如google drive 就可以这样子做

## 6. Network Topology

其实这个意思蛮简单的，不过是不清楚到底啥意思而已。 拓扑实际上就是布局设计把。

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309112735.png" alt="image-20210309112735158" style="zoom:67%;" />

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309112741.png" alt="image-20210309112741197" style="zoom:67%;" />

然后有分为两种，一种是物理的，另外的就是逻辑的，物理的拓扑应该是arrange 结点怎么去放置，而逻辑的话就是处理data flow的，处理单工，双工，半双工之类的

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309112747.png" alt="image-20210309112747575" style="zoom:67%;" />

然后这里也有几种分类，不过不知道和上面的区别是啥

### 1. Bus Topology(总线拓扑)

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309112754.png" alt="image-20210309112754079" style="zoom:67%;" />

其实就像一个辆公交车一样，就是一条线上的。那么他的传输数据的方式的话就会比较直线把，没错的，比如你要从A把数据传给B，那你的信息整条线路上的都可能会收到，只不过可能会拒绝而已。

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309112801.png" alt="image-20210309112800760" style="zoom:67%;" />

所以他这里说了优势和劣势

1. 因为只用一条线，所以成本很低
2. 适合暂时的网络工作
3. 如果有的结点坏了，但是不影响别人

缺点：

1. 不具有容错性，不过我好像理解错容错性了，我之前理解的是如果一个坏了，那你有别的道路继续走，但是我觉得的意思是你这个坏了，但是不影响其他人进行，叫做容错性，而这里当坏的是某条线路的话，那你基本上整体都会坏掉，因为是共用的。
2. 不安全，虽然说别人可能拒绝你给的信息，但是万一拿了呢？那就不好了吧

### 2. Ring Topology(环形拓扑)

![image-20210309151326357](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309151326.png)

1. 环形拓扑也是一种总线拓扑，但是是闭环的
2. 是对等网络关系的局域网？所以大家都是平等的
3. 两个连接
4. 单向的(也就是只能顺时针or 逆时针，不能一下顺时针一下逆时针)
5. 发送信息和接受信息时需要用到token，也就是谁拿到token，谁就可以发送信息，不过他倒是没说接受信息怎么办，而且这个token是轮流拿的

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309152354.png" alt="image-20210309152353888" style="zoom:67%;" />

1. 有点奇怪把，虽然说是一种bus topology，但是呢连的方式还是有点不同的，他是node failure和link failure都会影响到整个的传输，奇怪吧，但是bus的node failure是影响不到的，所以你可以理解为，ring里面的每台电脑相当于门卫，而bus就是大家一起share一个过道而已。



![image-20210309154351667](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309154352.png)

1. 表现得比bus 好，他说是因为是closed的。
2. 但是link是weak的
3. 因为是p2p，所以是equal access

缺点

1. 单向的，node failure和link failure直接完蛋，不过找failure和修复会比bus简单
2. 应该是node越多，performance越差。
3. 因为你要给某个node传数据的时候会经过很多node，安全肯定是不够好的

### 3.  Star Topology(星形拓扑)

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309155049.png" alt="image-20210309155048864" style="zoom:67%;" />

1. 每个结点都和一个中心结点连接 hub or switch（暂时不知道有什么区别）
2. 中心管理
3. 所有的通路都会经过hub or switch，所以别的node不会拿到copy 数据了，安全性好

![image-20210309160423189](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309160423.png)

1. 很容易设计和实现，因为你可以直接加台设备进去就可以了
2. 是有中心管理的
3. 可扩展性的

缺点：

1. 如果中心的那个hub or switch坏了的话整个就会坏掉
2. 然后如果太多设备的话，中间的device 会overload，那就有可能会有瓶颈
3. 中间的部件是要钱的

![image-20210309160852249](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309160853.png)

然后两个星形拓扑可以连在一起通过一个repeater，不过这是啥我也不清楚哦

### 4. Mesh Topology(网状拓扑)

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309162534.png" alt="image-20210309162534253" style="zoom:67%;" />

就像一个网状的一样，和其他的电脑连了起来。而且是容错性的，因为你某个link failure了，不影响其他的交流，你可通过别的电脑再次和其他人交流，不过这样想起来就有点怪怪的把



<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309162637.png" alt="image-20210309162636853" style="zoom:67%;" />

1. 容错性，如果你某个link failure了，那你还是可以和其他link畅快地交流
2. reliable，可靠的，因为你无论怎么样，都可以把消息传到那个人手里（如果错的太多就不行了吧）

缺点：

1. 广播的时候会出现问题，但是没有例子吧，不知道这些东西平时哪里有出现。比如你要全部广播，然后被广播的那台机器又会广播？(那不是停不了了？)
2. 这个只适合小型的，不适合大型的网络

### 5. Hybrid Topology(混合拓扑)

![image-20210309165844211](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210309165845.png)

就是各种拓扑混合在一起。

## 7. IP Addressing

![image-20210310105728383](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310105728.png)

我感觉这里的笔记不见了？？？？？？？？？？？？

少了ipv6的东西哇。回头补吧

## 8. MAC Addressing(媒体访问控制)

![image-20210310110456641](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310110456.png)

mac address 是不会change的，一般大家的名字也不会改变，但是ip address是会change的，你在不同的地方就会有不同的ip地址

![image-20210310110642340](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310110642.png)

他说router需要ip address，switch需要mac address，等会哈，有点奇怪把。

这个的确是和我想的不一样，虽然之前我也不懂到底是怎么传输的。

可以想象成你要发送信息给别的地方，那你首先要把他的名字？和ip地址拿出来(你知道他的名字吗？)然后switch看名字，哦你要发送啊，再看看你要给的名字和地址？？？我觉得怎么说呢，很奇怪。

mac 地址就是**物理地址**，是局域网内的地址。而ip地址是连接不同网络之间的地址

![image-20210310114037049](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310114037.png)

1. 局域网的每个结点都是根据mac 地址来分辨的
2. 是物理地址
3. 独有的
4. 不能改变
5. 厂家决定的
6. 十六进制表示
7. 举个例子，48 bits = 4 * 12 = 4 * 2 * 6

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310173321.png" alt="image-20210310173320681" style="zoom:67%;" />

1. ip 是 32bit，mac是48bit都清楚了吧
2. ip是用十进制表示的，mac是用十六进制表示的
3. router需要ip地址，switch需要mac地址

有一个有趣的例子，因为我之前一直不知道到底信息是怎么样通过ip地址传输的，但是我感觉现在我有点头绪了。

比如有人传给你消息，然后通过你的ip地址找到你的wifi-局域网，然后wifi局域网是通过你的物理地址把信息传给你的！

## 9. Port Addressing

![image-20210310182719019](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310182719.png)

这只是一个举例，但我觉得还是没有那么恰当把，因为ip address就可以追踪到局域网了，然后靠mac address去识别是哪台设备，然后port address是设备上的应用程序

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310182906.png" alt="image-20210310182906645" style="zoom:67%;" />

![image-20210310183018849](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310183019.png)

![image-20210310200538311](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210310200538.png)

反正这几个都要就对了，但是我们现在连的时候好像又不要用mac address

总的来说，这个也很好理解吧，毕竟之前也明白过了

## 10. Switching techniques in Computer Network

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210312175030.png" alt="image-20210312175029077" style="zoom:67%;" />

之前了解过的switch是开关的意思，那这里的switch算是开关道路把，这样让你去最优的道路。不过one-to-one connection啥意思我就不知道了

![image-20210312204727637](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210312204728.png)

有三种switching techniques,分别是线路交换，报文交换，分组交换。

### 1. Circuit Switching(线路交换)

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210312205105.png" alt="image-20210312205104914" style="zoom:67%;" />

首先看名字就是以circuit 为准的，所以的话circuit是比较重要的，而线路交换这个词反而让我难以记住把。

其实看步骤，很简单就三步，这个path是专用的，也就是没有其他communication和你shared这个path

1. 先建立连接
2. 进行数据传输
3. 关闭连接

举个例子就是打电话，先要接通了再能说话，说完话就挂掉了

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210312205515.png" alt="image-20210312205514900" style="zoom:67%;" />

这个绿色的线就代表接通好的线路

### 2. Message Switching(报文交换)

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210312205822.png" alt="image-20210312205821991" style="zoom:67%;" />

其实就是专门用来传输信息的，电话已经有了，现在就轮到短信了。

比如sender传输一个数据，~~比较大，所以就要break into small pieces~~，那传出去之后，中间结点就会拿一个箱子去收集这些small pieces，然后再forward转发别人。

为什么不适合实时应用？因为你要store啊，那应该是一个完整信息了，比如就传一句话，一句话就是完整的信息，但是实时应用你哪知道什么时候是个头啊，所以不可以这样子哈

![image-20210312225820384](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210312225820.png)

我感觉neso 这里讲错了，message switching没有分成small packets，顺便说一句，这个switching的出现顺序是按照这里来的

所以message 的话是整个报文传到一个结点，store之后根据他上面写的地址进行转发，所以的话可能会有延时把，因为要等待，但是不用先去建立连接。

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210312205938.png" alt="image-20210312205938225" style="zoom: 67%;" />

这就是一个传输中的模拟，还挺简单的

### 3. Packet Switching(分组交换)

![image-20210312210335241](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210312210335.png)

那这个和报文交换是同级别的啊，我觉得有点奇怪把，因为感觉像是报文交换的具体细节。就像是发送消息不就既是报文交换，又是分组交换吗

1. 因特网就是用这种交换的
2. 信息被broken into 各个chunks被叫做packets
3. 每个packet是独立送过去的
4. 每个packet都有出发地和 目的地的ip地址和sequence number
5. sequence number的作用
   1. 用来编号，这样送过来的packet才可以正确排序
   2. 可以查看漏了哪些packet
   3. 可以利用编号告诉他1号packet收到了，也是保证完整性把

看到这里就会想这个和报文交换的区别在哪里？

首先报文交换是采用 store and foward的形式的，而且没有small pieces，所以也不需要sequence number了，而分组交换的话是分成每个package 的，所以每个package可以分为固定路线传输和不固定路线传输的情况，也就是一下的两种

![image-20210312210716981](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210312210717.png)

还有两种方式呢

#### 1. Datagram Approach

![image-20210312211152359](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210312211153.png)

1. 无连接的交换，也就是每个packet是不连接的，所以可以你走这条路我走另外一条路
2. 每一个small piece都可以叫做datagram
3. datagram里面有关于目的地的信息，就像一个包裹一样，到中转站后才知道把你送去那里
4. 路线是不固定的
5. 中间节点决定packet的方向

![image-20210312211338756](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210312211339.png)

有四个packet

![image-20210312211359063](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210312211359.png)

每个packet可以走不同的方向，由中间节点决定

![image-20210312211412020](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210312211412.png)

最后因为有sequence number就可以排序

#### 2. Virtual Circuit Approach

![image-20210312211456192](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210312211456.png)

1. 是有向连接的交换，也就是路线是固定好的，像是circuit switching 的这种
2. 在发送之前有一个计划好的路线
3. 有专门的请求和接受的packet去建立连接
4. 这个路线是固定的

那和circuit switching的区别在哪里呢？

virtual的path不是dedicated的，可以和别的communication共享，而单纯的circuit是专用的

## 11. Layering in Computer Network

![image-20210313101139787](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313101140.png)

就是分层的意思，分成多个层

1. 提供模块化的设计
2. 很容易发现出错的地方

![image-20210313103521469](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313103521.png)

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313103603.png" alt="image-20210313103603568" style="zoom:67%;" />

### 1. OSI Model

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313103628.png" alt="image-20210313103628748" style="zoom:67%;" />

开放式系统互联通信参考模型

1. OSI的全称是 open system interconnection,开放式系统互联通信
2. 是一个模型，用来理解和设计互联网的使他能适应，健壮，而且能在不同的系统进行的，比如windows和linux
3. 不是一种协议，协议是规则，必须遵守，但这个的话有些是可以不遵守的

![image-20210313105015924](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313105016.png)

1. 如何便利不同系统之间的通信，在不改变硬件软件逻辑的情况下
2. 不是全部都用上的

#### 1. Part I

Part I 主要是让我们了解这些层里面有什么东西

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313111418.png" alt="image-20210313111418337" style="zoom:67%;" />

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313111513.png" alt="image-20210313111513331" style="zoom:67%;" />

笑死了，帮我们找了种记的方式

![image-20210313111831240](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313111831.png)

粗略地讲了一下两个devices之间是怎么样传输的，在传给中间结点前，sender要由上至下最后到第一层，中间相邻层之间会交互，但是中间结点也会进行最后三层的传输，一般是不会操作三层以上的，因为涉及到数据的东西了。最后receiver接收的时候也是由下往上进行交互的。

其实这么看的话本来你的数据就是来自一个应用，最后通过物理的线传输出去的。

#### 2. Part II

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313113856.png" alt="image-20210313113856416" style="zoom:67%;" />

模拟一个传送数据的过程

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313113936.png" alt="image-20210313113936239" style="zoom:67%;" />

在这里进行了转换。

![image-20210313114011289](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313114011.png)

虽然我也不知道session layer在这里干了啥子

![image-20210313114038195](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313114038.png)

给了传输层之后，传输层会加点info在里面

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313114107.png" alt="image-20210313114107289" style="zoom:67%;" />

网络层也会给点info在里面

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313114144.png" alt="image-20210313114144812" style="zoom:67%;" />

数据链路层也会加点信息进去

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313114215.png" alt="image-20210313114215680" style="zoom:67%;" />

最后物理层把数据转成二进制

##### (1) Application Layer

![image-20210313114941468](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313114941.png)

首先应用层是最接近用户的一层，他能够让用户去获得网络资源，应用层提供的服务如下，应该是用户可以选择的服务

1. **Mail Services:** This layer provides the basis for E-mail forwarding and storage.

   **邮件服务：**此层为电子邮件转发和存储提供了基础。

2. **Network Virtual Terminal:** It allows a user to log on to a remote host. The application creates software emulation of a terminal at the remote host. User's computer talks to the software terminal which in turn talks to the host and vice versa. Then the remote host believes it is communicating with one of its own terminals and allows user to log on.

   **网络虚拟终端：**它允许用户登录到远程主机。 该应用程序在远程主机上创建终端的软件仿真。 用户的计算机与软件终端对话，而软件终端又与主机对话，反之亦然。 然后，远程主机认为它正在与其自己的终端之一进行通信，并允许用户登录。

3. **Directory Services:** This layer provides access for global information about various services.

   **目录服务：**此层提供对各种服务的全局信息的访问。(不过感觉也不懂啥意思把)

4. **File Transfer, Access and Management (FTAM):** It is a standard mechanism to access files and manages it. Users can access files in a remote computer and manage it. They can also retrieve files from a remote computer.

   **文件传输，访问和管理(FTAM)：**这是访问文件并进行管理的标准机制。 用户可以访问远程计算机中的文件并进行管理。 他们还可以从远程计算机检索文件。

##### (2) Presentation Layer

![image-20210313115801224](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313115801.png)

表示层负责的是两个系统之间交换的信息的语法和语义。 表示层要注意以如下方式发送数据：接收方将理解信息(数据)并能够使用该数据。 两种通信系统的语言(语法)可以不同。 在这种情况下，表示层将扮演角色**翻译器**的角色。

1. 能够进行翻译，因为不同计算机可能会使用不同编码方法，那表示层就要负责能让对面的系统看懂(可能会有约定好的统一编码格式)
2. 能够对信息进行加密
3. 能压缩信息，减少占用的空间

##### (3) Session Layer

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313152024.png" alt="image-20210313152024362" style="zoom:67%;" />

这让我想起了之前上面的图，上面四层都是p2p连起来的，所以我当时就在想虽然是一层一层往下传输的，但应该session层的时候就可以和别人沟通了吧？

**会话层允许不同计算机上的用户在它们之间建立活动的通信会话。**

维护和同步通信系统之间的交互。 会话层管理和同步两个不同应用程序之间的对话。 在会话层中，数据流被标记并正确地重新同步，这样消息的末端就不会过早地被切断，从而避免了数据丢失。

1. **Dialog Control :** This layer allows two systems to start communication with each other in half-duplex or full-duplex.

   **对话控制：**此层允许两个系统以半双工或全双工方式开始相互通信。(但是通话干嘛呢？看别的资料说相当于外联部)

2. **Token Management:** This layer prevents two parties from attempting the same critical operation at the same time.

   **令牌管理：**此层可防止两方同时尝试相同的关键操作。

3. **Synchronization :** This layer allows a process to add checkpoints which are considered as synchronization points into stream of data. Example: If a system is sending a file of 800 pages, adding checkpoints after every 50 pages is recommended. This ensures that 50 page unit is successfully received and acknowledged. This is beneficial at the time of crash as if a crash happens at page number 110; there is no need to retransmit 1 to 100 pages.

   **同步：**此层允许进程将检查点添加到数据流中，这些检查点被视为同步点。 示例：如果系统正在发送800页的文件，则建议每50页之后添加检查点。 这样可确保成功接收并确认50页单位。 这在崩溃时很有好处，就像崩溃发生在第110页时一样； 无需重新传输1至100页。

   所以数据在这一层可能还会有包装。

#### 3. Part III

##### (1) Transport Layer

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210314205627.png" alt="image-20210314205626450" style="zoom:67%;" />

传输层的基本功能是接受来自上一层的数据，将其拆分成较小的单元，然后将这些数据单元传递到网络层，并确保所有数据块正确到达另一端。其实下面三层都是中间结点有的层了，那transport layer就可以相当于你 这台电脑的接收员。

1. 端口号寻址，该层把消息发送到相应的应用程序当中，而下面的网络层才是把消息发送到正确的计算机上

2. **Segmentation and Reassembling:** A message is divided into segments; each segment contains sequence number, which enables this layer in reassembling the message. Message is reassembled correctly upon arrival at the destination and replaces packets which were lost in transmission.

   **分段和重组：**消息分为多个部分； 每个段都包含序列号，这使该层可以重新组合消息。 消息在到达目的地后会正确重组，并替换传输中丢失的数据包。

3. **Connection Control:** It includes 2 types:

   **连接控制：**它包括2种类型：

   - Connectionless Transport Layer : Each segment is considered as an independent packet and delivered to the transport layer at the destination machine.
   - Connection Oriented Transport Layer : Before delivering packets, connection is made with transport layer at the destination machine.

   我是这样想，switch techniques里面有不分成segment的，但是传输层都在做关于segment的活，难道说osi只用报文交换的technique？

4. **Flow Control:** In this layer, flow control is performed end to end.

   **流控制：**在此层中，端到端执行流控制。

   如果sender和receiver之间速度不平衡的话，传输层就会进行control

5. **Error Control:** Error Control is performed end to end in this layer to ensure that the complete message arrives at the receiving transport layer without any error. Error Correction is done through retransmission.

   **错误控制：**在该层中端到端执行错误控制，以确保完整的消息到达接收传输层而没有任何错误。 纠错是通过重传完成的。

   这个就对应上了上面的分段和重组中提到的会替换传输中丢失的数据包。

##### (2) Network Layer

![image-20210314205823846](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210314205824.png)

网络层控制子网的操作。 该层的主要目的是通过多个链路(网络)将数据包从源传送到目的地。 如果两台计算机(系统)连接在同一链路上，则无需网络层。 它通过不同的通道将信号路由到另一端，并充当网络控制器。

It also divides the outgoing messages into packets and to assemble incoming packets into messages for higher levels.

它还将传出的消息划分为数据包，并将传入的数据包组合为更高级别的消息。

In broadcast networks, the routing problem is simple, so the network layer is often thin or even non-existent.

在广播网络中，路由问题很简单，因此网络层通常很薄，甚至根本不存在。

1. It translates logical network address into physical address. Concerned with circuit, message or packet switching.

   它将逻辑网络地址转换为物理地址。 与电路，消息或数据包交换有关。其实就是ip地址，这个是通过ip地址把数据传输到指定的计算机上

2. Routers and gateways operate in the network layer. Mechanism is provided by Network Layer for routing the packets to final destination.

   路由器和网关在网络层中运行。 网络层提供了将数据包路由到最终目的地的机制。

3. Connection services are provided including network layer flow control, network layer error control and packet sequence control.

   提供的连接服务包括网络层流控制，网络层错误控制和数据包序列控制。

4. Breaks larger packets into small packets.

   将较大的数据包分解为小数据包。

##### (3) Data Link Layer

![image-20210314212236130](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210314212236.png)

怎么说呢，感觉网络层是控制整个数据链路层的，真的不好分啊喂。网络层是负责把data从origin 传到destination，那数据链路层就是这里的搬运工。

数据链路层执行最可靠的节点到节点的数据传递。 它根据从网络层接收到的数据包形成帧，并将其提供给物理层。 它还同步要通过数据传输的信息。 错误控制很容易完成。 编码后的数据然后传递到物理。

错误检测位由数据链路层使用。 它还可以纠正错误。 外发邮件被组装成框架。 然后，系统等待传输后接收到确认。 发送消息是可靠的。

**数据链路层**的主要任务是将原始传输设备转换为一条线路，该线路看起来没有出现未发现的到网络层的传输错误。 它通过使发送方将输入数据分解为**数据帧** (通常为几百个或几千个字节)并顺序传输这些帧来完成此任务。 如果服务可靠，则接收器通过发送回**确认帧**来**确认**每个帧的正确接收。

1. **Framing:** Frames are the streams of bits received from the network layer into manageable data units. This division of stream of bits is done by Data Link Layer.

   **帧：**帧是从网络层接收到的可管理数据单元中的比特流。 比特流的这种划分是由数据链路层完成的。

2. **Physical Addressing:** The Data Link layer adds a header to the frame in order to define physical address of the sender or receiver of the frame, if the frames are to be distributed to different systems on the network.

   **物理寻址(mac address)：**如果要将帧分发到网络上的不同系统，则数据链路层会在帧中添加标头，以定义帧的发送者或接收者的物理地址。

3. **Flow Control:** A flow control mechanism to avoid a fast transmitter from running a slow receiver by buffering the extra bit is provided by flow control. This prevents traffic jam at the receiver side.

   **流控制：**流控制提供了一种流控制机制，该机制通过缓冲多余的位来避免快速的发送器运行慢的接收器。 这样可以防止接收方的交通阻塞。

4. **Error Control:** Error control is achieved by adding a trailer at the end of the frame. Duplication of frames are also prevented by using this mechanism. Data Link Layers adds mechanism to prevent duplication of frames.

   **错误控制：**通过在帧的末尾添加预告片来实现错误控制。 使用此机制还可以防止帧重复。 数据链路层增加了防止帧重复的机制。

5. **Access Control:** Protocols of this layer determine which of the devices has control over the link at any given time, when two or more devices are connected to the same link.

   **访问控制：**当两个或多个设备连接到同一链路时，该层的协议确定在任何给定时间哪个设备可以控制该链路。

##### (4) Physical Layer

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210315205812.png" alt="image-20210315205811974" style="zoom:67%;" />

物理层是OSI参考模型的最低层。 它负责将位从一台计算机发送到另一台计算机。 该层不关心位的含义，而是处理与网络的物理连接的建立以及信号的发送和接收。

1. **Representation of Bits:** Data in this layer consists of stream of bits. The bits must be encoded into signals for transmission. It defines the type of encoding i.e. how 0's and 1's are changed to signal.

   **位表示：**该层中的数据由位流组成。 这些位必须编码为信号才能传输。 它定义了编码类型，即如何将0和1更改为信号。

2. **Data Rate:** This layer defines the rate of transmission which is the number of bits per second.

   **数据速率：**该层定义传输速率，即每秒的位数。

3. **Synchronization:** It deals with the synchronization of the transmitter and receiver. The sender and receiver are synchronized at bit level.

   **同步：**处理发送器和接收器的同步。 发送方和接收方在位级别同步。

4. **Interface:** The physical layer defines the transmission interface between devices and transmission medium.

   **接口：**物理层定义设备与传输介质之间的传输接口。

5. **Line Configuration:** This layer connects devices with the medium: Point to Point configuration and Multipoint configuration.

   **线路配置：**此层将设备与介质连接：点对点配置和多点配置。

6. **Topologies:** Devices must be connected using the following topologies: Mesh, Star, Ring and Bus.

   **拓扑：**必须使用以下拓扑连接设备：网状，星形，环形和总线。

7. **Transmission Modes:** Physical Layer defines the direction of transmission between two devices: Simplex, Half Duplex, Full Duplex.

   **传输模式：**物理层定义了两个设备之间的传输方向：单工，半双工，全双工。

8. Deals with baseband and broadband transmission.

   处理基带和宽带传输。

#### 4. Part 4

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210317205954.png" alt="image-20210317205953705" style="zoom:50%;" />

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210317210130.png" alt="image-20210317210130114" style="zoom:50%;" />

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210317210834.png" alt="image-20210317210833745" style="zoom: 67%;" />

这里说一下，这张图加的address都很好理解，搞清楚那一层加port，哪一层加ip，哪一层加mac就好了，但是注意一下数据链路层这里会加一个header和trailer，header里面是source 和 destination的mac地址，但是trailer的话是和error control 有关的

### 2. TCP/IP Model

![image-20210313105427735](https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210313105427.png)

1. 传输控制协议/网际协议
2. 在OSI model之前就出现了
3. 因此，在tcp/ip协议的层不全和OSI的一样
4. TCP/IP 是一个等级分明的协议，由交互式模块组成，每个模块有特定的功能，比如一个模块关注ip地址，另外一个模块关注mac 地址

## 

![image-20210314114232347](C:%5CUsers%5Czbr%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20210314114232347.png)