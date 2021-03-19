![image-20200325004746597](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325004746597.png)

![image-20200325004753069](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325004753069.png)

![image-20200325004757938](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325004757938.png)

![image-20200325004802145](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325004802145.png)

![image-20200325004816523](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325004816523.png)

![image-20200325004822249](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325004822249.png)

![image-20200325004827357](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325004827357.png)

![image-20200325004831811](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325004831811.png)

![image-20200325004839276](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325004839276.png)

![image-20200325004845448](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325004845448.png)

![image-20200325004852873](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325004852873.png)

![image-20200325004859861](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325004859861.png)

![image-20200325004912374](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325004912374.png)

所以到底HashMap 实现的原理是什么

首先(1)hashcode

hash code 实际上是一个证明，每个object都有一个hashcode，是的，但是我们这里只需要key的hash就可以了。hashcode 实际上由hashing 搞的，key 反正可已转化为一个数字，用这个数字去对16取模之后获得的数字是hashcode，这个hashcode实际上是map中对应的一个object的hashcode， 他的hashcode 是这样的来的，其他的不知道怎么的来的。不过可能也差不多。

(2)这就证明了hashmap 可以有空值作为key

然后把整个entry 变为一个linked list 放到数组中去，链表中有hashing，key,value,next node

为什么 是链表呢，因为取模的话会有对象有相同的hashcode(解释原因了哈)，那怎么存放呢，那就用链表指向下一个有相同hashcode 的entry

然后有相同hashcode 的组成了一个bucket。 

（3）hashcode相同怎么找，用value 去比对

(4)那如果一个bucket中太多了怎么办，超过8个以上就要用，红黑树了，但是我现在还不知道红黑树怎么用的哈，反正情况就是这样

over