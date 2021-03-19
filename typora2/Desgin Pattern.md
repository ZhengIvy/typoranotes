## 设计模式

> 前言是我真的无语了被自己，觉得自己很傻逼，没有去关注到这些东西，所以现在我要练习改代码，把模式学会后，看下可以用在哪些方面然后进行改代码

### 1. Strategy Pattern + Factory Pattern

> 简而言之呢，就是这时候需要用到

**定义一系列的算法**,**把每一个算法封装起来, 并且使它们可相互替换**

策略模式把对象本身和运算规则区分开来，因此我们整个模式也分为三个部分。

环境类(Context):用来操作策略的上下文环境，也就是我们游客。抽象策略类(Strategy):策略的抽象，出行方式的抽象具体策略类(ConcreteStrategy):具体的策略实现，每一种出行方式的具体实现。

策略模式实际上是会和工厂模式结合起来的，因为你需要从别人那里获得相应的type，object所以就是需要的哈。



emem现在目前获得的信息是在用计算价格，用优惠券那里比较实用，目前对我的登录系统代码好像没有什么用，

![image-20200424162734480](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200424162734480.png)

![image-20200424162750996](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200424162750996.png)

![image-20200424162801020](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200424162801020.png)

![image-20200424162809281](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200424162809281.png)

![image-20200424162815169](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200424162815169.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200424162847321.png" alt="image-20200424162847321" style="zoom:33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200424162828845.png" alt="image-20200424162821741" style="zoom:33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200424162903831.png" alt="image-20200424162903831" style="zoom:33%;" />



![image-20200427123723667](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200427123723667.png)

应该是明白了，context 还是必要 的，减少代码的改变	

```java
public class Factory {
    private static Map<String, Fruit> fruitMap = new HashMap<>();
    static {

        fruitMap.put("apple", new Apple());

        fruitMap.put("banana", new Banana());

        fruitMap.put("watermelon", new Watermelon());

    }
    public static Fruit getFruit(String fruitType) {

        return fruitMap.get(fruitType);
    }
}
```

使用map 这个是目前比较容易理解的一个，无语兜兜转转竟然还是回到了这里，真的无语哈。

is that neccessary?

```java
public class Context {
    private Fruit fruit;

    public Context(Fruit fruit){
        this.fruit = fruit;
    }

    public String executeStrategy(){
        return fruit.eat();
    }
}
```

```java
public class StrategyPattern {
    public static void main(String[] args) {
        //这一部是工厂来的
        Fruit fruit = Factory.getFruit("apple");
        Context context = new Context(fruit);
        System.out.println(context.executeStrategy());
    }
}
```

暂时是这样子的。工厂类+策略类的结合，等等看下有没有那个的。我好像不是很明白的一点是为什么有 creator的接口，怎么说呢，我这里有product的接口，但是没有creator 因为我是把creator混在了一起，也可以把这个factory搞成一个abstract class 然后的gettype变成abstract ，接着就可以用一些特殊的在里面，但我这里没有是因为好像不需要哈，后面要再看吧，大概差不多是这样吧我觉得，那种abstract的话，我现在不知道能不能用到，先这样

![image-20200425074938015](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200425074938015.png)，



## 2. Observer Pattern



![image-20200425080817085](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200425080817085.png)



![image-20200425080822479](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200425080822479.png)



![image-20200425080827646](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200425080827646.png)

![image-20200425080833529](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200425080833529.png)

![image-20200425080839044](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200425080839044.png)

![image-20200425080844303](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200425080844303.png)

![image-20200425080850204](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200425080850204.png)

![image-20200425080855863](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200425080855863.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200425080902488.png" alt="image-20200425080902488" style="zoom:33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200425080912535.png" alt="image-20200425080912535" style="zoom:33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200425080919919.png" alt="image-20200425080919919" style="zoom:33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200425081001309.png" alt="image-20200425081001309" style="zoom:33%;" />

说实话，目前能想到利用这个的地方是做聊天区功能的时候，没错，聊天区哈，

<img src="D:\tim\1097641461\FileRecv\MobileFile\IMG_4643.PNG" alt="IMG_4643" style="zoom:33%;" />

### 3.适配器模式

、适配器模式应用场景



类适配器与对象适配器的使用场景一致，仅仅是实现手段稍有区别，二者主要用于如下场景：



　　**（1）想要使用一个已经存在的类，但是它却不符合现有的接口规范，导致无法直接去访问，这时创建一个适配器就能间接去访问这个类中的方法。**

> 我觉得这个我还是经常遇到的。可以考虑一下，后面做的时候再来



　　（2）我们有一个类，想将其设计为可重用的类（可被多处访问），我们可以创建适配器来将这个类来适配其他没有提供合适接口的类。



　　以上两个场景其实就是从两个角度来描述一类问题，那就是要访问的方法不在合适的接口里，一个从接口出发（被访问），一个从访问出发（主动访问）。



接口适配器使用场景：



　　（1）想要使用接口中的某个或某些方法，但是接口中有太多方法，我们要使用时必须实现接口并实现其中的所有方法，可以使用抽象类来实现接口，并不对方法进行实现（仅置空），然后我们再继承这个抽象类来通过重写想用的方法的方式来实现。这个抽象类就是适配器。





总而言之，就是关于不同adapter的问题，刚刚看哪个视频的话对具体应用不是很清楚，但现在应该了解差不多了，就是你需要一个Target，换成什接口，需要一个adapter 一个adaptee 前者是你要转换的，后者是你自己，差不多就是这样，了解了比较简单的例子，还需要别的东西哈

![IMG_4646](D:\tim\1097641461\FileRecv\MobileFile\IMG_4646.PNG)

![IMG_4645](D:\tim\1097641461\FileRecv\MobileFile\IMG_4645.PNG)

![IMG_4644](D:\tim\1097641461\FileRecv\MobileFile\IMG_4644.PNG)

## 4.装饰器模式

他说他并不推荐当物体仅有

properties的区别时，在这里就是价格区别时，并不推荐，用的有些浪费了，比较推荐时是behavior的不同，不然就感觉没啥用哈。  

  ![IMG_4888](D:\tim\1097641461\FileRecv\MobileFile\IMG_4888.PNG)



![IMG_4889](D:\tim\1097641461\FileRecv\MobileFile\IMG_4889.PNG)



![IMG_4890](D:\tim\1097641461\FileRecv\MobileFile\IMG_4890.PNG)





![IMG_4906](D:\tim\1097641461\FileRecv\MobileFile\IMG_4906.PNG)



![IMG_4907](D:\tim\1097641461\FileRecv\MobileFile\IMG_4907.PNG)





![IMG_4908](D:\tim\1097641461\FileRecv\MobileFile\IMG_4908.PNG)





![IMG_4909](D:\tim\1097641461\FileRecv\MobileFile\IMG_4909.PNG)







## 5.单例模式



![IMG_4913](D:\tim\1097641461\FileRecv\MobileFile\IMG_4913.PNG)





![IMG_4914](D:\tim\1097641461\FileRecv\MobileFile\IMG_4914.PNG)





![IMG_4915](D:\tim\1097641461\FileRecv\MobileFile\IMG_4915.PNG)

## 6.命令模式

是什么东西呢？他首先是拿了一个遥控器去举的例子，就是你那种遥控器按不同的按钮去控制开关的那种，那里面的封装到底是怎么样的呢，他说的是有一层封装，还有一层queue？？不过也当然是queue？ 但是do 和undo 指的是什么？

我好像没get到，看看后面能不能想起来

![IMG_5001](D:\tim\1097641461\FileRecv\MobileFile\IMG_5001.PNG)

这里的invoker就是遥控器，receiver 就是灯啦，还有个command 的interface，里面有execute 和unexecute 就是 执行和不执行的意思吧。怎么说呢，因为一般遥控器上面的开关是共用的，所以我觉得按的时候会去判断状态然后去搞，我猜是这样哈

![IMG_5002](D:\tim\1097641461\FileRecv\MobileFile\IMG_5002.PNG)

invoker 和 receiver 我觉得都不需要interface 因为说实话也没啥共用的地方，除非有些产品上类型差不多，但是总的来说觉得是不需要的把



![IMG_5003](D:\tim\1097641461\FileRecv\MobileFile\IMG_5003.PNG)

然后ICommand 这里的话的类都是一些具体的，比如说lighton command呀，lightdown command 这种，然后这个command 需要一个构造器，去传一个东西进去，

```java
class LightOnCommand implements Command{
    Light light;
	LightOnCommand(Light light) {
        this.light = light;
    }
    public execute(){
        this.light.on();
    }
    public unexcute(){
        this.light.off();// 怎么说呢，我觉得，这里要么写on 要么写off，但具体的东西呢，可能要交到另外一个地方去判断。emem 让我想想哈，可能在灯内部自行判断是有的。
}
}


```

这样子，然后就会去调用



![IMG_5004](D:\tim\1097641461\FileRecv\MobileFile\IMG_5004.PNG)





![IMG_5005](D:\tim\1097641461\FileRecv\MobileFile\IMG_5005.PNG)





![IMG_5006](D:\tim\1097641461\FileRecv\MobileFile\IMG_5006.PNG)





![IMG_5008](D:\tim\1097641461\FileRecv\MobileFile\IMG_5008.PNG)

```java
class light{
    ICommand on;
    ICommand off;
    ICommand up;
    ICommand down;
    
    light(ICommand on, ICommand off, ICommand up, ICommand down){
        this.on = on;
        this.off = off;
        this.up = up;
        this.down = down;
    }
    
    public void clickOn(){
        this.on.execute();
    }
    public void clickOff(){
        this.on.unexecute();
    }
}
```

emem，差不多是这样了，其他的例子我后面再去举例子哈





## 6.外观模式

![IMG_5009](D:\tim\1097641461\FileRecv\MobileFile\IMG_5009.PNG)



![IMG_5010](D:\tim\1097641461\FileRecv\MobileFile\IMG_5010.PNG)

你怎么理解这玩意呢。就是内部很复杂，比如说一栋房子里面的东西的线路很复杂，但是为了解耦啊，你可以自己内部设计好这玩意。。emme 我tmd 怎么感觉是那个遥控器，你内部很复杂，你已经设计好，然后你这个外观直接就给别人用就好了，给client端用ok哈。

怎么说呢，这些东西后面 学完框架回来是要继续看的，因为懂，但是完全不懂用





## 7.代理模式



![IMG_5011](D:\tim\1097641461\FileRecv\MobileFile\IMG_5011.PNG)





![IMG_5012](D:\tim\1097641461\FileRecv\MobileFile\IMG_5012.PNG)





![IMG_5013](D:\tim\1097641461\FileRecv\MobileFile\IMG_5013.PNG)





![IMG_5014](D:\tim\1097641461\FileRecv\MobileFile\IMG_5014.PNG)





![IMG_5015](D:\tim\1097641461\FileRecv\MobileFile\IMG_5015.PNG)





![IMG_5016](D:\tim\1097641461\FileRecv\MobileFile\IMG_5016.PNG)



![IMG_5017](D:\tim\1097641461\FileRecv\MobileFile\IMG_5017.PNG)

但是他讲的还是不够详细把。