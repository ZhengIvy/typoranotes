# 1. 什么是juc

**业务：普通的线程代码 Thread**

`Runnable`:没有返回值、效率相比Callable相对较低

# 2. 线程和进程

进程：是一个程序，QQ.exe Music.exe 程序的集合，一个进程可以包含多个线程，至少包含一个！

java默认有几个线程？ 2个 main，GC(主线程和垃圾回收机制)

线程：开了一个进程Typora,写字，自动保存(线程负责的)

**java真的可以开启线程吗** 开不了

```java
    public synchronized void start() {
        /**
         * This method is not invoked for the main method thread or "system"
         * group threads created/set up by the VM. Any new functionality added
         * to this method in the future may have to also be added to the VM.
         *
         * A zero status value corresponds to state "NEW".
         */
        if (threadStatus != 0)
            throw new IllegalThreadStateException();

        /* Notify the group that this thread is about to be started
         * so that it can be added to the group's list of threads
         * and the group's unstarted count can be decremented. */
        group.add(this);

        boolean started = false;
        try {
            start0();
            started = true;
        } finally {
            try {
                if (!started) {
                    group.threadStartFailed(this);
                }
            } catch (Throwable ignore) {
                /* do nothing. If start0 threw a Throwable then
                  it will be passed up the call stack */
            }
        }
    }
//本地方法、底层的c++，Java无法直接操作硬件
    private native void start0();
```

为什么说开不了呢，因为java可以开启线程的方式是`Thread,Runnable,Callable`这些，但是这些的内部调用是用一个本地的`start0()`方法，是底层的c++方法，怎么说呢，通过别人之手去开启线程，行吧，不是自己搞的，但感觉说是自己搞的也没错啊





并行编程：并发、并行

并发编程: 并发、并行

并发(多线程操作同一资源) `Concurrent`:所以是共同发生，但是是假的 "并行"

- CPU一核，模拟出来的多条线程

- 我理解的就是一个服务员处理多个业务，看起来是同时的，只不过是一个处理一下，另外一个处理一下， 处理地比较快罢了，这里的一个服务员就是一个CPU，多个业务就是多个线程

- CPU多核，多个线程同时处理，线程池

- ```java
  public class test {
      public static void main(String[] args) {
          //获取cpu的核数
          //CPU密集型、IO密集型
          System.out.println(Runtime.getRuntime().availableProcessors());
      }
  }
  ```

  这个nb，之前不知道的	

- 并发编程的本质：充分利用CPU的资源

并行(多个人一起行走) : `parallel` 真的共同发生，互不相关的那种



## 线程有几个状态？

```java
public enum State {
        /**
         * 新生
         */
        NEW,

        /**
         * 可执行状态
         */
        RUNNABLE,

        /**
         *阻塞
         */
        BLOCKED,

        /**
         *等待，死死地等	
         */
        WAITING,

        /**
         * Thread state for a waiting thread with a specified waiting time.
         * A thread is in the timed waiting state due to calling one of
         * the following methods with a specified positive waiting time:
         * 超时等待，就是等一定的时间，没来我就跑了
         */
        TIMED_WAITING,

        /**
         * Thread state for a terminated thread.
         * The thread has completed execution.
         *终止
         */
        TERMINATED;
    }

下面将对每种状态进行详细解析:

1.新建(new):线程刚被创建，但是并未启动。还没调用start方法。
2.锁阻塞(Blocked):当一个线程试图获取一个对象锁，而该对象锁被其他的线程持有，则该线程进入Blocked状态；当该线程持有	锁	时，该线程将变成Runnable状态。
3.可运行(Runnable):线程可以在java虚拟机中运行的状态，可能正在运行自己代码，也可能没有，这取决于操 作系统处理器。
4.计时等待(Timed Waiting):同waiting状态，有几个方法有超时参数，调用他们将进入Timed Waiting状态。这一状态 将一直保持	到超时期满或者接收到唤醒通知。带有超时参数的常用方法有Thread.sleep 、 Object.wait。
5.无限等待(Waiting):一个线程在等待另一个线程执行一个(唤醒)动作时，该线程进入Waiting状态。进入这个 状态后是不能自动唤	醒的，必须等待另一个线程调用notify或者notifyAll方法才能够唤醒。
6.被终止(Teminated):因为run方法正常退出而死亡，或者因为没有捕获的异常终止了run方法而死亡。
————————————————
原文链接：https://blog.csdn.net/weixin_39517902/article/details/111579316
```

## wait/sleep区别

1. 来自不同的类 wait->Object sleep->Thread,但是我们企业一般不用sleep，而是用

   `TimeUnit.DAYS.sleep(1);` `TimeUnit.SECONDS.sleep(2);`

2. 关于锁的释放，wait会释放锁，sleep不会释放锁

3. 使用的范围不同 sleep只能在任何地方睡，wait必须在同步代码块中

4. 是否需要捕获异常 wait和 sleep必须要捕获异常

# 3. Lock锁

传统Synchronized

```java
/**
 * 真正的多线程开发，公司中的开发,降低耦合性
 * 线程就是一个单独的资源类，没有任何附属的操作
 * 1. 属性、方法
 */
public class SaleTicketDemo1 {
    public static void main(String[] args) {
        //并发：多线程操作同一资源类,把资源类丢入线程
        Ticket ticket = new Ticket();

        //@FunctionalInterface 函数式接口，jdk1.8 Lambda表达式()->{}
        //替换的是new Runnable(),可以这样替换的原因是他知道你这个是Runnable，所以的话可以直接这样子写哈
        //这里的写法跟以前学的写法不一样，思考一下，之前都是直接Runnable的，耦合性不好，不是把资源类当做一个OOP
        //想想用Thread直接不好用，会占掉一个父类名额，但是用Runnable也不好用
        new Thread(()->{
            for(int i = 1; i < 40; i++) {
                ticket.sale();
            }
        }, "A").start();
        new Thread(()->{
            for(int i = 1; i < 40; i++) {
                ticket.sale();
            }
        }, "B").start();
        new Thread(()->{
            for(int i = 1; i < 40; i++) {
                ticket.sale();
            }
        }, "C").start();

    }
}
//资源类
class Ticket{
    //属性、方法
    private int number = 30;

    //卖票的方式
    public void sale(){
        if(number > 0){
            System.out.println(Thread.currentThread().getName()+"卖出了"+(number--)+"张票");
        }
    }
}
```

Lock接口

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210311002055.png" alt="image-20210311002055125" style="zoom:67%;" />

两个实现方法

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210311002112.png" alt="image-20210311002112454" style="zoom:67%;" />

三个实现类



## 公平锁

<img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210311002134.png" alt="image-20210311002133971" style="zoom:67%;" />

公平锁：十分公平，可以先来后到，怎么个公平法，是按排队的顺序执行的，而非公平的话是每执行一个人之后就重新进行抢占位置

非公平锁：十分不公平，可以插队(默认)

## synchronized 和 Lock锁的区别

1. synchronized 内置的java关键字，Lock锁是一个java类

2. synchronized无法判断获取锁的状态，Lock可以判断是否获取到了锁

3. synchronized可以自动释放锁，lock必须要手动释放锁，如果不释放锁，就会造成死锁

4. synchronized 线程1(获得锁，阻塞)、线程2(等待、傻傻地等)；Lock锁不一定会等(trylock()方法，但是我觉得讲的不够细致)

   <img src="https://raw.githubusercontent.com/ZhengIvy/Figurebed/main/img/20210311002145.png" alt="image-20210311002145234" style="zoom:67%;" />

   看这里哈，大概明白啥意思了，就是你的线程尝试去获取锁，这种情况感觉就适用于多种情况选择的时候，等个固定时间后等不到就做别的去了，不用死磕着

5. synchronized 可重入锁，不可以中断的，非公平的；Lock,可重入锁，可以判断锁，非公平(可以自己设置)

6. synchronized 适合锁少量的代码同步问题，Lock锁适合锁大量的代码问题

锁是什么？如何判断锁的是谁？ 怎么说呢我有一点想法，就是一把钥匙，一次只能进去一个人，那么就要设置一个共同的锁，共同的一把钥匙，否则有好几把钥匙进得去那就没意义了，因此这样的话就相当于一个类

# --------anki 2021.3.11--------------------------------

# 4. 生产者和消费者问题

## 1. synchronized版   wait  notify

出现了一个问题，当不只A,B线程来操作的时候会出现什么样的状况？ 虚假唤醒

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210206153604088.png)

把if改成while

```java
package pc;


/**
 * 线程之间的通信问题：生产者和消费者问题 等待唤醒，通知唤醒
 * 线程交替执行 A B 操作同一个变量  num = 0
 * A num+1
 * B num-1
 * 有点久时间没有写久又有点陌生了hh
 */
public class test1 {
    public static void main(String[] args) {
        Data data = new Data();
        new Thread(()->{
            for (int i = 0; i < 30; i++){
                try{
                    data.increment();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "A").start();
        new Thread(()->{
            for (int i = 0; i < 30; i++){
                try{
                    data.decrement();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "B").start();
        //会出现虚假唤醒的情况，想想为什么，而且是if造成的
        //我懂了哈！没有搞清楚一次只能一个线程去搞一个锁，所以理解出现了偏差
        new Thread(()->{
            for (int i = 0; i < 30; i++){
                try{
                    data.increment();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "C").start();
        new Thread(()->{
            for (int i = 0; i < 30; i++){
                try{
                    data.decrement();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "D").start();
    }
}

//等待，业务，通知
class Data{//数字，资源类
    private int number = 0;

    //+1
    public synchronized void increment() throws InterruptedException {
        while(number != 0){
            //通知
            this.wait();

        }
        number++;
        System.out.println(Thread.currentThread().getName()+"=>"+number);
        //通知其他线程，我+1完毕了
        this.notifyAll();
    }

    //-1
    public synchronized  void decrement() throws InterruptedException {
        while(number == 0){
            //等待
            this.wait();
        }
        number--;
        System.out.println(Thread.currentThread().getName()+"=>"+number);
        //通知其他线程，我-1完毕了
        this.notifyAll();
    }
}
```

这里有几个值得思考的问题

1. 虚假唤醒是什么原因造成的？是一个怎么样的过程

   因为if，首先假设A,B是加法线程，A先抢到后，进行++，接下来到B，因为！=0，只能锁上，然后A再抢一次，也wait了，接下来就是减法线程来抢了，减完变成0之后，B++，A++，变成了2，然后再减一下变成了1，接着又是这个过程，然后就变成了3，总而言之就是 +1 - 1 +2 -1 +2的情况

2. 为什么改成while之后就没有问题了？

   因为while的情况下，你的另外一个线程不会被虚假唤醒，比如A->B->A->C->D->A->B的这些情况，

   num = 1-> B wait->A wait->num = 0 notifyAll,A,B都被唤醒了，但是下一步的执行必须要拿到锁才可以->A拿到锁，num = 1->C和D拿到锁，被锁住，基本就是这些状态的循环，但是你主要要知道的是 **wait被唤醒之后需要重新拿到锁才能执行下一步！**





## 2. juc版的生产者和消费者问题

![image-20210206164356787](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210206164356787.png)

就像lock代替了synchronized一样，wait和notify也会被替换变成Condition监视对象

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210206164515899.png" alt="image-20210206164515899" style="zoom:67%;" />

![image-20210206164555163](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210206164555163.png)

```java
package pc;

import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class test2 {
    public static void main(String[] args) {
        Data2 data = new Data2();
        new Thread(()->{
            for (int i = 0; i < 30; i++){
                try{
                    data.increment();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "A").start();
        new Thread(()->{
            for (int i = 0; i < 30; i++){
                try{
                    data.decrement();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "B").start();
        //会出现虚假唤醒的情况，想想为什么，而且是if造成的
        //我懂了哈！没有搞清楚一次只能一个线程去搞一个锁，所以理解出现了偏差
        new Thread(()->{
            for (int i = 0; i < 30; i++){
                try{
                    data.increment();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "C").start();
        new Thread(()->{
            for (int i = 0; i < 30; i++){
                try{
                    data.decrement();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "D").start();
    }
}
//等待，业务，通知
class Data2{//数字，资源类
    private int number = 0;

    Lock lock = new ReentrantLock();
    Condition condition = lock.newCondition();
    //+1
    public  void increment() throws InterruptedException {
        lock.lock();
        try {
            while (number != 0) {
                condition.await();
            }
            number++;
            System.out.println(Thread.currentThread().getName() + "=>" + number);
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            condition.signalAll();
        }
    }

    //-1
    public  void decrement() throws InterruptedException {
        lock.lock();
        try {
            while (number == 0) {
                condition.await();
            }
            number--;
            System.out.println(Thread.currentThread().getName() + "=>" + number);
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            condition.signalAll();
        }
    }
}
```

Condition不仅要又wait 和notify的效果，还有更强的功能,精准通知和唤醒线程

![image-20210206170628775](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210206170628775.png)

来了，精准唤醒

```java
package pc;


import java.util.concurrent.locks.Condition;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

/**
 * A 执行完 调用B，B执行完C，C执行完调用A
 */
public class test3 {
    public static void main(String[] args) {
        Data3 data = new Data3();
        new Thread(()->{
            for (int i = 0; i < 10; i++){
                data.printA();
            }
        }, "A").start();
        new Thread(()->{
            for (int i = 0; i < 10; i++){
                data.printB();
            }
        }, "B").start();
        new Thread(()->{
            for (int i = 0; i < 10; i++){
                data.printC();
            }
        }, "C").start();
        
    }
}

class Data3{
    private Lock lock = new ReentrantLock();

    Condition condition1 = lock.newCondition();
    Condition condition2 = lock.newCondition();
    Condition condition3 = lock.newCondition();
    private  int number = 1;// 1A 2B 3C
    public void printA(){
        lock.lock();
        try{
            //业务，判断—> 执行->通知
            while(number != 1){
                condition1.await();
            }
            System.out.println(Thread.currentThread().getName()+"AAA");
            //唤醒，唤醒指定的人，B
            number = 2;
            condition2.signal();
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            lock.unlock();
        }
    }
    public void printB(){
        lock.lock();
        try{
            //业务，判断—> 执行->通知
            while(number != 2){
                condition2.await();
            }
            System.out.println(Thread.currentThread().getName()+"BBBB");
            number = 3;
            condition3.signal();
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            lock.unlock();
        }
    }
    public void printC(){
        lock.lock();
        try{
            //业务，判断—> 执行->通知
            while (number != 3){
                condition3.await();
            }
            System.out.println(Thread.currentThread().getName()+"CCCC");
            number = 1;
            condition1.signal();
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            lock.unlock();
        }
    }

    //生产线： 下单->支付->交易->
}
```

其实这个很好理解，你可以想象成每一个线程都有一个监视器，告诉你什么时候可以动，什么时候要停下来，就像rm的pd一样

# -----------anki 3.11---------------------------------------

# 5. 八锁现象

```java
package lock8;

import java.util.concurrent.TimeUnit;

/**
 * 八锁，就是关于锁的八个问题
 * 1. 标准情况下，两个线程先打印 发短信还是打电话?  1/发短信  2/打电话
 * 2. send 延迟4s， 两个线程先打印send还是call 1.发短信   2.打电话
 */
public class test1 {
    public static void main(String[] args) {
        Phone phone = new Phone();

        //锁的存在
        new Thread(()->{
            phone.send();
        }, "A").start();
        try {
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        new Thread(()->{
            phone.call();
        }, "B").start();
    }
}

class Phone{
    //synchronized 锁的对象是方法的调用者
    //两个方法使用的是同一个锁，谁先拿到谁执行
    public synchronized void send(){
        try {
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("send");
    }

    public synchronized  void call(){
        System.out.println("call");
    }
}

```

```java
package lock8;

import java.util.concurrent.TimeUnit;

/**
 * 3. 增加了一个普通方法，先执行send还是hello？ 普通方法，其实主要还是看睡眠的时间，不是一定的
 * 4. 两个对象，两个同步方法 其实还是看延迟的时间没别的，先call再send
 */
public class Test2 {
    public static void main(String[] args) {
        //两个对象
        Phone2 phone1 = new Phone2();
        Phone2 phone2 = new Phone2();

        //锁的存在
        new Thread(()->{
            phone1.send();
        }, "A").start();
        try {
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        new Thread(()->{
            phone2.call();
        }, "B").start();
    }
}

class Phone2{
    //synchronized 锁的对象是方法的调用者
    //两个方法使用的是同一个锁，谁先拿到谁执行
    public synchronized void send(){
        try {
            TimeUnit.SECONDS.sleep(4);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("send");
    }

    public synchronized  void call(){
        System.out.println("call");
    }

    //这里没有锁，不是同步方法，不受锁的影响
    public void hello(){
        System.out.println("hello");
    }
}

```

```java
public static void main(String[] args) {
        //两个对象
        Phone3 phone1 = new Phone3();
        Phone3 phone2 = new Phone3();

        //锁的存在
        new Thread(()->{
            phone1.send();
        }, "A").start();
        try {
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        new Thread(()->{
            phone2.call();
        }, "B").start();
    }
}

class Phone3{
    //synchronized 锁的对象是方法的调用者
    //两个方法使用的是同一个锁，谁先拿到谁执行
    //static 静态方法，锁的是class对象哈，其实结果是一样的
    public static synchronized void send(){
        try {
            TimeUnit.SECONDS.sleep(4);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("send");
    }

    public static synchronized  void call(){
        System.out.println("call");
    }

    //这里没有锁，不是同步方法，不受锁的影响
    public void hello(){
        System.out.println("hello");
    }
}

```



```java
package lock8;

import java.util.concurrent.TimeUnit;

/**
 *1. 1个静态的同步方法，1个普通的同步方法，一个对象，先打印发短信还是打电话
 */
public class Test4 {
    public static void main(String[] args) {
        //两个对象
        Phone4 phone1 = new Phone4();
        Phone4 phone2 = new Phone4();

        //锁的存在
        new Thread(()->{
            phone1.send();
        }, "A").start();
        try {
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        new Thread(()->{
            phone2.call();
        }, "B").start();
    }
}

class Phone4{
    //synchronized 锁的对象是方法的调用者
    //两个方法使用的是同一个锁，谁先拿到谁执行
    //static 静态方法，锁的是class对象哈，其实结果是一样的
    public static synchronized void send(){
        try {
            TimeUnit.SECONDS.sleep(4);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("send");
    }

    //普通的同步方法
    public synchronized   void call(){
        System.out.println("call");
    }

    //这里没有锁，不是同步方法，不受锁的影响
    public void hello(){
        System.out.println("hello");
    }
}

```

## 总结

上面的内容其实很简单，其实要搞清楚的就亮点

1. 一个锁和两个锁执行的区别
2. 锁到底锁的是什么？ 有对象和类的两种，当用到static的时候是类，当用到对象的时候是该对象，可以有好几把锁

# 6. Concurrent

## 1. CopyOnWrite

### 1. List

![image-20210209004501774](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210209004501774.png)

看个源码，这里是重新再复制一份的，为啥？

和Vector的区别又在哪里？ 感觉讲地比较模糊把，还是觉得讲地不清楚，明天再看看

我觉得我好像懂了，首先

1. Vector用的是传统的synchronized,本身效率就会比lock差
2. vector是每个方法都有synchronized，所以不能同时读和写，不够友好
3. 而copyonwrite是写的时候线程安全，但读的时候并不是这样子的，因此的话可以读写分离。

详情看 https://www.cnblogs.com/jmcui/p/12377081.html

```java
//ConcurrentModificationException  并发修改异常
public class ListTest {
    public static void main(String[] args) {
        //并发下ArrayList 不安全的
        /**
         * 解决方案：
         * 1. List<String> list = new Vector<>(); vector是线程安全的
         * 但我们一般都不用vector啊
         * 2.  List<String> list = Collections.synchronizedList(new ArrayList<>());
         * 还有一种是这个方法，但其实我也不怎么知道哈，具体的原理真的不清楚哇
         * 3.  List<String> list = new CopyOnWriteArrayList<>();
         *
         */
        //CopyOnWrite写入时复制 COW 计算器设计领域的一种优化策略
        // 多个线程调用的时候,List,读取的时候时固定的，写入的(覆盖)
        // 在写入的时候避免覆盖，造成数据问题
        // 读写分离
        //拿CopyOnWrite 和 Vector相比牛在哪里
        List<String> list = new CopyOnWriteArrayList<>();
        //这啥啊?
//        list.forEach(System.out::println);
        for (int i = 0; i < 10; i++){
//            list.add(UUID.randomUUID().toString().substring(0 ,5));
//            System.out.println(list);
            new Thread(()->{
                list.add(UUID.randomUUID().toString().substring(0 ,5));
                System.out.println(list);
            },String.valueOf(i)).start();
        }
    }
}
```

### 2. Set

![image-20210209215448805](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210209215448805.png)

阻塞队列再这里看到了

```java
package unsafe;

import java.util.Collections;
import java.util.HashSet;
import java.util.Set;
import java.util.UUID;
import java.util.concurrent.CopyOnWriteArraySet;

/**
 * 同理可证：
 * ConcurrentModificationException  并发修改异常
 * 1.Set<String> set = Collections.synchronizedSet((new HashSet<>()));
 * 2.Set<String> set = new CopyOnWriteArraySet<>();
 */
public class SetTest {
    public static void main(String[] args) {
//        Set<String> set = new HashSet<>();
//        Set<String> set = Collections.synchronizedSet((new HashSet<>()));
        Set<String> set = new CopyOnWriteArraySet<>();
        for (int i = 1; i <= 10; i++) {
            new Thread(()->{
                set.add(UUID.randomUUID().toString().substring(0,5));
                System.out.println(set);
            }, String.valueOf(i)).start();

        }
    }
}
```

Set也遇到了差不多的问题，但解决方法是类似的

hashSet底层是什么

```java
public HashSet(){
    map = new HashMap<>();
}
//add set本质是map key是无法重复的
public boolean add(E e){
    return map.put(e, PRESENT == null);
}
```

![image-20210209225212166](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210209225212166.png)

https://www.jianshu.com/p/64f6de3ffcc1 为什么是0.75的加载因子

## 2. ConcurrentMap

```java

public class MapTest {
    public static void main(String[] args) {
        //map 是这样用的吗？ 不是,工作中不用HashMap
        // 默认等价于什么 new HashMap<>(16,0.75);
        Map<String, String> map = new ConcurrentHashMap<>();
        //加载因子， 初始化容量

        for (int i = 1; i<=30; i++){
            new Thread(()->{
                map.put(Thread.currentThread().getName(), UUID.randomUUID().toString().substring(0,5));
                System.out.println(map);
            }, String.valueOf(i)).start();
        }

    }
}
```

其实这里的话和上面的List和Set是差不多的，但是换了个名字而已。

# 7. Callable

![image-20210209231900273](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210209231900273.png)

差点忘了这个东西，反正就是比Runnable高级的东西

1. 可以有返回值
2. 可以抛出异常
3. 方法不同

![image-20210210145122136](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210210145122136.png)

还有一个泛型，泛型的参数的方法的返回值

```java

public class CallableTest {
    public static void main(String[] args) throws ExecutionException, InterruptedException {

        new Thread().start();
        MyThread thread = new MyThread();
        FutureTask futureTask = new FutureTask(thread);
        new Thread(futureTask, "A").start();
        new Thread(futureTask, "B").start();
        Integer o = (Integer) futureTask.get();//这个get方法可能会产生阻塞，因为如果call方法很耗时的话，这个get就没那么块拿得到哈，所以一般就放在最后来
        System.out.println(o);
    }
}
class MyThread implements Callable<Integer> {

    @Override
    public Integer call() {
        System.out.println("call()");
        return Integer.parseInt("1234");
    }
}public class CallableTest {
    public static void main(String[] args) throws ExecutionException, InterruptedException {

        new Thread().start();
        MyThread thread = new MyThread();
        FutureTask futureTask = new FutureTask(thread);
        new Thread(futureTask, "A").start();
        Integer o = (Integer) futureTask.get();//获取Callable的返回结果
        System.out.println(o);
    }
}
class MyThread implements Callable<Integer> {

    @Override
    public Integer call() {
        System.out.println("call()");
        return Integer.parseInt("1234");
    }
}
```

![image-20210210164712984](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210210164712984.png)

但是呢FutureTask只执行一次，所以只会输出一次的结果。

1. 可能会有阻塞，所以get放到最后
2. 会有缓存？

# 8. 常用的辅助类

## 8.1 CountDownLatch

![image-20210210164939032](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210210164939032.png)

```java
package add;

import java.util.concurrent.CountDownLatch;

/**
 * 计数器
 */
public class CountDownLatchDemo {
    public static void main(String[] args) throws InterruptedException {
        //总数是6,必须要执行任务的时候，再使用
        CountDownLatch countDownLatch = new CountDownLatch(6);
        for (int i = 1; i <= 6 ; i++) {
            new Thread(()->{
                System.out.println(Thread.currentThread().getName()+"Go out");
                countDownLatch.countDown();//数量减1
            }, String.valueOf(i)).start();
        }
        countDownLatch.await();//等待计数器归零，再向下执行
        System.out.println("close door");
    }
}

```

其实原理挺简单，你可以想象成一个教室，必须等到全部人走之后才可以关门，这里的6代表的就是要等的人数，countDown()代表的是--，出去了一个人了，最后的await是让所有人都出去了，再执行下面的代码

## 8.2 CyclicBarrier

![image-20210210170715233](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210210170715233.png)

可以当作是加法计数器

```java
package add;

import java.util.concurrent.BrokenBarrierException;
import java.util.concurrent.CyclicBarrier;

public class CyclicBarrierDemo {
    public static void main(String[] args) {
        /**
         * 集齐七颗龙珠召唤神龙
         */
        //召唤龙珠的线程
        CyclicBarrier cyclicBarrier = new CyclicBarrier(7, ()->{
            System.out.println("召唤神龙成功");
        });
        for (int i = 1; i <= 7 ; i++) {
            //要这样的原因是lambda操作不到i就拿不到i的值，这样的话需要让一个固定的变量去等于i，而不是一个摸不到的值
            final int temp = i;
            //lambda能操作到i吗,不行哈
            new Thread(()->{
                System.out.println(Thread.currentThread().getName()+"收集"+temp+"个龙珠");
                try {
                    //这里有点不一样了吼,是通过await来计数的，await之后本次现车给会被阻塞，直到神龙召唤吼才能执行
                    //和前面的countdown的区别？ 这个感觉像一个集体，那个的话更像一个独立的个体，完了就完了
                    cyclicBarrier.await();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                } catch (BrokenBarrierException e) {
                    e.printStackTrace();
                }
            }, String.valueOf(i)).start();

        }
    }
}

```



## 8.3 Semaphore

semaphore:信号量

![image-20210212173226559](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210212173226559.png)

抢车位

6车--3个停车位

`semaphore.acquire()`获得，假设如果已经满了，等待，等待被释放为止

`semaphore.release()`：释放，会将当前的信号量释放+1，然后唤醒等待的线程

作用：多个共享资源互斥的使用，并发限流，控制最大的线程数

```java
package add;

import java.util.concurrent.Semaphore;
import java.util.concurrent.TimeUnit;

public class SemaphoreDemo {
    public static void main(String[] args) {
        //线程数量：停车位!限流
        Semaphore semaphore = new Semaphore(3);

        for (int i = 1; i <= 6 ; i++) {
            new Thread(()->{
                //acquire() 得到
                try {
                    semaphore.acquire();
                    System.out.println(Thread.currentThread().getName()+"抢到车位");
                    TimeUnit.SECONDS.sleep(2);
                    System.out.println(Thread.currentThread().getName()+"离开车位");
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }finally {
                    semaphore.release();
                }
                // release() 释放
            }, String.valueOf(i)).start();
        }
    }
}
```



# 9. 读写锁

ReadWriteLock

![image-20210212205033059](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210212205033059.png)

```java
package rw;

import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReadWriteLock;
import java.util.concurrent.locks.ReentrantLock;
import java.util.concurrent.locks.ReentrantReadWriteLock;

/**
 * 独占锁（写锁）一次只能被一个线程占有
 * 共享锁（读锁）多个线程可以同时占有
 * 这种读写分离的思想感觉再很多地方都看得到，redis里面就学到了
 * 读- 读 可以共存
 * 读- 写 不可以共存
 * 写-写  不能共存！
 */
public class ReadWriteLockDemo {
    public static void main(String[] args) {
        MyCacheLock myCache = new MyCacheLock();

        //写入
        for (int i = 1; i <= 5 ; i++) {
            final  int temp = i;
            new Thread(()->{
                myCache.put(temp+"",temp+"");
            }, String.valueOf(i)).start();
        }

        //读取
        for (int i = 1; i <= 5 ; i++) {
            final  int temp = i;
            new Thread(()->{
                myCache.get(temp+"");
            }, String.valueOf(i)).start();
        }


    }
}

/**
 * 自定义缓存？？
 * 这是啥啊
 */
class MyCache{

    private volatile Map<String, Object> map = new HashMap<>();

    //存，写
    public void put(String key, Object value){
        System.out.println(Thread.currentThread().getName()+"写入"+key);
        map.put(key, value);
        System.out.println(Thread.currentThread().getName()+"写入OK");
    }
    //取，读
    public void get(String key){
        System.out.println(Thread.currentThread().getName()+"读取"+key);
        Object o = map.get(key);
        System.out.println(Thread.currentThread().getName()+"读OK");
    }
}
//加锁的
class MyCacheLock{

    private volatile Map<String, Object> map = new HashMap<>();
    //读写锁：更加细粒度的控制
    private ReadWriteLock lock = new ReentrantReadWriteLock();

    //存，写，写入的时候，只希望同时只有一个线程写
    public void put(String key, Object value){
        lock.writeLock().lock();
        try{
            System.out.println(Thread.currentThread().getName()+"写入"+key);
            map.put(key, value);
            System.out.println(Thread.currentThread().getName()+"写入OK");
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            lock.writeLock().unlock();
        }

    }
    //取，读 所有人都可以读,这里为什么要加锁呢？理解的意思是万一还在写呢？那你拿的数据就不对了
    public void get(String key){
        lock.readLock().lock();

        try{
            System.out.println(Thread.currentThread().getName()+"读取"+key);
            Object o = map.get(key);
            System.out.println(Thread.currentThread().getName()+"读OK");
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            lock.readLock().unlock();
        }

    }
}
```

附上自己的理解把，我觉得专门做出来的这个锁是表示一种状态，当你再这种状态下，somehow你的效率就会变高，尽管一开始觉得可以用普通的锁和不加锁取代替，但是她不能解决一种情况把，处理要读和写之间的矛盾。像redis中是如果你读的时候刚好也再写，拿你读的就不算，要重新再读一遍，不过我不清楚这里的，是读的时候不能写吗？

1. 当有读锁的时候，不能获取写锁，所以还是跟redis有点不一样的把
2. 其他的我就不知道了

# 10. 阻塞队列

![image-20210213151001637](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210213151001637.png)

阻塞队列：

![image-20210213151125318](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210213151125318.png)

什么情况下会使用阻塞队列

多线程并发处理，线程池

![image-20210213152633632](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210213152633632.png)

添加、移除

**四组API**

| 方式           | 抛出异常 | 不会抛出异常，有返回值 | 阻塞等待 | 超时等待 |
| -------------- | -------- | ---------------------- | -------- | -------- |
| 添加           | add      | offer                  | put      | offer    |
| 移除           | remove   | poll                   | take     | poll     |
| 检测队列首元素 | element  | peek                   |          |          |

```java
 /**
     * 抛出异常
     */
    public static void test1(){
        //队列的大小
        ArrayBlockingQueue blockingQueue = new ArrayBlockingQueue<>(3);
        System.out.println(blockingQueue.add("a"));
        System.out.println(blockingQueue.add("b"));
        System.out.println(blockingQueue.add("ac"));

        //IllegalStateException: Queue full 抛出异常
//        System.out.println(blockingQueue.add("ad"));
        System.out.println("=============");
        System.out.println(blockingQueue.remove());
        System.out.println(blockingQueue.remove());
        System.out.println(blockingQueue.remove());

        //NoSuchElementException 抛出异常
//        System.out.println(blockingQueue.remove());
    }
```

```java

    /**
     *有返回值，没有异常
     */
    public static void test2(){
        ArrayBlockingQueue blockingQueue = new ArrayBlockingQueue<>(3);
        System.out.println(blockingQueue.offer("a"));
        System.out.println(blockingQueue.offer("b"));
        System.out.println(blockingQueue.offer("c"));
        System.out.println(blockingQueue.offer("d")); //false 不抛出异常

        System.out.println("==============");
        System.out.println(blockingQueue.poll());
        System.out.println(blockingQueue.poll());
        System.out.println(blockingQueue.poll());
        System.out.println(blockingQueue.poll()); //null 不抛出异常
    }
```

```java
/**
     * 等待，阻塞(一直)
     */
    public static void test3() throws InterruptedException {
        ArrayBlockingQueue blockingQueue = new ArrayBlockingQueue(3);
        //一直阻塞
        blockingQueue.put("a");
        blockingQueue.put("b");
        blockingQueue.put("c");
//        blockingQueue.put("d");//队列没有位置了，一直阻塞

        System.out.println(blockingQueue.take());
        System.out.println(blockingQueue.take());
        System.out.println(blockingQueue.take());
        System.out.println(blockingQueue.take()); //没有这个元素,那就会一直等下去
    }
```

```java
/**
     * 等待，阻塞(等待超时),所以这个就是在有返回值的方法上进行重载而已
     */
    public static void test4() throws InterruptedException {
        ArrayBlockingQueue blockingQueue = new ArrayBlockingQueue(3);

        blockingQueue.offer("a");
        blockingQueue.offer("b");
        blockingQueue.offer("c");

        //只有offer可以这样子设置，put和add都不行， 2s之后超时退出
        blockingQueue.offer("d",2, TimeUnit.SECONDS);

        System.out.println("============");
        System.out.println(blockingQueue.poll());
        System.out.println(blockingQueue.poll());
        System.out.println(blockingQueue.poll());
        System.out.println(blockingQueue.poll(2, TimeUnit.SECONDS));
    }
```



1. 抛出异常
2. 不会抛出异常
3. 阻塞等待
4. 超时等待

超时等待好熟哈，就是前面线程的状态哪里有讲到

## 同步队列

没有容量，进去一个元素，必须等待取出来之后，才能再往里面放一个元素

```java
package bq;

import java.util.concurrent.SynchronousQueue;
import java.util.concurrent.TimeUnit;

/**
 * 同步队列
 * 和其他的队列不一样，同步的所以是只能进一出一，相当于容量就只为1，不存储元素
 */
public class SynchronizedQueueDemo {
    public static void main(String[] args) {
        SynchronousQueue<String> synchronousQueue = new SynchronousQueue<String>();

        new Thread(()->{
            try {
                System.out.println(Thread.currentThread().getName()+"put 1");
                synchronousQueue.put("1");
                System.out.println(Thread.currentThread().getName()+"put 2");
                synchronousQueue.put("2");
                System.out.println(Thread.currentThread().getName()+"put 3");
                synchronousQueue.put("3");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }, "T1").start();

        new Thread(()->{
            try {
                TimeUnit.SECONDS.sleep(3);
                System.out.println(Thread.currentThread().getName()+synchronousQueue.take());
                TimeUnit.SECONDS.sleep(3);
                System.out.println(Thread.currentThread().getName()+synchronousQueue.take());
                TimeUnit.SECONDS.sleep(3);
                System.out.println(Thread.currentThread().getName()+synchronousQueue.take());
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }, "T2").start();

    }
}
```

但其实还是有比较大的区别的，不过呢，我还是不会用吧

# 11. 线程池(重点)

> 池化计数

程序的运行，本质：占用系统的资源，优化资源的使用-》池化技术

线程池、连接池、内存池、对象池  创建、销毁，十分浪费资源

池化技术：事先准备好一些资源，有人要用，就来我这里拿，用完之后还给我

**线程池的好处：**

1. 降低资源的消耗
2. 提高响应的速度
3. 方便管理

**线程复用，可以控制最大并发数，管理线程**

之前的理解是，比如你的出行，不管理的话就是每人造辆自行车然后出发，用完就销毁，你知道把，很浪费资源的，那我就搞共享单车，骑完不用报废，而且消耗时间少，也方便管理，给定一定数量的单车，而不是无节制地造。



阿里巴巴手册规定

![image-20210214215444115](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210214215444115.png)

```java
package threadpool;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

/**
 * Excutors 工具类的三大方法
 * 使用了线程池之后，使用线程池来创建线程
 */
public class Demo01 {
    public static void main(String[] args) {
//        ExecutorService threadPool = Executors.newSingleThreadExecutor();//单个线程
        //最多有五个线程执行，因为设置为5哈
//        ExecutorService threadPool = Executors.newFixedThreadPool(5);//创建一个固定的线程池的大小
         ExecutorService threadPool = Executors.newCachedThreadPool();//可伸缩的，遇强则强，遇弱则弱
        try {
            for (int i = 0; i < 10; i++) {
                threadPool.execute(()->{
                    System.out.println(Thread.currentThread().getName()+" ok");
                });
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //线程池用完，程序结束，关闭线程池
            threadPool.shutdown();
        }
    }
}
```



> 7大参数

源码分析

```java
    public static ExecutorService newSingleThreadExecutor() {
        return new FinalizableDelegatedExecutorService
            (new ThreadPoolExecutor(1, 1,
                                    0L, TimeUnit.MILLISECONDS,
                                    new LinkedBlockingQueue<Runnable>()));
    }

  public static ExecutorService newFixedThreadPool(int nThreads) {
        return new ThreadPoolExecutor(nThreads, nThreads,
                                      0L, TimeUnit.MILLISECONDS,
                                      new LinkedBlockingQueue<Runnable>());
    }

    public static ExecutorService newCachedThreadPool() {
        return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
                                      60L, TimeUnit.SECONDS,
                                      new SynchronousQueue<Runnable>());
    }

本质：ThreadPoolExecutor
        public ThreadPoolExecutor(int corePoolSize,//核心线程大小，最小的线程数
                              int maximumPoolSize,//最大核心线程池大小
                              long keepAliveTime,//超时了没有人用就释放
                              TimeUnit unit,//超时单位
                              BlockingQueue<Runnable> workQueue,//阻塞队列
                              ThreadFactory threadFactory,//线程工厂，创建线程的，一般不用动
                              RejectedExecutionHandler handler//拒绝策略) {
        if (corePoolSize < 0 ||
            maximumPoolSize <= 0 ||
            maximumPoolSize < corePoolSize ||
            keepAliveTime < 0)
            throw new IllegalArgumentException();
        if (workQueue == null || threadFactory == null || handler == null)
            throw new NullPointerException();
        this.acc = System.getSecurityManager() == null ?
                null :
                AccessController.getContext();
        this.corePoolSize = corePoolSize;
        this.maximumPoolSize = maximumPoolSize;
        this.workQueue = workQueue;
        this.keepAliveTime = unit.toNanos(keepAliveTime);
        this.threadFactory = threadFactory;
        this.handler = handler;
    }
```

怎么去理解那个核心线程数，感觉是你并发处理的时候，你最弱可以使用到多少来跑，对于Single那就最小是1最大也是1，而固定的话是最小喝最大都是那个值，先不谈有没有可能达到这个线程数哈，而Cache那里就像是伸缩的，你最弱可以是0，当你不需要线程跑的时候就当然是0，那你5的话就用5个线程跑，而比如固定是3，那你最大也是用3来跑，不过这样会有问题是你线程数量大时你理论上可以用超多线程跑，但是问题时你不符合实际，太多线程会内存溢出的，所以我们一般要用原生的线程池哈



![image-20210215144546438](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210215144546438.png)

这个例子挺好的，那我的Core和Max是没有理解错的，123是正常情况下开的，45开的时候是人超级多的时候，那你等的人满了，站在外面的人怎么班？ 那这个就是拒绝的策略

![image-20210215150523019](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210215150523019.png)

超时等待的意思，就是加班的点把，345是突然被叫来加班的，再等等看有没有人，没认就走了

> 4个拒绝策略

```java
package threadpool;

import java.util.concurrent.*;

/**
 * Excutors 工具类的三大方法
 * 使用了线程池之后，使用线程池来创建线程
 */
public class Demo01 {
    public static void main(String[] args) {
        //自定义线程，工作都是自己创建的
        ExecutorService threadPool = new ThreadPoolExecutor(2, 5, 3, TimeUnit.SECONDS,
                new LinkedBlockingDeque<>(3),
                Executors.defaultThreadFactory(),
//                new ThreadPoolExecutor.AbortPolicy());//银行满了，还有人进来，不处理这个人的，抛出异常
//                new ThreadPoolExecutor.CallerRunsPolicy()); //哪来的去哪里，就比如说你去银行满了，你从公司过来的那就让公司的人帮你搞，nb啊这个
//                new ThreadPoolExecutor.DiscardPolicy()); //队列满了，丢掉任务，不会抛出异常
                new ThreadPoolExecutor.DiscardOldestPolicy());//队列满了，尝试去和最早的竞争？？ 并不，看看源码一会儿

        try {
            //最大承载：Deque + max
            //超过最大的承载 RejectedExecutionException
            //但我觉得还不够好，你起码也得等等啊，万一下一个人好了呢
            for (int i = 1; i <= 9; i++) {
                threadPool.execute(()->{
                    System.out.println(Thread.currentThread().getName()+" ok");
                });
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            //线程池用完，程序结束，关闭线程池
            threadPool.shutdown();
        }
    }
}
```





> 小结和扩展

了解：IO密集型，CPU密集型，调优

```java
        //最大线程到底如何定义
        //1.CPU密集型  几核，就是几，可以保持CPU的效率最高！
        //2.IO密集型 > 判断你程序中十分耗IO的线程，
```

# 12. 四大函数式接口(必须掌握)

新时代的程序员：lambda表达式、链式编程、函数式接口、Stream流式计算

> 函数式接口，只有一个方法的接口，原来是这个就是`Functional Interface`,可以用lambda表达式的

比如Runnable，简化编程模型，在新版本的框架底层大量应用

foreach(消费者类的函数式接口)

![image-20210216124057214](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210216124057214.png)

因为这四个词是原生的词，不是由其他的词组成的

代码测试：

![image-20210216124359518](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210216124359518.png)

```java
package function;

import java.util.function.Function;

/**
 * Function 函数型接口,有一个输入参数，有一个输出
 * 只要是 函数型接口 可以用lambda表达式简化
 */
public class Demo01 {
    public static void main(String[] args) {
        //工具类：输出输入的值
//        Function function = new Function<String, String>() {
//            @Override
//            public String apply(String s) {
//
//                return s;
//            }
//        };
        Function function = (s)->{return s;};
        System.out.println(function.apply("123"));
    }
}
```



> 断定型接口: 有一个输入参数，返回值只能是布尔值

```java
package function;

import java.util.function.Predicate;

/**
 * 断定型接口：有一个输入参数，返回值只能是布尔值
 */
public class Demo02 {
    public static void main(String[] args) {
        //判断字符串是否为空
//        Predicate predicate = new Predicate<String>() {
//            @Override
//            public boolean test(String s) {
//                return s.isEmpty();
//            }
//        };
//        System.out.println(predicate.test("123"));

        Predicate<String> predicate = (str)->{
          return   str.isEmpty();
        };
        System.out.println(predicate.test("123"));
    }
}
```





> Consumer 消费型接口

![image-20210217091633133](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210217091633133.png)

```java
/**
 * Consumer 消费型接口：只有输入，没有返回值，的确就是消费了，用了后没出来啥东西
 */
public class Demo03 {
    public static void main(String[] args) {
//        Consumer<String> consumer = new Consumer<String>() {
//            @Override
//            public void accept(String string) {
//                System.out.println(string);
//            }
//        };
        Consumer<String> consumer = (str)->{
            System.out.println(str);
        };
        consumer.accept("123");
    }
}
```



> Supplier 供给型接口

![image-20210217092235760](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210217092235760.png)

```java
/**
 * Supplier 供给型接口  没有参数，只有返回值
 */
public class Demo04 {
    public static void main(String[] args) {

//        Supplier<Integer> supplier = new Supplier<Integer>() {
//            @Override
//            public Integer get() {
//                System.out.println("get()");
//                return 1024;
//            }
//        };
        Supplier<Integer> supplier = ()->{
            return 1024;
        };
        System.out.println(supplier.get());
    }
}

```

这些有什么用呢？我目前是不知道的，但他好像就是jdk1.8的新特性，跟你要会反射，枚举，泛型之类差不多的

# 13. Stream流式计算

> 什么是Stream流式计算

大数据：存储+计算

存储：集合、Mysql 本质就是存储东西，计算都应该交给流来操作

```java
/**
 * 题目要求：
 * 现在有5个用户：筛选：
 * 1.ID必须是偶数
 * 2.用户名转为大写字母
 * 3.年龄必须大于23岁
 * 4.用户名字母倒着排序
 * 5.只输出一个用户！
 */
public class Test {
    public static void main(String[] args) {

        User u1 = new User(1, "a", 21);
        User u2 = new User(2, "b", 22);
        User u3 = new User(3, "c", 23);
        User u4 = new User(4, "d", 24);
        User u5 = new User(6, "e", 25);
        //集合就是存储
        List<User> list = Arrays.asList(u1, u2, u3, u4, u5);

        //计算交给流,这个map有点意思，有点像重写toString的感觉哈，然后这里的sorted我想了很久，
        //他到底是根据什么来进行sort的？然后答案是map出来的东西，你可以理解成map推出了一个大家可以看到的东西
        //所以的话都是用推出来的东西进行比较的
        list.stream().filter(u->{return u.getId() % 2 == 0;})
                .filter(u->{return u.getAge()>23;})
                .map(u->{return u.getName().toUpperCase();})
                .sorted((user1, user2)->{return user2.compareTo(user1);})
                .limit(1)
                .forEach(System.out::println);
    }
}

```



# 14. ForkJoin

> 什么是ForkJoin

ForkJoin 在JDK 1.7，并行执行任务！提高效率，大数据量

![image-20210217103037382](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210217103037382.png)

分治法的感觉，就是把大任务拆成小任务然后一个个任务完成之后进行合并

> ForkJoin: 工作窃取

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210217103859708.png" alt="image-20210217103859708" style="zoom:67%;" />

这张图表示的是当两个线程在执行任务时，B线程率先执行完，但A没有，那B怎么办？那他就偷A的任务过来执行，进行工作窃取，这个功能实现的基础在于是双端队列哈，但说实话有啥关系嘛？不是双端队列就执行不了了吗？噢，的确是，你偷的话得偷他不在执行的啊，也可以说是最低端的。

就像两家咖啡店，一家哇超多人，排在队尾的人就被另外一家没人的咖啡店拉过去了

> ForkJoin的操作

![image-20210217111027371](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210217111027371.png)

代码：

```java

/**
 * 我现在听的是完全懵逼的状态，等会可能要再思考一遍哈
 * 求和计算的任务
 *如何使用forkjoin
 * 1. forkjoinPool 通过他来执行
 * 2. 计算任务 forkjoinPool.execute(ForkJoinTask task)
 * 3. 计算类要继承ForkJoinTask
 */
public class ForkJoinDemo extends RecursiveTask<Long> {
    private Long start;
    private Long end;

    //临界值
    private Long temp = 10000L;

    public ForkJoinDemo(Long start, Long end) {
        this.start = start;
        this.end = end;
    }
    
    //计算方法
    @Override
    protected Long compute() {
        if((end - start) < temp){
            Long sum = 0L;
            for (Long i = start; i <= end ; i++) {
                sum+=i;
            }
            return sum;
        }else{
            //中间值
            long middle = (start + end) / 2;
            ForkJoinDemo task1 = new ForkJoinDemo(start, middle);
            task1.fork(); //拆分任务，把任务压入线程队列
            ForkJoinDemo task2 = new ForkJoinDemo(middle + 1, end);
            task2.fork();
            return  task1.join() + task2.join();
        }
    }
}

```

```java
public class Test {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        test3();
    }
    //普通的方法
    public static void test1(){
        long start = System.currentTimeMillis();

        Long sum = 0L;
        for (Long i = 1L; i <= 10_0000_0000 ; i++) {
            sum+=i;
        }
        long end = System.currentTimeMillis();
        System.out.println("sum="+"时间"+ (end-start));


    }
    //会使用ForkJoin
    public static void test2() throws ExecutionException, InterruptedException {
        long start = System.currentTimeMillis();
        ForkJoinPool forkJoinPool = new ForkJoinPool();
        ForkJoinTask<Long> task = new ForkJoinDemo(0L, 10_0000_0000L);
//        forkJoinPool.execute(task);
        ForkJoinTask<Long> submit = forkJoinPool.submit(task);
        Long sum = submit.get();
        long end = System.currentTimeMillis();
        System.out.println("sum="+"时间"+ (end-start));
        System.out.println(sum);


    }
    public static void test3(){
        long start = System.currentTimeMillis();
        //Stream并行流() (]
        long sum = LongStream.rangeClosed(0L, 10_0000_0000L).parallel().reduce(0, Long::sum);
        long end = System.currentTimeMillis();
        System.out.println("sum="+"时间"+ (end-start));
    }
}

```

> 这里只是简单的求和计算罢了，但是有着不同的方法，比如这里的ForkJoin,相当于你分配任务到各组，各组再分配到各人身上，最后把结果汇总起来，这个是总的原理。

从我们使用的类上来看，有用到的是`ForkJoinPool ForkJoinTask`,从需要返回值上来看这个就是用到了Callable而不是Runnable，而且`ForkJoinPool`是继承`ExecutorService`的，所以是线程池，而`ForkJoinTask`则是实现了`Future`接口，所以的话可以有返回值，那怎么把这些东西联系起来呢？

首先我有一个任务，把这个任务拿出来

可以是`ForkJoinTask<Long> task = new ForkJoinDemo(0L, 10_0000_0000L);` 也可以是`ForkJoinDemo task = new ForkJoinDemo(0L, 10_0000_0000L);`,表示任务创建好啦，然后利用`forkJoinPool`提交任务，最后有一个返回值表示你完成好的任务，你可以拿到任务的各种信息把，结果之类的，那差不多就是这个逻辑

# 15. 异步回调

> 设计的初衷，对将来的某个事件的结果进行建模

![image-20210217154707933](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210217154707933.png)

```java
/**
 * 异步调用：Ajax,我倒是理解了这个代码，问题是怎么进行异步回调的我咋不懂呢？
 * 好像又明白了，之前是不懂回调？的关系
 */
public class Demo01 {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        //发起一个请求
        CompletableFuture<Void> completableFuture = CompletableFuture.runAsync(() -> {
            System.out.println(Thread.currentThread().getName() + "没有返回，Update my sql ok");
        });

        completableFuture.get();
        CompletableFuture<Integer> integerCompletableFuture = CompletableFuture.supplyAsync(() -> {
            System.out.println(Thread.currentThread().getName() + "没有返回，Update my sql ok");
//            int age = 10 / 0;
            return 1024;
        });
        System.out.println(integerCompletableFuture.whenComplete((t, u) -> {
            System.out.println("****t: " + t);
            System.out.println("****u: " + u);
        }).exceptionally(f -> {
            System.out.println("***exception:" + f.getMessage());
            return 4444;
        }).get());

    }
}
```

首先，回调的意思是

> A callback is a function that is passed as an argument to another function and is executed after its parent function has completed.

 **B函数被作为参数传递到A函数里，在A函数执行完后再执行B**。

ok，我还是不理解哈

我现在好像又理解了，https://www.cnblogs.com/liujiarui/p/13395424.html,这篇感觉对我而言帮助蛮大的。

其实老师一直前面讲的例子就有说到，但我可能是没反应过来之类的把，之前问问题其实就是异步回调，回调代表的是你问某人问题，他给你的回答就是回调，可以分为你一直等他回答或者是你问完他之后，就拜拜做自己的事情，然后最后他来找你告诉你他的答案。

但这个谁调谁的问题还是懵懵的，感觉的话还是理解不透彻，感觉他讲的也不透彻啊！但我现在大概是知道这么个理罢了

# 16. JMM

Votaile是java虚拟机提供**轻量级的同步机制**

1. 保证可见性
2. 不保证原子性
3. 禁止指令重排

JMM：java内存模型，不存在的东西，概念！

**关于JMM的一些同步的约定**：

1. 线程解锁前、，必须把共享变量 立刻刷回主存
2. 线程加锁前，必须读取主存中的最新值到工作内存中
3. 加锁和解锁是同一把锁

线程 工作内存、主内存

**8种操作**：

![image-20210218110926163](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210218110926163.png)

这个store和write反了

![image-20210218111355164](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210218111355164.png)

![image-20210218111518022](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210218111518022.png)

![image-20210218111832588](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210218111832588.png)

程序不知道主内存的值已经被修改过了

# 17. Volatile

> 1.保证可见性

```java
package volatiledemo;

import java.util.concurrent.TimeUnit;

public class JMMDemo {
    //不加volatile 程序就会死循环！
    //加volatile可以保证可见性
    private volatile static int num = 0;
    public static void main(String[] args) {
        new Thread(()->{ //线程1对主内存的变化是不知道的
            while (num == 0){

            }
        }).start();

        try {
            TimeUnit.SECONDS.sleep(1);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        num = 1;
        System.out.println(num);
    }
}

```

> 2. 不保证原子性

原子性：不可分割

线程A在执行任务的时候，不能被打扰的，也不能被分割的，要么同时成功，要么同时失败

？？其实我不是很懂这里，感觉他给的代码和这句话无关啊，这里的打扰我倒是理解倒了，线程不安全的话就会被打扰，分割啥的我就不懂了呃

使用原子类解决原子问题

```java
package volatiledemo;

import java.util.concurrent.atomic.AtomicInteger;

/**
 * 不保证原子性
 */
public class VolatileDemo {
//    private static int num = 0;
    private volatile static AtomicInteger num = new AtomicInteger();
    public synchronized static void add(){
//        num++;// 不是一个原子性操作
        num.getAndIncrement(); //AtomicInteger + 1 方法，CAS
    }

    public static void main(String[] args) {
        //理论上num结果应该为2万
        for (int i = 1; i <= 20 ; i++) {
            new Thread(()->{
                for (int j = 0; j < 1000; j++) {
                    add();
                }
            }).start();
        }

        while(Thread.activeCount() > 2){
            Thread.yield();
        }

        System.out.println(Thread.currentThread().getName()+" " + num);
    }
}

```

这些类的底层都是直接和操作系统挂钩，在内存中修改值  Unsafe

# 18. Volatile(尚硅谷版)

1. 保证可见性
2. 不保证原子性
3. 禁止指令重排

## JMM

java内存模型

![image-20210220153907673](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210220153907673.png)

![image-20210220154013653](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210220154013653.png)

这个就讲的更我i详细点，让我知道的是共享内存就是主内存，然后每个线程都有自己的工作内存，因此每次线程对变量进行操作的时候，都是操作的变量拷贝，因此操作完之后就得去修改主内存的值，主内存的值改变了，其他线程要去重新进行变量拷贝才行的



而JMM要保证的特性是

1. 可见性
2. 原子性
3. 有序性

## Volatile不保证原子性

而volatile只保证可见性和有序性

![image-20210221093055313](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210221093055313.png)

```java
class MyData{
     int number = 0;
    public  void addTo60(){
        this.number = 60;
    }

    //请注意，此时number前面时加了关键字修饰的
    public void addPlus(){
        number++;
    }
    AtomicInteger atomicInteger  = new AtomicInteger();
    public void addAtomic(){
        atomicInteger.getAndIncrement();
    }
}

/**
 * 1. 验证volatile的可见性
 * 1.1 假如int number = 0; number变量之前根本没有添加volatile关键字修饰， 没有可见性
 *
 * 2. 验证volatile不保证原子性
 *  2.1原子性什么意思？
 *      不可分割，完整性，也即某个线程正在做某个具体业务时，中间不可以被加塞或者被分割，需要整体完整，
 *      要么同时成功，要么同时失败。
 *  2.2 volatile不保证原子性的案例演示
 *
 *  2.3 why
 *
 *  2.4 如何解决原子性
 *      1.加sync
 *      2.AtomicInteger
 *      但原理？ 为什么AtomicInteger可以呢？ 就要看后面的CAS了
 */
public class VolatileDemo2 {
    public static void main(String[] args) {

        MyData myData = new MyData();
        for (int i = 1; i <= 20 ; i++) {
            new Thread(()->{
                for (int j = 1; j <= 1000 ; j++) {
                    myData.addPlus();
                    myData.addAtomic();
                }
            },String.valueOf(i)).start();
        }

        //需要等待上面20个线程,我觉得我已经把yield忘得差不多了
        //首先yield是放弃cpu执行权的，我tmd又有一个疑问了哈，为什么要抢呢？
        //现在差不多理解了是多核cpu的问题，多核cpu是可以处理多个线程的，所以你yield了之后感觉也是yiield了个寂寞，
        //因为你释放掉你就可以马上抢得到，又不是单核cpu。
        //所以在这里的话如果是很多个线程的话这样的确会比较快，一直放弃，因此去掉的话也不是不行，只是速度会慢些罢了
        //主要还是Thread.activeCount在起作用哈
        while (Thread.activeCount() > 2){
            Thread.yield();
        }
        System.out.println(Thread.currentThread().getName()+"\t int type, finally number value: "+myData.number);
        System.out.println(Thread.currentThread().getName()+"\t AtomicInteger type, finally number value: "+myData.atomicInteger);
    }
    public static void seeOkByVolatile(){
        MyData myData = new MyData();
        new Thread(()->{
            System.out.println(Thread.currentThread().getName() + "\t come in");
            try {
                TimeUnit.SECONDS.sleep(3);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            myData.addTo60();
            System.out.println(Thread.currentThread().getName()+"\t update number value:" + myData.number);
        }, "AAA").start();

        //第二个线程就是main线程
        while (myData.number == 0){
            //main 线程就一直在这等待循环，直到number不再等于0
        }
        System.out.println(Thread.currentThread().getName()+"\t mission is over");
    }
}
```

##  禁止指令重排

![image-20210221104342434](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210221104342434.png)

他最后这句话说的理解是像考试一样，会做的先做了，不会做的先跳过去，

而且 多线程的执行本来就是一个没有固定顺序的， https://bbs.csdn.net/topics/360085086

![image-20210221105509272](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210221105509272.png)



### 重排1

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210221105839406.png" alt="image-20210221105839406" style="zoom:67%;" />

你写的代码顺序编译器不一定会这么执行，所以可能会有好几种顺序，但是呢，这个问题的答案是否，因为数据是有依赖性的，前面有提到。

1. y没有定义
2. x~~的值也是不确定，可以是11.也可以是16(所以我之前还以为可以这样的)~~ 存疑？

![image-20210221114555246](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210221114555246.png)

我觉得这个有点问题把，他这个没保证可见性啊，看起来怪怪的，先不管这个了，但这个就表示如果你指令重排可能会有这种结果，所以每次运行结果都不同？那我觉得上面的说法不正确，感觉差不多的



### 重排2

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210221144404243.png" alt="image-20210221144404243" style="zoom:67%;" />

这里是另外一个情况，但是我好像不知道他们的区别呃，一会再看看？这里还是因为顺序的问题，如果

```java
flag = true;
//如果在这时这个线程去执行了method02()里面的代码，进入到了if语句，这样就变成了a= 0 + 5 等于5了，其实我觉得a = 1也时有可能的?要不试试
a = 1

```

而且这里关于可见性的问题我时这么想的，你多个线程去直接执行这两个方法，就不会有可见性的问题了。

试玩了，说实话可能时线程数不够，出不来那个结果，没有出现指令重排的现象哈，而且呢，我觉得会有非原子性的问题？woc，好像时的把，无语

![image-20210221155843940](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210221155843940.png)

![image-20210221160309508](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210221160309508.png)

![image-20210221160828202](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210221160828202.png)

![image-20210221162310296](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210221162310296.png)

然后 **synchronized**也可以实现可见性的！！之前不知道！！！

JMM关于synchronized的两条规定：

　　1）线程解锁前，必须把共享变量的最新值刷新到主内存中

　　2）线程加锁时，将清空工作内存中共享变量的值，从而使用共享变量时需要从主内存中重新获取最新的值

　　　（注意：加锁与解锁需要是同一把锁）

   通过以上两点，可以看到synchronized能够实现可见性。同时，由于synchronized具有同步锁，所以它也具有原子性



还有对于指令重排导致的可见性问题？时指上面的样例2吗？？？？？？？？？/我真的学的挺懵逼的

## 单例模式与指令重排

```java
package singleton;

public class SingletonDemo {
    private static volatile SingletonDemo instance = null;
    private SingletonDemo(){
        System.out.println(Thread.currentThread().getName() +"\t 我是构造方法SingletonDemo()");
    }
    //DCL (Double Check Lock)双端检索机制
    //这个是之前就有讲过的噢，把他比喻成排队买票就可以啦！
    //d但是这个机制不一定线程安全，因为有指令重排序的存在，加入volatile可以禁止指令重排
    //原因在于某一个线程执行到第一行检测，读取到的instance不为null时，
    public static  SingletonDemo getInstance(){
        if(instance == null){
            synchronized (SingletonDemo.class){
                if(instance == null){
                    instance = new SingletonDemo();
                }
            }
        }
        return instance;
    }

    public static void main(String[] args) {

        //单线程(main线程的操作动作)
//        System.out.println(SingletonDemo.getInstance() == SingletonDemo.getInstance());
//        System.out.println(SingletonDemo.getInstance() == SingletonDemo.getInstance());
//        System.out.println(SingletonDemo.getInstance() == SingletonDemo.getInstance());

        //并发多线程后，情况发生了很大的变化
        for (int i = 1; i <= 10; i++) {
            new Thread(()->{
                SingletonDemo.getInstance();
            },String.valueOf(i)).start();
        }
    }
}
```

![image-20210302214224036](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210302214224036.png)

![image-20210302215829929](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210302215829929.png)

操，我不懂，不是加锁了吗？加锁内部不就时单线程吗？但是你出来锁以后可能还会继续执行你在锁里面的代码？所以释放锁的标志到底是什么？

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210303112142354.png" alt="image-20210303112142354" style="zoom:50%;" />

> 我好像懂了，是我被弹幕误导，然后理解错了，那就重新来过把。
>
> 为什么讲到了单例模式？因为这里涉及到了一个因为指令重排而不安全的问题。
>
> 上面的双端模式之前也接触过，也就是懒汉式保证线程安全的一个改进，但是还有不好的地方，因为指令重排，锁里面可以算是单线程，但也会进行指令重排，只要不影响结果，虽然说jmm是这么说，但不代表着他会帮你这么做，所以呢，在创建对象那里，实际上可能执行三行代码，正常情况下先分配空间，初始化一下(我的理解是给你搞个形状出来？)，然后再让instance去等于他，但因为指令重排先让instance去等于他，但是这时候还没初始化好呢，也就是人还没来呢，然后外面的线程遇到`if(instance == null)`,就认为是有了，然后就返回instance，但是这里是有错误的啊！你的instance实际上是没有的，具体后面发生了什么我就不知道了。

[由一个单例模式引发的对指令重排的思考]([(11条消息) 由一个单例模式引发的对指令重排的思考_以码为梦-CSDN博客](https://blog.csdn.net/yuruixin_china/article/details/80550209))

# 19. CAS

![image-20210303212812655](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210303212812655.png)

> CAS 的本质就是 `Compare And Set`,和GitHub遇到冲突的情况很像，先比较你的期望值是不是和实际值一不一样，一样的话就改，不一样的话就不改。

![image-20210303230159444](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210303230159444.png)

![image-20210303230224049](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210303230224049.png)

![image-20210303230256795](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210303230256795.png)

![image-20210303225858511](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210303225858511.png)

感觉基本上就是乐观锁哈

![image-20210304092006520](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210304092006520.png)

而且好像是自旋锁的原理

![image-20210304092431526](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210304092431526.png)

![image-20210304092639134](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210304092639134.png)

## 缺点

1. 如果CAS失败，就会一直尝试，如果CAS长时间一直不成功，可能会给CPU带来很大的开销。
2. 只能保证一个共享变量的原子操作
3. ABA问题(最重要的问题)

关于第二点的理解，我猜的是底层硬件的`getAndAddInt`方法，有点公用的感觉？但我也不确定，所以 一次只能操作一个共享变量，你要操作多个的话就得加锁把

## ABA

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210305204859212.png" alt="image-20210305204859212" style="zoom:67%;" />

![image-20210305204801485](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210305204801485.png)

其实ABA问题不难理解，看第一张图，假设有两个线程，A和B，A可能10s中执行完，B是2s中，其实之前我就对这里有些疑问，因为我一直没考虑到时间的问题，以为会马上执行，但其实内部里的东西我也不是很懂。那这里的情况是B线程快，他们都是操作同一个内存空间，比如原始是A，然后B线程给他改成了B，过了一会又改回A，那A的话就没发现这个改动，不知道，那他以为每人改动过，就把自己的值去update了。但是这个过程是有问题的，实际上还是不安全的

## 解决ABA问题

用版本号就可以了，是真正的乐观锁了


![](https://github.com/Ivy0700/Figurebed/raw/main/img/20210306161511.png)

![](https://Ivy0700.github.io/Figurebed/raw/img/%E5%9B%BE%E7%89%87.jpg)

```html
<img src = "https://github.com/Ivy0700/Figurebed/raw/main/img/20210306161511.png"/>
```

```html

```



