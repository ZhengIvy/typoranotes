# 1、NoSQL 入门

![image-20210119122446978](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119122446978.png)

![image-20210119122600382](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119122600382.png)

读写分离，读是从库，写是主库

![image-20210119123240374](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119123240374.png)

![image-20210119152244232](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119152244232.png)

好久没有接触过这种图了，原来买东西和订单过后就是这样子的表哈，就分得很细，不过还是情有可源，这个customer to Address是一对多的关系哈

![image-20210119152655371](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119152655371.png)

![image-20210119152938794](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119152938794.png)

这个就是nosql的好处，如果你要搞成sql的话，你要先创个表，搞个数据，而这里的话nosql，json格式的数据搞定就可以了

![image-20210119153818153](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119153818153.png)

不像SQL的参数一样，SQL有varchar,int,date等等类型，这里的数据模型叫做聚合模型，KV键值，BSON，列族和图形四种，第一二种挺常见的把，列族的话就是把原本横着的表竖过来，然后字段就变为key和value两个 了，图形的话就是图吧，但我们还是接触前两个比较多点

![image-20210119155213260](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119155213260.png)

![image-20210119155443684](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119155443684.png)

## 2. CAP原理

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119200730576.png" alt="image-20210119200730576" style="zoom:67%;" />

![image-20210119200849895](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119200849895.png)

![image-20210119200928076](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119200928076.png)

这个nosql的CA的性质了

![image-20210119204429045](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119204429045.png)

怎么说呢，就真的不是很明白

![image-20210119205533742](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119205533742.png)

首先对NOSQL，最低的要求是P，分布式容忍性，允许错误的，但具体的用处我也不是很清楚把，

他讲完这个之后明白了一些，拿现在的双十一当做例子，高可用可以理解为网站不崩掉，强一致性就是你收藏点击能实时看到，没有延时。但是呢，对于双十一我们一般对强一致性没有太大的要求，主要是你的网站崩不崩，我能不能买上我要的东西而已，所以现在的大多数网站京东，淘宝等都要的是AP，而CP的话就用在当我们需要统计浏览数啥的时候咯，怎么说呢，感觉CP的还是没有那么好理解吧

怎么说呢，就是CP是对传统数据库的缓存，缓解了压力，用CP可以去实现AP？？？ 所以我目前的理解是CP和AP都用哈？感觉还是不够理解，后面查下还有没有别的方法去理解一下

![image-20210119211257043](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119211257043.png)

![image-20210119213151757](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119213151757.png)

一开始的标题就是BASE + CAP哈，这里讲的是BASE的解决方案，一般情况下是满足基本可用和软状态，但是要求最后是达到一致的，意思就是当我们双十一买东西的时候，虽然说浏览量啥的可以没有那么快实时统计出来，但是要求最后还是要一致性的，也就是该统计出来的就要统计出来的哈

## 分布和集群

![image-20210119214820453](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119214820453.png)

懂了，分布和集群的区别，分布就是分工合作，每人做不同的东西，集群就是人多力量大，每个人做相同的东西

# 2. redis 的四问

## 1. 是什么

![image-20210119220954997](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119220954997.png)

![image-20210119221054658](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119221054658.png)

这个master-slave的话就是主从关系，主的话就是写，从的话就是读？？

## 2. 干什么

![image-20210119220923087](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119220923087.png)

这几个定时器、计数器啥的目前还不知道哈

## 3. 事务更灵活？？？ 不是很懂哈

![image-20210120160903981](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210120160903981.png)



# 3. redis的知识讲解

## 1. redis启动后杂项基础知识讲解

![image-20210122094231754](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210122094231754.png)

启动后杂项基础知识讲解：默认16个数据库，默认端口6379，而且是单进程就对了，用epoll包装的

就注意这几个命令把，之前我还不知道这个的 `Dbsize,Flushdb,Flushall`一个是删除全部库，一个是清空当前库的，就尽量不要用这种东西吧



## 2. redis的数据类型

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210122110910041.png" alt="image-20210122110910041" style="zoom: 50%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210122111923560.png" alt="image-20210122111923560" style="zoom: 50%;" />

五个，就很基本的，String，Hash,List,Set,ZSet

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210122120556531.png" alt="image-20210122120556531" style="zoom:50%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210122120624656.png" alt="image-20210122120624656" style="zoom:67%;" />

![image-20210122120813857](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210122120813857.png)

![image-20210122120833308](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210122120833308.png)

![image-20210122120908320](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210122120908320.png)

感觉跟个排名的一样，就是你玩游戏差不多的时候就会有一个排名出来，前百分几百分之几的这种，分数是可以重复的但是成员是不行的，

### 1. key

![image-20210122123839189](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210122123839189.png)

这个也不难，不过感觉之前我学redis的时候没有用过的感觉哈，可以移除到别的库去，还可以expire key，哈可以看多少秒过期，还可以去查询你的key是什么类型的

### 2. string

#### （1）getrange setrange

![image-20210123103054256](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123103054256.png)

![image-20210123110648741](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123110648741.png)

对值是数字的进行incr和decr咯，这个默认为1的，你想多几个的话就可以用incrby这种的

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123110620546.png" alt="image-20210123110620546" style="zoom: 50%;" />

这个getrange是对值进行index，而且是左开右闭的关系，所以的话0 -1 表示的是整个显示，包括不属于数字的也显示出来，而让左边是0的情况就是把非数字的值也显示出来，然后

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123111359802.png" alt="image-20210123111359802" style="zoom:67%;" />

然后目前认为的是如果左边为0 的话那就会把非数字的也给显示了，但如果右边为-1的话那就什么都不知道了





而setrange其实就是覆盖把，从index开始覆盖就可以了



#### （2） setex setnx

setex(set with expire)键秒值，在设值的时候还可以设置过期的时间

setnx(set if not exist)这个的话感觉应该会蛮实用的，因为我们知道redis的赋值时覆盖的，这样你使用这个的话就不会覆盖了

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123112223255.png" alt="image-20210123112223255" style="zoom:67%;" />

#### （3） mset mget msetnx

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123112540601.png" alt="image-20210123112540601" style="zoom:67%;" />

这个m应该就是multiple的意思，所以是多次set，和多次get，比较方便哈

![image-20210123112616798](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123112616798.png)

msetnx的话就必须你的key都是一样的情况，不能一个存在一个不存在哈

### 3. list

![image-20210123124906770](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123124906770.png)

lindex很简单，就不演示了哈

#### （1） LPUSH RPUSH LRANGE

![image-20210123125536075](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123125536075.png)

这个已经不是key了，是list，所以的话你看list的内容得用range，而不是用get哈，而且这里的LPUSH 和 RPUSH有区别，你可以理解为LPUSH就是每次添加的时候往左边添加，所以是倒过来的顺序，RPUSH就是每次添加的时候往右边添加，是正过来的顺序，然后你要看里面的内容又什么的话，就得用lrange，从左边一个个看哈

#### （2）LPOP RPOP

![image-20210123130308440](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123130308440.png)

其实这个也不是很难，就是你看成往左边和往右边就可以了哈，所以LPOP list01就是把5搞出来，LPOP02就是把1搞出来，反正的话就是很简单的，懂得原理就行了

#### （3） LREM

![image-20210123131054908](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123131054908.png)

这个就是remove的意思，remove几个为x的值

#### （4）LTRIM

![image-20210123131649222](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123131649222.png)

这个的话就是截取一段之后重新赋值哈，是[a,b]这种情况的哈

#### （5）RPOPLPUSH

![image-20210123132034791](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123132034791.png)

有这种操作吼，不过的话就只操作一个呢，这样的话意思就是 `list01 RPOP list02 LPUSH`,那也非常easy了，把4拿到list02的最左边哈

#### （6）lset key index value

![image-20210123132236804](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123132236804.png)

作用的 话就是对list的某个index进行赋值哈

#### （7）	LINSERT key after /before 

#### ![image-20210123132400316](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123132400316.png) 

这个就是在之前插入和之后插入

#### 性能总结

![image-20210123132446232](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123132446232.png)

所以是一个链表

### 4. set

![image-20210123145010159](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123145010159.png)

这个就是不能重复的啦，然后的话就查询这个set有什么的时候就用的是smembers了，和查询该set中是否有这个元素的话就是ismember了，集合哈

#### （1）sadd 、smembers、sismember

![image-20210123145712377](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123145712377.png)

就这样吧，而且你硬是要搞一样的进去的话也不会报错，也只是去掉重复的而已

#### （2）scard（获取集合中元素的个数）、srem key value(删除集合中的某个元素)、srandmember key(随机出几个数)

list中也有一个length把

![image-20210123145914986](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123145914986.png)

![image-20210123150017799](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123150017799.png)

![image-20210123150158141](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123150158141.png)

就这样子哈，也very easy，这个的话感觉就可以用到抢红包啊之类的，就很快

#### （3）spop(随机出栈)、smove(把key1中的值move到key2中去)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123150426534.png" alt="image-20210123150426534" style="zoom:67%;" />

![image-20210123150630513](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123150630513.png)

#### （4）sdiff(差集)、sinter(交集)、sunion(并集)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123151036747.png" alt="image-20210123151036747" style="zoom:67%;" />

![image-20210123151052866](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123151052866.png)

### 5. hash

![image-20210123152431173](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123152431173.png)

hash就像是java中的一个javabean对象哈，虽然我对为什么hash可以这样操作有点懵，感觉之间少了点什么东西，但是大概明白了吧

#### （1）hset、hget、hmset、hmget、hgetall、hdel

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123154730561.png" alt="image-20210123154730561" style="zoom:67%;" />

你就可以set值，和get值，可以一次性set和get，也可以直接hgetall，del也很简单嘛

#### （2）hlen、hexists key 在key里面的某个值的key

![image-20210123155043057](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123155043057.png)

#### （3）hkeys、hvals

![image-20210123155426477](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123155426477.png)

就直接获取keys的值和val的值哈

#### （4）hincrby、hincrbyfloat

这个从字面意思也能理解的对吧

![image-20210123155621169](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123155621169.png)

![image-20210123155640868](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123155640868.png)

### 6. zset

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123160841733.png" alt="image-20210123160841733" style="zoom:67%;" />

#### （1）zadd、zrange(withscores)

![image-20210123161122116](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123161122116.png)

就是这个了吧，这个跟set的用法就不一样了哈，set之前是有member之类的，这里的话就很像range了，所以的话是zrange这种东西哈

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123162304080.png" alt="image-20210123162304080" style="zoom: 67%;" />

然后呢，这个range的话可以有多种截取操作吧，注意的是 `(`，他表示的意思是不包括等于的意思哈，所以加上这个符号就表示的是小于 or 大于哈，另外的limit limit的话就很像是分页罢了

#### （2）zrem key 

某 score下对应的value，作用是删除元素

![image-20210123185406695](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123185406695.png)

#### （3）zcard、zcount、zrank、zscore

![image-20210123191450193](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123191450193.png)

很明显哈，zcard是拿长度哈，zcount也可以是拿长度，但是可以看上下限，而zrank的话则是看排名，zscore的话就根据数值来看score

#### （4）zrevrank 逆序获得下标的值、zrevrange

![image-20210123191916142](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123191916142.png)

![image-20210123191958938](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123191958938.png)

这个是要反转的哈，毕竟这是个有序的集合，不反转的话不是浪费掉了吗

# 4. redis 配置文件

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123204354199.png" alt="image-20210123204354199" style="zoom:67%;" />

他这里说了一点是配置文件需要拷贝出来，一定要备份原件的，很多情况下都是对配置文件的修改

## 1. units单位

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123211654155.png" alt="image-20210123211654155" style="zoom:67%;" />

注意哈拉，大小写不敏感

## 2. includes

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123221924439.png" alt="image-20210123221924439" style="zoom:67%;" />

这个明白哈，spring搞配置文件的时候也是这样子的，作为总闸，包含其他

## 3. General

他这些东西都在视频讲了，很杂碎，所以的话不好搞记笔记，不过要知道一点的是

![image-20210123225954225](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123225954225.png)

印象比较深刻的是这一点，首先这两行可以启动redis，而且的话你在哪个文件夹下启动都是可以的，所以的话你的redis的日志都会不一样，意思就是你在redis上的操作记录得不一致，所以的话还是要专挑一个地方启动redis





<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210123230217205.png" alt="image-20210123230217205" style="zoom:67%;" />

这个是设置redis的密码的一项，因为你会发现诶，mysql要密码登录，怎么redis就不用呢，因为他就是这样子的

## 4. LIMITS（限制）

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124001745860.png" alt="image-20210124001745860" style="zoom:67%;" />

![image-20210124004002801](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124004002801.png)

maxclients的话就已经知道了咯，限制你的访问量？然后呢 maxmemory的话是依照一定的规则进行的，

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124094422770.png" alt="image-20210124094422770" style="zoom:67%;" />

lru：最近最少使用的算法，ttl： time to live

![image-20210124101242766](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124101242766.png)

![image-20210124101428767](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124101428767.png)

![image-20210124101446629](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124101446629.png)

## 5. 持久化

- rdb (redis database)
- aof (append only file)

持久化啥意思？我觉得是你redis保存到磁盘中的一种说法，而保存的方式是有不同的

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124105011805.png" alt="image-20210124105011805" style="zoom:67%;" />

### 1. rdb

#### 1.是什么？

![image-20210124105209493](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124105209493.png)

怎么理解？

就是隔断时间进行缓存，比如说5分钟进行一次的这种，这种就是快照？因为snapshot听起来像拍照一样，所以是快照文件？应该是这样子吧，那么他搞的时候就是单独创建一个子进程进行持久化的，将数据写入到一个临时文件中，待持久化进程都结束了，这个临时文件就会替换上次持久化好的文件。所以的话性能就比较高，感觉就是后台在备份而已，但是如果最后一次出了问题的话，那最后一次持久化后的数据可能丢失，懂把，总而言之，就是像拍照一样，隔几分钟备份一次。

这个主进程的事的话就有可能主进程在灌数据，但是你的子进程在备份

#### 2. fork

![image-20210124154202163](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124154202163.png)

fork，好像github里面也有一个fork，但是我没有学git，到时候学下把，这个像是备份把？数值和愿景城一致，是全新的进程，但是缺点就是万一数据量很大，你还要fork一份的话，那是会死的！

#### 3. 保存的文件

rdb保存的是dump.rdb文件

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124161609622.png" alt="image-20210124161609622" style="zoom:67%;" />

快照保存的规则！因为我们也没有手动保存啊，那他就是自动保存的，自动保存触发的条件又三个，就是中间的三个after

但是有一种情况是你比如马上清库，然后关机，不到1分钟，那你会不会更新缓存文件，这个答案是会的，因为触发`shutdown 和flushall`不管多快是会自动更新缓存文件的

不过这里之前就有一份备份的文件，所以的话你再把备份文件搞回来就可以了

![image-20210124165459453](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124165459453.png)

#### 4. snapshot快照

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124165827443.png" alt="image-20210124165827443" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124165925758.png" alt="image-20210124165925758" style="zoom:67%;" />

这个就是rdb怎么备份的

不过你也可以自己手动备份，你嫌慢还是怎么样的就可以自己手动备份

![image-20210124170140480](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124170140480.png)

save就可以

如何启动快照，就是这样子的

![image-20210124171205279](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124171205279.png)

一般备份机和操作机得是两台机器，不然的话你备份同一台机你备份好了也没得恢复



![image-20210124171439013](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124171439013.png)

原来save和bgsve两种，background save？我觉得bgsave一般用吧，不然的话就不好搞啊



![image-20210124171600287](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124171600287.png)

就是一般的启动目录吧

#### 5. stop-writes-on-bgsave-error

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124170329378.png" alt="image-20210124170329378" style="zoom:67%;" />

这个指令的意思是在你save出错的时候会停止写，就像一个游泳池，一个入水口一个出水口，当你出水口发现诶水不对啊，那你就会叫入水口别装水了 

#### 6. rdbcompression

![image-20210124170751499](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124170751499.png)

压缩成rdb文件把，否的话压缩成啥啊

#### 7. rdbchecksum

![image-20210124170948901](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124170948901.png)

他说这个没必要关掉，能用钱解决的事情哈

#### 8. 优势 劣势

![image-20210124171658840](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124171658840.png)

![image-20210124171711850](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124171711850.png)

![image-20210124171734118](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124171734118.png)

![image-20210124171758092](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124171758092.png)

### 2. aof

aof就是为了解决rdb的缺点，但老师说其实这个好像问题不大，这个缺点，不是很有必要的感觉，不过aof就是解决了这个问题，他的原理是你的写命令(比如select这种不会搞，只是写操作)全都复制备份一份，而rdb则是备份内容，而且基本上是每秒的程度，那这样的话是基本不会丢失内容的，但缺点就是很笨，而且量非常大，

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124201026280.png" alt="image-20210124201026280" style="zoom:67%;" />

![image-20210124202820614](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124202820614.png)

![image-20210124203343355](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124203343355.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124210853459.png" alt="image-20210124210853459" style="zoom:67%;" />

我可能现在明白了为什么启动的时候要搞配置文件了，就像是给你一个基本人物，你对他进行装扮，设置属性之类的，而你要使用aof的备份方式的话，那你就要修改一个append only 的属性改为yes，忘记是哪个了然后保存的文件后缀也变成了aof，不过有点奇怪的是dump.rdb还是有诶，可能是默认开启rdb模式，然后aof模式也是可以开着的

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124204516223.png" alt="image-20210124204516223" style="zoom:67%;" />

你看，就又有aof。又有rdb，不过有一个思路，你可以在appendonly.aof中修改，但一般人不这么做哈

![image-20210124205825020](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124205825020.png)

然后这里有一个思路，就是如果你突然关掉电源，或者有些故障，导致你的aof文件中有些奇怪识别不了的东西，那这样就会导致你的redis完全打不开，因为加载不了，就像你的spring，里面有的bean没有的话那也会报错，也因此的出来一个结论，rdb和aof先加载的文件是aof

![image-20210124210312762](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124210312762.png)

解决方案是可以用那种东西哈，check-aof,check-dump这些的

![image-20210124220100379](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124220100379.png)



![image-20210124234233994](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124234233994.png)

这个情况就是呢比如说你不断的incr,incr,一万次，但其实和直接incr 一万没区别，这种情况就是可以压缩的

![image-20210124234705653](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124234705653.png)

![image-20210124234854783](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124234854783.png)

#### 总结

![image-20210124235309087](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124235309087.png)

### 3. rdb 和 aof 的比较

![image-20210124235405146](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124235405146.png)

![image-20210124235538147](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210124235538147.png)

![image-20210125000007469](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210125000007469.png)

总的来说是两个都开把，而且最好不要只开aof，但是其实aof也有问题，太慢了，所以又出现了一种master-slave的，那还是可以的哈，解决了aof的问题，但应该是在后面学

# 5. 事务

## 1. 四问

### 1. 是什么

![image-20210125000504785](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210125000504785.png)

### 2. 能干嘛

![image-20210125000546150](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210125000546150.png)

### 3. 怎么玩

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210125000658163.png" alt="image-20210125000658163" style="zoom:50%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210125000918598.png" alt="image-20210125000918598" style="zoom:50%;" />

感觉这些锁都还没有接触到过啊，标记一个事务的开始？明白了，怎么说呢，你直接看英文的`MULTI`感觉更容易理解，就表示你要一次性搞多个sql

#### 1.正常事务

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210125222253129.png" alt="image-20210125222253129" style="zoom:67%;" />

这个是正常执行的情况，可以多条执行，`MULTI`就是开启事务的意思，然后`EXEC`直接执行就可以了

#### 2. 放弃事务

![image-20210125222522189](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210125222522189.png)

就是你写着写着就不想要了，放弃事务也是ok 的

#### 3. 全体连坐

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210125223243278.png" alt="image-20210125223243278" style="zoom:67%;" />

这个就是当有一个命令是出错的话，那你就算执行了也会被discard、掉

#### 4. 冤有头债有主

![image-20210126095010182](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126095010182.png)

意思就是你谁出错就找谁，其他的照样可以执行，因此可以得出一个结论redis是部分事务，并不是一有错就全部都不可以提交，但是和上面的全体连坐有什么区别呢，什么时候是全体连坐，什么时候是冤有头债有主呢？其实很好理解，就像是编译时异常和运行时异常一样，一个是在之前就让try-catch，而另外一个Integer/0这种是你运行之后才会 出现的异常，意思也就是你执行这个语句之后，会立马发现不对的，那就是连坐，而是执行之后才发现不对的，那就是单独惩罚你，这里的是因为k1不能++哈，是字母咧。

#### 5. watch监控

![image-20210126100018760](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126100018760.png)

他这里讲锁还蛮有意思的吼，首先是引入并发性和一致性的对立的问题，你想要追求高并发，那你的一致性就会弱些，只是会尽量地去模拟一致性，而你完全追求一致性，那你的并发性就会弱些，就像是上厕所，就是一致性的，那你当只有一个厕所的时候，哇，那你的并发性就非常差了

##### 1. 悲观锁

![image-20210126101326450](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126101326450.png)

悲观锁很形象，他很悲观地认为每次去拿数据的时候都会有别人去修改，因此每次拿数据的时候，就会上把锁，别人进不来，比如表锁，表锁的意思就是把整个表锁了，这个一听起来就感觉非常地不好，而行锁呢，就是把他正在操作的某行给锁了，这行只能他来操作，这样的话听起来会比较好一些，就像是你上厕所前会先关门，关门之后再去上厕所。

虽然说不怎么样，但并不意味着不用他，比如说备份的时候就可以用，把表都给锁了，没有人可以动，这种适合夜深人静的时候干活

##### 2. 乐观锁

![image-20210126102015016](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126102015016.png)

乐观锁，但这样的话感觉还是有点不安全？？？当只读的时候？万一你改了呢？

简而言之，每次去拿数据的时候都觉得别人不会修改，因此就不会上锁，但是在更新的时候会判断别人有没有更新数据，

其实也就是，在表的最后一行加一个version表示版本号，你改完之后的版本号为+1之类的嘛，但是在这之前会判断你改后的版本是否大于当前的版本，意思就是在你改的时候是不是别人已经改好提交了，如果是这种情况的话，那么他就会让你重来改，也就是拿别人改好的数据进行相应的修改，这种情况波及他人较小，还是挺不错的。

##### 3. watch 监控

感觉懂了又感觉有些奇怪，大概懂什么意思，但是不清楚why？为何要这样子进行操作

![image-20210126105502795](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126105502795.png)

首先是这种，

![image-20210126110322635](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126110322635.png)

无加塞的篡改，就单纯是watch balance而已，也就这样了

但有的情况是

![image-20210126110504740](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126110504740.png)

![image-20210126110515885](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126110515885.png)

有两个终端，在他`EXEC`之前，改掉balance的值，然后``EXEC`会发现啥也没有执行，这个就有点像乐观锁的把，提交完之后诶，已经被改过了，因此你要在改过的数据上进行修改，但我总觉得没有完全懂，不过他也会说后面会细讲 的。

所以的话这应该是乐观锁的操作了

##### 4. unwatch

![image-20210126112854221](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126112854221.png)

诶怎么说呢，这个应该是在模拟一种情况，当别人有在动数据的时候，这个`set balance 500`就动了数据，那你就不能开启事务啊！所以你就`UNWATCH`，重新来，那你的`WATCH`到底啥子用哦，

![image-20210126113715537](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126113715537.png)

好像现在又懂了一些东西，watch监控的话首先是一个锁，可以保证你watch之后，在事务执行之前的改动会被感知到，这时候就已经预判到结果了，然后执行失败，你就又得重新来，那unwatch针对的是自己改的情况，就像是你在排队买东西，unwatch就会告诉你售空了走人把，而不是排到你的时候才说售空了。懂了！

##### 5. 总结

![image-20210126114012566](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126114012566.png)

![image-20210126114039874](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126114039874.png)

![image-20210126114101379](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126114101379.png)

# 6.  发布订阅机制

了解一下，redis有这个功能，但我们一般都不会用redis去做这个活

![image-20210126115111637](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126115111637.png)

![image-20210126115619965](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126115619965.png)

# 7. 主从复制

![image-20210126135431277](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126135431277.png)

## 1. 是什么？

![image-20210126135759892](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126135759892.png)

## 2. 能干嘛

![image-20210126135831701](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126135831701.png)

## 3. 怎么玩

这个就相当于本来大家都是平等的，然后呢，主就不变，但是从要往后退一步，所以这个就是配从不配主

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126140059142.png)

![image-20210126140113535](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126140113535.png)

![image-20210126143617526](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126143617526.png)

的确是首先配置文件，按照上面的第三点来看，拷贝多个redis.conf,pid文件名字改下，端口也改了，一共有三个端口，分别是`6379,6380,6381`哈，第三点的都改了。

接着便是用各自的配置文件运行redis，同时用各自设置的端口号打开

不过在这之前要声明一个`info replication?`，没错哈

![image-20210126145849650](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126145849650.png)

这个代表的是让6380和6381的端口去跟着6379的端口，在SLAVEOF 那里进行声明，而且他是先开始设了k1,k2,k3的三个值这之后再进行的，这之后再k4，已经进行备份了，那在之前的k1,k2,k3呢？答案也是可以的，不可以的话多不行啊

### 1. 从机想写会发生什么？

![image-20210126150609091](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126150609091.png)

没错，老师说了我们在学习过程中就是要不断地搞破坏，不然那么顺利地学下去没有用的哈！

所以这里实验了一下子，之前不是说主机写，从机读吗? 那我在这里试试让从机写你说会怎么样？没错，报错了！

### 2. 主机SHUTDOWN之后，从机会篡位还是原地待命？

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126151644103.png" alt="image-20210126151644103" style="zoom:67%;" />

原地待命哈，然后回来之后还是照样可以备份，相当于出差一样，变化并不大

### 3. 从机SHUTDOWN之后，还能跟个没事人 一样嘛？

![image-20210126152152216](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126152152216.png)

答案 是不能，回来就变master了，所以你要重新slave才行哈

## 4.薪火相传

![image-20210126155159421](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126155159421.png)

前面有讲到一主二仆，其实也可以一主多仆把，但这样的话这个主就会非常累，像讲课一样，一个老师对多个学生讲课，其实也不是不行，不过有另外一种方法是老师给一个人讲，这个人给下一个人讲这样子，但这种方法有些缺点，会造成失真，每个人漏点东西，对于redis 的话就是延时，传到最后一个人就会慢

![image-20210126160432949](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126160432949.png)

但是不知道怎么操作吼，并不，只是我想复杂了，他的结果和一主二仆没区别，但现在还看不出来哪个好哪个坏，也就这样吧。

具体怎么薪火相传呢，也就是你SLAVE OF的时候指定6380就好啦，6379<-6380<-6381这样子。

## 5. 反客为主

从字面意思上理解就是slave翻身当master了。

![image-20210126163828233](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126163828233.png)

然后完全是打乱了秩序把，那也很简单理解啦，也没啥把，然后原来的master回来之后也只是新的领导，没啥关联了

## 6. 复制原理

![image-20210126164100914](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126164100914.png)

噢，原来是分为两种复制啊，第一次的时候是全量复制，就一次性把数据全拿过来嘛，后面的话就是给点你就复制点

## 7. 哨兵模式

![image-20210126165924251](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126165924251.png)

毕竟老大阵亡的时候，总得有人接班把，自动点好不好啊

![image-20210126170327181](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126170327181.png)

操，我好累啊

![image-20210126170955208](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126170955208.png)

![image-20210126171013568](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126171013568.png)

ok，明白了回答几个问题

1. 启动哨兵

   ![image-20210126175739666](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210126175739666.png)

2. 一开始就是正常的主从关系

3. 当你原有的master挂了，哨兵立刻监视到，然后进行选举，还是要花个几十秒的时间的，选好之后，他就成功当上master，原来的slave也转了

4. 那问你原来的master重新回来开工会怎么样？sorry，变成slave了，slaveto现在的master，跟手动挡的主从关系不是很一样哈。