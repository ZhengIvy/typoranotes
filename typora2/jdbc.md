### 1.batch process

1. not allow select 
2. group of queries
3. reduce time
4. ddl dml dql

![image-20200328203033786](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200328203033786.png)

![image-20200328203038594](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200328203038594.png)

![image-20200328203049670](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200328203049670.png)

他说这个Statement 是一个object 但我实际上不是很了解到底是什么东西额，然后拿个PS 拿到那里是干嘛 用到呵，目前不知道

反正这个是成批的操作，如果你个个send 的话需要很多时间，这个直接放到一个object 里面进行send 就可以了，然后是以方法进行的，，然后就可以进行执行，执行后直接进行返回一个数组，这时候你就拿到了数据

注意执行后的数据是FIFO ，而且是一条一条来的，不然的话不能发现那里又错误这样子，

然后哦你可以选择清除batch 这个object

### ? . 与java 的连接



![image-20200326202056138](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200326202056138.png)

可以分为DDL , DML, DQL

然后不是很明白的是关于字符的拼接，为什么里面还要再打个引号？？？



等会再来更新个不同的东西，因为这三种对应的功能时不同的





```java
public class Main {
    public static void main(String[] args) throws ClassNotFoundException{

        Class.forName("Javalearning.Pqr");


    }
}
    class Pqr{
        static{
            System.out.println("In static");
        }
        {
            System.out.println("in instance");
        }
    }
```

这节是在讲`forName` 是干嘛的，就一个loader，如果你不想instantiate 也没关系



```java
public class Main {
    public static void main(String[] args) throws ClassNotFoundException, IllegalAccessException, InstantiationException {

        Class.forName("Javalearning.Pqr").newInstance();
    }
}
    class Pqr{
        static{
            System.out.println("In static");//In static
        }
        {
            System.out.println("in instance");//in instance
        }
    }
```

你用 这个newInstance 就相当于实例化了

![image-20200326221812036](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200326221812036.png)

![image-20200327211607189](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200327211607189.png)

![image-20200329081911506](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200329081911506.png)

![image-20200329081917494](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200329081917494.png)

![image-20200329081922069](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200329081922069.png)



### 3. preparedstatement

你觉得preparedstatement 是什么呢

应该是statement 中的一环，的一子接口，然后 那你要怎么把东西给他呢，用的是 connection中的东西，

不过ps 是动态的存放，

可以有三种execute  ps 和 s 存放query 的地方不同，前者在statement 就发了，后者在execute 哪里才放的

(boolean)execute ：  所有都可以，但是return true iff 放进去的是 select ， 其他都会return false

(ResultSet)executeQuery ：返回的是结果，只接受 select

(int)executeUpdate  ：这个用途比较多了 dml 那些的，但是呢，就select 也可以用

ps 和 s 中都有，那区别是什么呢，害，等会反正 ps 会快点，不知道为啥，

s中的不用

里面的quotation mark  在后面可以进行set (第几个问号，值) 就是binding了

前面进行ps 的时候就已经把相应的文字语言translate 好交给pst了，再让pst执行就ok

![image-20200329102555501](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200329102555501.png)

![image-20200329102601479](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200329102601479.png)

![image-20200329102608067](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200329102608067.png)