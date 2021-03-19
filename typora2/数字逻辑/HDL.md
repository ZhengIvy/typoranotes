![image-20210104102517756](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104102517756.png)

![image-20210104102718579](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104102718579.png)

![image-20210104102822092](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104102822092.png)

这个到时看懂了，module后面跟着的是既有output也有input哈，然后下面就是定义port Types,input 和output都有

![image-20210104102943920](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104102943920.png)

这个好像也可以

![image-20210104103023872](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104103023872.png)

![image-20210104103359072](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104103359072.png)

![image-20210104103446023](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104103446023.png)

![image-20210104104748677](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104104748677.png)

我懂他的意思了，就是说一个halfadder本来的port端口就是(carry,sum,a,b)的，第一种写法就是直接按顺序来，但是其实不是很好，和java比较像把，第二种的话就对应的，啥是啥就很好看出来，order doesn't matter哈，感觉都是输出写在前面，输入写在后面 的

![image-20210104105048339](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104105048339.png)

他这个的意思就是说吧，输入的只能是net，但是输出的话就可以是net or variable

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104105321118.png" alt="image-20210104105321118" style="zoom:67%;" />

这个就说的是parameter和local param的区别把，后者像是final的值，不能被改动



<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104105805415.png" alt="image-20210104105805415" style="zoom:67%;" />

然后终于懂这些数字要怎么写啦！!!，`<size>'<base format><number>`，但是你可以不写哦，那就有默认值了，不写size的话默认为32bit，不写baseformat的话就默认是十进制了哈

![image-20210104110606318](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104110606318.png)

这个的话也不要大惊小怪哈，还是有可能的啦，这个负数的注意一下吧，但我个人感觉没有用到过负数哇

![image-20210104111235785](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104111235785.png)

这个怎么说了，了解到了一点，如果任何一个operand有 Z or X的话，那么结果就是X， unknown，还有注意精度损失的问题哈

![image-20210104111554015](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104111554015.png)

懂了懂了，也不难哈，each bit pairing的，就是每个bit进行运算的哈，向左扩展是这个意思嘛？ 像加法一样？自动填充为0？

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104111856874.png" alt="image-20210104111856874" style="zoom:67%;" />

这里来了个内部的啦，也很好理解

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104111935454.png" alt="image-20210104111935454" style="zoom:67%;" />

这个的返回值都是1bit的，也很好看懂和明白，但是呢，和unknown比结果还是unknown诶，这里有点不一样哈拉，就很奇怪，我以为是可以比的

![image-20210104113140544](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104113140544.png)

这里的话equality 和 case equality是有区别的，主要就是体现在unknown value上面，对于equality的话这个看起来就是我们平常会用的思路，但case 的话就把 X Z 当成一个确定的value，这时候就要看长得一不一样了

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104113504300.png" alt="image-20210104113504300" style="zoom:67%;" />

这个的话也是unknown的还是unknown处理啊，不过这里的话就会有些different，他是把每个operand看做一个整体了，所以返回的结果只有0or1，然后非零值都可以看成1，所以就大概是这样啦

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104114148343.png" alt="image-20210104114148343" style="zoom:67%;" />

又是这个，我真的记不住哈，先这样，有遇到的再看

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104114649467.png" alt="image-20210104114649467" style="zoom:67%;" />

还有这种的啊，conditional的就是判断true or false咯，{}的话就是连接，{{}}这个就是replicate的咯

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104114843270.png" alt="image-20210104114843270" style="zoom:67%;" />

这个也是后面再看吧，真遇到了再说

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104115042973.png" alt="image-20210104115042973" style="zoom:67%;" />

这个我有在书本上看到吼，只不过不知道左边必须是net data type罢了，然后实时更新这个我懂，不过最下面的这个是啥啊我不懂了，懂了，也是实时更新，但是是5 s? ms? 之后再更新 5 times unit later，也不知道说的是哪种哈

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104115703427.png" alt="image-20210104115703427" style="zoom:67%;" />

原来nested是嵌套的意思啊，是我不行哈，注意是 **parallel**哈，里面就是sequentially的

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104115842157.png" alt="image-20210104115842157" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104115935189.png" alt="image-20210104115935189" style="zoom:67%;" />

所以 always的block是循环的啊？如果多个always block的话，就互不影响把，各自执行各自的

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104120526754.png" alt="image-20210104120526754" style="zoom:67%;" />

刚开始看的时候是懵逼的，然后好像就懂了？这就是toggle的意思，但我不明白的是为啥parameter前面要加一个#?

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104120915065.png" alt="image-20210104120915065" style="zoom:67%;" />

这个two types的话目前有些懵逼哈

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104121250748.png" alt="image-20210104121250748" style="zoom:67%;" />

清晰明了，perfect！

![image-20210104121955978](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104121955978.png)

这个很有趣啊天哪，就蛮清晰的，怎么解释呢，这个，非阻塞的这里那就是同时的，同时都会产生这种情况，所以的话就是同步的，需要两个时钟脉冲哈，那这样的话就是感觉把，接触多了可能会不一样哈

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104122531089.png" alt="image-20210104122531089" style="zoom:67%;" />

懂了吧！nonblocking就是来搞sequential的

![image-20210104150114060](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104150114060.png)

哈，sensitive的意思应该是有这个东西的时候就会响应哈，*号代表全部的意思，然后下面还会根据clock响应，但是不包括data和enableinput？ 啥意思，是只搞异步的吗？

说一点：only execute after a change in any signal in sensitivity list，也就是说有变量change的时候always block 才起效 ？

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104150816964.png" alt="image-20210104150816964" style="zoom:67%;" />

这个也没啥，我们基本上接触过很多了

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104150949968.png" alt="image-20210104150949968" style="zoom:67%;" />

这个数据选择器嘛，蛮好理解的

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104151049981.png" alt="image-20210104151049981" style="zoom:67%;" />

this one also

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104151151686.png" alt="image-20210104151151686" style="zoom:67%;" />

这个啊，这个 我就先放这，不管了哈

##  forever loop & repeat loop & while loop

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104151832479.png" alt="image-20210104151832479" style="zoom:67%;" />

怎么说呢，就这样子吧

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104151925582.png" alt="image-20210104151925582" style="zoom:67%;" />

用的是begin哈，注意一下

## for loop

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104152518195.png" alt="image-20210104152518195" style="zoom:67%;" />

怎么说呢，我大概懂这个input[7:4]的意思了，就是从位4到位7的意思哈，result[3:0]就是从位0到位3，然后注意一下for这里也是begin和end一起用的啦

## Synchronous vs Asynchronous

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104153754530.png" alt="image-20210104153754530" style="zoom:67%;" />

天，我终于懂了同步清零和异步清零的区别，结合之前学的寄存器的同步和异步置数，我明白了！所以在这里只要你的clear变了，那你就去清零！

同步置数的就是马上同步嘛？为啥？因为是和时钟一起同步的哈！那异步呢就不和时钟同步，那到这里来就是同步你必须得等时钟脉冲，异步的话你只要满足你自己设置的一个条件就完全ok！

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104153948204.png" alt="image-20210104153948204" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104154148421.png" alt="image-20210104154148421" style="zoom:67%;" />

没错！ 这也没啥

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104155651385.png" alt="image-20210104155651385" style="zoom:67%;" />

怎么说呢，刚刚也想了一些问题，对于一直习以为常的东西发出提问，为啥sequential里面都用 <=，不会出问题吗？答案是不会的，不过他前面给我们举的例子都是if else case这种，我觉得是变相的=号了，但是为了表示我们是时序电路所以用的是<=

## Functions and tasks

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104160244157.png" alt="image-20210104160244157" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104160517956.png" alt="image-20210104160517956" style="zoom:50%;" />

就是有点奇怪把，看起来，但是呢，他这里的意思是你function的返回值是传给函数名的，所以呢，这里的begin开始得也好奇怪啊，可能下面其他的是参数把？ 然后begin开始之后才是{}逻辑代码

好像懂了，hxd，这个的话不熟悉，看起来就的确会有点久哈，这个直接用b来搞没有把b具体到b[0],b[1],b[2],这种的我比较惊讶，那其他也没啥了，多看几个应该能懂的把？

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104162531292.png" alt="image-20210104162531292" style="zoom:67%;" />

这个懂吧

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104163039684.png" alt="image-20210104163039684" style="zoom:67%;" />

有种懂了却又不知道他这个到底是什么的感觉

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104163145137.png" alt="image-20210104163145137" style="zoom:67%;" />

## Demo看下

怎么说呢，我又觉得奇怪了，上面说input的类型必须是wire，可能是定义的时候得是wire，但想输入值进行的话就可以是？？reg之类的，reg是寄存器实际上，可以保存数据的，这个reg像是指针一样吧，怎么说呢啊。

![image-20210104164930903](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104164930903.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104165234975.png" alt="image-20210104165234975" style="zoom:67%;" />

## $random%b

$random%51 表示产生-50~50的随机数哈

## reg变量

reg变量只能在initial 和 alwaysblock中被赋值哈，规定把，不懂啊

赋值的时候比如说pa= -2,这种 -2的补码是1110，但他不管你是补码，直接就为14哈。所以reg[3:0]pa 内部实际上是1110，那我懂了哈，你要他的值那就是他的二进制值

## 阻塞与非阻塞到底看前面还是看自己！

回答，看前面！

一个简单的例子

```vhdl
X = 2'b11;
X <= 2'b10;
$display("%t,%b",$time,X);
#5;
$display("%t,%b",$time,X);
```

结果 为

#0,11

#5,10

为什么第一个的结果是11而不是00，是因为第二句非阻塞，那第一个display直接输出了，但是当时的X还是11啊，所以哈哈哈

## 什么时候用wire什么时候用reg？

wire的话其实就相当于一条普通的线，可以连续赋值，但是reg的话可以always 和initblock里面搞，咋说呢，用wire的时候要搭配assign的

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210104191916677.png" alt="image-20210104191916677" style="zoom: 67%;" />

看看把

## 区别数组和向量

```vhdl
reg pa[2:0]; //pa为3个1位reg变量组成的数组
reg [4:0]pa; //pa为1个5位寄存器变量
```

可以这么理解  几位几个

所以第一个是1位3个，第二个是4位1个，感觉我们一般用的是第二个

## 琐碎知识点

1. ps是最小的单位
2. 标识符是以"\\"开头的
3. BCD码是位权码，也就是整个码都去表示一个0~9的数字
4. 负数的补码符号位是不变的，所以为1的必是负数哈
5. 标准与或式就是最小项之和
6. 搞卡诺图有几项要注意的！格雷码记住哈，所以最小项的别数错了！！，还有d是don't care意思
7. 编码器 -> 优先编码器，看怎么设置优先级的 还有 二-十进制普通编码器 BCD的
8. 编码器是74H148，低电平有效，啥都是反的，输出的也是反码，使能输入端也是低电平有效
9. 数据选择器设计思想就是由最小项组成的哈，74HC153是4x1选择器，然后可以用两个4x1 构成一个8x1哈，没有骚操作，只有使能输入端为1不工作而已。
10. 数据比较器内容很少，没啥复杂的，74HC85，就是记住Equal 的话是有规律的，用XAND? 异或取反叫啥来着忘了
11. 时序分析这里东西蛮多，也学到挺多的，传输延迟，好理解把，竞争冒险懂把，突然给你杀出个相反的，有三种解决方法：滤波，增加冗余项，选通法，我最喜欢第二个
12. 能实现并行数据转换成串行数据的是 **数据选择器**
13. 约束项就是don't care
14. D是上升沿的
15. posedge 清零是个啥啊？ 我看到一个异步清零这么写，好像明白了，pos就是1的时候清零，neg就是为0的时候清零
16. & | 也可以搞到1位上去
17. 161 CET CEP使能控制端，CET为1时才能输出进位的值
18. 时序逻辑电路的显著特点是内部包含状态寄存器，电路在不同的状态之间切换，由于状态切换寄存器数目有限，电路可以达到的状态有限，因此，时序逻辑电路有时称为有限状态机
19. 状态译码，状态寄存器，输出译码
20. 在EDA中，IP的中文含义是 知识产权编程
21. 在EDA中，能将硬件描述语言转化为硬件电路的重要工具软件称为 综合器
22. 在EDA工具中，能完成在目标系统期间上布局布线的软件称为 适配器
23. 布局布线在 Designer那里
24. D 触发器是上升沿有效
25. JK 触发器是下降沿有效
26. T触发器上升沿有效
27. 



```vhdl
`timescale 1ns/10ps
    module testbench;
reg[7:0] in;
wire[2:0] out;
wire EO;
initial
    begin
        in='b00000001;
        repeat(9)
        #20 in = in<<1;
    end
encoder8_3_1 testbench_8_3encoder(in,EO,out);
endmodule
```



