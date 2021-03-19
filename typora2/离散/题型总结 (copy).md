# 题型总结



## 1. 最小生成树

### 1. 一个图中有多少个不同的生成树？

这个7C5 的意思是排列组合，从7个边中挑出5个边进行，再减去形成cycle的圈数就是了



##  





### 2.最小生成树（就是权最小的）

#### a.Prime's 算法(好像就是避圈法？)





就是首先选最小的那条边，然后再沿旁边的点进行选择，然后依次下去就可以了，如果有cycle就要避开的



#### b. Kruskal's 算法

这个算法呢就是不沿着边去搞，而是直接把最小的依次挑出来，如果有cycle就跳过那条边，就ok

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622101620119.png" alt="image-20200622101620119" style="zoom: 50%;" />





## 2.  判断是否为xx图

热知识：平凡图是欧拉图，哈密顿图，偶图，平面图？

#### a、欧拉图

> 1. 无向图**G**是欧拉图当且仅当**G **连通且无奇度数顶点**.**
>
> 2. 无向图**G**是半欧拉图**当且仅当** **G** **连通且恰有两个奇度顶点**.
>
> 3. **有向图** **D** **是欧拉图** **当且仅当** **D** **是强连通的且每个顶点的入度都等于出度**.
>
> 4. **有向图** **D** **是半欧拉图** **当且仅当** **D** **是单向连通的，且**
>
>    **D** **中恰有两个奇度顶点，其中一个的入度比出度大** **1** **，另一个**
>
>    **的出度比入度大** **1** **，而其余顶点的入度都等于出度** **.** (说实话，这个好像是在哪里见过啊，可能我嫌麻烦就没有加进去罢了)

 

##### Fleury 算法

就是你已经知道这是个欧拉回路了，然后你要求一条路径出来哈，是不唯一的，但就是可以，然后在高数叔里面就没讲到了，孤立的顶点应该也是可以的





> 到底是怎么用的呢，就是直接删，从哪开始基本都ok的，但是要注意删之前的话要看下删后会不会形成分支，变成noconnected  必须要connect 起来哈，基本就是这样子把



#### b、哈密顿图

>1. **设** **G** **是** **n** **阶无向简单图，若对于任意不相邻的顶点** **v** **i** **,** **v** **j** **，均有** 
>
>​           **d** **(** **v** **i** **) +** **d** **(** **v** **j** **)** **≥** **n** **-** **1       (** * **)**
>
>​			**则** **G** **中存在哈密顿通路** **.** 
>
>(有没有发现这个和之前判断简单图是否为连通图是否为回路那里很像啊，是的，**不过那里是每一对边**，这里是任意的顶点，而且这里刚好的也是哈密顿通路啊)？？？？？
>
>2. **设** **G** **为** **n** **(** **n** **³** **3)** **阶无向简单图，若对于** **G** **中任意两个**
>
>   **不相邻的顶点** **v** **i** **,** **v** **j** **，均有**
>
>   ​              **d** **(** **v** **i** **) +** **d** **(** **v** **j** **)** **≥** **n**         **——** **①** 
>
>   **则** **G** **中存在哈密顿回路，从而** **G** **为** **哈密顿图** **.**
>
>3. 以上注意都为充分条件，是哈密顿图的就不一定符合

#### c、偶图

> 怎么说了咧，他经常分为两个V ，以为一个对应一边嘛
>
> **V** **1** **和** **V** **2** **称为** **互补结点子集** **，偶图通常记为** **G = <V** **1** **,E,V** **2** **>** **。**
>
> 偶图是没有自回路的// 无闭环的意思

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622153939610.png" alt="image-20200622153939610" style="zoom:33%;" />

**无向图** **G = <V, E>** **为偶图的充分必要条件是** **G** **中所有回路的长度均为** **偶数** **。**

记住是所有回路哈，所以相当于有连通分支中的回路

##### 匹配

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622155710446.png" alt="image-20200622155710446" style="zoom: 50%;" />

就单射把

> 存在匹配的充要条件是霍尔定理
>
> **偶图** **G = <V** **1** **, E, V** **2** **>** **中存在从** **V** **1** **到** **V** **2** **的匹配的充分必要条件是** **V** **1** **中任意** **k** **个结点至少与** **V** **2** **中的** **k** **个结点相邻** **，** **k = 1, 2,** **…** **, |V** **1** **|** **。**就每个都试一遍？
>
>   **定理** **11.4.2** **中的条件通常称为** **相异性条件** **(Diversity Condition)** **。**
>
> <img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622160429978.png" alt="image-20200622160429978" style="zoom: 33%;" />



#### d.平面图

**如果** **能** **把一个无向图** **G** **的所有结点和边** **画在平面上** **，使得** **任何两边除公共结点外没有其他交叉点** ** **，则称** **G**  **为** **平面图** **(Plane Graph)** **，否则称** **G** **为*** **非平面图** **(Nonplanar Graph)** **。**

> 
>
> 1. **当且仅当一个图的每个连通分支都是平面图时，这个图是平面图。**
>
> <img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622161526348.png" alt="image-20200622161526348" style="zoom: 33%;" />
>
> 2. **平面图中所有面的次数之和等于边数的二倍。**  
>
> 3. **设G = <V, E>是连通平面图，若它有n个结点、m条边和r个面，则有**
>
> **n-m+r = 2**
>
> 4. **设G是一个(n,m)简单连通平面图，若m＞1，则有**
>
>    **m≤3n-6**
>
> 5. **一个简单连通图，若不满足m≤3n-6，则一定是非平面图。**
>
> 6. **定理11.5.3(库拉托夫斯基定理) 一个图是平面图的充分必要条件是它的任何子图都不可能收缩为K5或K3,3。**
>
>    **推论11.5.3 一个图是非平面图的充分必要条件是它存在一个能收缩为K5或K3,3的子图。**
>
>    <img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622165100629.png" alt="image-20200622165100629" style="zoom: 33%;" />
>
>    为什么是K5？ 因为K5 本身就是会交叉的，K3,3 也是哈

## 3. 关系

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622172654134.png" alt="image-20200622172654134" style="zoom: 33%;" />

**注意。空集这五个性质都有哈，怕的就是漏掉，所以要五个五个来哈**

### (1). 自反关系,反自反关系

> R在A上是自反的Û("x)(x∈A→<x,x>∈R)=1
>
> R在A上是反自反的Û("x)(x∈A→<x,x> R)=1

> a)因为A任意x，都有<x,x>∈R，
>
> 所以R是自反的；
>
>    b）因为A中"x，都有<x,x>  S，
>
> ​    所以S是反自反的；

###      (2). 对称关系，反对称关系

> 1）R在A上是对称的Û对"x,y∈A，有：
>
> <x,y>∈R并且<y,x>∈R或<x,y> ∉R并且<y,x>∉ R。
>
> （2）R在A上是反对称的Û对"x,y∈A，如果x≠y，则<x,y> ∉R或<y,x> ∉R。
>
> （3）R在A上不是对称的Û$x,y∈A，有<x,y>∈R但<y,x>∉ R或者<x,y>∉ R但<y,x>∈R；
>
> （4）R在A上不是反对称的Û $x,y∈A，有<x,y>∈R且<y,x>∈R。

### (3). 传递关系

> ![image-20200622172636528](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622172636528.png)
>
> 1）对任意的x,y,z∈A，如果<x,y>∈R，<y,z>∈R且<x,z>∈R，则R在A上是传递的；
>
> （2）对任意的x,y,z∈A，如果<x,y> R或者<y,z> R，则R在A上是传递的
>
> （3）R在A上不是传递的当且仅当存在x,y,z∈A，有<x,y>∈R且<y,z>∈R，但<x,z> R。 

## 4. 关系的表示方式

### (1).图

> （**1）A≠B**
>
> **设A＝{a1,a2,...,an},B＝{b1,b2,...,bn}，R是**
>
> **从A到B的一个二元关系，则规定R的关系图如下：**
>
> 　**①.设a1,a2,...,an和b1,b2,...,bn分别为图中的结点，用“。”表示；**　
>
> **②.如<ai,bj>ÎR,则从ai到bj可用有向边ai。。bj相连。<ai,bj>为对应图中的有向边。**

### (2). 矩阵

§关系矩阵是0-1矩阵，称为布尔矩阵。可达矩阵也是布尔的把，目前先这样子哈

无语子，为什么我老是记不住呢。

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622175050164.png" alt="image-20200622175050164" style="zoom: 33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622175111396.png" alt="image-20200622175111396" style="zoom: 33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622175136529.png" alt="image-20200622175136529" style="zoom: 33%;" />

### (3). 复合运算

> 定义6.3.1 设A,B,C是三个集合，R是从A到B的关系
>
> (R:A→B)，S是从B到C的关系(S:B→C)，则R与S的复
>
> 合关系(合成关系)(Composite)RoS是从A到C的关
>
> 系，并且：
>
>    **RoS＝{<x,z>|x∈A∧z∈C∧**
>
>  **(存在y)(y∈B∧xRy∧ySz)}**
>
> 运算“o”称为复合运算(CompositeOperation)。

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622175947902.png" alt="image-20200622175947902" style="zoom: 33%;" />

前后关系很重要的，到后面多起来的话，就是要判断谁在前面谁在后面的 

> 设A、B、C和D是任意四个集合，R是从A到B的关系，S1，S2是从B到C的关系，T是从C到D的关系，则：
>
> 　1)、R o (S1∪S2) = (R o S1)∪(R o S2)
>
> 　2)、R o(S1∩S2) Í (R o S1)∩(R o S2)
>
> 　3)、(S1∪S2)oT = (S1 o T)∪(S2 o T)
>
> 　4)、(S1∩S2)o T 属于 (S1 o T)∩(S2 o T)

### (4).逆运算

就是直接颠倒ok

### (5). 幂运算

> 设R是集合A上的关系，则R的n次幂，记为Rn,定义如下：
>
> (1) R0＝IA＝{<a,a>|a∈A}；
>
> (2) R1＝Ｒ；
>
> (3) Rn+1＝RnoR＝RoRn。

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622180657718.png" alt="image-20200622180657718" style="zoom:50%;" />

## 5.闭包

### (1). 自反闭包 r(R)

r(R)＝R∪IA。

### (2). 对称闭包  s(R)

s(R)＝R∪R-1。

### (3). 传递闭包

这个就有点麻烦把，脑袋里一直出现关于距离的，这是在哪出现的呢？ 应该是在连通性那里出现的，

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622190223987.png" alt="image-20200622190223987" style="zoom:50%;" />

我好像为什么知道要这样做了，为什么我之前不思考呢？因为是你加上一个之后又发现有些传递不了，就一直乘乘乘，乘到最后传递为止

![image-20200622201447827](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622201447827.png)

最后你差不多相当于记住就可以了

这个是用序列进行表示的，还可以用矩阵进行表示

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622201710055.png" alt="image-20200622201710055" style="zoom: 33%;" />

然后呢？？不知道了，，好像是拿最后一个矩阵诶

## 6. 等价关系

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622203534637.png" alt="image-20200622203534637" style="zoom: 33%;" />

证明等价关系的示例哈，

划分呢，就你想想同个高中的例子就好了

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622204906451.png" alt="image-20200622204906451" style="zoom: 33%;" />

然后我遇到这个又懵逼了一会，谁是x谁是y呢，你想想，肯定同个高中的是xy啊，所以这就是等价类

### (1).等价类定义：[x]R＝{y|y∈A∧<x,y>∈R}

### (2). 商集

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622205057388.png" alt="image-20200622205057388" style="zoom: 33%;" />

就是这么表示的哈

## 7. 特殊关系

### (1). 拟序

> R是拟序关系 推出 R同时具有反自反性和传递性；

### (2).偏序

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622213604801.png" alt="image-20200622213604801" style="zoom: 33%;" />

注意要从下往上啊，因为推的时候就是这么推的

### (3).特殊元素

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622215031656.png" alt="image-20200622215031656" style="zoom: 33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622215228778.png" alt="image-20200622215228778" style="zoom: 33%;" />

所以上界和下届都是多个的ok 然后确界的话就是求临界值 把

## 8.函数(一种特殊的关系)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622220236170.png" alt="image-20200622220236170" style="zoom: 33%;" />

### 如何证明单射，满射，双射

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622220610062.png" alt="image-20200622220610062" style="zoom: 33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622220817600.png" alt="image-20200622220817600" style="zoom: 33%;" />

## 9.图

### (1). 邻接矩阵

之前有个关系矩阵把，那里的关系矩阵就是个布尔矩阵，但这里的话可达矩阵才是布尔矩阵把  

> 仅由孤立结点组成的图称为零图(Null Graph)；
>
> 仅含一个结点的零图称为平凡图

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622224815609.png" alt="image-20200622224815609" style="zoom:50%;" />

### (2). 怎么从有向矩阵中求回路

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622230621601.png" alt="image-20200622230621601" style="zoom: 33%;" />

这个有向和无向的差不多是一样的把，然后怎么求通路呢，你把全部值相加就ok了，怎么求回路呢，对角线相加没错的！

### (3). 用邻接矩阵判断是否可达

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622232404321.png" alt="image-20200622232404321" style="zoom: 33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622232524649.png" alt="image-20200622232524649" style="zoom:33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200622232626247.png" alt="image-20200622232626247" style="zoom: 33%;" />