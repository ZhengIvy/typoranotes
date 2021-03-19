## spring概念

![image-20200810155300630](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200810155300630.png)



> class a中使用class b 的属性或方法，叫作class a 依赖class b，和maven的依赖不一样哈

![image-20200810160939645](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200810160939645.png)

## ioc

![image-20200810161514241](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200810161514241.png)

> IoC（Inversion of Control）:控制反转，是一个理论，概念，思想，把对象的创建，赋值，管理工作都交给代码之外的容器实现，也就是对象的创建是由其他外部的资源完成
>
> 控制：创建对象，对象的属性赋值，对象之间的关系管理。
>
> 反转：把原来的开发人员管理，创建对象的权限转移给代码之外的容器实现，由容器代替开			发人员管理对象，创建对象，给属性赋值
>
> 正转：由开发人员在代码中，使用new构造方法，创建对象，开发人员主动管理对象。
>
> ​			`Student student = new Student();//在代码中，创建对象--正转`	
>
> 容器：是一个服务器软件，一个框架(spring)
>
> 为什么使用ioc：目的就是减少对代码的改动，也能实现不同的功能，实现解耦合。
>
> java中创建对象有哪些方式：
>
> 1. 构造方法，new Student()
> 2. 反射
> 3. 序列化
> 4. 克隆？？
> 5. ioc：容器创建对象
>
> ioc的体现：servlet:
>
> 1. 创建类继承`HttpServlet`
>
> 2. 在`web.xml`注册servlet,使用<servlet-name>myservlet</servlet-name>
>
>    ​											<servlet-class>com.zbr.controller.MyServlet</servlet-class>
>
> 3. 没有创建Servlet对象，没有 `MyServlet myservlet = new MyServlet();`
>
> 4. Servlet是Tomcat服务器他能帮你创建的，Tomcat 也被称为容器
>
>    Tomcat作为容器：里面存放的由Servlet对象，Listener，Filter对象

### ioc的技术实现

> DI是ioc的技术实现 ，DI：依赖注入，`Dependency Injection`,只需要在程序中提供要使用的对象的名称就可以了，至于对象如何在容器中创建，赋值，查找都由容器内部实现。
>
> spring是使用di实现ioc的功能，spring底层创建对象，使用的是反射机制

实现步骤：

1. 创建maven项目

2. 加入maven的依赖

   spring的依赖，版本5.2.5版本

   junit依赖 

3. 创建类（接口和他的实现类）

   和没有使用框架一样，就是普通的类

4. 创建spring需要使用的配置文件

   声明类的信息，这些类由spring的创建和管理

5. 测试spring创建的对象

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200810234552780.png" alt="image-20200810234552780" style="zoom:67%;" />

> 这个xml不是简单的xml
>
> <img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200810234618308.png" alt="image-20200810234618308" style="zoom:67%;" />
>
> 的spring Config

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">
<!--

告诉spring创建对象
声明bean，就是告诉spring要创建某个类的对象
id：对象的自定义名称，唯一值。spring通过这个名称来找到这个对象
class：类的全限定名称(不能是接口，因为spring是反射机制创建对象，必须使用类)

spring就完成 SomeService someService = new ServiceImpl();
spring是创建好的对象放到map中，spring框架中有一个map存放对象。
    springMap.put(id的值，对象);
    例如 springMap.put("someService", new SomeServiceImpl());
一个bean标签声明一个对象。
-->
    <bean id="someService" class="com.zbr.service.impl.SomeServiceImpl"/>

<!--
    spring能创建一个非自定义类的对象吗，创建一个存在的某个类的对象
-->
    <bean id="mydate" class="java.util.Date"/>
</beans>
<!--
    spring的配置文件
    1.beans：是根标签，spring把java对象成为bean。
    2.spring-beans.xsd 是约束文件，和mybatis指定 dtd是一样的。

-->
```

```java
public interface SomeService {
    void doSome();
}

public class SomeServiceImpl implements SomeService {
    @Override
    public void doSome() {
        System.out.println("执行SomeServiceImpl的doSome方法");
    }

    public SomeServiceImpl() {
        System.out.println("SomeServiceImpl的无参方法");
    }
}


public class MyTest {

    @Test
    public void test01(){
        SomeService service = new SomeServiceImpl();
        service.doSome();
    }

    /**
     * spring默认创建对象的时间：在创建spring的容器时，会创建配置文件中的所有的对象
     * spring创建对象：默认调用的是无参构造方法
     */
    @Test
    public void test2(){
        //使用spring容器创建的对象
        //1.指定spring配置文件的名称
        String config = "beans.xml";
        //2.创建表示spring容器的对象,ApplicationContext
        //ApplicationContext 就是表示Spring容器，通过容器对象获取对象了
        //ClassPathXmlApplicationContext: 表示从类路径中加载spring的配置文件

        ApplicationContext ac = new ClassPathXmlApplicationContext(config);

        //从容器中获取某个对象，你要调用对象的方法
        //getBean("配置文件中的bean的id值")
        SomeService service = (SomeService) ac.getBean("someService");

        //使用spring创建好的对象那个
        service.doSome();
    }
    /*
    获取spring容器中java对象中的信息
     */
    @Test
    public void test03(){
        String config = "beans.xml";
        ApplicationContext ac = new ClassPathXmlApplicationContext(config);
        //使用spring中提供的方法，获取容器中定义的对象的数量
        int nums = ac.getBeanDefinitionCount();
        System.out.println(nums);
        //容器中每个定义对象的名称
        String[] names = ac.getBeanDefinitionNames();
        for(String name: names){
            System.out.println(name);
        }
    }

    /**
     * 获取一个非自定义类对象
     */
    @Test
    public void test04(){
        String config = "beans.xml";
        ApplicationContext ac = new ClassPathXmlApplicationContext(config);
       //使用getBean();
        Date my = (Date) ac.getBean("mydate");
        System.out.println(my);
    }
}

```









![image-20200810190612655](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200810190612655.png)

常用的实现类

### 给java对象赋值

>di:依赖注入，表示创建对象，给属性赋值
>
>di的实现有两种：
>
>1. 在spring的配置文件中，使用标签和属性完成，叫做基于XML的di实现
>2. 使用spring中的注解，完成属性赋值，叫做基于注解的di实现
>
>di的语法分类：
>
>1. set注入(设置注入)：spring调用类的set方法，在set方法可以实现属性的赋值
>
>   80左右都是使用set注入,注意要有set方法
>
>2. 构造注入，spring调用类的有参数构造方法，创建对象。在构造方法中完成赋值。

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
<!--
 声明Student 对象
 注入：就是赋值的意思
 简单类型：spring中规定java的基本数据类型和字符串都是简单类型
 di:给属性赋值
 1. set注入(设置注入)：spring调用类的set方法，你可以在set中完成方法的属性赋值
    1）简单类型的set注入
        <bean id="xx" class="yyy">
            <property name="属性赋值" value="此属性的值">
            一个property只能给一个属性赋值
            <property.....>
        </bean>
        还有一点发现没这里无论是int还是String类型都要有""，这是本身xml文件规定的
-->
    <bean id="myStudent" class="com.zbr.ba01.Student">
        <property name="name" value="李四"/><!--setName("李四") -->
        <property name="age" value="20"/><!--setAge(21) -->
<!--        在这里面没有email这个属性照样能执行，因为本质还是调用set的方法-->
        <property name="email" value="lisi@qq.com"/>
    </bean>
</beans>
```

> 其他的就没写，主要是这个比较重要和关键

#### 引用类型的set注入

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
<!--
 声明Student 对象
 注入：就是赋值的意思
 简单类型：spring中规定java的基本数据类型和字符串都是简单类型
 di:给属性赋值
 1. set注入(设置注入)：spring调用类的set方法，你可以在set中完成方法的属性赋值
    1）简单类型的set注入
        <bean id="xx" class="yyy">
            <property name="属性赋值" value="此属性的值">
            一个property只能给一个属性赋值
            <property.....>
        </bean>
        还有一点发现没这里无论是int还是String类型都要有""，这是本身xml文件规定的

    2) 引用类型的set注入：spring调用累的set方法
        <bean id="xxx" class="yyy">
            <property name ="属性名称" ref="bean的id(对象的名称)">
        </bean>
-->
    <bean id="myStudent" class="com.zbr.ba02.Student">
        <property name="name" value="李四"/><!--setName("李四") -->
        <property name="age" value="20"/><!--setAge(21) -->
<!--        引用类型-->
        <property name="school" ref="mySchool"/><!--setSchool(mySchool) -->

    </bean>

<!--    声明School对象-->
    <bean id="mySchool" class="com.zbr.ba02.School">
        <property name="name" value="北京大学"/>
        <property name="address" value="北京的海淀区"/>
    </bean>
</beans>
```

这个也没多大区别，也是差不多这么用

### 构造注入

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
<!--
 声明Student 对象
 注入：就是赋值的意思
 简单类型：spring中规定java的基本数据类型和字符串都是简单类型
 di:给属性赋值
 1. set注入(设置注入)：spring调用类的set方法，你可以在set中完成方法的属性赋值
    1）简单类型的set注入
        <bean id="xx" class="yyy">
            <property name="属性赋值" value="此属性的值">
            一个property只能给一个属性赋值
            <property.....>
        </bean>
        还有一点发现没这里无论是int还是String类型都要有""，这是本身xml文件规定的

    2) 引用类型的set注入：spring调用累的set方法
        <bean id="xxx" class="yyy">
            <property name ="属性名称" ref="bean的id(对象的名称)">
        </bean>

 2.构造注入：spring调用类有参数构造方法，在创建对象的同时，在构造方法中给属性赋值
    构造注入使用<constructor-arg>标签
    <constructor-arg> 标签：一个<constructor-arg>表示构造一个参数
    <constructor-arg> 标签属性：
        name:表示构造方法的形参名
        index:表示构造方法的参数的位置,参数从左往右，0,1,2的顺序
        value：构造方法的形参类型是简单类型，使用value
        ref：构造方法的形参类型是引用类型的，使用ref

-->
<!--    使用name属性实现构造注入-->
    <bean id="myStudent" class="com.zbr.ba03.Student">
        <constructor-arg name="myname" value="张三"/>
        <constructor-arg name="myage" value="20"/>
        <constructor-arg name="myschool" ref="mySchool"/>


    </bean>
<!--    使用index属性-->
    <bean id="myStudent2" class="com.zbr.ba03.Student">
        <constructor-arg index="0" value="李四"/>
        <constructor-arg index="1" value="26"/>
        <constructor-arg index="2" ref="mySchool"/>
    </bean>

<!--    声明School对象-->
    <bean id="mySchool" class="com.zbr.ba03.School">
        <property name="name" value="清华大学"/>
        <property name="address" value="北京的海淀区"/>
    </bean>
</beans>
```

推荐构造注入的第一种方法，可读性更高

### idea扫描xml中的bean

```html
<<bean id="myStudent" class="com.zbr.ba02.Student">
        <property name="name" value="李四"/><!--setName("李四") -->
        <property name="age" value="20"/><!--setAge(21) -->
<!--        引用类型-->
        <property name="school" ref="mySchool"/><!--setSchool(mySchool) -->
    </bean>

<bean id="mySchool" class="com.zbr.ba03.School">
        <property name="name" value="北京大学"/>
        <property name="address" value="北京的海淀区"/>
    </bean>
```

> 可能会想这样子`School`的类的创建应该在Student前面把，不然的话不会报错吗，不会的，因为会多次扫描创建对象，第一次把能创建的都创建了，不行的话再扫描一遍进行创建

![image-20200811115629534](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200811115629534.png)

![image-20200811120059835](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200811120059835.png)

![image-20200811120249717](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200811120249717.png)

> 刚刚还讲到一个东西，我觉得是在说明用spring创建对象的好处的。比如说你做项目的时候换了数据库，换成了oracle，这时候你用到的daoImpl 就改变了，如果你还是原来那样创建对象的话，那你基本上有多少个service就要改多少次，就很麻烦，用了spring就不会了，只改变一次创建的daoImpl的对象就可以了

### 自动注入

```html
<!--
    引用类型的自动注入：spring框架根据某些规则可以给引用类型赋值不用你再赋值了
    使用的规则常用的是byName，byType
    1.byName（按名称注入）：java类中引用类型的属性名和spring容器中的（配置文件）<bean>的id名称一样，
                          且数据类型是一致的，这样容器中的bean，spring能够赋值给引用类型
    语法：
    <bean id="xx" class="yyy" autowire="byName">
        简单类型属性赋值
    </bean>


    2.byType(按类型注入): java类引用类型的数据类型和spring容器中(配置文件中)<bean>的class属性是同源关系的，
        这样的bean能够赋值给引用类型
      同源就是一类的意思：
      1.java类中引用类型的数据类型和bean的class值是一样的
      2.java类中引用类型的数据类型和bean的class值是父子类关系的
      3.java类中引用类型的数据类型和bean的class值的是接口和实现类关系的
      <bean id="xx" class="yyy" autowire="byType">
        简单类型属性赋值
    </bean>

    注意：在byType中，在xml配置文件中声明bean只能有一个符合条件的，
        多余一个是错误的

-->
```

2020.8.12补充：

今天测试了一下，用byName使用接口和实现类也是可以的，但是当时视频里没强调同源的关系是因为？类型的话才讲同源吧，byName的话完全就是根据你个人指定的，在能够使用的情况下你想赋给谁就赋给谁

#### byName

```html
 <bean id="myStudent" class="com.zbr.ba04.Student" autowire="byName">
        <property name="name" value="李四"/><!--setName("李四") -->
        <property name="age" value="20"/><!--setAge(21) -->
<!--        引用类型-->
<!--        <property name="school" ref="mySchool"/>&lt;!&ndash;setSchool(mySchool) &ndash;&gt;-->

    </bean>
```

#### byType

```html
 <bean id="myStudent" class="com.zbr.ba05.Student" autowire="byType">
        <property name="name" value="张三"/>
        <property name="age" value="20"/><!--setAge(21) -->
<!--        引用类型-->
<!--        <property name="school" ref="mySchool"/>&lt;!&ndash;setSchool(mySchool) &ndash;&gt;-->

    </bean>
```

> 其实都不难，不过要注意一下限定条件罢了

### 多个配置优势

1. 每个文件的大小比一个文件要小很多。效率高
2. 避免多人竞争带来的冲突

如果你的项目有多个模块(相关的功能在一起)，一个模块一个配置文件

学生考勤模块一个配置文件，张三

学生成绩一个配置文件，      李四

多文件的分配方式

1. 按功能模块，一个模块一个配置文件
2. 按类的功能，数据库相关的配置一个文件，做事务的功能一个配置文件，做service功能一个配置文件等

![image-20200811190503872](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200811190503872.png)

total.xml

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

<!--
    包含关系的配置文件:
    spring-total 表示主配置文件：包含其他的配置文件，主配置文件一般是不定义对象的
    语法：<import resource="其他配置文件的路径"/>
    关键字："classpath:"表示类路径(class文件所在的文件),
    在spring的配置文件中要指定其他文件的位置，
    需要使用classpath，告诉spring到哪去加载读取文件
-->
<!--    加载的是文件列表-->
<!--    <import resource="classpath:ba06/spring-school.xml"/>-->
<!--    <import resource="classpath:ba06/spring-student.xml"/>-->

<!--
    在包含关系的配置文件中，可以通配符：(*:表示任意字符)
    注意：主配置文件名称不能包含在通配符的范围内(不能叫做spring-total.xml)陷入死循环
-->
    <import resource="classpath:ba06/spring-*.xml"/>
</beans>
```

spring-student.xml

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
<!--
    student模块所有bean的声明，
    -->
    <bean id="myStudent" class="com.zbr.ba06.Student" autowire="byType">
        <property name="name" value="张三"/>
        <property name="age" value="30"/><!--setAge(21) -->
<!--        引用类型-->
<!--        <property name="school" ref="mySchool"/>&lt;!&ndash;setSchool(mySchool) &ndash;&gt;-->

    </bean>

</beans>
```

spring-school.xml

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
<!--
    School模块所有的声明,School模块的配置文件
-->

<bean id="mySchool" class="com.zbr.ba06.School">
    <property name="address" value="北京市海淀区"/>
    <property name="name" value="航空大学"/>
</bean>

```

### 指定多种包的方式

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
         https://www.springframework.org/schema/context/spring-context.xsd">
<!--    声明组件扫描器(component-scan),组件就是java对象
        base-package：指定注解在你的项目中的包名
        component-scan工作方式：spring会扫描遍历base-package指定的包，
        把包中和子包中的所有类，找到类中的注解，按照注解的功能创建对象或给属性赋值

        加入了component-scan标签，配置文件的变化：
        1.加入一个新的约束文件，spring-context.xsd
        2.给这个新的约束文件起个命名空间的名称
-->
<!--    <context:component-scan base-package="com.zbr.ba01"/>-->

<!--    指定多个包的三种方式-->
<!--    第一种方式：使用多次组件扫描器，指定不同的包-->
<!--    <context:component-scan base-package="com.zbr.ba02"/>-->

<!--    第二种方式：使用分隔符(;或,)-->
<!--    <context:component-scan base-package="com.zbr.ba01;com.zbr.ba02"/>-->
<!--    第三种方式：指定父包-->
<!--    <context:component-scan base-package="com.zbr"/>-->
<!--    不建议直接com，效率低-->
</beans>
```





### 注解赋值

>基于注解的di：通过注解完成java对象创建，属性赋值。代替xml文件
>
>使用注解的步骤：
>
>1. 加入maven的依赖 spring-context,在你加入spring-context的同时，间接加入spring-aop的依赖，使用注解必须使用spring-aop依赖
>2. 在类中加入spring的注解(多个不同功能的注解
>3. 在spring的配置文件中，加入一个组件扫描器的标签，说明注解在你的项目中的位置
>4. 使用注解创建对象，创建容器ApplicationContext
>
>学习的注解：
>
>1. `@Component`
>2. `@Respository`
>3. `@Service`
>4. `@Controller`
>5. `@Value`
>6. `@Autowired`
>7. `@Resource`

1. `@Component`

   ```java
   /*
    *   @Component:创建对象的，等同于<bean>的功能
    *      属性：value：就是对象的名称，也就是bean的id值
    *          value的值是唯一的，创建的对象在整个spring的容器中就一个
    *      位置：在类的上面
    *
    * @Component(value = "myStudent")等同于
    * <bean id="myStudent" class="com.zbr.ba01.Student"/>
    *
    * spring中和@Component功能一致，创建对象的注解还有：
    * 1.@Repository(用在持久层类的上面):放在dao的实现类，表示创建dao对象，dao对象是能够访问数据库的。
    * 2.@Service(用在业务层类的上面):放在service的实现类上面
    *                              创建service对象是做业务处理的，可以由事务等功能
    * 3.@Controller(用在控制器上面)：放在可能感知器(处理器)类的上面，创建控制器对象的，
    *                              控制器对象，能够接受用户提交的参数，显示请求的处理结果。
    * 以上三个注解的使用语法和@Component一样的，都能创建对象，但是这三个注解还有额外的功能。
    * 是给项目的对象分层的。
    * 基本功能一致，但是那三个还有角色的体现。
    * 怎么判断什么时候用Component？ 不是以上三个的话就可能可以用
    */
   //使用value属性，指定对象名称
   //@Component(value = "myStudent")
   @Component("myStudent")
   
   //不指定对象名称，由spring提供默认名称:类名的首字母小写
   //@Component
   public class Student {
   
       private String name;
       private Integer age;
   
       public Student() {
           System.out.println("student无参数构造方法");
       }
   
       public void setName(String name) {
           this.name = name;
       }
   
       public void setAge(Integer age) {
           this.age = age;
       }
   
       @Override
       public String toString() {
           return "Student{" +
                   "name='" + name + '\'' +
                   ", age=" + age +
                   '}';
       }
   }
   
   
   
   @Component("myStudent")
   public class Student {
       /*简单类型的属性赋值
           属性：value是String类型的，表示简单类型的属性值
           位置:1. 在属性定义的上面，无需set方法，推荐使用
               2.在set方法上面
        */
   
       @Value(value = "张飞")
       private String name;
       @Value(value = "29")
       private Integer age;
   
       public Student() {
           System.out.println("student无参数构造方法");
       }
   //
   //    @Value(value = "张飞") 第二种
   //    public void setName(String name) {
   //        this.name = name;
   //    }
   //
   //    public void setAge(Integer age) {
   //        this.age = age;
   //    }
   ```

   > 总的来说，创建对象的时候还是使用到map，跟上面bean讲过的一样哈

   真正的赋值来了，引用类型

   #### 1.@Autowired

   ```java
   /*    引用类型
           @Autowired:spring框架提供的注解，实现引用类型的赋值。
           spring中通过注解给引用类型赋值，使用的是自动注入原理，支持byName,byType
           @Autowired:默认使用的是byType自动注入
   
           位置：1.在属性定义的上面，无需set方法，推荐使用
                2.在set方法上面
    */
   
       @Autowired
       private School school;
   ```

   #### 2.@Qualifier

   ```java
   /*  
   如果要使用byName的方式，需要做的是：
           1.在属性上面加入@Autowired
           2.在属性上面加入@Qulifier(value="bean的id")：表示使用指定名称的bean完成赋值
    */
   
   //  byName自动注入
       @Autowired
       @Qualifier("mySchool")
       private School school;
   ```

   #### 4.@Autowired的required属性

   ```java
   /*    引用类型
           @Autowired:spring框架提供的注解，实现引用类型的赋值。
           spring中通过注解给引用类型赋值，使用的是自动注入原理，支持byName,byType
           @Autowired:默认使用的是byType自动注入
   
           属性：required,是一个boolean类型的，默认true
               required=true:表示说引用类型赋值失败，程序报错，并终止执行
               required=false:引用类型如果赋值失败，程序正常执行，引用类型是null
           位置：1.在属性定义的上面，无需set方法，推荐使用
                2.在set方法上面
   
           如果要使用byName的方式，需要做的是：
           1.在属性上面加入@Autowired
           2.在属性上面加入@Qulifier(value="bean的id")：表示使用指定名称的bean完成赋值
    */
   
   //  byName自动注入
       @Autowired(required = false)
       @Qualifier("mySchool")
       private School school;
   ```

   一般使用true把，毕竟能报错提醒呀

   

   #### 5.@Resource

   注意这个是jdk的，用之前要导个annotation的包

   ```java
   /*    引用类型
           @Resource:来自jdk中的注解，spring框架提供了对这个注解的功能支持，可以使用给引用类型赋值
           使用的也是自动注入的原理，支持byName，byType，默认是byName
   
         位置：1.在属性定义的上面，无需set方法，推荐使用
               2.在set方法上面
   
    */
   
   //  默认是byName：先使用byName自动注入，如果byName赋值失败，再使用byType
       @Resource
       private School school;
   ```

   #### 6.@Resource只使用byName

   ```java
   /*    引用类型
           @Resource:来自jdk中的注解，spring框架提供了对这个注解的功能支持，可以使用给引用类型赋值
           使用的也是自动注入的原理，支持byName，byType，默认是byName
   
         位置：1.在属性定义的上面，无需set方法，推荐使用
               2.在set方法上面
           @Resource只使用byName方式，需要增加一个属性name
           name的值是bean的id(名称)
    */
   
   //  只使用name
       @Resource(name = "mySchool")
       private School school;
   ```

   

   

![image-20200812161350854](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200812161350854.png)

### 注解 好还是xml好？

> 看情况，但大部分情况下还是选择注解，注解使用在不经常变化的情况下，xml如果属性值经常变则推荐使用。
>
> 还有一种是可以在注解中使用`${}`，这个我还真的不怎么了解，我对这个仅限在xml文件中，如果要这么使用的话要把属性放在`properties`文件中，再在xml中引入properties.

![image-20200812171911040](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200812171911040.png)

![image-20200812172237224](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200812172237224.png)

![image-20200812172600398](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200812172600398.png)

### 在UserService中使用需要注意的一点

`UserService`会用到`UserDao`去通过持久层来访问数据库，那这时候的如果直接用`Autowired`的话就默认使用`byType`了，但问题是，你的`UserDao`往往对应多个`UserDaoImpl`，那用哪个？所以得改为`byName`的。

所以在这里我也产生了一个疑问，之前说byName不是要数据类型相同的吗？ 这时候又？？？？？？？？？？？

## 动态代理

> 动态代理：在程序的执行过程中，创建代理对象。
>
> 通过代理对象执行方法，给目标类的方法增加额外的功能(功能增强)
>
> jdk动态代理的实现步骤：
>
> 1. 创建目标类，`SomeServiceImpl`目标类，给他的`doSome,doOther`增加输出时间，事务、
> 2. 创建`InvocationHandler`接口的实现类，在这个类实现给目标方法增加功能。
> 3. 使用jdk中类proxy，创建代理对象，实现创建对象的能力 

这里先写了个例子引入aop，想不改变源代码的情况下，在该方法实现的前面和后面添加功能

```java
public interface SomeService {

    void doSome();
    void doOther();
}

public class SomeServiceImpl implements SomeService {
    @Override
    public void doSome() {
//        ServiceTools.doLog();
        System.out.println("业务方法doSome");
//        ServiceTools.doTrans();
    }

    @Override
    public void doOther() {
//        ServiceTools.doLog();
        System.out.println("业务方法doOther");
//        ServiceTools.doTrans();
    }
}

```



```java
public class MyInvocationHandler implements InvocationHandler {
   //目标对象
    //SomeServiceImpl
    private Object target;

    public MyInvocationHandler(Object target) {
        this.target = target;
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        //通过代理对象执行方法时，会调用执行这个invoke()
        System.out.println("执行InvocationHandler中的invoke()");
        String methodName = method.getName();
        System.out.println("method名称:"+methodName);
        Object res = null;

        if("doSome".equals(methodName)){
            ServiceTools.doLog();
            //执行目标类的方法，通过Method类实现
            //SomeServiceImpl.doSome()
            res = method.invoke(target,args);
            ServiceTools.doTrans();
        }else {
            //SomeServiceImpl.doOther();
            res = method.invoke(target,args);
        }
        return res;
    }
}


public class ServiceTools {
    public static void doLog(){
        System.out.println("非业务方法执行时间:"+ new Date());

    }

    public static void doTrans(){
        System.out.println("非业务方法，方法执行完毕后，提交事务");
    }
}

```

```java
/**
 * 这里的要求是doSome()方法显示时间和事务提交
 * 而doOther()没有以上两个功能
 */
public class MyApp {
    public static void main(String[] args) {
//        //调用doSome，doOther
//        SomeService service = new SomeServiceImpl();
//        service.doSome();
//        System.out.println("=================");
//        service.doOther();
        //使用jdk的Proxy创建代理对象
        //创建目标对象
        SomeService target = new SomeServiceImpl();

        //创建InvocationHandler对象
        InvocationHandler handler = new MyInvocationHandler(target);

        //使用Proxy创建代理
        SomeService proxy = (SomeService) Proxy.newProxyInstance(target.getClass().getClassLoader(),
                target.getClass().getInterfaces(), handler);

        //通过代理执行方法，会调用handler中的invoke()
        proxy.doSome();
        System.out.println("==============");
        proxy.doOther();
    }
}
```





## aop

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200812235716471.png" alt="image-20200812235716471" style="zoom:67%;" />

>1. jdk代理上面讲过了，这里讲cglib
>
>2. cglib动态代理：第三方工具库，创建代理对象，原理是继承，通过继承目标类，创建子类，子类就是代理对象，要求目标类不能是final的，方法也不能是final的
>
>3. aop：面向切面变成，基于动态代理，可以使用jdk，cglib两种代理方式
>
>4. aop就是动态代理的规范化，把动态代理实现的步骤，方式都定义好了，让开发人员用一种统一的方式，就用动态代理
>
>5. AOP(Aspect Orient Programming):面向切面编程
>
>  Aspect:切面，给你的目标类增加的功能，就是切面，像上面用的日志，事务都是切面
>
>  ​			切面的特点：一般都是非业务方法，独立使用的
>
>  Orient：面向，对着
>
>  Programming:编程
>
>  怎么理解面向切面编程？
>
>  1. 需要在分析项目功能时，找出切面
>  2. 合理的安排切面的执行时间(在目标方法前，还是在目标方法后)
>  3. 合理的安全切面执行的位置，在哪个类，哪个方法增加增强的功能
>
>  术语：
>
>  1. Aspect:切面，表示增强的功能，就是一堆代码，完成某个一个功能。非业务功能，常见的切面功能有日志，事务，统计信息，参数检查，权限验证
>  2. `JoinPoint`:连接点，连接(目标类中的)业务方法和切面的位置，就是某类中的业务方法(我觉得是`InvocationalHandler`里面的，在上面的例子就是那个if判断，将业务方法(目标类中的)和切面连接了)
>  3. `Pointcut`:切入点，指多个连接点方法的集合。多个方法
>  4. 目标对象：给哪个类的方法增加功能，这个类就是目标对象
>  5. Advice：通知，通知表示切面功能执行的时间。(方法之前还是之后)
>
>  说一个切面有三个关键的要素
>
>  1. 切面的功能代码，切面干什么
>
>  2. 切面的执行位置，使用PointCut表示切面的执行的位置
>
>  3. 切面执行时间，时间用Advice表示
>
>     实际上就是 what where when
>
>6. aop的实现
>
>  aop是一个规范，是一个动态的一个规范化，一个标准
>
>  aop的技术实现框架：
>
>  1. spring：spring在内部实现了aop规范，能做aop的工作
>
>     ​			spring主要在事务处理时使用aop
>
>     ​			我们项目开发中很少使用spring的aop实现，因为spring的aop比较笨重
>
>  2. aspectJ:一个开源的专门做aop的框架。spring框架中继承了aspectj框架，通过spring就能使用aspectj的功能。
>
>     aspectJ框架实现aop有两种方式：
>
>     1. 使用xml的配置文件：配置全局事务
>     2. 使用注解，我们在项目中要做aop功能，一般都使用注解，aspectj有5个注解
>
>3. 学习aspectj框架的使用
>
>   - 切面的执行时间，执行时间在规范中叫做`Advice(通知，增强)`
>
>   在aspectj框架中使用注解表示。也可以使用xml配置文件中的标签
>
>   1. `@Before`
>   2. `@AfterReturning`
>   3. `@Around`
>   4. `@AfterThrowing`
>   5. `@After`
>
>   - 表示切面执行的位置，使用的是切入点表达式
>
>   - ![image-20200813115800715](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200813115800715.png)
>
>     ​	最常用的就是中间标红的两种，黑的是可以省略的
>
>     ![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200813120904730.png)
>
>     ![image-20200813122344915](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200813122344915.png)
>
>     ![image-20200813123418806](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200813123418806.png)
>
>     ![image-20200813123455680](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200813123455680.png)

使用aspectj实现aop基本步骤

1. 新建maven项目

2. 加入依赖

   - spring依赖
   - aspectj依赖
   - junit单元测试

3. 创建目标类：接口和他的实现类。

   要做的是给类中的方法增加功能

4. 创建切面类：普通类

   1. 在类的上面加入`@Aspect`

   2. 在类中定义方法，方法就是切面要执行的功能代码

      在方法的上面加入aspectj中的通知注解，例如`@Before`

      还需要指定切入点表达式`execution()`

5. 创建spring的配置文件：声明对象，把对象交给容器统一管理

   声明对象可以使用注解或者xml配置文件<bean>

   1. 声明目标类对象

   2. 声明切面类对象

   3. 声明aspectj框架中的自动代理生成器标签

      自动代理生成器，用来完成代理对象的自动创建功能的

6. 创建测试类，从spring容器中获取目标对象(实际就是代理对象)

   通过代理执行方法，实现aop的功能增强

![image-20200813234305874](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200813234305874.png)

![image-20200814003950656](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200814003950656.png)

### @Before

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200814184904681.png" alt="image-20200814184904681" style="zoom:67%;" />

`applicationContext.xml`

这个后面不写了，都是一样的，改下包名就好了

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/aop https://www.springframework.org/schema/aop/spring-aop.xsd">
<!--把对象交给spring容器，由spring容器统一创建，管理对象-->
<!--    声明目标对象-->
    <bean id="someService" class="com.zbr.ba08.SomeServiceImpl"/>

<!--    声明切面对象-->
    <bean id="myAspect" class="com.zbr.ba08.MyAspect"/>

<!--    声明自动代理生成器:使用aspectj框架内部的功能，创建目标对象的代理对象。
        创建代理对象是在内存中 实现的，修改目标对象的内存中的结构，创建为代理对象
        所以目标对象就是被修改后的代理对象

        aspectj-autoproxy:会把spring容器中的所有的目标对象，一次性都生成代理对象
-->
<!--    <aop:aspectj-autoproxy/>--> 一般是用用这个
<!--
    如果你期望目标类有接口，使用cglib代理
    proxy-target-class="true":告诉框架，要使用cglib动态代理
-->
    <aop:aspectj-autoproxy proxy-target-class="true"/>
</beans>
```



```java
/*
这里的注解我按视频的方法用不了，另外上网从查的
 */
/*
@Aspect:是aspectj框架中的注解。
作用：表示当前类时切面类
切面类：是用来给业务方法增加功能的类，在这个类中有切面的功能代码
位置：在类定义的上面
 */
@Aspect
public class MyAspect {
    /*
    定义方法，方法是实现切面功能的。
    方法的定义要求：
    1. 公共方法 public
    2.方法没有返回值
    3.方法名称自定义
    4.方法可以有参数，也可以没有参数
        如果有参数，参数不是自定义的，有几个参数类型可以使用
     */

    /**
     * @Before:前置通知注解
     *  属性：value，是切入点表达式，表示切面的功能执行的位置
     *  位置：在方法的上面
     * 特点：
     * 1.在目标方法之前先执行的
     * 2.不会改变目标的执行结果
     * 3.不会影响目标方法的执行
     */
//    @Before(value = "execution(public void com.zbr.ba01.SomeServiceImpl.doSome(String, Integer))")
//    public void myBefore(){
//        //就是你切面要执行的功能代码
//        System.out.println("前置通知，切面功能：在目标方法之前输出执行时间："+new Date());
//    }
    //如果写错了参数类型，只是找不到罢了，并不会报错
//    @Before(value = "execution(public void com.zbr.ba01.SomeServiceImpl.doSome(Integer))")
//    public void myBefore(){
//        //就是你切面要执行的功能代码
//        System.out.println("前置通知，切面功能：在目标方法之前输出执行时间："+new Date());
//    }

//    @Before(value = "execution(void com.zbr.ba01.SomeServiceImpl.doSome(String, Integer))")
//    public void myBefore(){
//        //就是你切面要执行的功能代码
//        System.out.println("1=========前置通知，切面功能：在目标方法之前输出执行时间："+new Date());
//    }
//    @Before(value = "execution(void *..SomeServiceImpl.doSome(String, Integer))")
//    public void myBefore(){
//        //就是你切面要执行的功能代码
//        System.out.println("2=========前置通知，切面功能：在目标方法之前输出执行时间："+new Date());
//    }
//    @Before(value = "execution(* *..SomeServiceImpl.doSome(..))")
//    public void myBefore(){
//        //就是你切面要执行的功能代码
//        System.out.println("3=========前置通知，切面功能：在目标方法之前输出执行时间："+new Date());
//    }
    /*
    指定通知方法中的参数:JoinPoint
    JoinPoint:业务方法，要加入切面功能的业务方法(我觉得意思是对这个业务方法进行的操作来获取信息)
        作用是：可以在通知方法中获取方法执行时的信息，例如方法名称，方法的实参
        如果你的切面功能中需要用到方法的信息，就加入JoinPoint
        这个JoinPoint参数的值是由框架赋予，必须是第一个位置的参数

     */
    @Before(value = "execution(public void com.zbr.ba01.SomeServiceImpl.doSome(String, Integer))")
    public void myBefore(JoinPoint jp){
       //获取方法的完整定义
        //方法的签名(定义)=void com.zbr.ba01.SomeService.doSome(String,Integer)
        System.out.println("方法的签名(定义)="+jp.getSignature());
        System.out.println("方法的名称="+jp.getSignature().getName());
        //获取方法的实参
        //参数=lisi
        //参数=20
        Object[] args = jp.getArgs();
        for(Object arg :args){
            System.out.println("参数="+arg);
        }
        //就是你切面要执行的功能代码
        System.out.println("前置通知，切面功能：在目标方法之前输出执行时间："+new Date());
    }
}

```

```java
public interface SomeService {

    void doSome(String name,Integer age);
}

//目标类
public class SomeServiceImpl implements SomeService {

    @Override
    public void doSome(String name, Integer age) {
        //给doSome方法增加功能，在doSome()执行之前，输出方法的执行时间
        System.out.println("===目标方法doSome()===");
    }
}

```

测试类

```java
public class MyTest01 {

    @Test
    public void test01(){
        String config = "applicationContext.xml";
        ApplicationContext ctx  = new ClassPathXmlApplicationContext(config);
        //从容器中获取目标对象
        SomeService proxy = (SomeService) ctx.getBean("someService");
        //com.sun.proxy.$Proxy10:jdk动态代理
        System.out.println("proxy:"+ proxy.getClass().getName());
        //通过代理的对象执行方法，实现目标方法执行时，增强了功能
        proxy.doSome("lisi",20);
    }
}

```

### @AfterReturning

```java
/*
这里的注解我按视频的方法用不了，另外上网从查的
 */
/*
@Aspect:是aspectj框架中的注解。
作用：表示当前类时切面类
切面类：是用来给业务方法增加功能的类，在这个类中有切面的功能代码
位置：在类定义的上面
 */
@Aspect
public class MyAspect {
    /*
    后置通知定义方法，方法是实现切面功能的。
    方法的定义要求：
    1. 公共方法 public
    2.方法没有返回值
    3.方法名称自定义
    4.方法有参数的,推荐使用Object，参数名自定义
     */

    /**
     *
     * @AfterReturning:后置通知
     *  属性：1.value 切入点表达式
     *       2.returning 自定义的变量，表示目标方法返回值
     *       自定义变量名必须和通知方法的形参名一样
     *  位置：在方法定义的上面
     *  特点：
     *      1.目标方法之后执行的
     *      2.可以获取目标方法的返回值，可以根据返回值做不同处理功能
     *      Object res = doOther();
     *      3.可以修改这个返回值
     *
     *    后置通知的执行
     *    Object res =  doOther();
     *    myAfterReturning (res);
     */
    @AfterReturning(value = "execution(* *..SomeServiceImpl.doOther(..))",
                    returning = "res")
    public void myAfterReturning(JoinPoint jp,Object res){
        //注意上面的参数，JointPoint必须在第一个哈
        //Object res:是目标方法执行后的返回值，根据返回值做你的切面的功能处理
        System.out.println("后置通知，方法定义"+jp.getSignature());
        System.out.println("后置通知：在目标方法之后执行，获取的返回值是"+res);
        if(res.equals("abcd")){
        //做一些功能
        }else{
            //做其他功能
        }

        //修改目标方法的返回值，看一下是否会影响，最后的方法调用结果
        if(res != null){
            res = "Hello Aspectj";
        }
    }


    @AfterReturning(value = "execution(* *..SomeServiceImpl.doOther2(..))",
            returning = "res")
    public void myAfterReturning2(Object res){
        //Object res:是目标方法执行后的返回值，根据返回值做你的切面的功能处理
        System.out.println("后置通知：在目标方法之后执行，获取的返回值是"+res);
        if(res.equals("abcd")){
            //做一些功能
        }else{
            //做其他功能
        }

        //修改目标方法的返回值，看一下是否会影响，最后的方法调用结果
       //如果修改res的内容，属性值等，是不是会影响最后的调用结果呢
        Student student = (Student) res;
        student.setAge(21);
    }
}

```

```java
public interface SomeService {

    void doSome(String name, Integer age);
    String doOther(String name,Integer age);

    Student doOther2(String name, Integer age);
}


//目标类
public class SomeServiceImpl implements SomeService {

    @Override
    public void doSome(String name, Integer age) {
        //给doSome方法增加功能，在doSome()执行之前，输出方法的执行时间
        System.out.println("===目标方法doSome()===");
    }

    @Override
    public String doOther(String name, Integer age) {
        System.out.println("===目标方法doOther()===");
        String str = new String("abcd");
        return str;
    }

    @Override
    public Student doOther2(String name, Integer age) {
        Student student = new Student();
        student.setName("lisi");
        student.setAge(20);
        return student;
    }
}


public class Student
{

    private String name;
    private int age;

    public void setEmail(String email){
        System.out.println("setEmail="+email);
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }


}

```

测试类

```java
public class MyTest02 {

    @Test
    public void test01(){
        String config = "applicationContext.xml";
        ApplicationContext ctx  = new ClassPathXmlApplicationContext(config);
        //从容器中获取目标对象
        SomeService proxy = (SomeService) ctx.getBean("someService");

        //通过代理的对象执行方法，实现目标方法执行时，增强了功能
        String str = proxy.doOther("zs", 29);
        System.out.println("str===="+str);
    }

    @Test
    public void test02(){
        String config = "applicationContext.xml";
        ApplicationContext ctx  = new ClassPathXmlApplicationContext(config);
        //从容器中获取目标对象
        SomeService proxy = (SomeService) ctx.getBean("someService");

        //通过代理的对象执行方法，实现目标方法执行时，增强了功能
        Student student = proxy.doOther2("zs", 20);
        //改变了，因为传的是地址
        System.out.println(student);

    }
}

```

### @Around

```java
@Aspect
public class MyAspect {
    /*
    环绕通知方法定义格式
        1.public
        2.必须有一个返回值，推荐使用Object类型
        3.方法名称自定义
        4.方法有参数，固定的参数ProceedingJointPoint
     */

    /**
     * @Around:环绕通知
     *  属性：value 切入点表达式
     *  位置：在方法的定义上面
     *
     * 特点：
     *  1.它是功能最强的通知
     *  2.在目标方法的前和后都能增强功能、
     *  3.控制目标方法是否被调用执行
     *  4.修改原来的目标方法的执行结果，影响最后的调用结果
     *
     *  环绕通知，等同于jdk动态代理，InvocationHandler 接口(那不就是前两个通知的结合？ 但是的话这个可以控制方法执行，还是有些不一样哈)
     *  参数：ProceedingJoinPoint 等同于jdk中的Method
     *        作用：执行目标方法的
     *  返回值：就是目标方法的执行结果，可以被修改
     *
     *  环绕通知：经常做事务，在目标方法之前开启事务，执行目标方法，在目标方法之后提交事务
     */
    @Around(value = "execution(* *..SomeServiceImpl.doFirst(..))")
    public Object myAround(ProceedingJoinPoint pjp) throws Throwable {
        String name = "";
        //获取第一个参数值
        Object[] args = pjp.getArgs();
        if(args!= null && args.length > 1){
            Object arg = args[0];
            name = (String) arg;
        }
        //实现环绕通知
        System.out.println("环绕通知：在目标方法之前，输出时间："+ new Date());
        Object result = null;
        //1.目标方法的调用,method.invoke();
        if("zhangsan".equals(name)){
            //符合条件，调用目标方法
            result = pjp.proceed();
        }

        System.out.println("环绕通知，在目标方法之后，提交事务");

        //2.在目标方法的前或者后加入功能

        //修改目标方法的执行结果，影响方法最后的调用结果
        if(result != null){
            result = "Hello Aspectj AOP";
        }
        return result;
    }
}

```

```java
public interface SomeService {

    void doSome(String name, Integer age);
    String doOther(String name, Integer age);

   String doFirst(String name,Integer age);
}


//目标类
public class SomeServiceImpl implements SomeService {

    @Override
    public void doSome(String name, Integer age) {
        //给doSome方法增加功能，在doSome()执行之前，输出方法的执行时间
        System.out.println("===目标方法doSome()===");
    }

    @Override
    public String doOther(String name, Integer age) {
        System.out.println("===目标方法doOther()===");
        String str = new String("abcd");
        return str;
    }

    @Override
    public String doFirst(String name, Integer age) {
        System.out.println("====业务方法doFirst()====");
        return "doFirst";
    }


}

```

测试类

```java
public class MyTest03 {

    @Test
    public void test01(){
        String config = "applicationContext.xml";
        ApplicationContext ctx  = new ClassPathXmlApplicationContext(config);
        //从容器中获取目标对象
        SomeService proxy = (SomeService) ctx.getBean("someService");

        //通过代理的对象执行方法，实现目标方法执行时，增强了功能
        //myAround()
        String str = proxy.doFirst("zhangsan", 20);
        System.out.println("str===="+str);
    }

}
```

### @AfterThrowing

```java
@Aspect
public class MyAspect {
    /*
    异常通知方法定义格式
        1.public
        2.没有返回值
        3.方法名称自定义
        4.方法可以有一个参数Exception，如果还有，就是JointPoint
     */

    /**
     * @AfterThrowing:异常通知
     *      属性：1.value 切入点表达式
     *           2.throwing 自定义变量，表示目标方法抛出的异常对象
     *              变量名必须和方法的参数名一样
     *
     *  特点：
     *      1.在目标方法抛出异常时执行的
     *      2.可以做异常的监控程序，监控目标方法执行时是不是有异常
     *          如果有异常，可以发送短信，邮件进行通知
     *      执行：
     *      try{
     *          SomeServiceImpl.doSecond(..)
     *
     *      }catch(Exception e){
     *          myAfterThrowing(e);
     *      }
     * @param ex
     */
    @AfterThrowing(value = "execution(* *..SomeServiceImpl.doSecond(..))",
            throwing ="ex" )
    public void myAfterThrowing(Exception ex){
        System.out.println("异常通知：方法发生异常时执行："+ ex.getMessage());
        //发送短信，邮件通知开发人员
    }
}

```

```java
public interface SomeService {

    void doSome(String name, Integer age);
    String doOther(String name, Integer age);

   String doFirst(String name, Integer age);

   void doSecond();
}


//目标类
public class SomeServiceImpl implements SomeService {

    @Override
    public void doSome(String name, Integer age) {
        //给doSome方法增加功能，在doSome()执行之前，输出方法的执行时间
        System.out.println("===目标方法doSome()===");
    }

    @Override
    public String doOther(String name, Integer age) {
        System.out.println("===目标方法doOther()===");
        String str = new String("abcd");
        return str;
    }

    @Override
    public String doFirst(String name, Integer age) {
        System.out.println("====业务方法doFirst()====");
        return "doFirst";
    }

    @Override
    public void doSecond() {
        System.out.println("执行业务方法doSecond()"+(10/0));
    }


}

```

测试类

```java
public class MyTest04 {

    @Test
    public void test01(){
        String config = "applicationContext.xml";
        ApplicationContext ctx  = new ClassPathXmlApplicationContext(config);
        //从容器中获取目标对象
        SomeService proxy = (SomeService) ctx.getBean("someService");

        //通过代理的对象执行方法，实现目标方法执行时，增强了功能
        proxy.doSecond();

    }


}

```

### @After

```java
@Aspect
public class MyAspect {
    /*
    最终通知方法定义格式
        1.public
        2.没有返回值
        3.方法名称自定义
        4.方法没有参数，如果有，就是JointPoint
     */


    /**
     * @After:最终通知
     *      属性：value 切点表达式
     *      位置：在 方法上面
     * 特点：
     *      1.总是会执行
     *      2.在目标方法之后执行的
     *
     *      try{
     *          SomeServiceImpl.doThird(..)
     *      }catch(Exception e){
     *
     *      }finally{
     *          myAfter();
     *      }
     *
     */
    @After(value = "execution(* *..SomeServiceImpl.doThird(..))")
    public void myAfter(){
        System.out.println("执行最终通知，总是会被执行的代码");
        //一般做资源清除工作的

    }
}

```

```java
public interface SomeService {

    void doSome(String name, Integer age);
    String doOther(String name, Integer age);

   String doFirst(String name, Integer age);

   void doSecond();

   void doThird();
}

//目标类
public class SomeServiceImpl implements SomeService {

    @Override
    public void doSome(String name, Integer age) {
        //给doSome方法增加功能，在doSome()执行之前，输出方法的执行时间
        System.out.println("===目标方法doSome()===");
    }

    @Override
    public String doOther(String name, Integer age) {
        System.out.println("===目标方法doOther()===");
        String str = new String("abcd");
        return str;
    }

    @Override
    public String doFirst(String name, Integer age) {
        System.out.println("====业务方法doFirst()====");
        return "doFirst";
    }

    @Override
    public void doSecond() {
        System.out.println("执行业务方法doSecond()"+(10/0));
    }

    @Override
    public void doThird() {
        System.out.println("执行业务方法doThird()"+(10/0));

    }


}

```

```java
public class MyTest05 {

    @Test
    public void test01(){
        String config = "applicationContext.xml";
        ApplicationContext ctx  = new ClassPathXmlApplicationContext(config);
        //从容器中获取目标对象
        SomeService proxy = (SomeService) ctx.getBean("someService");

        //通过代理的对象执行方法，实现目标方法执行时，增强了功能
       proxy.doThird();

    }


}

```

### @PointCut

```java
@Aspect
public class MyAspect {

    @After(value = "mypt()")
    public void myAfter(){
        System.out.println("执行最终通知，总是会被执行的代码");
        //一般做资源清除工作的

    }
    @Before(value = "mypt()")
    public void myBefore(){
        System.out.println("前置通知，在目标方法前面执行的");

    }
    /**
     * @PointCut:定义和管理切入点，如果你的项目有多个切入点表达式是重复的，可以复用的。
     *              可以使用@PointCut
     *     属性：value 切入点表达式
     *     位置：在自定义的方法上面
     *  特点：
     *      当使用@PointCut定义在一个方法的上面，此时这个方法的名称就是切入点表达式的别名
     *      其他的通知中，value属性就可以使用这个方法名称，代替切入点表达式了
     */
    @Pointcut(value = "execution(* *..SomeServiceImpl.doThird(..))")
    private void mypt(){
        //无需代码
    }
}

```

```java
public interface SomeService {

    void doSome(String name, Integer age);
    String doOther(String name, Integer age);

   String doFirst(String name, Integer age);

   void doSecond();

   void doThird();
}


//目标类
public class SomeServiceImpl implements SomeService {

    @Override
    public void doSome(String name, Integer age) {
        //给doSome方法增加功能，在doSome()执行之前，输出方法的执行时间
        System.out.println("===目标方法doSome()===");
    }

    @Override
    public String doOther(String name, Integer age) {
        System.out.println("===目标方法doOther()===");
        String str = new String("abcd");
        return str;
    }

    @Override
    public String doFirst(String name, Integer age) {
        System.out.println("====业务方法doFirst()====");
        return "doFirst";
    }

    @Override
    public void doSecond() {
        System.out.println("执行业务方法doSecond()"+(10/0));
    }

    @Override
    public void doThird() {
        System.out.println("执行业务方法doThird()");

    }


}

```

```java
public class MyTest06 {

    @Test
    public void test01(){
        String config = "applicationContext.xml";
        ApplicationContext ctx  = new ClassPathXmlApplicationContext(config);
        //从容器中获取目标对象
        SomeService proxy = (SomeService) ctx.getBean("someService");

        //通过代理的对象执行方法，实现目标方法执行时，增强了功能
       proxy.doThird();
    }
}
\
```

### cglib代理

当去掉接口的时候，框架默认使用cglib代理

如果存在接口还想使用cglib的话需要在配置文件中设置

```html
<!--
    如果你期望目标类有接口，使用cglib代理
    proxy-target-class="true":告诉框架，要使用cglib动态代理
-->
    <aop:aspectj-autoproxy proxy-target-class="true"/>
```

```java
public class MyTest07 {

    @Test
    public void test01(){
        String config = "applicationContext.xml";
        ApplicationContext ctx  = new ClassPathXmlApplicationContext(config);
        //从容器中获取目标对象
        SomeServiceImpl proxy = (SomeServiceImpl) ctx.getBean("someService");
        /**
         * 目标类没有接口，使用cglib动态代理，spring框架会自动应用cglib
         * com.zbr.ba07.SomeServiceImpl$$EnhancerBySpringCGLIB$$ece8bea0
         */
        System.out.println("proxy:"+proxy.getClass().getName());
        //通过代理的对象执行方法，实现目标方法执行时，增强了功能
       proxy.doThird();

    }


}



```

![image-20200815120100915](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200815120100915.png)

--------------------------------------------------------------------------------------------anki在这-------------------------------------------------------------------

## spring的ioc与mybatis的集成

### 简介：

> 为什么ioc？ 能把mybatis和sprin集成在一起，像一个框架，是因为ioc能创建对象。
>
> 可以把mybatis中的对象交给spring统一管理，开发人员从spring中获取对象。开发人员就不用同时面对两个或多个框架，就面对一个spring
>
> mybatis使用步骤，对象
>
> 1. 定义dao接口，`StudentDao`
>
> 2. 定义mapper文件，`StudentDao.xml`
>
> 3. 定义mybatis的主配置文件 `mybatis.xml`
>
> 4. 创建dao的代理对象，`StudentDao studentDao = SqlSession.getMapper(StudengtDao.class)`
>
>    `List<Student> students = dao.selectStudents();`
>
> 要使用dao对象，需要使用`getMapper()方法`，怎么能使用`getMapper()方法，需要哪些条件`
>
> 1. 获取`SqlSession`对象，需要使用`SqlSessionFactory的openSession()方法`
>
> 2. 创建`SqlSessionFactory对象`。通过读取mybatis的主配置文件，能创建`SqlSessionFactory`对象
>
>    
>
>    我们会使用独立的连接池类替换mybatis默认自己有的，把连接池类也交给spring创建
>
> 主配置文件：
>
> 1. 数据库信息，后面项目的时候把他写到properties文件中去了
> 2. mapper文件的位置

通过以上说明，需要spring创建以下对象

1. 独立的连接池对象，使用阿里的druid连接池
2. `SqlSessionFactory对象`
3. 创建出dao对象

需要学习的就是三个对象创建语法，使用xml的bean标签（因为我们之前学过的`@Component`创建对象，是自定义的，直接在类上面加注解，然后配置文件扫描创建ok，但是你这个类都是凭空出现的啊，所以暂且用bean）

### 步骤：

1. 新建maven项目
2. 加入maven依赖
   1. spring依赖
   2. mybatis依赖
   3. mysql驱动
   4. spring的事物的依赖
   5. mybatis和spring集成的依赖：mybatis官方提供的，用来spring项目中创建mybatis的`SqlSessionFactory,dao对象`
3. 创建实体类
4. 创建dao接口和mapper文件
5. 创建mybatis主配置文件
6. 创建Service的接口和实现类，属性是dao
7. 创建spring的配置文件：声明mybatis的对象就给spring创建
   1. 数据源DataSource（数据库的相关信息？）
   2. `SqlSessionFactory`
   3. dao对象
   4. 声明自定义的service
8. 创建测试类，获取Service对象，通过Service调用dao完成数据库的访问

#### pom依赖

```html
<dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>5.2.5.RELEASE</version>
    </dependency>
<!--    做spring事务用到的-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-tx</artifactId>
      <version>5.2.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>5.2.5.RELEASE</version>
    </dependency>
<!--    mybatis依赖-->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.5.1</version>
    </dependency>
<!--    mybatis和spring集成的依赖-->
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>1.3.1</version>
    </dependency>
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.19</version>
    </dependency>
<!--    阿里公司的数据库连接池-->
    <!-- https://mvnrepository.com/artifact/com.alibaba/druid -->
    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>druid</artifactId>
      <version>1.1.23</version>
    </dependency>

  </dependencies>
```

#### resources

applicationContext.xml

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
<!--
    把数据库的配置信息，写在一个独立的文件，编译修改数据库的配置内容
    spring知道jdbc.properties文件的位置
-->
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <!--    声明数据源DataSource，作用是连接数据库的-->

    <bean id="myDataSource" class="com.alibaba.druid.pool.DruidDataSource" init-method="init"
          destroy-method="close">
<!--        set注入给DruidDataSource提供数据库信息-->
<!--
            使用属性配置文件中的数据，语法是${key}
-->
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
<!--            <property name="url" value="jdbc:mysql://localhost:3306/ssm?serverTimezone=GMT%2B8"/>-->
<!--            <property name="username" value="root"/>-->
<!--            <property name="password" value="123456"/>-->
        <property name="maxActive" value="${jdbc.max}"/>
     </bean>

<!--    声明的是mybatis中提供的SqlSessionFactoryBean类，这个类内部创建SqlSessionFactory
-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
<!--        set注入，把数据库连接池赋给了dataSource-->
        <property name="dataSource" ref="myDataSource"/>
<!--
    mybatis主配置文件的位置
        configLocation是Resource类型，读取配置文件
        它的配置，使用value，指定文件路径，使用classpath：表示文件的位置
-->


        <property name="configLocation" value="classpath:mybatis.xml"/>
    </bean>

<!--    创建dao对象，使用SqlSession的getMapper(StudentDao.class)
        MapperScannerConfigurer:在内部调用getMapper()生成每个dao接口的代理对象
-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
<!--        指定SqlSessionFactory对象的id-->
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
<!--        指定包名，包名是dao接口所在的包名
            MapperScannerConfigurer会扫描这个包中的所有接口，把每个接口都执行
            一次getMapper()方法，得到每个接口的dao对象。
            创建好的dao对象放入到spring容器中的. dao对象的默认名称是接口首字母小写(感觉跟resultType那里别名直接用类名表示差不多，也是直接变小写(不确定是不是这里))
            两个包之间可以打逗号
-->
        <property name="basePackage" value="com.zbr.dao"/>

    </bean>

    <bean id="studentService" class="com.zbr.service.Impl.StudentServiceImpl">
        <property name="studentDao" ref="studentDao"/>
    </bean>
</beans>
```

本来数据库都是写在mybatis中的，但是mybatis和spring集成了，因为要创建数据源对象，要创建对象，就需要在spring中创建，所以这里需要使用配置文件一起创建了数据源对象，那用来干什么呢？回想之前用mybatis，数据源相当数据库的连接了，你对应的dao有sql语句了，那你需要东西在代码中去把这些联系起来，这时候你需要`SqlSession对象`去获取接口对象(通过动态代理)进而去调你要使用的方法，这时候就需要我们去创建`SqlSession`对象，用注解不会创建，所以写到bean中来了，`SqlSession`对象需要数据源，所以他两一起写这了，而且`SqlSession`在mybatis中不仅要读取数据源，而且要看映射了哪些dao，就哪些dao可以通过这个对象对数据库进行操作，所以`SqlSession`创建的时候需要两个属性，而且呢创建的是`SqlSessionFactory`哦，想想吼，`SqlSession`的时候已经可以获取对象了，所以获取数据的操作应该是`Factory`操作的。

我们已经知道`SqlSession`是可以获取接口的dao对象的，但这时候我们连`SqlSessionFactory`都是bean创建的，肯定触碰不了代码，那你怎么拿到dao对象呢？这时候就需要一个`MapperScannerConfigurer`,这时候dao对象被扫描到就自动创建了，由于Service中的属性有dao，那直接`ref`一下就好啦。

其他的东西都差不多一样，我直接上测试类，主要就是在配置文件这里搞





mybatis.xml

```html
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>


    <settings>
        <!--        设置mybatis输出日志-->
        <setting name="logImpl" value="STDOUT_LOGGING"/>
    </settings>
<!--    设置别名-->
    <typeAliases>
<!--        name:实体类所在的包名 -->
        <package name="com.zbr.domain"/>
    </typeAliases>
    <mappers>
        <!--
    一个mapper标签指定一个文件的位置，
       从类路径开始的路径信息。 target/classes(类路径)
-->
        <package name="com.zbr.dao"/>
<!--        <mapper resource=""/>-->

    </mappers>
</configuration>
```

jdbc.properties

```
jdbc.url=jdbc:mysql://localhost:3306/ssm?serverTimezone=GMT%2B8
jdbc.username=root
jdbc.password=123456
jdbc.max=20
```

#### dao

```java
public interface StudentDao {

    int insertStudent(Student student);
    List<Student> selectStudents();
}
```

StudentDao.xml

```html
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.zbr.dao.StudentDao">
    <insert id="insertStudent">
        insert into student values (#{id},#{name},#{email},#{age})
    </insert>
    <select id="selectStudents" resultType="com.zbr.domain.Student">
        select * from student order by id desc
    </select>
</mapper>
```

#### domain

```java
public class Student {
    //属性名和列名一样
    private Integer id;
    private String name;
    private String email;
    private Integer age;


    public Student() {
    }

    public Student(Integer id,String name,String email,Integer age){
        this.id = id;
        this.name = name;
        this.email = email;
        this.age = age;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public Integer getAge() {
        return age;
    }

    public void setAge(Integer age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Student{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", email='" + email + '\'' +
                ", age=" + age +
                '}';
    }
}
```

#### Service

```java
public interface StudentService {

    int addStudent(Student student);
    List<Student> queryStudents();
}
```

Impl

```java
public class StudentServiceImpl implements StudentService {

    //引用类型
    private StudentDao studentDao;

    //使用set注入赋值
    public void setStudentDao(StudentDao studentDao) {
        this.studentDao = studentDao;
    }

    @Override
    public int addStudent(Student student) {
        int nums = studentDao.insertStudent(student);
        return nums;
    }

    @Override
    public List<Student> queryStudents() {
        List<Student> students = studentDao.selectStudents();
        return students;
    }
}
```

## spring事务

1. 什么事务

   讲mysql的时候，提出了事务，事务是指一组sql语句的集合，集合中有多条sql语句，可能是insert，update，select，delete，我们希望这些多个sql语句都能成功，或者都失败，这些sql语句的执行时一致的，作为一个整体执行

2. 什么时候想到使用事务

   当我操作涉及到多个表或者是多个sql语句insert，update，delete。需要保证这些语句都是成功才能完成我的功能,或者都失败，保证操作是符合要求的

   在java代码中写程序，控制事务，此时事务应该放在哪里呢？ service类的业务方法上，因为业务方法会调用多个dao方法，执行多个sql语句

3. 通常使用JDBC访问数据库，还是mybatis访问数据库怎么处理事务

   jdbc访问数据库，处理事务	`Connection conn; conn.commit();conn.rollback();`

   `mybatis`访问数据库，处理事务，`SqlSession.commit();SqlSession.rollback();`

   hibernate访问数据库，处理事务，`Session.commit(),Session.rollback()`

4. 3问题中事务的处理方式，有什么不足

   1. 不同的数据库访问技术，处理事务的对象，方法不同，需要了解不同数据库访问技术使用事务的原理(应该是除了单纯的jdbc还有别的)
   2. 掌握多种数据库中事务的处理逻辑，什么时候提交事务，什么时候回滚事务
   3. 处理事务的多种方法。

   总结：就是多种数据库的访问技术，有把不同的事务处理的机制，对象，方法。

5. 怎么解决不足

   spring提供一种处理事务的统一模型，能够使用统一的步骤，方式完成多种不同数据库访问技术的事务处理

   使用spring的事务处理机制，可以完成mybatis访问数据库的事务处理

   使用spring的事务处理机制，可以完成hibernate访问数据库的事务处理

![image-20200815213341269](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200815213341269.png)

 6. 处理事务，需要怎么做，做什么

    spring处理事务的模型，使用的步骤都是固定的，把事务使用的信息提供给spring就可以了

    1. 事务内部提交，回滚事务，使用的事务管理器对象，代替你完成commit，rollback

       事务管理器是一个接口和他的众多实现类。

       接口：`PlatFormTransactionManager`,定义了事务重要方法`commit，rollback`

       实现类：有很多，spring把每一种数据库访问技术对应的事务处理类都创建好了(nb)，

       ​			mybatis访问数据库---spring创建好的是`DataSourceTransactionManager`

       ​			`hibernate访问数据库---spring创建的是HibernateTransactionManager`

       怎么使用：你需要告诉spring你用的是哪种数据库的访问技术，怎么告诉spring呢？

       声明数据库访问技术对于的事务管理器实现类，在spring的配置文件中使用`<bean>`声明就可以了，例如，你要使用mybatis访问数据库，你应该在xml配置文件中

       <bean id="xxx" class="...DataSourceTransactionManager">

    2. 你的业务方法需要什么样的事务，说明需要事务的类型

       说明方法需要的事务：

       1. 事务的隔离级别：有四个值，

          ![image-20200815214551697](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200815214551697.png)

          目前需要掌握的是默认的，（后面的不懂，我觉得需要重看一下）

       2. 事务的超时时间：表示一个方法最长的执行时间，如果方式执行时超过了时间，事务就回滚。单位是s，整数值，默认是-1，(但是我们在项目开发中一般不设置，因为影响因素比较多，而且这个超时时间让我联想起`maxAlive数据库连接池里面的，只不过指的是没有运行时能撑的最长时间`)

       3. 事务的传播行为：控制业务方法是不是有事务的，是什么样的事务的。

          7个传播行为，表示你的业务方法在调用时，事务在方法之间是如何使用的

          ![image-20200815220434773](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200815220434773.png)

          红色的三个需要掌握，下面的可以说是不用记，因为几乎不用

          ![image-20200815221843322](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200815221843322.png)

          ![image-20200815221726304](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200815221726304.png)

          实际上一个例子比较生动，就是打游戏的时候有李四和张三，李四先问张三你有流量吗，有的话就给我开个热点呗，如果有的话就给李四用，没有的话李四就说那行吧，我自己开4g了，有点心机的感觉。但是对于这个事务是多个sql语句诶，怎么创建多个sql语句呢？





![image-20200815222106311](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200815222106311.png)		

​		

比如说查询操作

![image-20200815222745002](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200815222745002.png)

![image-20200815222756440](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200815222756440.png)



3. 事务提交事务，回滚事务的时机

   1. 当你的业务方法，执行成功，没有异常抛出，当方法执行完毕，spring在方法执行后提交事务。事务管理器commit

   2. 当你的业务方法抛出运行时异常或`ERROR`，spring执行回滚，调用事务管理器的rollback

      运行时异常的定义：`RuntimeException`和他的子类都是运行时异常，例如`NullPointerException`,`NumberFormatException`

   3. 当你的业务方法抛出非运行时异常，主要是受查异常异常时，提交事务（~~大概是不执行方法，然后提交表示出现异常的信息？我好像明白了，应该是像`RandomAccessFile`里面的rwd一样，会同步直到出现了异常，就是即使发生了错误也会把没错的给提交了~~ 好像不是，提交事务明明是成功的意思，当有异常的时候如何提交？？？？？？？？？然后我这个结论是通过下面 的代码得出的，问题是下面抛出的异常时运行异常诶，所以目前结论不成立。）

      受查异常：在你写代码中，必须处理的异常，例如`IOException,SQLException`

**总结spring的事务：**

1. 管理事务的是事务管理器和他的实现类
2. spring的事务是一个统一模型
   1. 指定要使用的事务管理器实现类，使用<bean>
   2. 指定哪些类，哪些方法需要加入事务的功能
   3. 指定方法需要的隔离级别，传播行为，超时

你需要告诉spring，你的项目中类信息，方法的名称，方法的事务传播行为

### 实例：

![image-20200815231910109](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200815231910109.png)



不能用float和double代表数据？？

实现步骤：

1. 新建maven项目

2. 加入maven依赖

   1. spring依赖
   2. mybatis依赖
   3. mysql驱动
   4. spring的事物的依赖
   5. mybatis和spring集成的依赖：mybatis官方提供的，用来spring项目中创建mybatis的`SqlSessionFactory,dao对象`

3. 创建实体类

   Sale,Goods

4. 创建dao接口和mapper文件

   SaleDao接口，GoodsDao接口

   SaleDao.xml,GoodsDao.xml

5. 创建mybatis主配置文件

6. 创建Service的接口和实现类，属性是saleDao,goodsDao

7. 创建spring的配置文件：声明mybatis的对象就给spring创建

   1. 数据源DataSource（数据库的相关信息？）
   2. `SqlSessionFactory`
   3. dao对象
   4. 声明自定义的service

8. 创建测试类，获取Service对象，通过Service调用dao完成数据库的访问

===========================代码部分==================================

先写基本操作吧，还没加上事务处理方面的，

`applicationContext.xml`

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">
<!--
    把数据库的配置信息，写在一个独立的文件，编译修改数据库的配置内容
    spring知道jdbc.properties文件的位置
-->
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <!--    声明数据源DataSource，作用是连接数据库的-->

    <bean id="myDataSource" class="com.alibaba.druid.pool.DruidDataSource" init-method="init"
          destroy-method="close">
<!--        set注入给DruidDataSource提供数据库信息-->
<!--
            使用属性配置文件中的数据，语法是${key}
-->
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
<!--            <property name="url" value="jdbc:mysql://localhost:3306/ssm?serverTimezone=GMT%2B8"/>-->
<!--            <property name="username" value="root"/>-->
<!--            <property name="password" value="123456"/>-->
        <property name="maxActive" value="${jdbc.max}"/>
     </bean>

<!--    声明的是mybatis中提供的SqlSessionFactoryBean类，这个类内部创建SqlSessionFactory
-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
<!--        set注入，把数据库连接池赋给了dataSource-->
        <property name="dataSource" ref="myDataSource"/>
<!--
    mybatis主配置文件的位置
        configLocation是Resource类型，读取配置文件
        它的配置，使用value，指定文件路径，使用classpath：表示文件的位置
-->


        <property name="configLocation" value="classpath:mybatis.xml"/>
    </bean>

<!--    创建dao对象，使用SqlSession的getMapper(StudentDao.class)
        MapperScannerConfigurer:在内部调用getMapper()生成每个dao接口的代理对象
-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
<!--        指定SqlSessionFactory对象的id-->
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
<!--        指定包名，包名是dao接口所在的包名
            MapperScannerConfigurer会扫描这个包中的所有接口，把每个接口都执行
            一次getMapper()方法，得到每个接口的dao对象。
            创建好的dao对象放入到spring容器中的. dao对象的默认名称是接口首字母小写(感觉跟resultType那里别名直接用类名表示差不多，也是直接变小写(不确定是不是这里))
            两个包之间可以打逗号
-->
        <property name="basePackage" value="com.zbr.dao"/>

    </bean>

   <bean id="buyService" class="com.zbr.service.impl.BuyGoodsServiceImpl">
    <property name="goodsDao" ref="goodsDao"/>
       <property name="saleDao" ref="saleDao"/>
   </bean>
</beans>
```

mybatis.xml跟前面没啥区别就不写了，基本上后面没怎么动过，因为他就配配映射就可以了

`SaleDao 和 GoodsDao`

```java
public interface GoodsDao {
    //更新库存
    //goods表示本次用户购买的商品信息，id，购买数量
    int updateGoods(Goods goods);

    //查询商品的信息
    Goods selectGoods(Integer id);
}

public interface SaleDao {
//    增加销售记录
    int insertSale(Sale sale);

}

```

`SaleDao.xml 和 GoodsDao.xml`

```html
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.zbr.dao.GoodsDao">

    <select id="selectGoods" resultType="com.zbr.domain.Goods">
        select * from goods where id=#{gid}
    </select>

    <update id="updateGoods">
        update goods set amount = amount - #{amount} where id = #{id}
    </update>
</mapper>


<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.zbr.dao.SaleDao">

    <insert id="insertSale">
        insert into sale(gid,nums) values (#{gid},#{nums})
    </insert>
</mapper>

```

domain中的Sale 和 Goods

```java
public class Goods {
    private Integer id;
    private  String name;
    private Integer amount;
    private Float price;

    //省略getter 和 setter 和 toString方法
}

public class Sale {
    private Integer id;
    private Integer gid;
    private Integer nums;

//省略getter 和 setter 和 toString方法
}

```

自定义的异常

```java
//自定义的运行时异常
public class NotEnoughException extends RuntimeException{
    public NotEnoughException() {
        super();
    }

    public NotEnoughException(String message) {
        super(message);
    }
}

```

BuyGoodsService

```java
public interface BuyGoodsService {
    //购买商品的方法，goodsId：购买商品的编号，nums：购买商品的数量
    void buy(Integer goodsId,Integer nums);
}

```

**重点是这里哈**

```java
public class BuyGoodsServiceImpl implements BuyGoodsService {

    private SaleDao saleDao;
    private GoodsDao goodsDao;


    @Override
    public void buy(Integer goodsId, Integer nums) {
        System.out.println("=====buy方法的开始=======");
        //记录销售的信息，向sale表添加记录
        Sale sale = new Sale();
        sale.setGid(goodsId);
        sale.setNums(nums);
        saleDao.insertSale(sale);
        //更新库存
        Goods goods = goodsDao.selectGoods(goodsId);
        if(goods == null){
            //商品不存在
            throw  new NullPointerException("编号是："+goodsId+"商品不存在");
        }else if (goods.getAmount() < nums){
            //商品库存不足
            throw  new NotEnoughException("编号是："+goodsId+"商品不足");
        }
        //修改库存了
        Goods buyGoods = new Goods();
        buyGoods.setId(goodsId);
        buyGoods.setAmount(nums);
        goodsDao.updateGoods(buyGoods);
        System.out.println("=====buy方法的完成=======");

    }


    public void setSaleDao(SaleDao saleDao) {
        this.saleDao = saleDao;
    }

    public void setGoodsDao(GoodsDao goodsDao) {
        this.goodsDao = goodsDao;
    }
}

```

> 上面还没有对事务的任何处理，而且你注意这个service写代码的顺序，是先添加再查库存再改库存，但在查库存这里会遇到问题，当遇到这个问题时，这样写的顺序是为了证明出现了异常在没有干预的情况下是如何进行的，不会回滚，会直接提交事务的一部分，不能算成功完成事务，这样的处理时失败的，所以需要用到事务的处理。

==========================代码部分==================================





#### spring框架中提供的事务处理方案

1. #### 适合中小项目使用的，注解方案

   spring框架自己用aop实现给业务方法增加事务的功能，使用`@Transactional`注解增加事务，是spring框架自己的注解，放在public方法的上面，表示当前方法具有事务，可以给注解的属性赋值，表示具体的隔离级别，传播行为，异常信息等。

![image-20200816095702606](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200816095702606.png)

​	使用`@Transactional`的步骤：

1. 需要声明事务管理器对象

   <bean id="xx" class="DataSourceTransactionManager">

2. 开启事务注解驱动，告诉spring，我要用注解的方式管理事务

   spring使用aop机制，创建`@Transactional`所在的类代理对象，给方法加入事务功能。

   spring给业务方法加事务：
   	在你的业务方法执行之前，先开启事务，在业务方法之后提交或回滚事务，使用aop的环绕通知

   ```java
   
   @Around("你要增加的事务功能的业务方法名称")
   Object myAround(){
   	//开启事务，spring给你开启
   	try{
      buy(1001,10);
      spring的事务管理器.commit();
   		}catch(Exception e){
   		spring的事务管理.rollback();       
      }
   }
   
   
   ```

3. 在你方法上面加入`@Transactional` 

代码：

1. 多了两个依赖

```html
<dependency>
      <groupId>org.aspectj</groupId>
      <artifactId>aspectjrt</artifactId>
      <version>1.7.3</version>
    </dependency>
    <dependency>
      <groupId>org.aspectj</groupId>
      <artifactId>aspectjweaver</artifactId>
      <version>1.7.3</version>
    </dependency>
```

2. `applicationContext.xml`

   ```html
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:context="http://www.springframework.org/schema/context" xmlns:tx="http://www.springframework.org/schema/tx"
          xsi:schemaLocation="http://www.springframework.org/schema/beans
           http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">
   <!--
       把数据库的配置信息，写在一个独立的文件，编译修改数据库的配置内容
       spring知道jdbc.properties文件的位置
   -->
       <context:property-placeholder location="classpath:jdbc.properties"/>
       <!--    声明数据源DataSource，作用是连接数据库的-->
   
       <bean id="myDataSource" class="com.alibaba.druid.pool.DruidDataSource" init-method="init"
             destroy-method="close">
   <!--        set注入给DruidDataSource提供数据库信息-->
   <!--
               使用属性配置文件中的数据，语法是${key}
   -->
           <property name="url" value="${jdbc.url}"/>
           <property name="username" value="${jdbc.username}"/>
           <property name="password" value="${jdbc.password}"/>
   <!--            <property name="url" value="jdbc:mysql://localhost:3306/ssm?serverTimezone=GMT%2B8"/>-->
   <!--            <property name="username" value="root"/>-->
   <!--            <property name="password" value="123456"/>-->
           <property name="maxActive" value="${jdbc.max}"/>
        </bean>
   
   <!--    声明的是mybatis中提供的SqlSessionFactoryBean类，这个类内部创建SqlSessionFactory
   -->
       <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
   <!--        set注入，把数据库连接池赋给了dataSource-->
           <property name="dataSource" ref="myDataSource"/>
   <!--
       mybatis主配置文件的位置
           configLocation是Resource类型，读取配置文件
           它的配置，使用value，指定文件路径，使用classpath：表示文件的位置
   -->
   
   
           <property name="configLocation" value="classpath:mybatis.xml"/>
       </bean>
   
   <!--    创建dao对象，使用SqlSession的getMapper(StudentDao.class)
           MapperScannerConfigurer:在内部调用getMapper()生成每个dao接口的代理对象
   -->
       <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
   <!--        指定SqlSessionFactory对象的id-->
           <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
   <!--        指定包名，包名是dao接口所在的包名
               MapperScannerConfigurer会扫描这个包中的所有接口，把每个接口都执行
               一次getMapper()方法，得到每个接口的dao对象。
               创建好的dao对象放入到spring容器中的. dao对象的默认名称是接口首字母小写(感觉跟resultType那里别名直接用类名表示差不多，也是直接变小写(不确定是不是这里))
               两个包之间可以打逗号
   -->
           <property name="basePackage" value="com.zbr.dao"/>
   
       </bean>
   
      <bean id="buyService" class="com.zbr.service.impl.BuyGoodsServiceImpl">
       <property name="goodsDao" ref="goodsDao"/>
          <property name="saleDao" ref="saleDao"/>
      </bean>
   <!--    使用spring的事务处理-->
   <!--    1.声明事务管理器-->
       <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
   <!--        需要连接的数据库,指定数据源-->
           <property name="dataSource" ref="myDataSource"/>
       </bean>
   
   <!--    2.开启事务注解驱动，告诉spring使用注解管理事务，创建代理对象
           transaction-manager:事务管理器对象的id
           感觉那是基本默认事务会和动态代理绑在一起了，也可以说是代理的切面类是内部执行的，@Around就是，
           你看你也没写这个切面类
   -->
   
       <tx:annotation-driven transaction-manager="transactionManager"/>
   </beans>
   ```

3. `BuyGoodsServiceImpl`

   ```java
   public class BuyGoodsServiceImpl implements BuyGoodsService {
   
       private SaleDao saleDao;
       private GoodsDao goodsDao;
   
   
       /**
        *
        * rollbackFor:表示发生指定的异常一定回滚
        *  处理逻辑：1.spring框架会首先检查方法抛出的异常是不是在rollback的属性值中
        *            如果异常在rollbackFor列表中，不管是什么类型的异常，一定回滚
        *          2.如果你的抛出的异常不在rollbackFor列表中，spring会判断异常是不是RuntimeException,
        *              如果是一定回滚
        */
   //    @Transactional(
   //            propagation = Propagation.REQUIRED,
   //            isolation = Isolation.DEFAULT,
   //            readOnly = false,
   //            rollbackFor = {
   //                    NullPointerException.class,
   //                    NotEnoughException.class
   //            }
   //    )
       //只写这个就好了，和上面是完全等效的，使用的是事务控制的默认值，默认的传播行为REQUIRED,默认的隔离级别是DEFAULT，
       //默认你抛出运行时异常回滚事务
       @Transactional
       @Override
       public void buy(Integer goodsId, Integer nums) {
           System.out.println("=====buy方法的开始=======");
           //记录销售的信息，向sale表添加记录
           Sale sale = new Sale();
           sale.setGid(goodsId);
           sale.setNums(nums);
           saleDao.insertSale(sale);
           //更新库存
           Goods goods = goodsDao.selectGoods(goodsId);
           if(goods == null){
               //商品不存在
               throw  new NullPointerException("编号是："+goodsId+"商品不存在");
           }else if (goods.getAmount() < nums){
               //商品库存不足
               throw  new NotEnoughException("编号是："+goodsId+"商品不足");
           }
           //修改库存了
           Goods buyGoods = new Goods();
           buyGoods.setId(goodsId);
           buyGoods.setAmount(nums);
           goodsDao.updateGoods(buyGoods);
           System.out.println("=====buy方法的完成=======");
   
       }
   
   
       public void setSaleDao(SaleDao saleDao) {
           this.saleDao = saleDao;
       }
   
       public void setGoodsDao(GoodsDao goodsDao) {
           this.goodsDao = goodsDao;
       }
   }
   ```

   其他基本一样，所以把不一样的拿出来了

##### 2. 适合大型项目，有很多的类，方法，需要大量的配置事务，使用aspectj框架功能，在spring配置文件中声明类，方法需要的事务，这种业务方法和事务配置完成分离。

​	实现步骤：都是在选xml配置文件中实现

1. 要使用的是aspectj框架，需要加入(上面用注解时也一样)
2. 声明事务管理器对象
3. 声明方法需要事务类型(配置方法的事务属性【隔离级别，传播行为，超时】)
4. 配置aop：指定哪些类要创建代理

和注解的区别就是把事务的代码都移到了xml文件中

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context" xmlns:tx="http://www.springframework.org/schema/tx"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd http://www.springframework.org/schema/aop https://www.springframework.org/schema/aop/spring-aop.xsd">
<!--
    把数据库的配置信息，写在一个独立的文件，编译修改数据库的配置内容
    spring知道jdbc.properties文件的位置
-->
    <context:property-placeholder location="classpath:jdbc.properties"/>
    <!--    声明数据源DataSource，作用是连接数据库的-->

    <bean id="myDataSource" class="com.alibaba.druid.pool.DruidDataSource" init-method="init"
          destroy-method="close">
<!--        set注入给DruidDataSource提供数据库信息-->
<!--
            使用属性配置文件中的数据，语法是${key}
-->
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
<!--            <property name="url" value="jdbc:mysql://localhost:3306/ssm?serverTimezone=GMT%2B8"/>-->
<!--            <property name="username" value="root"/>-->
<!--            <property name="password" value="123456"/>-->
        <property name="maxActive" value="${jdbc.max}"/>
     </bean>

<!--    声明的是mybatis中提供的SqlSessionFactoryBean类，这个类内部创建SqlSessionFactory
-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
<!--        set注入，把数据库连接池赋给了dataSource-->
        <property name="dataSource" ref="myDataSource"/>
<!--
    mybatis主配置文件的位置
        configLocation是Resource类型，读取配置文件
        它的配置，使用value，指定文件路径，使用classpath：表示文件的位置
-->


        <property name="configLocation" value="classpath:mybatis.xml"/>
    </bean>

<!--    创建dao对象，使用SqlSession的getMapper(StudentDao.class)
        MapperScannerConfigurer:在内部调用getMapper()生成每个dao接口的代理对象
-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
<!--        指定SqlSessionFactory对象的id-->
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
<!--        指定包名，包名是dao接口所在的包名
            MapperScannerConfigurer会扫描这个包中的所有接口，把每个接口都执行
            一次getMapper()方法，得到每个接口的dao对象。
            创建好的dao对象放入到spring容器中的. dao对象的默认名称是接口首字母小写(感觉跟resultType那里别名直接用类名表示差不多，也是直接变小写(不确定是不是这里))
            两个包之间可以打逗号
-->
        <property name="basePackage" value="com.zbr.dao"/>

    </bean>

   <bean id="buyService" class="com.zbr.service.impl.BuyGoodsServiceImpl">
    <property name="goodsDao" ref="goodsDao"/>
       <property name="saleDao" ref="saleDao"/>
   </bean>

<!--    声明使事务处理，和源代码完全分离-->
<!--   1. 声明事务管理器对象-->
    <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="myDataSource"/>
     </bean>

<!--    2.声明业务方法他的事务属性(隔离级别，传播行为，超时时间)
        id:自定义名称，表示tx:advice 和 </tx:advice>之间的配置
        transaction-manager:事务管理器对象的id
-->
        <tx:advice id="myAdvice" transaction-manager="transactionManager">
<!--         tx:attributes:配置事务属性   -->
            <tx:attributes>
<!--                tx:method:给具体的方法配置事务属性
                    name:方法名称，1.完整的方法名称，不带有包和类
                                 2.方法可以使用通配符,*表示任意字符
                    propagation:传播行为，枚举值
                    isolation：隔离级别
                    rollback-for：你指定的异常类名，全限定类名。发生异常一定回滚

                    你看下面有三种，完整方法名，一半*,和全*，那到底怎么匹配呢，全*就意味着所有方法都可以了呀？
                    所以有优先级的，分别是1,2,3，所以是越完整越优先
-->
                <tx:method name="buy"  propagation="REQUIRED" isolation="DEFAULT"
                           rollback-for="java.lang.NullPointerException,com.zbr.excep.NotEnoughException"/>
<!--                使用通配符，可以指定很多方法，因为写方法的时候基本是有一套名字规范的-->
                <tx:method name="add*" propagation="REQUIRES_NEW"/>
<!--                指定修改方法-->
                <tx:method name="modify*"/>
<!--                指定删除方法-->
                <tx:method name="remove*"/>
<!--                查询方法，query，search，search，find-->
                <tx:method name="*" propagation="SUPPORTS" read-only="true"/>
            </tx:attributes>
        </tx:advice>

<!--    配置aop-->
    <aop:config>
<!--        配置切入点表达式：指定哪些包中类，要使用事务
            id:切入点表达式的名称，唯一值
            expression：切入点表达式，指定哪些类要使用事务，aspectj会创建代理事务
            com.zbr.service
            com.crm.service
            com.service
-->
        <aop:pointcut id="servicePt" expression="execution(* *..service..*.*(..))"/>
<!--        配置增强器：关联advice和pointcut
            advice-ref:通知，上面tx：advice那里的配置
            pointcut-ref：切入点表达式id
-->
        <aop:advisor advice-ref="myAdvice" pointcut-ref="servicePt"/>
     </aop:config>
<!--    其实可以这么理解，他们本来感觉上就是分开的，transaction和aop，只不过注解的时候合在了一起。这样分开两个看会不会更好理解点？-->

</beans>
```

>这里配的比较复杂，但是适合大型项目进行，真的，通配符很好使。
>
>不过和前面的配置文件相比就是多了两个东西，一个advice一个config，你想你要配事务，那你要把你要进行事务处理的方法拿出来标一下吧，但这时候只是完整名称，buy这种，连包都无，所以下面就是配包的，使用切入点表达式。

## web项目中怎么使用容器对象

1. 做的是javase项目有main方法的，执行代码是执行main方法的。在main里面创建的容器对象

   `ApplicationContext ctx = new ClassPatjXmlApplicationContext("applicationContext.xml");`

2. web项目是在tomcat服务器上运行的，tomcat一启动，项目一直运行的

（我觉得是因为想要启动这个容器是有条件的，比如经过某个页面才会去实现某些代码，你想想怎么写呢？所以最好是放在监听器上把）

实现步骤：

1. 创建maven，web项目

2. 加入依赖

   拷贝`ch07-spring-mybatis`中依赖

   jsp，servlet依赖

3. 拷贝`ch07-spring-mybatis`的代码和配置文件

4. 创建一个jsp发送请求，有参数id，name，email，age

5. 创建`Servlet`，接受请求参数，调用`Service`,调用dao完成注册

6. 创建一个jsp作为显示结果页面

### 需求：

web项目中容器对象只需要创建一次，把容器对象放入放到全局作用域(application作用域)的`ServletContext(服务器只会创建一个)中`

怎么实现？

使用监听器，当全局作用域对象呗创建时， 创建容器，存入`ServletContext`

监听器作用：

1. 创建容器对象，执行`ApplicationContextctx = new ClassPatjXmlApplicationContext("applicationContext.xml");`
2. 把容器对象放入到`ServletContext,ServletContext.setAttribute(key,ctx);`

监听器可以自己创建，也可以使用框架中提供好的`ContextLoaderListener`

`private WebApplicationContext context;`

`public interface WebApplicationContext extends ApplicationContext`

`ApplicationContext:javase使用的容器对象`

`WebApplicationContext:web项目中使用的容器对象`

把创建的容器对象，放入到全局作用域



**代码**

我把有区别的给写出来了，这里的话主要是在Servlet 和web.xml中写

多加的依赖

```html
<dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>javax.servlet.jsp</groupId>
      <artifactId>jsp-api</artifactId>
      <version>2.2.1-b03</version>
      <scope>provided</scope>
    </dependency>

<!--    为了使用监听器对象，需要加入依赖-->
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>5.2.5.RELEASE</version>
    </dependency>
```

Servlet

```java
public class RegisterServlet extends HttpServlet {
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        String strId = request.getParameter("id");
        String strName = request.getParameter("name");
        String strEmail = request.getParameter("email");
        String strAge = request.getParameter("age");

        //创建spring的容器对象
//        String config = "spring.xml";
//        ApplicationContext ctx = new ClassPathXmlApplicationContext(config);
        WebApplicationContext ctx = null;
        //获取ServletContext中的容器对象，创建好的容器对象，拿来就用
//        String key = WebApplicationContext.ROOT_WEB_APPLICATION_CONTEXT_ATTRIBUTE;
//        Object attr = getServletContext().getAttribute(key);
//        if(attr != null){
//            ctx = (WebApplicationContext) attr;
//        }
        //使用框架中的方法，获取容器对象
        ServletContext sc = getServletContext();
        ctx = WebApplicationContextUtils.getRequiredWebApplicationContext(sc);


        System.out.println("容器对象的信息======="+ctx);

        //获取service
        StudentService studentService = (StudentService) ctx.getBean("studentService");
        Student student = new Student();
        student.setId(Integer.parseInt(strId));
        student.setName(strName);
        student.setAge(Integer.parseInt(strAge));
        student.setEmail(strEmail);
        studentService.addStudent(student);

        //给一个页面
        request.getRequestDispatcher("/result.jsp").forward(request,response);
    }

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    }
}

```

web.xml

```html
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <servlet>
        <servlet-name>RegisterServlet</servlet-name>
        <servlet-class>com.zbr.controller.RegisterServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>RegisterServlet</servlet-name>
        <url-pattern>/reg</url-pattern>
    </servlet-mapping>
    
<!--    注册监听器ContextLoaderListener
        被创建对象后，会读取/WEB-INF/spring.xml
        为什么要读取文件？因为在监听器中要创建ApplicationContext.xml就是监听器默认读取的spring配置文件路径

        可以修改默认的文件位置，使用context-param重新指定文件的位置

        配置监听器：目的是创建容器对象，创建了容器对象，就能把spring.xml配置文件中所有对象都创建好
        用户发起请求就可以直接使用对象了
-->
<!--    感觉这个东西只有一个使用的地方，就是给spring使用-->
    <context-param>
<!--
    contextConfigLocation:表示配置文件的路径
  -->
        <param-name>contextConfigLocation</param-name>
<!--        自定义配置文件的路径，为什么这么写？是参照类路径的，你看看类路径那里
            WEB-INF/classes下的路径就是
    -->
        <param-value>classpath:spring.xml</param-value>
    </context-param>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>

    </listener>
</web-app>
```







**终于完结了，历经千辛万苦，但我还没写anki，加油吧**