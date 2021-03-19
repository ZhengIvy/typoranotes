# Java 面向对象(OOP)学习笔记

<img src="https://i.loli.net/2020/03/13/VSKHlUGMD6bodtw.png" alt="java" style="zoom:33%;" />

### 一、面向对象的三大特征：封装、继承、多态

#### (1)、封装（Encapsulation）

<img src="https://i.loli.net/2020/03/13/abihm3c4Ktu217A.png" alt="image" style="zoom:50%;" />

> 个人想法：在实践JAVA的过程中，能清楚地感受到与C的不同,首先在于创建一个JAVA文件之后要首先建立一个package，package里面就含有众多类 class，class不能脱离于package存在，class是属于package的一个集合，在这个时候就有些许感受到了类似于”封装”的感觉。
>
> 但是，class与c中的structure 和 c++中的class 很相像，不过在c中，函数与结构体是脱离存在的，像一堆游离的函数和游离的变量，但你需要一个函数使用的时候才会去调用，对于JAVA而言，如上图，就是像是直接有了一个装满函数的包裹，使用对象很明确，包裹将内部的函数都封装了起来。

#### **严谨地讲，封装就是``隐藏实现细节``，仅对外``提供访问接口``，实现细节``部份包装``、``隐藏``起来的方法。**

对于实现一个模块化的东西，而不是像只用一次的程序，具有巨大用处。

````java
public class Human{
			String name;//成员变量有name,weight,age,gender
			int weight;
			int age;
			String gender;
			public Human(String name,int weight,int age,String gender){//一个构造器(constructor)，必须与类同名
				this.age=age;//利用this 给成员变量赋值
				this.gender=gender;
				this.weight=weight;
				this.name=name;
		}
		public void speaking() {
			System.out.println("Hello,my name is "+name);
			System.out.println("My age is "+ age);
			System.out.println("My weight is "+ weight);
			System.out.println("My gender is " + gender);
		}
		public void eating() {//类中的方法method
			System.out.println("I'm eating");
		}
		public void working() {
			System.out.println("I'm working");
		}
````

**封装的思想保证了类内部数据结构的完整性，使用户无法轻易直接操作类的内部数据，这样降低了对内部数据的影响，提高了程序的安全性和可维护性。**

> 就像是一个DVD，遥控器属于在main函数中对类的引用，DVD内部复杂的结构就是封装的结果。

与getter and setter 进行连接



#### (2)、继承(inheritance)

<img src="https://i.loli.net/2020/03/13/E8x1mpgskoDaWf4.png" alt="inheritance" style="zoom:33%;" />

> 人类有分为男女两种生理性别，男和女可以继承人类的特点和功能，但在某些方面也仍存在不同的地方(这部分在接口和多态的地方有更深入的解释)

**继承就是子类继承父类的特征和行为，使得子类对象（实例）具有父类的实例域和方法，或类从父 类继承方法，使得子类具有父类相同的行为。**

```java
public class Female extends Human{//女性是人类的一个子类，子类只能有一个父类，但是子类再往下也有子类，即在这里Female也可以分为不同种类型的Female
	public Female(String name, int weight, int age, String gender) {//继承了人类的特点，名字，体重，年龄等
		super(name, weight, age, gender);
		// TODO Auto-generated constructor stub
	}

	public void dress() {
		System.out.println("I have skirts");
	}
	public void makeup() {
		// TODO Auto-generated method stub
		System.out.println("Female sometimes do makeups");
	}
	public void wakeup() {
		System.out.println("I wake up at 7 a.m every day.");	
	}
}
```

```java
public class Earth {
	public static void main(String[] args) {//在main函数中
		Female Maria = new Female("Maria",50,17,"Female");//在堆上给Female分配内存后 Maria 获得该地址
		Maria.working();
		Maria.dress();
		Maria.speaking();//虽然在Female里面没有speaking这个method 但是由于她继承了人类，所以也可以使用
		Human humanbeing = new Human("Human",70,100,"Female or Male");
		humanbeing.speaking();
        //humanbeing.dress(); 这个是不可以的。
	}	
	
}
//I'm working
//I have skirts
//Hello,my name is Maria
//My age is 17
//My weight is 50
//My gender is Female
//Hello,my name is Human
//My age is 100
//My weight is 70
//My gender is Female or Male
```

#### 关于继承：

* 像上面的例子，Female 和人类有很多共通的特性，如果不使用继承的话，会造成重复的编写，代码共享，减少创建类的工作量，每个子类都拥有父类的方法和属性
* 让类与类之间产生了关系，是多态的前提

感觉动态调度机制可以和继承和多态联系在一起，

#### （3)、多态 (polymorphism)（内含接口和抽象类）

>只是初步理解，如果理解有错误，请指正
>
>我认为多态的来源，因为存在不同，就如上图举的例子，男和女共同继承了人的特性，但是也有不同的地方，因为这世界本就是多态的。子类继承父类，但子类也有属于父类没有的东西。比如说动物类可以分为鸟和鱼，他们有共同的特性，但在行动方式上就是有所不同，那如果在JAVA 里面进行手动添加各个行动方式，就会造成麻烦。但面向对象的目的就是为了减少不必要的麻烦，不要向c中一样对于不同种情况进行switch case。

```java
public class Female extends Human implements Height{//在继承父类的基础上对接口的实现，在实际操作中就避免了手动输入造成的麻烦
	public Female(String name, int weight, int age, String gender) {
		super(name, weight, age, gender);
		// TODO Auto-generated constructor stub
	}
	public void height() {
		// TODO Auto-generated method stub
		System.out.println("The average height is 1.58m.");	
	}
}


public class Male extends Human implements Height {

	public Male(String name, int weight, int age, String gender) {
		super(name, weight, age, gender);
		// TODO Auto-generated constructor stub
	}
    public void height() {
		// TODO Auto-generated method stub
		System.out.println("The average height is 1.69m.");
	}

}
public interface Height {//接口类的多态
	public void height();
}


public class Earth {
	public static void main(String[] args) {
		Female Maria = new Female("Maria",50,17,"Female");
		Maria.height();
		Male Tom = new Male("Tom",60,18,"Male");
		Tom.height();
	}	
}
//The average height is 1.58m.
//The average height is 1.69m.

```

#### 　**接口的特点**

* 接口用关键字interface表示。即interface 接口名 { }
* 类实现接口用implements表示。即class 类名 implements 接口名 { }
*  接口不能实例化。



>接口内的方法是抽象方法，像是一个合同，对于使用接口的就可以签这个合同。
>
>利用接口就可以避免对于不同的特性在继承父类的基础上手动添加的操作。如果这里不使用接口的话，在上图例子身高问题上就要自己进入Female 和Male中手动输入一遍



#### 抽象类

抽象类在一定程度上和接口是有联系的，接口的内的方法是抽象方法，抽象类中的方法也有抽象方法。

> 对于抽象类的更深一步理解，是很看逻辑，
>
> Has is 之间的逻辑，interface 则不这样，感觉强调的是一个功能，has is 更逻辑的感觉

```java

public abstract class Human{//抽象类
	
		public abstract void height();//不可以对抽象的方法进行实例
		public abstract void wakeup();
		}


public class Female extends Human{
	public Female() {
		super();
		// TODO Auto-generated constructor stub
	}

	public void wakeup() {
		System.out.println("I wake up at 7 a.m every day.");

	}
	@Override
	public void height() {
		// TODO Auto-generated method stub
		System.out.println("The average height is 1.58m.");		
	}
}


public class Male extends Human {

	public Male() {
		super();
		// TODO Auto-generated constructor stub
	}
	public void wakeup() {
		// TODO Auto-generated method stub
		System.out.println("I wake up at 10 a.m.");
	}
	public void height() {
		// TODO Auto-generated method stub
		System.out.println("The average height is 1.69m.");
	}
}
```

```java
public class Earth {
	public static void main(String[] args) {
		Human Maria = new Female();//抽象类不可以实例化
		Human Tom = new Male();
		Tom.height();
		Maria.height();
		System.out.println();
		different(Tom);
		different(Maria);
	}	
	public static void different(Human humanbeing) {//可以直接输出两者不同的地方
		humanbeing.wakeup();
		humanbeing.height();
	}
}
//The average height is 1.69m.
//The average height is 1.58m.
//
//I wake up at 10 a.m.
//The average height is 1.69m.
//I wake up at 7 a.m every day.
//The average height is 1.58m.
```

#### 抽象类的特点：

* 如果子类想要继承抽象类，就必须实现抽象类中的所有的抽象方法（在上面的例子中就是Female 和Male 一定要有Human的抽象方法 否则会报错）
* 抽象类是服务类，成员一般使用public或者protected

#### 关于抽象类和接口的区别：

* 一个类可以实现多个接口，但是一个类只能继承一个抽象类
* 接口强调特定功能的实现，而抽象类强调所属关系。
* 接口被用于常用的功能，便于日后维护和添加删除，而抽象类更倾向于充当公共类的角色，不适用于日后重新对立面的代码修改。功能需要累积时用抽象类，不需要累积时用接口。(接口强调的是功能，在上面的两个类中插入功能，虽然抽象类也能实现这一功能，但是设计抽象类会较为复杂)



编译多态和运行多态：前者是重载，后者是重写

### 二、类（内部类、静态类和包含类，ps：抽象类在上面有讲过）

#### 1.内部类

* 定义：定义在其他类内部的类

* 成员内部类的的使用格式:定义在外部类的里边,所以必须通过外部类才能找到内部类

>内部类可以理解为在人类中可以再分一个类器官，也就是人类身体的组成部分。

```java
public  class Human{
		Organ myorgan;//organ 为 Human的内部类
		}
```

```java
public class Organ {
	String name;
	int number;
	public void speaking() {
		System.out.println("I'm organ");
		System.out.println("My name is "+ name);
		System.out.println("The number is "+ number);
	}
}
```

```java
public class Earth {
	public static void main(String[] args) {
	Organ my_organ = new Organ();//从堆上分配内存给物体Organ，my_organ 获得相应的地址
	Human humanbeing = new Human();
	humanbeing.myorgan = my_organ;//内部类myorgan获得my_organ的地址，两者指向同一个物体
	humanbeing.myorgan.name="Lung";
	humanbeing.myorgan.number = 60;
	my_organ.speaking();
	}	
	
}

//I'm organ
//My name is Lung
//The number is 60

```

### 特点：

* 内部类可以达到类似"多重继承"的效果

* 外部类名.内部类名 对象名 = 外部类对象.new 内部类名()



### 2.静态类

```java
public  class Human{
		public static void main(String[] args) {
            Abc.show();//静态类可以直接引用，不用实例化，在程序加载类的字节码的时候就加载到一个静态内存区域里面去了，而且一直在程序运						行中存在，不会随着方法的调用结束而消失
            Abc abc = new Abc();
            abc.number=5;//如果想对number进行定义的话就需要实例化，因为number 是不属于静态的
		}
}

public class Abc{
    int number;// 可以改成 static int number; 
    public static void show(){
        System.out.println("show");
        //改成static int number 之后， 才可以 System.out.println(number);
    }
}
```

#### 特点：

* 静态类实际上是与内部类紧密联系的，静态类不能作为外部类单独存在，必须定义在内部类中，最简单的例子就是main 函数。
* 静态类不需要实例化



#### 3.包含类

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200313174541439.png" alt="image-20200313174541439" style="zoom:50%;" />

与基本类相像，但基本类没有方法与属性，包装类之后就像被封装了一样拥有了方法与属性



#### 三、面向过程和面向对象的区别

| 面向对象                                                     | 面向过程                                           |
| ------------------------------------------------------------ | -------------------------------------------------- |
| 与数据打交道，当遇到一个数据需要功能去解决时，可以直接使用已知的方法 | 与算法打交道，当遇到一个问题的时候用自己的算法去算 |
| 程序是由对象组成的                                           | 程序是由函数组成的                                 |
| 安全性比较高                                                 | 安全性较低                                         |
| JAVA                                                         | C                                                  |



#### 四、Java 和C的联系与区别

##### 联系：

* 从c到学Java，我认为Java是基于c的，c中的函数功能没有像Java那么强大，像c中要用的很多功能都得自己写，像求数组长度，输出数组等等。但Java 就不一样了，像扔了块资源包一样，要啥有啥，不用自己去写需要用到的功能，好比说洗衣服，java像一个洗衣机，c就是自己手洗。

##### 区别

| c                        |             java             |
| ------------------------ | :--------------------------: |
| 面向过程                 |           面向对象           |
| 注重算法                 |          不注重算法          |
| 速度较快                 |           速度较慢           |
| 通用性更差               | 通用性更好，可以在多平台实现 |
| 在堆上的数据需要手动释放 | 有垃圾回收机制，不用手动释放 |
| 有指针                   |           没有指针           |





