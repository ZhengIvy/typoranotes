## 1. Insertion Sort

> 重新回顾了一遍，实际上的话和你玩扑克时候给牌排序的方式差不多吧

![image-20200913214255666](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200913214255666.png)

蛮有趣的哈

### 循环不变量？

按照书中的意思是在这个排序中，`1~j-1`都是排序好的，所以`A[1..j-1]都是不变的了`，在每轮循环中这些值都是不变的，所以叫`loop variant`

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200913220152058.png" alt="image-20200913220152058" style="zoom:67%;" />

主要是可以证明循环的正确性啊哈

### pseudocode  conventions

1. `for j = 2 to A.length` `to`表示increment 1,`downto`表示 decrement 1 ，` by` 的话`loop counter`改变的数超过2
2. return 允许返回多个值
3. `and or`是短路

### 推算Insertion sort的时间复杂度

![image-20200920194122204](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200920194122204.png)

出现best case 的情况

![image-20200920194158124](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200920194158124.png)

出现worst case的情况

![image-20200920194316850](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200920194316850.png)

> 首先是学了他是怎么推insertion sort的时间复杂度的。然后告诉我们把具体的时间用字母代替 后面字母也可以忽略掉 因为在超大数字的面前是系数都是无关紧要的。
> 接着给我们推了最坏的例子和最好的例子的情况，还说了一下平均的情况，但其实也差不多吧，因为可以视为一半是排序好的，一半没有。这样的话还是不能改变，只是改变了系数罢了。为什么通常情况下我们要考虑最坏情况呢

### 但是一般情况下，我们研究的是worst case

1. 给了一个上限，有个底
2. 最坏的情况经常出现，比如说在数据库中找不存在的东西就经常发生
3. 平均情况和最坏情况是大致相同的



------------------------------------9.27 anki------------------------------------

## 2.分治法(divide and conquer)

有很多有用的算法是递归的，这种算法基本上都会采用分治法，把问题化为多个小问题，不断循环地去解决问题，然后把这些解法结合起来就能让原问题有一个解决方案。

1. `Divide` 把这个问题分成多个相似的小问题
2. 不断地解决问题，当一个问题足够小的时候就可以用直接的方法去解决
3. 把小问题的解决方法结合起来

`Merge Sort`就是依照着这种定式

1. 分解待排序的n 个元素的序列成各具n/2个元素的子序列
2. 解决：使用归并排徐递归地排序两个子序列
3. 合并：合并两个已排序的子序列以产生已排序的答案

归并排徐的关键操作就是合并，我们通过调用一个辅助过程来`MERGE(A,p,q,r)来完成合并，其中A是一个数组，p,q和r是数组下标，满足p≤q＜r`，假设子数组A[p,q]和A[q+1..r]都已排好序，这样就可以合并为一个子数组A[p+r],其中`n=r-p+1`是待合并元素的个数

> 回到我们使用扑克牌的例子，有两堆已经拍好序的牌，然后再次排好序合为1个堆，这就是合并的核心，基本步骤就是在堆上两张牌选最小的，然后放到一个堆里面去，直到两个堆中的一个堆为空，再把剩下的牌直接放上去就好了。这时候n个变量，我们最多就执行n个步骤(因为每张牌就比一次)，所以合并就需要`θ(n)`的时间。
>
> 但在伪代码中有一个变化是增加了一张哨兵牌作为无穷大，避免在每个基本步骤中检查堆是否为空,这样的话就像不用每次比较都喊话你好了没，你好了没，而是被动地告知我好了，然后就明白了，就可以提高效率嘛，不用一个for循环去找有没有越界的问题啦

![image-20200920211348230](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200920211348230.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200920211331934.png" alt="image-20200920211331934" style="zoom:67%;" />

![image-20200920211405271](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200920211405271.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200920211512474.png" alt="image-20200920211512474" style="zoom:67%;" />

具体就是这张图啦

![image-20200920212622085](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200920212622085.png)

#### 哨兵牌的作用

> ### 查找中免去越界判断
>
> 
>
> ​    这种在查找方向的尽头设置“哨兵”免去了在查找过程中每次比较后都要判断查找位置是否越界的小技巧，看似与原先差别不大，但在总数据较多时，效率提高很大，是非常好的编程技巧。



> 总结出这个merge sort 每次merge都创一个数组来储存，缺点可能就是空间复杂度会比较高把
>
> 然后也没什么别的难度了吧

## 3.merge sort的时间复杂度

> 其实也蛮简单的，主要是怎么证明整个复杂度合起来是(nlgn),实际上就是可以用数学推出来，之前也推过每次合并是`cn`,那就主要看多少次咯？而且这个n是相对的，与原长度相比就有可能是`n/a`了，而且我们把长度定为`2^b`，这样好算点，

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200924093123052.png" alt="image-20200924093123052" style="zoom:67%;" />

看下这个图，就基本很明白了哈，每level加起来都是cn，就看有多少个就可以了

悄咪咪说下，之前不是说过merge sort在input size很小的时候就比不过insertion sort，很多排序都是这样子，二者不能兼顾的，所以书上说就可以在排到很小的时候换成别的算法来排？(是一种想法，就是不知道可不可以)



## 插个题外话 k阶的斐波那契数列

> 这个我看了好久，然后才发现这个跟正常的斐波那契数列不是一个意思哈，算法也不是一个意思呢，无语哈，这件事告诉我们该放手时就放手，不要留着

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200927195505438.png" alt="image-20200927195505438" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200927195524329.png" alt="image-20200927195524329" style="zoom:67%;" />



> 原来就是这样子的哈，所以并不是前两项相加的和，而是前k项哈，真的十分有意思呢，我们真的不可以在一道题上滞留太久

## 4. Growth of Functions

### θ-notation

> 之前在书里说过insertion sort 的worst case是`θ(n^2)`，那这里就来讲这个符号了

![image-20200927202102540](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200927202102540.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200927202131075.png" alt="image-20200927202131075" style="zoom:67%;" />

> 就像一个三明治夹在中间一样，`θ(g(n))是一个集合`，所以的话我们就可以写∈符号，但是我们通常会让他`=`,不过其实是一个意思<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200927202322932.png" alt="image-20200927202322932" style="zoom:50%;" />

不过注意，不是所有input都符合的，他其实有限制`n>n0`,因为你也知道insertion sort的best case 就是不符合的

### O-notation

> O是上限
>
> ![image-20200927203723853](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200927203723853.png)
>
> 虽然是这么说，但一般所有input都是符合的,我们用来表示最坏的情况

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200927204233892.png" alt="image-20200927204233892" style="zoom:50%;" />

## 第二个题外话：稀疏矩阵

sparse matrix

是什么呢？就是一个矩阵里面有很多0，只有少部分有值的

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200927204625372.png" alt="image-20200927204625372" style="zoom:67%;" />

写成这样的话应该是比较好存储表示一个矩阵

## 6. Standard notations and common functions

![image-20201013132252437](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013132252437.png)

### 取模

![image-20201013132313334](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013132313334.png)

### exponential

![image-20201013132943337](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013132943337.png)

不知道为啥讲到了这个？

![image-20201013133010019](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013133010019.png)

![image-20201013133733874](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013133733874.png)![image-20201013133745303](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201013133745303.png)

# Sorry，我还是看视频了

看书是真的头疼哈

## static array

![image-20201014210105133](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014210105133.png)

静态array就是固定好长度的嘛，额，感觉也就这样了吧

## Dynamic Array

![image-20201014210527599](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014210527599.png)

看看就好 啊

## Singly Linked Lists vs Doubly Linked Lists

![image-20201014210609635](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014210609635.png)

> 这些pros and cons 你应该也是知道的把

![image-20201014210650662](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014210650662.png)

![image-20201014210710942](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014210710942.png)

解释下为什么`remove at tail`是为啥哈，因为你remove的同时要把他的前一个的next改为null，不过后面的有些我觉得也不是很准，说实话啦，按你自己理解来，相信你的理解是对的



看看java doubly linked list 写的源码

![image-20201014211129978](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211129978.png)

![image-20201014211153302](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211153302.png)

![image-20201014211210725](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211210725.png)

![image-20201014211220269](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211220269.png)

![image-20201014211227782](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211227782.png)

## 栈？

![image-20201014211240900](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211240900.png)

![image-20201014211250988](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211250988.png)

想想用途哈，看起来还是蛮有趣的对吧，今天搞了那个括号的，其实蛮简单的

![image-20201014211552254](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211552254.png)

![image-20201014211559899](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211559899.png)

![image-20201014211620254](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211620254.png)

### pushing

![image-20201014211630497](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211630497.png)

## queue

![image-20201014211639738](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211639738.png)

![image-20201014211645243](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211645243.png)

![image-20201014211650353](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211650353.png)

### BFS 使用queue

![image-20201014211704704](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211704704.png)

这个bfs啥意思呢，就是你查找的时候是按邻居一个个来查的，比如第一个0，那就查9,1，再查8，这样的话你就需要某种东西去协助你看哪些visited没，哪些要visited，下面入队和出队就是记录这个过程哈

![image-20201014211710142](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211710142.png)

![image-20201014211716341](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211716341.png)

![image-20201014211721651](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211721651.png)



---------------------------------------------2020.10.24 anki----------------------------

## 优先队列

![image-20201014211730190](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211730190.png)

![image-20201014211735095](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211735095.png)

![image-20201014211739885](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211739885.png)

![image-20201014211751158](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211751158.png)

![image-20201014211756081](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201014211756081.png)

> 优先队列我觉得就是重写Comparable类似？默认的方式是按照队列的优先是按照大小来的，但是这里的话就说你可以自己规定你比较优先级的方式，差不多就是这样