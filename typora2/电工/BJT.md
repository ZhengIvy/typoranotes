## BJT

> 首先这是重新看的，学到了啥，反正就是分三种情况的common，回忆起了KCL 那里的事情，通过β讲了放大原理，还有啥？差不多了吧

### 1. Common Emitter Configuration

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704083231510.png" alt="image-20200704083231510" style="zoom:67%;" />

> 注意一下这个逻辑，是Vce reduce Ib 也reduce ，这里的Ib 并不是因变量，因变量是Vce

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704090235944.png" alt="image-20200704090235944" style="zoom:67%;" />

> 咋回事呢，实际上就是，你控制变量，像在这里上面的那个图像你控制Vbe不变，当你increase Vce的时候，Ib是如何变化的，那这里的话是首先增加了Vce，一年春Vcb升高，这样的话内电场作用加强，更多的electronic 去collector，更少在base结合，因此Ib就减小了

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704090744932.png" alt="image-20200704090744932" style="zoom:67%;" />

> 的确是有道理把，因为Vce increase ，所以这边Ic 的电流相应的也是increase 的

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704091206574.png" alt="image-20200704091206574" style="zoom:67%;" />

> 当你同个Vce的时候，你Ib 变大，那你的Ic自然也是变大的

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704092109839.png" alt="image-20200704092109839" style="zoom:67%;" />

> 你学到了什么？ emem 怎么说呢，他给 我讲为什么那里是截止区，但我大概有点懵把，反正就差不多那样把，还讲到了在ac dc中β可以当做是一样的，电阻基本上是在几千欧之间，虽然说看起来很大，但实际上和common base 比起来算小的了。。。 这个最后高的就是high power把

### 2. Q point

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704093327900.png" alt="image-20200704093327900" style="zoom:67%;" />

q point 实际上是工作点把，可以在放大区任取 的，而且估计有削波

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704093458536.png" alt="image-20200704093458536" style="zoom:67%;" />

ic不可以为0 噢

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704093651953.png" alt="image-20200704093651953" style="zoom:67%;" />

breakdown region ，should be avoided

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704093909256.png" alt="image-20200704093909256" style="zoom:67%;" />

可能会被temperature影响，这时候就需要稳定性 

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704095121867.png" alt="image-20200704095121867" style="zoom:67%;" />

这个倒的确是，你可以看做E 那里接地 了，所以那个点的电压就是Vbe

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704095341871.png" alt="image-20200704095341871" style="zoom:67%;" />

output side 这边也差不多吧

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708171550549.png" alt="image-20200708171550549" style="zoom:67%;" />

我懂了 这个其实是分了两条路，一条从Rb开始，一条从Rc开始的，然后要做题才知道把，后面就不知道有啥了

#### a. load line

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704095645080.png" alt="image-20200704095645080" style="zoom:67%;" />

这个就是他们那里讲的，直流负载线，这个式子是通过Ic 那边推出来的，所以的话就可以凑出一个线性方程

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704095838086.png" alt="image-20200704095838086" style="zoom:67%;" />

那这个线上的点是？干嘛的我也不清楚，放大区符合的值把。 所以我们基本上看这个点？ 不然的话其他的点感觉哦，不是静态的，就是肯定有某样的东西是在变化的

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704100441253.png" alt="image-20200704100441253" style="zoom:67%;" />

就基本上是每个Rc 可以对应每个静态点，高中的时候好像有类似的，但是有些忘记了，如果Rc 变大，那就往左边移，也是往下移的意思，x轴的交点不变是因为Vcc没变

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704100624467.png" alt="image-20200704100624467" style="zoom:67%;" />

这个是当Vcc 增大的时候，那就是变成这样了，这里x轴的交点变化了，  因为就是Vcc 变了，因为是Vcc变了，Rc 没变，所以的话斜率就没有发生变化

总的而言是Vcc 影响的是与坐标轴相交的值

Rc 影响的是斜率的问题，但是与x轴的交点不变

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704101410074.png" alt="image-20200704101410074" style="zoom:67%;" />

有点strange，是的，因为呢，你这里就换了一个放大倍数，然后你的值就跑到下面去了，可能是我觉得这个Ib 这条线时本来就有规定好他对应的放大倍数是多少，这里的话是一百的话就刚刚好，而β change的话好像是和温度有关

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704102810632.png" alt="image-20200704102810632" style="zoom:67%;" />

这是一个range哈，due to temperature or due to the change in the transistor<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704104437776.png" alt="image-20200704104437776" style="zoom:67%;" />

噢，我记起来了哈，也就是呢，你本来的Ie 的确是 Ib + Ic 的，然后呢，Ib太小了所以Ic就等于Ie 了（这里没有等于也是可以的，直接来），之后呢，当你的β increase，你的Ic increase，那你的voltage drop increase 在 Re 的地方，那你就相当于Vbe 也increase了，那你的Ib相当于decrease，引起Ic decrease，然后又恢复正常了



<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708181126397.png" alt="image-20200708181126397" style="zoom: 50%;" />

你要Ic 与 β independent 的话 你就需要这个条件咯，虽然我不知道为什么需要independent，就β怎么变，那Ie 的值都不会被影响到

#### b. 多加了一个resistor Re

#### c. don't know what?

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708181707871.png" alt="image-20200708181707871" style="zoom:67%;" />

Rb 很小的时候

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708181915297.png" alt="image-20200708181915297" style="zoom:67%;" />![image-20200708182033751](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708182033751.png)<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708181915297.png" alt="image-20200708181915297" style="zoom:67%;" />![image-20200708182033751](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708182033751.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708181915297.png" alt="image-20200708181915297" style="zoom:67%;" />![image-20200708182033751](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708182033751.png)<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708181915297.png" alt="image-20200708181915297" style="zoom:67%;" />![image-20200708182033751](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708182033751.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708181915297.png" alt="image-20200708181915297" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708182033751.png" alt="image-20200708182033751" style="zoom:67%;" />



<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708182105438.png" alt="image-20200708182105438" style="zoom:67%;" />

这时候还是当与β无关的时候哈，与β无关的结果和条件吧算是，就是上面延伸出来的结果，他要你Rb很小才能，那这时候就是很小的结果了

#### d.如何判断截止和饱和？

截止的话就是Ib 那里为0  了 Ic 也很低

饱和的时候是

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708184439358.png" alt="image-20200708184439358" style="zoom:67%;" />

就是正偏，然后Vce 的区别就不大了， 当Ic的电流大于饱和的时候，就是饱和状态，但已经是最大值了，当你increase Ib 的时候 Ic这边remain the same，就是当你大于的时候你就在饱和区了，这样的话饱和区的β值更小

**这个好像就已经算是深度饱和了**

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708185038967.png" alt="image-20200708185038967" style="zoom:67%;" /><img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708185038967.png" alt="image-20200708185038967" style="zoom:67%;" />





截止区的时候就是你Vbb= 0 的时候

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708203352339.png" alt="image-20200708203352339" style="zoom:67%;" />

没错的对应的上

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708203714407.png" alt="image-20200708203714407" style="zoom:67%;" />

当你的Ib =0 Ic 也等于0，那这样的话你的 三极管在这里的电阻超大就相当于断路了

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708204146679.png" alt="image-20200708204146679" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708204356848.png" alt="image-20200708204356848" style="zoom:67%;" />



来啦，为什么相当于开关闭合的原因

### 3. 课件version？

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704104047304.png" alt="image-20200704104047304" style="zoom:67%;" />

你看 他是这样子连的，所以说是共集电极

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704104212052.png" alt="image-20200704104212052" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704112114964.png" alt="image-20200704112114964" style="zoom:67%;" />

但是他这里就是没有提到 Re 的作用

而且这里有的有估算 Ie 有的就又没有 sosososo？ 害，还是看参数把 是Ie 还是 Ib 这样子

### 4. 放大电路的静态分析

![image-20200704120956630](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704120956630.png)

> 用的是直流通路，使放大电路的放大信号不失真。
>
> 使放大电路工作在较佳的工作状态，静态是动态的基础。

![image-20200704121301100](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704121301100.png)

还要这样子的？？

### 5. 动态分析

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704135711994.png" alt="image-20200704135711994" style="zoom:67%;" />

这。。咱也不知道为啥，相当于Ucc这里连了个寂寞，变成接地的了

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704135842213.png" alt="image-20200704135842213" style="zoom:67%;" />

非线性元件吗，这我也不知道哇，，

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704141059646.png" alt="image-20200704141059646" style="zoom:67%;" />

这又突然冒出来一个式子，我是真的迷茫哈

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704141428607.png" alt="image-20200704141428607" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704141620747.png" alt="image-20200704141620747" style="zoom:67%;" />

这个菱形代表受控的意思，这个电阻太大了，可以直接看成开路的，然后就从B->E 了，B说不走到C了，因CE 那边电阻比较大了，对就是这样子

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704142306199.png" alt="image-20200704142306199" style="zoom:67%;" />

就是这样子换的	

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200704142820604.png" alt="image-20200704142820604" style="zoom:67%;" />

哇。这么多公式啊！实际上是呢，你要么就都用相量，你要么就 都用瞬时值，我肯定是用相量的，那个更好用一点，为什么那里有个负号呢，因为你的电流方向和你的U 的方向是相反的。而且RL‘ 指的是并联之后的电阻，你知道嘛，并联后的=都是变小的，所以当你的Rl 负载开路的时候，放大倍数是最大的，基本上就是这样子了把

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708214759242.png" alt="image-20200708214759242" style="zoom:50%;" />

这里多加了个Re，怎么说呢，那我就觉得这跟之前的电路好像没啥区别了？？

这里的Ic还是要留到Re，这里的，然后你比一下又发现有了Re 之后你的放大倍数就小了

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708215208170.png" alt="image-20200708215208170" style="zoom:67%;" />

可以接到一个信号源上，其实你可以当做呢放大电路自己就是一个输入电阻，可能一般情况下一个是不够的，所以你电阻大点，你给别人损耗的就小了，就基本上是这样吧



<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708222419650.png" alt="image-20200708222419650" style="zoom:67%;" />

这个是算啥，就是算你的输入电阻嘛，第一个比较好算吧，后面的算开路就不算啦。

第二个的话是因为rbe 和re 那里流的电流都不同，你咋搞，所以的话就是搞成等效电阻，那这个等效电流是Ib 我就不知道了，应该是把

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708223341141.png" alt="image-20200708223341141" style="zoom:67%;" />

这样的就是Rb的电阻很大，比rbe 大很多，并联出小的来。

下面这个呢，一个更比一个大，至于为什么我就不知道了，所以的话这种等效电路的特点是，放大的倍数小，但是输入的电阻就大

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708225348122.png" alt="image-20200708225348122" style="zoom:67%;" />

这个挺迷茫的说实话

我可以尝试记住把，戴维宁是啥我都忘了哈

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200708225753360.png" alt="image-20200708225753360" style="zoom:67%;" />

来，求输出电阻

用戴维宁，我觉得呢是不是上面的Rs太大了，所以并联的时候就等于小的那个了

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709001017426.png" alt="image-20200709001017426" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709003818064.png" alt="image-20200709003818064" style="zoom:67%;" />

困了，看不懂了

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709004019678.png" alt="image-20200709004019678" style="zoom:67%;" />![image-20200709004108506](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709004108506.png)<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709004019678.png" alt="image-20200709004019678" style="zoom:67%;" />![image-20200709004108506](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709004108506.png)<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709004019678.png" alt="image-20200709004019678" style="zoom:67%;" />![image-20200709004108506](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709004108506.png)<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709004019678.png" alt="image-20200709004019678" style="zoom:67%;" />![image-20200709004108506](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709004108506.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709004108506.png" alt="image-20200709004108506" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709004459418.png" alt="image-20200709004459418" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709004509076.png" alt="image-20200709004509076" style="zoom:67%;" />

红色的是交流的，你看，并联之后总是变小的，所以呢 Rl prime就变小了

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709004852621.png" alt="image-20200709004852621" style="zoom:67%;" />

你看削平，到底是电流的削平还是电压的削平哈，而且通常情况下我们遇到的都是NPN

![image-20200709073516854](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709073516854.png)

的确失真的情况下对于截止来说来点电流啊，就减小下Rb

![image-20200709160037381](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709160037381.png)

截止，减小

### 6.静态工作点的稳定

上面的饱和失真和截止失真就是一种

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709075230429.png" alt="image-20200709075230429" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709075829716.png" alt="image-20200709075829716" style="zoom:67%;" />

话说这个Iceo是啥来着？？？

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709080350975.png" alt="image-20200709080350975" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709080446853.png" alt="image-20200709080446853" style="zoom:67%;" />

emem是的把，的确电流变大的话你的Q点也会跑到上面去 的，但不是很稳定，会有几种结果，

1. 负载点上移，饱和区失真，过热引起烧坏
2. 但如果这样我们可以做一个分压装置，通过反馈保持稳定

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709081957277.png" alt="image-20200709081957277" style="zoom:67%;" />

来了，这个感觉可以理解的把，因为之前做题的时候是猜测过？

本来等于那里就是没错的，不过因为I2给约等于了，那后面也是约等于的

![image-20200709082203953](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709082203953.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709083012304.png" alt="image-20200709083012304" style="zoom:67%;" />

我tmd 是没看懂，这讲的啥啊？？？？？？？？

不是说Ic≈Ie 是因为 Ib 没有嘛，那你说的是啥回事啊？？？？？？？？？这tmd 就怎么等于了

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709084106408.png" alt="image-20200709084106408" style="zoom:67%;" />

好像又不冲突了，等会看看把

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709084321808.png" alt="image-20200709084321808" style="zoom:67%;" />

还是觉得有一些奇怪哈，可以把，脑子没转过来，sorry。 因为Ve = Vb - Vbe 就是可以 的，这是个结果，不是一个过程，

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709085156900.png" alt="image-20200709085156900" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709085130169.png" alt="image-20200709085130169" style="zoom:67%;" />

这边选择做了一个戴维宁 看看另外一边要不要<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709085233649.png" alt="image-20200709085233649" style="zoom:67%;" />

![image-20200709085248699](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709085248699.png)

![image-20200709085600820](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709085600820.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709091921335.png" alt="image-20200709091921335" style="zoom:67%;" />

好像又可以理解了，怎么说，就是Ube下降的时候呢Ib的电流实际上就是那样来的，这样的话在Ib区与载流子结合的就少，然后就这样啦，Ib下降了，然后就负反馈啦

然后说下上面那个对交流对直流是什么意思，直流的确是像我学过的那样，有个负反馈作用，交流的时候，交流损失大是为啥我就不知道了。。。

![image-20200709092458240](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709092458240.png)

感觉没那么难

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709092805887.png)

所以总的来说就是Rbe小，另外一个是rc小

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709093330113.png" alt="image-20200709093330113"  />

不过感觉这里有讲过把

就是当你放大倍数变小的时候，你的输入电阻也会变大哈，输出电阻还是不变的。

等会看来是静态和动态时Re 的作用不同？

静态的时候呢Re起调节作用，动态的时候就是电阻问题？

![image-20200709095536206](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709095536206.png)

![image-20200709100601227](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709100601227.png)

这个看起来好像就没有那么难了

![image-20200709101603065](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709101603065.png)

![image-20200709102023948](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709102023948.png)

这啥？ 不清楚

Ui/Es 就是有多少电压被放到了放大电路上去

![image-20200709102226682](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709102226682.png)

哈！ 又是什么鬼东西，你不是说要和Re 共患难吗？ 你怎么把Re 给抛弃了晕

### 7.射极输出器

![image-20200709104027366](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709104027366.png)

![image-20200709104207059](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709104207059.png)

![image-20200709105711296](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709105711296.png)

？？？？？？？？？？？？？？？？？？？？？？？？？？？

![image-20200709105947101](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709105947101.png)

![image-20200709113359417](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709113359417.png)

电阻非常小，有很好的带负载能力

![image-20200709113443138](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709113443138.png)

![image-20200709113528114](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200709113528114.png)