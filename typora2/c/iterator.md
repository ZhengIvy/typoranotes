### 迭代器

之前一直没有仔细去了解这个，就过了，真的很无语哈。



![image-20200325140106473](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325140106473.png)

![image-20200325140111259](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325140111259.png)

![image-20200325140115933](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325140115933.png)

![image-20200325140121511](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325140121511.png)

![image-20200325140129838](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325140129838.png)

![image-20200325140135225](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325140135225.png)

![image-20200325140141654](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325140141654.png)

![image-20200325140145851](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325140145851.png)

他实际上是一个接口，然后list里面是有一个iterator 的方法的，这个方法的类型是一个接口？？没尝试过说实话。接口里面有接口？

先不管了，这个的用处就是用来遍历的。然后基本上最好的方法是

```java
while(it.hasNext()){
	System.out.println(it.next());
}
```

然后你也可以不创一个iterator 直接list.iterator().next() 也可以，但是你每次这样的话就表示相当创建一个新的monster，因为 你的iterator 的方法是return an array 每次都会return an array 就会产生很多array来

你一般list输出也可以不用迭代器，但是get 的话就太慢了不行。

你的迭代器可以不用，变成enhanced for loop is ok

but 先在遇到了一个问题  concurrent modification exception 这是啥？