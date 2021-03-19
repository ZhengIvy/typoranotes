## 1.可以用view给别人看，增加安全性

## 2.Integrity

1. Entity integrity  每行
2. Referential integrity 表要进行参考
3. Domain integrity  定义域把



## 3. atomic value

像name 要分成first name last name

## 4. 两种外键

post版下



## 5. 一对一

![IMG_4672](D:\tim\1097641461\FileRecv\MobileFile\IMG_4672.PNG)直接 外键就可以了，两个表就可以了，

![IMG_4670](D:\tim\1097641461\FileRecv\MobileFile\IMG_4670.PNG)

![IMG_4669](D:\tim\1097641461\FileRecv\MobileFile\IMG_4669.PNG)

![IMG_4668](D:\tim\1097641461\FileRecv\MobileFile\IMG_4668.PNG)

![IMG_4665](D:\tim\1097641461\FileRecv\MobileFile\IMG_4665.PNG)

![IMG_4664](D:\tim\1097641461\FileRecv\MobileFile\IMG_4664.PNG)

![IMG_4663](D:\tim\1097641461\FileRecv\MobileFile\IMG_4663.PNG)

![IMG_4662](D:\tim\1097641461\FileRecv\MobileFile\IMG_4662.PNG)

![IMG_4661](D:\tim\1097641461\FileRecv\MobileFile\IMG_4661.PNG)

![IMG_4659](D:\tim\1097641461\FileRecv\MobileFile\IMG_4659.PNG)

![IMG_4658](D:\tim\1097641461\FileRecv\MobileFile\IMG_4658.PNG)

![IMG_4657](D:\tim\1097641461\FileRecv\MobileFile\IMG_4657.PNG)

![IMG_4656](D:\tim\1097641461\FileRecv\MobileFile\IMG_4656.PNG)

![IMG_4654](D:\tim\1097641461\FileRecv\MobileFile\IMG_4654.PNG)

![IMG_4653](D:\tim\1097641461\FileRecv\MobileFile\IMG_4653.PNG)

![IMG_4652](D:\tim\1097641461\FileRecv\MobileFile\IMG_4652.PNG)

![IMG_4651](D:\tim\1097641461\FileRecv\MobileFile\IMG_4651.PNG)

![IMG_4650](D:\tim\1097641461\FileRecv\MobileFile\IMG_4650.PNG)

![IMG_4649](D:\tim\1097641461\FileRecv\MobileFile\IMG_4649.PNG)

![IMG_4648](D:\tim\1097641461\FileRecv\MobileFile\IMG_4648.PNG)

![IMG_4647](D:\tim\1097641461\FileRecv\MobileFile\IMG_4647.PNG)

















## 6.一对多

parent and child class 

就是多个外键就ok了

![image-20200427012154348](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200427012154348.png)

![image-20200427012247854](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200427012247854.png)

## 7. 多对多

需要中间表，联合外键作主键

![image-20200502224707073](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200502224707073.png)

## 8.super key and candidate key

![image-20200427012313048](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200427012313048.png)



![image-20200427012323156](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200427012323156.png)个人好像觉得这个super key 没啥用吼，这些key都不是在db中存在的，都是你在设计表的时候用到的

super key 的话就觉得make entity unique

candidate key 就是作为候选的pk

好像有个alternative key 应该是candidate没选上当alternative把

## 9. surrogate key and natrue key

![image-20200427012340303](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200427012340303.png)

这是主键的两种类型，一种是虚拟的，私人的就像user_id 一样，可以将多表联合起来，方便

natrue key 是现实中存在的，比如微信号啥的，然后呢不过我不知道这两者在用的区别在哪里哈



## 10. look up table

实际上就是之前有了解到过的bronze gold silver 用id 表示因为好修改方便修改，再用个外键连接上就可以了哈，

## 11. not null foreign key

还是要看情况的，比如你一个教室预约嘛假设是一对多的关系，class的预约状态可以是没有instructor老师的，因为这里的fk对应的是teacher id 所以呢这里就不好用not null key

如果是多对多的话就应该用到了哈

## 12.fk  constraint

首先是

onupdate ondelete 这是用来

还有别的东西哈

restrict的话就是不能删，主键那里不能删，应该也不能update

cascade就是同步把，

set null就是delete后set 对应的为null，

就这几种功能，也是算简单 的把，明天早点起把，把database给建了

![image-20200427012403584](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200427012403584.png)

![image-20200427012412322](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200427012412322.png)

![image-20200427012420062](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200427012420062.png)



## 13. composite key

![image-20200427012446124](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200427012446124.png)



![image-20200427012427788](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200427012427788.png)一般是natrue key噢

simple key是 一个column，难道大家都是simple key 都是一个基础？大家都是simple key把 我猜 就是有refer的，单纯只是一个值的就是不是啥key

composite compound 是两个column哈![image-20200426230238056](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200426230238056.png)

我好像明白了一个包括simple key 一个不包括 simple key 的

不过好像哪里都没看过alternative key 有 就是备选的，是我之前理解的那个样子

## 14. pk

![image-20200427012227741](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200427012227741.png)