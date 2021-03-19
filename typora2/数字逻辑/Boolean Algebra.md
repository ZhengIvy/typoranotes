## 	1. 普通的公式

![image-20200927205141638](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200927205141638.png)

> 额，没截清楚，主要要知道的是，`Distributive Rules`,`A+BC=(A+B)(A+C)` `A+A'B=A+B` `A'+AB=A'+B`,这个也很简单去验证。
>
> 

![image-20200927210615816](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200927210615816.png)

> 还有这个德摩根定律，无语哈，上次我卡了好久呢，其他的应该没啥了

## 2. Redundancy Theorem

冗余定理

满足几个条件

1. 三个变量
2. 每个变量出现了两次
3. 有一个变量是complimented的
4. Take the complimented variable

冗余嘛，就是去除掉一些多余的，相当于化简的效果

![image-20201008165556271](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201008165556271.png)

看看，就是这样子哈

![image-20201009152458676](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009152458676.png)

看看例题

## 3. Sum of Product

![image-20201009152528006](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009152528006.png)

就是最小项把，然后把最小项都加起来，一个最小项之间是由And连接起来的，然后多个最小项之间是由OR连接起来的，然后注意m的小标，这个怎么看的？实际上还是二进制把，你看从0开始，最高就7了

![image-20201009152937804](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009152937804.png)

![image-20201009153027510](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009153027510.png)

> 有一种是standard form还有的是最简式咯，也挺简单的，为什么要知道m小标怎么来的呢，你看由这种题把

## 4. Product of Sum

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009153816686.png)

> 这个的话就是最大项了，一个最大项之间是由or来连接的，多个最大项之间用and连接，至于为什么这样子定义呢，我也不知道啊，~~然后Y取反就直接是最小项了欸，~~，等会哈，感觉有点问题，噢，德摩根牛逼牛逼哈，看来好一会看出来了

![image-20201009154016472](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009154016472.png)

> m就自然地变为M了，然后的话这种form一般都是两种形式，一种是标准式，另外一种就是最简式，

## 5. SOP POS EXAMPLE

![image-20201009154221378](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009154221378.png)

还是很easy，自己看看哈，就没啥

![image-20201009154437467](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009154437467.png)

这里的话就是化简了

## 6. 标准式和最简式之间的转换

![image-20201009154537577](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009154537577.png)

首先讲的是最简式到标准式之间的变换，标准式的话就是变量都要出现一遍，相当于乘以1的话，那就用B+B`的形式来，emem那为什么会转到最小项的形式呢。。最大项化简也差不多是这样的把

![image-20201009165140903](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009165140903.png)

> 噢，原来时这样子啊，那我收回我上面说的话，它这种化简时完全靠技巧性的化简，不把括号拆开来的这种，那这里就主要找0咯，还是很有趣的嘛

### Example

![image-20201009190924857](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009190924857.png)

> 终于搞完了哈哈哈

## 7. positive and negative logic![image-20201020103217549](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201020103217549.png)

![image-20201019191121148](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019191121148.png)

这个就刚好是相反的，positive logic就是大的为1，小的为0

negative logic 是小的为1，大的为0

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019191248452.png" alt="image-20201019191248452" style="zoom: 25%;" />

## 8. Dual form 对偶式

![image-20201019191313597](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019191313597.png)

这个就是分别根据 + - 的or and gate写下来的东西

![image-20201019191359307](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019191359307.png)

![image-20201019191406497](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019191406497.png)

然后你发现了一个问题，`+ or`和`- and`的表就刚好是相同的,`- and`和`+ or`也是相同的

![image-20201019191531886](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019191531886.png)

![image-20201019191610204](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019191610204.png)

![image-20201019191616637](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019191616637.png)

> 所以他这里也就讲了关于这个对偶式的东西，对偶嘛，感觉像奇函数哈哈，但是这个不需要compliment，意思是你取AB值的时候就是反过来的

### self dual

![image-20201019191817376](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019191817376.png)

自偶啊，一般情况下要dual两次才能拿到原来的式子，而这个的意思是你dual一次就能拿到原来的式子了，神奇把哈拉

![image-20201019191922606](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019191922606.png)

额。但是我不是很明白这个式子什么意思了。真的不知道哈，因为我看书上没有说这个，我就默认不看了

## 9. BCD (binary coded decimal)

简而言之就是decimal digit的每位以4 bit的形式展现，应该就是书本上的位权码

![image-20201019192553585](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019192553585.png)

### 8421编码

![image-20201019192627566](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019192627566.png)

这个挺简单，就是每个digit都用二进制来表示

![image-20201019192655625](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019192655625.png)

上面是valid的情况，下面是invalid的情况

![image-20201019192724563](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019192724563.png)

![image-20201019192738344](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019192738344.png)

![image-20201019192751459](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019192751459.png)

这样直接给decimal number算的话就比较简单

### binary to BCD

![image-20201019192819130](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019192819130.png)

> emem 这个原理我是真的不明白，他是shift 3次，然后大于4 就加个3额，就得到了，不知道原理是什么

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019195035552.png" alt="image-20201019195035552" style="zoom:25%;" /><img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019195042995.png" alt="image-20201019195042995" style="zoom:25%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019195042995.png" alt="image-20201019195042995" style="zoom:25%;" />

别人说了个原理，看你看不看得懂把

### 2421 code

![image-20201019195551811](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019195551811.png)

这个是self complement的，他其实有两种方式，2421，其实也就是二进制，不过比较特别的是他的第四位也作为2进制，这样的话就会有相应的特性。要看set2的哈，能用2的是不会用4的，优先用靠近1的2，但4以后都要用到第一个2哈

![image-20201019200814874](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019200814874.png)

这是其他的 bcd 码，额，看你用不用了哈

## 10. gray code

![image-20201019200850628](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019200850628.png)

> 这个和上面的bcd不一样，是unweighted的，可以reduce operation

![image-20201019200935729](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019200935729.png)

![image-20201019200942173](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019200942173.png)

> 你观察一下就可以知道，他和二进制不一样，每次加1都只会改变一个bit，你观察下34那里，加1改变了多少bit

### 1. binary-> gray

![image-20201022091336291](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022091336291.png)

然后这个真值表实际上就是不进位的那个，`1 1 = 0, 0 1 = 1, 0 0 = 0 ,`

![image-20201022091341789](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022091341789.png)

b-> g 是往下的

### 2. gray -> binary

![image-20201022091408799](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022091408799.png)

![image-20201022091413804](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022091413804.png)

g -> b是往上的

## 11. logic gates

![image-20201022091430003](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022091430003.png)

![image-20201022091435657](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022091435657.png)

这个很简单，实际上就是非门，但是呢，有啥用呢，你看上面有两个的，最后的出来的结果不还是相同的吗？但是呢，这个是有用的，可以说是缓冲的作用，buffer，因为在这个operation里面会浪费一些时间，然后还有feedback，你看不是有一条线直接连到Y了吗，那实际上就是你只要输入了一次一个数字，就会不断地输出，输出作为feedback反过来作为输入进行。

![image-20201022091443662](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022091443662.png)

然后这里的话就是三个的，那就是更加delay了，周期你就看着这样算把

### part 2  AND GATE

![image-20201026183429461](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026183429461.png)

> 这里的话又来算enable和disable了，我是懂什么意思，就是控制一个变量的时候当另外一个变量变的时候，结果是保持不变还是变化，不变的话就等于你这个坏了，disable了，变了的话就是enable，enable to change

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026183436368.png" alt="image-20201026183436368" />

> 这里的话俺不懂ttl和ecl哈，反正嗯，就是ttl作为floating的时候是为1的，ecl是反过来哈

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026183504253.png" alt="image-20201026183504253" style="zoom: 33%;" />

> 这个电路是有讲是什么类型的，所以就可以看出来哈。

### part 3

![image-20201026185041027](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026185041027.png)

这就没啥好看点，懂得都懂

![image-20201026185059434](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026185059434.png)

> 这里还是讲到了个enable和disable的问题，enable的话实际上就可以作为一个buffer缓冲了。
>
> 当有一个unused input的时候在不同电路下展现的情况也就是不同的哈。

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026185107581.png" alt="image-20201026185107581" style="zoom:33%;" />

![image-20201026185124513](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026185124513.png)

这个的话看看就好

### part 4

![image-20201026185944699](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026185944699.png)

这个转换蛮有趣的哈，看看把其实就是德摩根定律嘛

![image-20201026185952437](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026185952437.png)

![image-20201026190002994](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026190002994.png)

没啥，基本都是和原来的 AND OR GATE差不多的

### part 5

![image-20201025094244075](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025094244075.png)

这个就是算进位的，也可以说是异或？我忘记了？，他里面的内部逻辑实际上是下面这个东西组成的，蛮有趣的哈。	

![image-20201025095342766](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025095342766.png)

这个也好有趣，能充当buffer和inverter的作用。反正我就发现他讲的时候都喜欢找enable和disable，然后就来判断他的性质

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025095724180.png" alt="image-20201025095724180" style="zoom:67%;" />

properties，其实第二个不难推，你把`C`的值带进去就ok了，问题不大

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025101418996.png" alt="image-20201025101418996" style="zoom:67%;" />

这个的话也不难哈

#### 利用性质解决问题

![image-20201025101639559](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025101639559.png)

### part 6(Exclusive NOR Gate)

![image-20201025103025576](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025103025576.png)

就是这个圆圈的，刚好反过来，都一样的话为1，有不同的就为0

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025103529842.png" alt="image-20201025103529842" style="zoom:67%;" />

这个就刚好和上面的反过来，不过也正常哈，上面当一个输入为0的时候，要求另外一个输入为1才能输出1，这里的话就要求相同，那就要求0就可以了

#### properties

![image-20201025104051515](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025104051515.png)

也是可以理解的哈

![image-20201025105806568](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201025105806568.png)

这个很有趣诶，就是他们是相等的呢，然后互为compliment要记住啊哈

对于偶数的那个也可以额进行直观的理解，把他分两拨，变成两个，然后你看下是不是刚好相反的，一个11=0，一个01=1。对嘛，就有趣。奇数的那个也差不多哈，是可以想的出来的

### NAND GATE AS UNIVERSAL

![image-20201026190800897](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026190800897.png)

这个的蛮有趣的诶，实际上就是NAND GATE去充当Universal gate，因为可以用NAND GATE去代表各个gate。

- 这里的not 的话就保持两个输入相同就可以了
- AND 的话就加个not的就好了，所以刚好就要两个 NAND GATE

![image-20201026190809747](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026190809747.png)

![image-20201026190815765](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026190815765.png)

![image-20201026190821210](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026190821210.png)

> 看下这个or gate，既然可以用来表示AND ，那or也是可以的哈，这里的话就是用到了三个 NAND GATE

![image-20201026190827020](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026190827020.png)

这个在 OR 前面加个 NOT 就ok了

![image-20201026190832860](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026190832860.png)

问题来了哈，这个按照最基本的公式的话就要求九个，然后你画完了图发现呢，可以把两个not的给去掉，所以减少成了5个，但是实际上还可以减少哈

![image-20201026190838863](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026190838863.png)

![image-20201026190844850](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026190844850.png)

![image-20201026190850263](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026190850263.png)

但是呢，这里给你提供了一个方法哈拉，我感觉我是自己想不出来的，用了很多德摩根，因为德摩根实际上感觉可以减少operator，

![image-20201026190855283](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026190855283.png)

然后根据前面的内容，算XOR的话直接+1就好了

![image-20201026190902103](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026190902103.png)

### NOR GATE AS UNIVERSAL

![image-20201026192951580](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026192951580.png)

这个实际上和上面的也是差不多的哈，都是not的时候一个gate，这里的话就是or变成两个gate，and变成三个gate了

![image-20201026192957460](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026192957460.png)

![image-20201026193003220](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026193003220.png)

![image-20201026193008641](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026193008641.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026193014033.png" alt="image-20201026193014033" style="zoom:50%;" />

![image-20201026193020762](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026193020762.png)

![image-20201026193025726](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026193025726.png)

![image-20201026193032567](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026193032567.png)

怎么说呢，直接就是从上面拿下来了额，但是这个思维有点跳跃我有点跟不上哈，所以的话那就这样吧，后面的话就跟着写一次

![image-20201026193039766](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026193039766.png)

答案分别是5和7哈

### K Map

> 感觉他的k map讲的好好，反正我现在是懂了原理，懂了为啥要用，然后一些具体的使用情况我也会了嘻嘻开心哈，虽然进度会比较慢，我得快点赶

![image-20201026195835324](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026195835324.png)

![image-20201026195841308](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026195841308.png)

> 这个就是化简标准式，你看看起来挺复杂有点难化简，那k map的作用就是让你迅速简单地化简哈哈

![image-20201026195846983](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026195846983.png)

> 注意k map是这样划分的，然后你看bc 第三列是1,0，你觉得合理吗啊，这个k map的核心过程就是pairing，那你的pairing中是根据格雷码来的，也就是你的两边必须只有一个数发生了变化，所以看下面的

![image-20201026195851678](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026195851678.png)

你看第三个的位置是m3，不是m2，因为我们要保证左右两边只变化一个数字，所以pairing的话最后一个和第一个也是可以的，那为什么要保证像格雷码那样呢，是因为你是为了使用`A+A'=1`,这个是核心，这个是为什么你要搞k map的原因，当你刚好是两个的时候，你就为了化简，把其中一个变量消掉，你跟我说有两个变量不一样的时候你怎么消掉嘛，肯定是不行的哈

![image-20201026195857573](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026195857573.png)

![image-20201026195903800](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026195903800.png)



![image-20201026195913283](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026195913283.png)

看看哈，流程就是这个样子的

#### example

![image-20201026195921454](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026195921454.png)

这个的话也就那样，找出不变的，然后就是那个值了哈。

![image-20201026202322008](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026202322008.png)

这个是可以重复的哈，因为`A+A=A`

![image-20201026202326663](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026202326663.png)

这个主意吼，直接可以用冗余定理来算，不过我觉得只用每项用上了就行，没有必要再用第二次

![image-20201026202331940](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026202331940.png)

这个是告诉我们，最后的式子的答案可能就不是唯一的，可能会有多个的，根据你选择化简的形式不同。

### Implicants

![image-20201029144235953](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029144235953.png)

能凑成一对的都是implicants，prime implicant是最大的可能的组合

![image-20201029144342671](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029144342671.png)

EPI，啊，有点忘记什么意思了，就是你最多只能这样组合，否则的话会剩一个1出来，这个是不算的。

![image-20201029144203674](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029144203674.png)

![image-20201029144824196](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029144824196.png)

因为2可以和旁边的组合，所以不是essential的

### K Map with 4 variables

![image-20201029144448951](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029144448951.png)

注意这个哈，column变4了那也要注意格雷码的问题。所以现在这个格子是12不是8

![image-20201029144503036](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029144503036.png)

![image-20201029144518423](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029144518423.png)



![image-20201029144531248](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029144531248.png)

看这个方法也是一样的

![image-20201029144545427](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029144545427.png)

这个就告诉我们框一定要选最大的！

### Don't care Map

![image-20201029150455306](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029150455306.png)

这个之前就遇到过 了，不过这里讲怎么有助于化简，就你想改成0就改成0，想改成1就改成1，所以的话最小项那就改成1，容易化简，最大项就反过来呗

![image-20201029150506928](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029150506928.png)

### K Map Using Max terms

![image-20201029150142990](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029150142990.png)

基本上就是这样，我们之前一直是？？？我这个很懵逼啊，为啥会一样。好像真的一样哈

## 12. Combinational Circuits

### 1.  Combinational 和 Sequential的区别

![image-20201101110202051](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101110202051.png)

![image-20201101110209068](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101110209068.png)

主要的区别就是一个输入就是输入，输出就是输出，但是时序电路的会是会有feedback的，你的输出会影响你自己的输入。



### 2. Half adder

![image-20201101110749643](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101110749643.png)

其实这个很简单，就是加法器，记录进位和sum就可以了。然后看下内在逻辑是不是这样的，但为什么说是half adder呢，要看到后面的full adder，half adder的话就功能没那么全，因为就两个输入。

### 3.  Full Adder

![image-20201101111230125](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101111230125.png)

这个是真的full adder哈，这个多加一个的是什么？其实可以充当进位的。没错把，这样多个full adder一起就可以完美地做加法了

![image-20201101111237121](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101111237121.png)

然后你就发现了Sum 是这个表达式，为啥？其实还是很简单的哈。异或的话不就是A'B+B'A把，那这两个就完全相反，那你可以在K Map中找到这种，你看那个图不是刚刚好吗。

![image-20201101111242222](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101111242222.png)

如果我们按我们之前说的最大pair grouping的话，那求出来就是第一个结果，但是课本上找到的是第二种表达方式，但是某问题，你用不同的方式group一起就可以得到了

![image-20201101111247737](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101111247737.png)

![image-20201101111254159](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101111254159.png)

这个是证明的，证明那两个相等





-----------------------------------anki 2020.11.9目前-------------------------------------------------------------

我觉得下一步搞进位器就可以了

###  4. Four Bit Parallel Adder using Full Adders

![image-20201101111305878](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101111305878.png)

![image-20201101111351713](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101111351713.png)

![image-20201101113834031](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101113834031.png)

![image-20201101112247101](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101112247101.png)

这个就是full adder的应用，其实很简单哈，你可以用两个full adder，第三个输入当做进位就好了，很简单的

### 5. half  subtractor

![image-20201104084604175](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201104084604175.png)

其实这个很简单哈，只是判断借位的问题，然后D又是异或，和加法一样

![image-20201104084614299](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201104084614299.png)

借位的话A为0，B为1，只有这种情况

### 6. full subtractor

![image-20201104084859147](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201104084859147.png)

full的话就多了个借位嘛

![image-20201104084911862](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201104084911862.png)

有趣哈。看看

### 7. 2-Bit Multiplier

![image-20201104085112438](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201104085112438.png)

![image-20201104085126880](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201104085126880.png)

![image-20201104085137428](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201104085137428.png)

其实很简单，解决进位的问题





### 8. Carry Look Ahead Adder(CLA Adder)

我疑惑了，这个c0和下一位cin不应该是相同的 吗

是的，没错，但是这里的真值表不是指你这个整个过程的，而是单纯指一次的结果，所以刚好就8种可能哈，就是与右边的机器是无关的，你单纯拿出一个来看就可以了

![image-20201104085407345](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201104085407345.png)

实际上是超前进位器，就是能很快地算出进位。

![image-20201104085416589](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201104085416589.png)

看看你怎么算进位的哈，首先你看这个进位好像和cin没关系啊？哦有关系的，所以分为两种情况进位，一种AB自己就能解决好，另外一种带上cin，所以是+号，一种11进位，另外是01，当cin是1就可以进位，所以很简单理解吧

![image-20201104085426197](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201104085426197.png)

然后写下这个公式就好

![image-20201104085437739](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201104085437739.png)

#### part 2

![image-20201104085452062](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201104085452062.png)

那为啥说这是超前呢？因为cin可以换成ci-1,那你就可以一直替换，最后知道c-1就可以了。一般都是算出sum才算出进位，有个依赖关系，这里就可以直接算

### 9. Multiplexers

其实也就是数据选择器罢了

![image-20201105094454582](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094454582.png)

数据选择器顾名思义就是选择数据的，通过一些手段来选择数据哈。那怎么做到这么多个输入一个输出呢？就是看那个selector了，有S0，S1了，其实就是二进制一样吧，一个对着一个，2:1的意思就是2个input，1个output。然后他也可以写成那样的形状，原来那个就是数据选择器啊

![image-20201105094508698](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094508698.png)

你看右下角在算个数是在算啥啊，其实就是你要多少个S能去表示input，然后这里还有个enable就是让你的选择器开关把我觉得

![image-20201105094513497](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094513497.png)

这个其实也没什么的哈，这就是表达式而已哈。

#### 4x1 Multlplexer

![image-20201105094536006](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094536006.png)

![image-20201105094541969](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094541969.png)

![image-20201105094549317](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094549317.png)

这些就没什么特别的，原理就是哪个样子哈

#### MUX TREE

![image-20201109193745399](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201109193745399.png)

![image-20201109193752705](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201109193752705.png)

![image-20201106184212716](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201106184212716.png)

8X1 MUX  using 2X1 MUX

![image-20201106205434801](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201106205434801.png)

![image-20201106205731313](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201106205731313.png)

#### Implementing 8X1 MUX using 4X1 MUX

![image-20201106211146045](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201106211146045.png)

这个很有趣哈，我以为是要用一个2X1 来连的，但是你可以用一个enable和disable来，就十分地简单有用了，那我觉得其他的也可以改装成这样吧。。我觉得可以啊哈哈。

#### Implementation of Boolean Function using Multiplexers

![image-20201106223445272](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201106223445272.png)

这个的话就是implementation了，把这个用到了之前学的东西中，所以的话是通过操控selector来输出function，对应的这个1的function，怎么说呢，自己看看把，还是蛮有趣的哈。

#### 1-Bit Full Adder using Multiplexer

![image-20201109194007002](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201109194007002.png)

怎么说呢，这就是用MUX 的好处把，如果你要按之前的ADDER来的话，你要用到超多gate的，就很不灵活，很麻烦，然后用数据选择器轻轻松松解决哈

![image-20201109194014739](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201109194014739.png)

#### Logic expression from MUX

![image-20201109195422326](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201109195422326.png)

就没了啊哈？

我看走眼了好几次了无语哈

这个和上面的长相 是亦一样的，但是结果不一样哈，就是另外一个例子罢了，没啥的

----------------------------anki 2020.11.15------------------------------------------------------------

## 10. Demultiplexer

实际上就是反过来，一个输入多个输出

然后这个怎么输出是根据enable 和selector来控制的哈

![image-20201109201931951](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201109201931951.png)

![image-20201109201937159](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201109201937159.png)

不过下面这个是啥，我好像不是很清楚哇

###  Demultiplexer as Decoder

来啦来啦，24译码器来了，其实还是蛮容易理解的把，其实就是之前 MUX 返回去咯， 就二进制那样一次次来，然后最后有值的就一个个来

![image-20201109201952260](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201109201952260.png)

![image-20201109201958577](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201109201958577.png)

## 11.2 Bit Comparator

实际上就是比较器啦，比较大小的，也没有啥子啦。

![image-20201112091011267](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112091011267.png)

![image-20201112091032438](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112091032438.png)

![image-20201112091043092](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112091043092.png)

其实也就这样吧，用个K Map很容易推出来的。



## 12. Encoder & Decoder

来啦来啦，n input and m output 这样子的，解码器和译码器的功能刚好是反过来的。

![image-20201112091408857](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112091408857.png)

像这个三八解码器还是译码器的话都不难哈，

![image-20201112091415066](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112091415066.png)

![image-20201112091420756](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112091420756.png)

### 1. priority encoder

![image-20201112145149854](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112145149854.png)

这个优先可以任意选你的优先，我们这里设置的优先是I3>I2>i1>i0这样子的，所以这里当I3为1的话，那后面你不管是否有没有1都不管哈。所以就可以变成Don't Care,这样的话也挺好搞的

![image-20201112145156263](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112145156263.png)

### 2. decimal to BCD encoder

![image-20201112145701501](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112145701501.png)

这个就是十进制转为BCD的编码器，然后也很简单哈

### 3. Combinational Logic Design using Decoders

![image-20201112150034415](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112150034415.png)

这个没啥子难的，但我觉得得用到了两个译码器把。是的把，所以我觉得这个说的还有点问题

### 4. problems

![image-20201112151212009](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112151212009.png)

这里的话是终于了解到最大项的符号了。

![image-20201112151220415](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112151220415.png)

其实也很简单。



## 13. Sequential Circuit

终于来啦，时序电路，之前讲过一些

![image-20201117115755909](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201117115755909.png)

很明显的就是他依靠着之前的输出作为输入的，比如说从1到10每次都加1，那你就要track上次是数到哪了吧，这个很明显就是需要时序电路的，然后的话那我们直接从output传到输入吗？不是的，我们通常会把他们存起来，那这个memory就是counter和 filp flops了。

### SR Latch

SR Latch 有两种,一种是用NOR ，一种是用NAND ,这里用的是NOR

![image-20201117120125373](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201117120125373.png)

latch有闭锁的意思，就是这个门不给你开不给你出去，可以存东西，但是要看情况啊，但目前具体存什么我还不清楚，因为目前就这个Q，也没感觉存啥，但是这个是基础原理把，他说懂了这个就可以懂flip flop啥的完全不在话下。

首先说下 R stands for `reset`,s stands for `set`,当R 是1 的时候，Q是0，S是1的时候Q是1，那么Q'就是0咯，然后你试试这个电路，保证行哈

![image-20201117120131950](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201117120131950.png)

然后看看这个真值表，这个是for nor gate的

![image-20201117120138112](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201117120138112.png)

![image-20201117120143380](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201117120143380.png)

case 2 就是发挥memory作用的，当你两个都置于0的时候你发现输出是不会改变的，也就是可以存东西了

![image-20201117120149135](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201117120149135.png)

但是case 3 的时候就不行，当你把正常情况下的其中一个0打为1时，就错误了，出现了奇怪的东西，啥都无了的感觉，说一不要这样子做哈。



### Clock

现在终于明白了原来 clock就是 clk啊，数字逻辑实验上面经常看到的

![image-20201118093108447](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118093108447.png)

clock的cycle就是50%，一半搞一半低，clock一般是用在latch那里的，后面再看吧，他这个clock好像主要看的是你变化的那里

### Triggering Method

![image-20201118094020068](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118094020068.png)

这个trigger分为两种，一种是level一种是edge，这里的clock就是edge的，从0到1的话就是positive edge，从1到0就是negative edge

这个clock的作用就是control input的

### How to get Edge Triggering

![image-20201118095037933](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118095037933.png)

![image-20201118095059672](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118095059672.png)

额，怎么说呢，他的确是拿到了个edge triggering，也不知道怎么的就有这个电路了，然后呢，input是这样子，算出来的input和output的关系刚好是有个一阶导的关系，所以和斜率有关，所以你看会有一个edge，那控制只有一个方向的edge的话就需要一个二极管差不多了哈。

### Difference between Latch and Flip Flop

![image-20201123220511180](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201123220511180.png)

![image-20201123220516470](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201123220516470.png)

我记得是latch看的是level trigger flip flop用clock去控制，那区别好像就是这个了

### Introduction to SR Flip Flop

咋了，也没啥难的把，其实这个和latch那边差不多的。

![image-20201123220832727](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201123220832727.png)

因为这里用的是NAND，所以是右边那张表，注意后面用的时候SR都是用外面的值了，所以会变成用NOR的table

![image-20201123220838302](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201123220838302.png)

看到没，上面和下面的表反过来了，然后你这 都没发现啊，无语	

![image-20201123220843494](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201123220843494.png)

### Characteristic table & excitation table for SR flip flop	

就是表把，但是我也不知道啥用的，他说对后面的counter有用呢

这个Qn+1 就是下一个的值，Qn是现在的值，其实你可以理解为Qn+1是现在的，Qn是上一个的，因为有memory所以是上一个的值。

![image-20201123222253355](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201123222253355.png)

![image-20201123222324471](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201123222324471.png)

也没啥哈，虽然不知道要不要记住，但是就先这样吧

### Introduction to D Flip Flop

这个D stands for data，他就说诶呀，你看你的SR，没有必要分开搞，直接连一条线过来就行了，所以就不是memory状态的时候，而是有赋值的时候。

![image-20201123222916567](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201123222916567.png)

![image-20201123222922280](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201123222922280.png)

所以就有了一个这样子的表

### Characteristic table & excitation table for D ff

![image-20201123223129528](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201123223129528.png)

这里 就一张图，也没啥，就看要不要记住啥的

### Introduction to JK Flip Flop

就是这里，刚开始我在想为啥子你用的是NAND，但表格却是NOR的，因为你有这个SR，你要反过来的啊大哥。

JK特殊的地方在于他会把not used 和CLK = 0那里利用起来，没看完，后面再补吧

![image-20201123231750825](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201123231750825.png)

### Characteristic table & excitation table for  JK ff

他这里其他的我验证过了，的确是可以的，这个JK ff的主要特点呢，就是把原本not used的情况也用了起来了。然后你发现用起来的话会变racing，我查了下是快速移动的意思啊。就是Qn+1 = (Qn)'

![image-20201130191344781](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201130191344781.png)

![image-20201130191350308](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201130191350308.png)

所以的 话就会有这样的结果哈。

### Race Around Condition

我这里其实没那么看得懂，然后返回去看了别的东西一遍真的是无语啊！这里想说的是波形图

![image-20201130192040625](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201130192040625.png)

![image-20201130192046929](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201130192046929.png)



他说的toggling是stable的，但是race around是not controlled，虽然都是1->0->1，这样子反复，所以到底啥子咯。

我现在明确的一点是clock就是一下高一下低，然后分为两种type，一个level triggering，一个edge triggering。所以的话那我觉得这里的图不是对的

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201130200621210.png" alt="image-20201130200621210" style="zoom:50%;" />

![image-20201130201616683](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201130201616683.png)

然后我又迷茫了

我所以现在他是在用level triggered来做，不是说了ff用edge trigger吗

![image-20201130203117305](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201130203117305.png)

怎么说呢，我算是终于懂了，因为我理解的目的错了，racing around就是010101010101，知道clock喊停，就是clock变0的时候，我以为他是要这样子，然后没想到这个ff是不想要这种情况发生，因为是uncertain的，这也是后面有一种解决方法是要用edge-trigger的，不要用level-trigger，因为edge-trigger时间很短，基本上是够的。

然后，如果T/2 < propagation of delay的，当input进去output出来的时候发现诶，怎么世界都变了呀，这时候就为0了，这种情况是我们想要的，clock可以去控制，不然的话input出来output出去那就是我们不想要的结果了，终于！！！！

![image-20201130203832622](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201130203832622.png)

所以有这几种方式去解决，刚好理解了。

### Master-Slave Operation of JK FF

![image-20201204112618367](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201204112618367.png)

这个就是解决round condition的哈！你看他的名字是master-slave，也就是一个控制着另外一个，你看他把输出都接到了另外一个这里来了，而且对应的clock值也有了变化，可以让race condition变成toggling

怎么控制呢，实际上就是看那个波形图啦

![image-20201204150908797](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201204150908797.png)

看当前一个在工作的时候后一个clock值为0，就是memory的意思，所以每当其中一个在工作的时候，另一个就是在保存，所以已经明显和之前的乱蹦是有区别的了，那看看下面的波形图把

当clock为0的时候，Qm看图啦，Q也看图，代表的都是J，也就是set，最开始的时候Qm为0，咋Q也为0啊，因为就相当于S = 0，那么Q出来就是等于0哈，没错，Qm的值也可以为1，就看当时的状态了。然后当clock变为1的时候，后面的就相当于memory了保持不动，前面的就开始工作，因为Q为0，所以这里的Qm就变为了1，这时候前面的就不动了，变成memory，就不断地往复往复把，是依据clock的cycle有cycle的，所以是稳定的，是toggling

### Behaviour of Master Slave D Flip Flop

![image-20201204154236235](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201204154236235.png)

![image-20201204162606530](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201204162606530.png)

我没做笔记吗诶，这个就是可以做到消除glitches

Qp的意思是 positive triggering  是1的时候only when low to high

Qn就是negative triggering 是1的时候only when high to low

### Introduction to T FF

![image-20201205221009064](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201205221009064.png)

真的非常easy，他说他就是要toggling状态的，那就连成一样的咯，不就是了。

### Characteristic & Excitation Table for T FF

![image-20201206193458528](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201206193458528.png)

我觉得这种东西就完全可以手推的，不过这个表达式也很明显了啊哈哈

### Flip Flop Conversion 

这是啥？

![image-20201206194910526](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201206194910526.png)

右边的那个table 没有jk时候就是 steps 中的2哈

![image-20201206195817171](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201206195817171.png)

噢，所以发现的是在相同input和output的情况下进行转换，而且其实也不一定是要characteristic，也不一定需要excitation，其实两个表的话都是差不多的，然后把两个表叠起来，但有些tricky把，怎么最后你的表达式就是这样和D有关了呢，那样的话也可以搞成Qn有关呀，不好说，看后面怎么搞的把

### T FF -> D FF

![image-20201206201641818](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201206201641818.png)

来了哈，不过也非常的简单把，这里的话T作为被改变的，那就是要xx = T了，所以的话T是这样子放的

### SR FF -> JK FF

![image-20201206202936159](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201206202936159.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201206203228321.png" alt="image-20201206203228321" style="zoom:50%;" />

这里其实就解释了为啥jk是那样变的，诶？循环了诶，不管了就是这样子变的



### Preset and Clear Inputs

![image-20201207115656492](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201207115656492.png)

![image-20201207120537202](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201207120537202.png)

## 14. State Diagram

可以告诉present state next state 之间的relationship

![image-20201209164028572](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201209164028572.png)

这里的状态图是复杂一点的，里面的数据是假设的，涉及到了多个ff，所以s就有四种，x代表的是输入，y代表的是输出，所以横线上就有输入和输出两种

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201209164855666.png)

老哥，这啥意思噢，state diagram就很简洁，能让你清楚地看到关系。

这里就拿了一个简单的jk ff来举例子，状态有 0，1，指的是每次的Qn，然后横线上的数字是input，是什么导致一个状态到另外一个状态，就非常清楚哈

### Mealy and Moore State Machines

#### Moore

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201215111148228.png" alt="image-20201215111148228" style="zoom:67%;" />

这个怎么说呢，看起来原理蛮简单的，但是他就像突然闯进来的一样，突然就有了下面的那个图，我都看得很懵逼一开始，Moore就是他的output表达式与input无关的。 Mealy的话就相反

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201215111258420.png" alt="image-20201215111258420" style="zoom:67%;" />

j就是这个图，就看起来懵逼了哈

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201215111828405.png" alt="image-20201215111828405" style="zoom:67%;" />

这里的话就是举了个例子

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201215112337399.png" alt="image-20201215112337399" style="zoom:67%;" />

这里的话就是告诉你怎么把original 的gram转成Moore state diagram，你只要把ouput的位置改变以下就可以了

#### Mealy

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201215112957766.png" alt="image-20201215112957766" style="zoom:67%;" />

他这个就没讲啥。。。

## 15. Analysis of Sequential Circuts

### D FF

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201215113615390.png" alt="image-20201215113615390" style="zoom:67%;" />

首先这个图应该是直接给的，我就不知道怎么来的了，首先你可以发现这是一个D FF，因为最上面有写个D，他的step1 时去写出input和output的表达式。

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201215113956743.png" alt="image-20201215113956743" style="zoom:67%;" />

这个Qn+1 = D还记得把？ 第二个是去找到state table present state 和next state 之间的关系与联系。

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201215114536984.png" alt="image-20201215114536984" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201215114942944.png" alt="image-20201215114942944" style="zoom:67%;" />

懂了，真的讲得很清楚，最后一步就是画出state diagram 了，真的简单

### JK FF

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201215120205681.png" alt="image-20201215120205681" style="zoom:67%;" />

这个也是same old stuff，找套路，第一步就找对应的equation

![image-20201215120922970](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201215120922970.png)

嘿嘿，记得 JK 的truth table吗，我记得哈哈

![image-20201215121057905](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201215121057905.png)

然后就这样了



我们就在这里停了，后面有一个是T FF的，我就跳过了

## 16. State Reduction and Assignment

![image-20201222145510998](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201222145510998.png)

里面这些有些是redundant的哈，所以需要reduction

![image-20201222151910229](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201222151910229.png)

​	![image-20201222153055246](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201222153055246.png)

所以就可以把g给去掉了

![image-20201222153149361](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201222153149361.png)

又删掉了一个

![image-20201222154053093](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201222154053093.png)

重新画好的图

## 17.  counter



### Introduction to counter

![image-20201228203841903](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228203841903.png)

![image-20201228203850258](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228203850258.png)

![image-20201228203859388](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228203859388.png)

晕，我怎么不做笔记啊，我懂了哈，要用下降沿的，这样就可以从0 count 到一定的数字了，啊，我突然觉得negative edge 和positive edge 没有区别啊！噢有区别了，sorry，异步的计数器的话是有区别的因为QB看的是QA哈

![image-20201228203910848](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228203910848.png)

![image-20201228203918688](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228203918688.png)





### Types of counter

![image-20201228203936046](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228203936046.png)

![image-20201228203942595](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228203942595.png)

![image-20201228203948382](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228203948382.png)

![image-20201228203954773](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228203954773.png)

### 3 bit Asynchronous up counter

![image-20201228204018146](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228204018146.png)

这样一看和寄存器的长得好像噢

![image-20201228204024997](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228204024997.png)

![image-20201228204030305](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228204030305.png)

![image-20201228204036041](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228204036041.png)

### 4 bit asynchronous up counter

![image-20201228144740595](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228144740595.png)

这里用到了T ff，因为我们就只需要toggling状态，那就没有必要用jk了，大材小用了a

![image-20201228145127199](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228145127199.png)

这个也很简单哈

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228145256858.png" alt="image-20201228145256858" style="zoom:67%;" />

也没啥区别把

### 3 bit & 4 bit asynchronous down counters

![image-20201228151905973](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228151905973.png)

这个真的可以，有两种变的方法哈，但俺们一般选的是下面那个吧，做可逆的时候方便点

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228153258159.png" alt="image-20201228153258159" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228153604991.png" alt="image-20201228153604991" style="zoom:67%;" />

后买你一个的话要等会才能实现？好像是的，因为最开始它并不为1啊

### 3 bit and 4 bit up/down ripple counters

![image-20201228155201737](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228155201737.png)

是异步的哈

![image-20201228160236156](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228160236156.png)

这里就有点像选择的感觉了 ，它这里认为规定M=0的时候代表向上数，M=1的时候代表向下数，然后向上数的时候Q和clock相连，向下数的时候Q` 和clock相连，那就是用上面讲的第二种方法啦，这个Y表示的意思是clock的值把，所以M=0的时候只看Q，M=1的时候只看Q'  ，无语哈，我还想了有点久，这M的表就是老实地跟Q输出或者Q compliment输出

为啥用第二种呢，这个真的让我觉得再学java的接口，要耦合，所以的话这里就轻松控制一下就可以改变是up or down，那么输出的值也得选同一个，所以和上面的相比的话肯定要选第二个，不选第一个

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228160658143.png" alt="image-20201228160658143" style="zoom:67%;" />

K Map是这个哟，头终于不痛了，那其实就是异或啦，数据选择器罢了，0的时候就选Qa，1的时候就选Qa compliment

![image-20201228160948944](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228160948944.png)

的确，没错，改装一下后就可以用啦

### -----------2021.1.5看到了这里

### Modulus of  the counter & counting up to Particular Value

![image-20201228162159671](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228162159671.png)

怎么说呢，它这个好像是在和我们讲modulus counter 是什么，其实也就是别名而已，没有别的意思，也并不是，看右边的ex，这样的话就可以去算到 6，7这种值。

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228163015714.png" alt="image-20201228163015714" style="zoom:67%;" />

这里的话需要用到preset 和clear

![image-20201228164050565](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228164050565.png)

就是怎么作用的话看这个，我就觉得怪怪的把，反过来的话还觉得好一点

![image-20201228164702687](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228164702687.png)

的确，nb，到6的时候clear那里都起作用了，然后就重新再来一遍，然后preset的话都会设置成1的哈

![image-20201228164956879](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228164956879.png)

的确哈

### State Diagram of  a  counter

![image-20201228165432952](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228165432952.png)

这个好像也没啥，就这样子画的，就很直接把

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228170320234.png" alt="image-20201228170320234" style="zoom:67%;" />

这个也很简单把



### Decade(BCD) Ripple Counter

![image-20201228170739717](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228170739717.png)

![image-20201228171329305](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228171329305.png)

然后这是实际上是上上个视频的延申，所以的画的是数10的时候，那我们还是用的是same trick，都是要用到nand gate的，因为我们要让结果back to 0，那这样的话那还是挺简单的哈，直接搞个就行。

![image-20201228171747597](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228171747597.png)

然后的话可以化简一下子

### How to design synchronous counters

![image-20201228184138919](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228184138919.png)

他说的是这个同步的计数器会比较难design出来，所以的话就要follow一下step

![image-20201228190221963](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228190221963.png)

![image-20201228190606271](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228190606271.png)

怎么说呢，这就是把，这种图都是因为你后面的J1,K1,J2,K2值很多就不是你想要的，也没有必要哈

![image-20201228191505727](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228191505727.png)

这个很tricky啊，就是自己设计出来的，像硬凑的一样，好nb

### 3-bit synchronous Up Counter

![image-20201228195249437](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228195249437.png)

![image-20201228195909437](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228195909437.png)

真的用了T FF 省事多了

![image-20201228200237811](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228200237811.png)

有趣，简单！

![image-20201228202549405](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201228202549405.png)

我有种看得停不下来的感觉怎么办呃



### 3-bit Up/Down Synchronous Counter

![image-20201230152154744](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230152154744.png)

这个就是再来一次一体化呗

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230153323239.png" alt="image-20201230153323239" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230153619745.png" alt="image-20201230153619745" style="zoom:67%;" />

![image-20201230154438210](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230154438210.png)

wow这个我没有精力去想为啥啦，但是呢，最后Tc连出去的话是他现场画出来的，搞成4-bit，好快啊，看来是有规律的，但是俺呢，没来得及搞哈，大概就这样吧



### Introduction to registers

![image-20201230161053323](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230161053323.png)

寄存器啦啦啦

他这里的clock的话大家都是一样的哈

## 18. registers

### 1. Introduction to registers

![image-20201230162214424](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230162214424.png)

怎么说呢，他这里说了我们之前用的ff也是可以用来memory的，但是呢一次就一位，所以不是很好，为了增大存储的容量，我们就去用多个ff，这多个ff合起来就叫做寄存器，专门就用来存的嘛，不过我们这里遇到了一个问题，我们用的是negative edge triggering，所以的话你一个周期之后就存不了了啊，我们不想要这样的结果，我们想要能控制的，所以这里引入了一个independent control，就是load，虽然俺也不知道啥用，为啥子要这样子搞，然后说了有两种情况，同步与异步，但是反正把load搞为0的时候就是可以存的哈

### 2. data formats & classification of registers

![image-20201230164147671](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230164147671.png)

就是你输data进去的时候可以有两种形式，一个是一个一个的输，另外一种是分别输入，同时的，extract出来的时候也是两种形式，serial的叫做 temporal code parallel的叫做special code

![image-20201230165815318](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230165815318.png) 

哇，分类来了，好激动，这个刚好和我们课本的对应上了，然后我终于明白并行输入，和串行输入了，就是这样shift 的话就是一个一个移动的，所以用的更多是serial把，storage就是不动的，所以用的是parallel把，真有趣真有趣哈哈



### 3. Shift Register(Serial In Serial Out)

![image-20201230185038103](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230185038103.png)

![image-20201230190703364](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230190703364.png)

懂了，刚开始我还在纳闷怎么这个Q3不是1嘛，咋D2不是1呢，因为这个clock是同步的，所以的话有clock过来就直接执行了，而不是等前面的过来。

![image-20201230191018624](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230191018624.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230191025398.png" alt="image-20201230191025398" style="zoom:67%;" />

![image-20201230191847305](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230191847305.png)

这个出去的话也是serial出去的，你看为什么叫移位寄存器啦，就很生动形象吧

### 4. Shift Register(SIPO & PIPO mode)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230192750376.png" alt="image-20201230192750376" style="zoom:67%;" />

这里讲了一个drawback，的确，我刚刚也想到了，因为你是一串输出来的，那你输出的就会很慢，而且要看，需要不止4个clock脉冲，你看你刚输出来的就是一堆无用的数据

![image-20201230193455007](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230193455007.png)

SIPO就很简单，你直接这样输出就可以了，四次应该就可以成功

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230194154927.png" alt="image-20201230194154927" style="zoom:67%;" />

在书本上的就是普通的寄存器哈

![image-20201230194803695](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230194803695.png)

这个就是PIPO，也并不难哈，我们一般会在trigger之前把值输进去，以防止delay，接着呢你就可以用clk = 0，把值存起来就好啦，接着说一下为什么是buffer，因为你输入什么就会输出什么act  as a buffer

![image-20201230195255917](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230195255917.png)

only need 1 clock pulse to store the data 

### 5. Shift Register(PISO Mode)

![image-20201230201215164](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230201215164.png)

这里有点不一样噢，这里用到了load，其实之前就有说要用到，但是都没有用到，不知道咋地这里就用到了，有load的话那就是同步的了啊，nonono，而且在这期间clock可以为1哈

![image-20201230202329135](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230202329135.png)

有趣，懂了，所以上面那个复杂的实际上就是在控制状态，一下子移位，一下子储存来着，可以的哈，不过首先要load mode 把，因为要store啊

![image-20201230204339188](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201230204339188.png)

怎么说呢，这里的确就是开始shift的，但我觉得还是有上面的情况，就是你先把自己push过去，因为是simultaneously，接着再是shift别人的 

怎么说呢，也没有那么难其实，就是我在考虑他是不是能马上出来考虑了一段时间，还有他的时钟要一直怎么样的时候考虑了时间，反正就各种考虑把