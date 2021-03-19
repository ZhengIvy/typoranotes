## 一、Spring Boot入门

### 1. Spring Boot 简介

> 简化Spring应用开发 的一个框架；
>
> 整个Spring技术栈的一个大整合；
>
> J2EE 开发的一站式解决方案

### 2. 微服务

2014 Martin Flower

微服务：架构风格

一个应用应该是一组小型服务；可以通过HTTP的方式进行互通



每一个功能元素最终都是一个可独立替换和独立升级的软件单元

> 1. jdk1.8
> 2. maven 3.x
> 3. intelliJIDEA
> 4. SpringBoot 1.5.9.RELEASE 1.5.9

### 3. Spring Boot HelloWorld

一个功能

浏览器发送hello请求，服务器接收请求并处理，相应`Hello World`字符串

1. 创建maven工程

2. 导入`spring boot 相关依赖`

   ```html
    <parent>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-parent</artifactId>
           <version>1.5.2.RELEASE</version>
   
       </parent>
   <!-- 
   这是Spring Boot的父级依赖，这样当前的项目就是Spring Boot项目了。
   spring-boot-starter-parent 是一个特殊的starter，它用来提供相关的Maven默认依赖。使用它之后，常用的包依赖可以省去version标签。
   
   -->
       <dependencies>
   <!-- 所以 这个是个web工程-->
           <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter-web</artifactId>
           </dependency>
       </dependencies>
   ```

   

3. 编写一个主程序：启动`Spring Boot 应用`

4. 编写相关的`Controller、Service`

   ```java
   @Controller
   public class HelloController {
   
       @RequestMapping("/hello")
       @ResponseBody
        public String hello(){
   
           return "HelloWorld";
        }
   }
   
   ```

5. 运行主程序测试

6. 简化部署

   ```xml
   <!--    这个插件，可以将应用打包成一个可执行的jar包;
           可是问题是原来不就有了吗？但是我试了一下，两个还是不一样的，多了一个东西？
   -->
       <build>
           <plugins>
               <plugin>
                   <groupId>org.springframework.boot</groupId>
                   <artifactId>spring-boot-maven-plugin</artifactId>
               </plugin>
           </plugins>
       </build>
   ```

   将这个应用打包成jar，直接使用`java-jar`的命令进行执行；

### 4.Hello World 探究

1. POM 文件

   1. 父项目

      ```xml
      <parent>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-parent</artifactId>
              <version>1.5.2.RELEASE</version>
      
          </parent>
      
      他的父项目是
      	<parent>
      		<groupId>org.springframework.boot</groupId>
      		<artifactId>spring-boot-dependencies</artifactId>
      		<version>1.5.2.RELEASE</version>
      		<relativePath>../../spring-boot-dependencies</relativePath>
      	</parent>
      他来真正管理Spring Boot应用里面的所有版本依赖
      ```

      Spring Boot的版本仲裁中心；

      以后我们导入依赖默认是不需要写:(没有在`dependencies`里面管理的依赖需要声明版本号)

   2. 导入的依赖

      ```xml
      <dependency>
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-starter-web</artifactId>
              </dependency>
      ```

      **spring-boot-starter**-web:spring-boot 场景启动器：帮我们导入了web模块正常运行所依赖的组件

      Spring Boot 将所有的功能场景都抽取出来，做成一个个的`starters`(启动器)，只需要在项目里面引入这些starter相关场景的所有依赖都会打入进来。要用什么功能就导入什么场景的启动器

      ---------------anki到这哈，希望明天起来下面可以画一个图哈

   3. 主程序类、主入口类
   
      ```java
      /**
       * @SpringBootApplication 来标注一个主程序类，说明这是个Spring Boot 应用
       */
      @SpringBootApplication
      public class HelloWorldMainApplication {
          public static void main(String[] args) {
              //Spring应用启动起来
              SpringApplication.run(HelloWorldMainApplication.class,args);
          }
   }
      ```

      `@SpringBootApplication:Spring Boot 应用标注在某个类上说明这个类是Spring Boot的主配置类，Spring Boot就应该运行这个类的main方法来启动SpringBoot应用`
   
      ```java
      @Target({ElementType.TYPE})
      @Retention(RetentionPolicy.RUNTIME)
      @Documented
      @Inherited
      @SpringBootConfiguration
      @EnableAutoConfiguration
      @ComponentScan(
          excludeFilters = {@Filter(
          type = FilterType.CUSTOM,
          classes = {TypeExcludeFilter.class}
      ), @Filter(
          type = FilterType.CUSTOM,
          classes = {AutoConfigurationExcludeFilter.class}
      )}
   )
      ```

      `@SpringBootConfiguration`:Spring Boot 的配置类：

      ​	标注在某个类上，表示这是一个`Spring Boot`的配置类：

      ​	`@Configuration:配置类上来标注这个注解`:

      ​	配置类 --- 配置文件：配置类也是容器中的一个组件：`@Component`(的确，总得还是有个配	置文件去搞这些的)

      `@EnableAutoConfiguration`:开启自动配置功能：

      ​		以前我们需要配置的东西，Spring Boot 帮我们自动配置：`@EnableAutoConfiguration`告诉Spring Boot开启自动配置功能；这样自动配置才能生效
   
      ```java
      @AutoConfigurationPackage
      @Import({EnableAutoConfigurationImportSelector.class})
   public @interface EnableAutoConfiguration {
      ```

      ​	`@AutoConfigurationPackage`:自动配置包

      ​			`@Import({Registrar.class})`:Spring的底层注解`@Import:给容器中导入一个组件；导入的组件由AutoConfigurationPackages.Register.class;`

      ​			**将主配置类(`@SpringBootApplication标注的类`)的所在包及下面所有子包里面的所有组件扫描到Spring容器中**

      ​		`@Import({EnableAutoConfigurationImportSelector.class})`;

      ​			给容器中导入组件？

      ​			`EnableAutoConfigurationImportSelector`:导入哪些组件的选择器；

      ​			将所有需要导入的组件以全类名的方式返回；这些组件会被添加到容器中

      ​			会给容器中导入非常多的自动配置类(xxxAutoConfiguration):就是给容器中导入这个场			需要的所有组件，并配置好这些组件；

      ![image-20200918112205321](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200918112205321.png)

      有了自动配置类，免去了我们手动编写配置注入功能组件等的工作

      `SpringFactoriesLoader.loadFactoryNames(EnableAutoConfiguration.class,classLoader)`

      从类路径下的`META-INF/spring.factories`中获取`EnableAutoConfiguration指定的值，将这些值作为自动配置类导入到容器中，自动配置类就生效，帮我们进行自动配置工作 `以前我们需要自己配置的东西，自动配置类帮我们；
   
      j2EE 的整体整合解决方法和自动配置都在`org.springframework\boot\autoconfigure-1.5.9.RELEASE.jar;`

### 5.使用`Spring Initializer快速创建Spring Boot项目`

​	IDEA都支持Spring的项目创建向导快速创建一个Spring Boot项目；

​	选择我们需要的模块，向导会联网创建Spring Boot项目

​	默认生成的Spring Boot项目：

- 主程序已经生成好了，我们只需要我们自己的逻辑
- resources文件夹中目录结构
  - static：保存所有的静态资源:js ,css , images; 
  - templates:保存所有的模板页面(Spring Boot 默认jar包使用嵌入式tomcat，默认不支持jsp页面)；可以使用模板引擎(freemarker,thymeleaf)
  - application.properties:Spring Boot应用的配置文件：可以修改一些默认设置；

> 总结下来，这里好多的东西，但总归来说就是看注解是怎么来实现配置文件的作用的。
>
> 我们在配置文件中会扫描组件创建对象还会加一些组件进去。那么`@AutoConfigurationPackage`就是这个作用的，可以扫描主程序所在的包及其子包下的组件。
>
> 第二个就是你怎么进行组件配置呢，比如aop的时候也是需要声明的呀，但是现在可以说是都帮你提前配置好了诶，就十分地nb哈



## 二、配置文件

### 1.配置文件

`SpringBoot 使用的一个全局的配置文件`,配置文件名是固定的

- application.properties
- application.yml

配置文件的作用：修改SpringBoot自动配置的默认值;SpringBoot在底层都给我们自动配置好

`YAML(YAML Ain't Markup Language)`

标记语言：

​		以前的配置文件：大多都使用的是`xxxx.xml`;

​		YAML:**以数据为中心**(没有冗余的东西)，比json、xml等更适合做配置文件;

​		YAML:配置例子

```java
server:
  port: 8081
```

​		XML:

```xml
<server>
<port>8081</port>
</server>
```

### 2. YAML 语法：

1. 基本语法

   k:(空格)v: 表示一对键值对(空格必须有)

   以空格的缩进来控制层级关系；只要是左对齐的一列数据，都是同一层级的

   ```yaml
   server:
   	port:8080
   	path:/hello
   ```

   属性和值也是大小写敏感；

2. 值的写法

   字面量：普通的值(数字、字符串、布尔)

   ​		k​ v:字面直接来写；

   ​		字符串默认不用加上单引号或者双引号；

   ​		""：双引号;不会转义字符串里面的特殊字符；特殊字符会作为本身想表示的意思

   ​		name:"zhangsan \n lisi":输出; zhangsan 换行 lisi

   ​		'':单引号：会转义特殊字符，特殊字符最终只是一个普通的字符串数据

   ​			name:'zhangsan \n lisi'; 输出; zhangsan \n lisi

   对象、Map(属性和值)(键值对)：

   ​	k​;v: 在下一行来写对象属性和值的关系；注意缩进

   ​		对象还是k : v 的方式

   ```yaml
   	friends:
   				lastName:zhangsan
   				age:20
   ```

   行内写法：

   ```yaml
   friends: {lastName:zhangsan,age:18}
   ```

   

   ​	

   数组：(List、Set)

   用- 值表示数组中的一个元素

   ```yaml
   pets:
   - cat
   - dog
   - pig
   ```

   行内写法

   ```yaml
   pets: [cat,dog,pig]
   ```

3. 获取配置文件值注入

   配置文件

   ```yaml
   server:
     port: 8081
   
   
   person:
       lastName: zhangsan
       age: 18
       boss: false
       birth: 2017/12/12
       maps: {k1: v1,k2 : 12}
       lists:
         - lisi
         - zhaoliu
       dog:
         name: 小狗
         age: 2
   ```

   javaBean:

   ```java
   /**
    * 将配置文件中配置的每一个属性值，映射到这个组件中
    * @ConfigurationProperties: 告诉SpringBoot将本类中所有属性和配置文件中相关的配置进行绑定；
    *      prefix = "person":配置文件中哪个下面的所有属性进行一一映射
    *
    *      只有这个组件是容器中的组件，才能使用容器提供的功能
    */
   @Component
   @ConfigurationProperties(prefix = "person")
   public class Person {
   
       private String lastName;
       private Integer age;
       private Boolean boss;
       private Date birth;
   
       private Map<String,Object> maps;
       private List<Object> lists;
       private Dog dog;
   
       public String getLastName() {
           return lastName;
       }
   
       public void setLastName(String lastName) {
           this.lastName = lastName;
       }
   
       public Integer getAge() {
           return age;
       }
   
       public void setAge(Integer age) {
           this.age = age;
       }
   
       public Boolean getBoss() {
           return boss;
       }
   
       public void setBoss(Boolean boss) {
           this.boss = boss;
       }
   
       public Date getBirth() {
           return birth;
       }
   
       public void setBirth(Date birth) {
           this.birth = birth;
       }
   
       public Map<String, Object> getMaps() {
           return maps;
       }
   
       public void setMaps(Map<String, Object> maps) {
           this.maps = maps;
       }
   
       public List<Object> getLists() {
           return lists;
       }
   
       public void setLists(List<Object> lists) {
           this.lists = lists;
       }
   
       public Dog getDog() {
           return dog;
       }
   
       public void setDog(Dog dog) {
           this.dog = dog;
       }
   
       @Override
       public String toString() {
           return "Person{" +
                   "lastName='" + lastName + '\'' +
                   ", age=" + age +
                   ", boss=" + boss +
                   ", birth=" + birth +
                   ", maps=" + maps +
                   ", lists=" + lists +
                   ", dog=" + dog +
                   '}';
       }
   }
   
   ```

   我们可以导入配置文件处理器，以后编写配置就有提示了

   ```xml
   <!-- 导入配置文件处理器，配置文件进行绑定后就会有提示-->
           <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-configuration-processor</artifactId>
               <optional>true</optional>
           </dependency>
   ```

   



### 3.配置文件的注入

还是有一个问题，那个properties到底为什么？

> 好像明白了。。就是首先字节流是 一个字节一个字节的传送的，但是idea整体是utf-8的编码，所以从配置文件中读取信息，那你就要保证
>
> 等会，我认为的编码是都是用2进制组成的不是吗？只是大家对待同样的编码理解方式不同而已，那这个到底是怎么回事？怎么还和ascii码有关，我是真的不懂了
>
> 我看什么时候能找到一些资料来深入了解一波

1. 在properties文件中输入中文会乱码，所以的话需要在`settings -- > file encoding 选中 utf-8 和旁边的打钩`

   具体原理的话我没那么懂，但这里放了一篇可以作为参考

   [file encoding](https://www.pianshen.com/article/9851770707/)

2. `@Value获取值和@ConfigurationProperties获取值比较`

   |                    | @ConfigurationProperties                 | @Value                                       |
   | ------------------ | ---------------------------------------- | -------------------------------------------- |
   | 功能               | 批量注入配置文件中的属性                 | 一个个指定                                   |
   | 松散绑定(松散语法) | 支持(可以驼峰，也可以-等)                | 不支持(值必须和properties的匹配，即一样)     |
   | SpEL               | 不支持                                   | 支持                                         |
   | JSR303数据校验     | 支持(如果不符合数据格式的要求会运行失败) | 不支持(就算不符合数据格式的要求也不会怎么样) |
   | 复杂类型封装       | 支持                                     | 不支持                                       |

   这个@Value应该是自动读取全局配置把？

   ![image-20200919153138996](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200919153138996.png)

   配置文件yml还是`properties`他们都能获取得到值；

   如果说，我们只是在某个业务逻辑中需要获取一下配置文件的某项值，使用`@Value`

   如果说，我们专门编写了一个javaBean来和配置文件进行映射，我们就直接使用`@ConfigurationProperties`

3. 配置文件注入值数据校验

   ```java
   /**
    * 将配置文件中配置的每一个属性值，映射到这个组件中
    * @ConfigurationProperties: 告诉SpringBoot将本类中所有属性和配置文件中相关的配置进行绑定；
    *      prefix = "person":配置文件中哪个下面的所有属性进行一一映射
    *
    *      只有这个组件是容器中的组件，才能使用容器提供的功能
    */
   @Component
   //@ConfigurationProperties(prefix = "person")
   @Validated
   public class Person {
   
       /**
        * <bean class="Person">
        *     <property name="lastName" value="字面量/${key}从环境变量、配置文件中获取值/#{SpEL}(Spring的EL表达式)"></property>
        * </bean>
        */
   //    @Value("${person.lastName}")
       @Email
       @Value("${person.last-name}")
       private String lastName;
   //    @Value("#{11*2}")
       private Integer age;
   //    @Value("true")
       private Boolean boss;
       private Date birth;
   
       private Map<String,Object> maps;
       private List<Object> lists;
       private Dog dog;
   
      //getter setter toString 方法
   }
   
   ```

4. `@PropertySource&@ImportResource`

   详情点击 https://www.cnblogs.com/asplover/p/13299496.html

   @**PropertySource**：加载指定的配置文件；
   
   实际就是把本来写在application里面的拿过来了，因为你全部写到全局配置那里不臃肿吗，所以这个就导入另外的properties 或 yml哈
   
   ```java
   /**
    * 将配置文件中配置的每一个属性值，映射到这个组件中
    * @ConfigurationProperties: 告诉SpringBoot将本类中所有属性和配置文件中相关的配置进行绑定；
    *      prefix = "person":配置文件中哪个下面的所有属性进行一一映射
    *
    *      只有这个组件是容器中的组件，才能使用容器提供的功能
    *      @ConfigurationProperties: 默认是从全局配置文件中获取值
    */
   @PropertySource(value = {"classpath:person.properties"})
   @Component
   @ConfigurationProperties(prefix = "person")
   //@Validated
   public class Person {
   
       /**
        * <bean class="Person">
        *     <property name="lastName" value="字面量/${key}从环境变量、配置文件中获取值/#{SpEL}(Spring的EL表达式)"></property>
        * </bean>
        */
   //    @Value("${person.lastName}")
   //    @Email
       @Value("${person.last-name}")
       private String lastName;
   //    @Value("#{11*2}")
       private Integer age;
   //    @Value("true")
       private Boolean boss;
       private Date birth;
   
   //    @Value("${person.maps}")
    private Map<String,Object> maps;
       private List<Object> lists;
    private Dog dog;
   ```

   `@ImportSource`:导入Spring的配置文件，让配置文件中的内容生效

   `Spring Boot里面没有Spring的配置文件，我们自己编写的配置文件，也不能自动识别`(额？那当时讲那么多注解时讲的扫描组件是啥？不是用容器来扫的吗？？？？还是这本身就越过了容器啊)

   额，说一下我上面疑问的那一点，其实是有的，只是我们自己再搞的你不加到注解上去你也用不了
   
   一般情况下我们自定义的xml配置文件，默认情况下这个bean是不会加载到Spring容器中来的。需要@ImportResource注解将这个配置文件加载进来。
   配置
   
   

   想让Spring的配置文件生效，加载进来；`@ImportResource`:标注在一个配置类上

   ```java
   @ImportResource(
       locations = {"classpath:beans.xml"}
   )
   //导入Spring的配置文件让其生效
   ```
   
   不来编写Spring的配置文件
   
```xml
   <?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   
    <bean id="helloService" class="com.zbr.springboot.service.HelloService"></bean>
   </beans>
```
   
   
   
   **小结**
   　　 @PropertySource 
     @PropertySource 用于引入*.Properties或者 .yml 用于给javabean实体类注入值
   
   ```
   @Component
   @ConfigurationProperties(prefix="bird2")  //需要与@Component 配合使用，没有使用@PropertySource(）则指向全局配置文件application.yml或application.properties
   //只能指向.properties文件，不可以指向.yml文件 没有此文件则指向主配置文件
   @PropertySource(value={"classpath:entity/pigean.properties"},ignoreResourceNotFound=false,encoding="UTF-8") 
   ```
   
   
     @ImportResource 用于引入.xml 类型的配置文件 在spring boot中已经被配置类替代,且要求放在配置启动类上
   
     @ImportResource一般用于启动类上
   
   
   
   `Spring Boot`推荐给容器中添加组件的方式；(推荐使用全注解的方式)
   
   1. 配置类======Spring配置文件
   
   2. 使用`@Bean`给容器中添加组件
   
      ```java
      /**
       * @Configuration： 指明当前类是一个配置类;就是来替代之前的Spring配置文件
       *
       * 在配置文件中用<bean><bean/>标签添加组件
       */
      @Configuration
      public class MyAppConfig {
      
          /**
           * 将方法的返回值添加到容器中；容器中这个组件默认的id就是方法名
           * emm,我的想法是又回来了，本来spring中想用大型项目的话用注解是比较麻烦的，但是一般通常情况下用的是注解
           * 然后springboot推荐这种情况来添加组件，感觉又回来了额
           */
          @Bean
          public HelloService helloService(){
              System.out.println("配置类@Bean给容器中添加组件了");
              return new HelloService();
      
          }
      }
      
      ```

### 4.配置文件占位符

1. 随机数

   ![image-20200919214525494](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200919214525494.png)

2. 占位符获取之前的配置，如果没有可以用:指定默认值

   ```properties
   person.last-name=张三${random.uuid}
   person.age=${random.int}
   person.birth=2017/12/15
   person.boss=false
   person.maps.k1=v1
   person.maps.k2=14
   person.lists=a,b,c
   # 如果${person.hello}不存在就只会当做一个普通的字符串罢了，但是也还可以赋值呢，只不过是默认罢了	
   person.dog.name=${person.hello:hello}_dog
   person.dog.age=15
   ```



### 5. Profile

> 如何理解Profile呢，应该是不同的环境把，就可以任意切换，比较简单，但我目前不知道这里的用途是什么哈

1. 多Profile文件

   我们在主配置文件编写的时候，文件名可以是`application-{profile}.properties/yml`

   默认使用`application.properties`的配置文件

2. yml支持多文档块方式

   ```yaml
   server:
     port: 8081
   spring:
     profiles:
       active: dev
   ---
   
   server:
     port: 8083
   spring:
     profiles: dev
   ---
   server:
     port: 8084
   spring:
     profiles: prod #指定属于哪个环境
   ```

3. 激活指定profile

   1. 在配置文件中指定`spring.profiles.active=dev`

   2. 命令行：

      `java-jar spring-boot-02-config-0.0.1-SNAPSHOT.jar--spring.profiles.active=dev;`

      上面这个是打包成jar，然后打开cmd搞的

      --`spring.profiles.active=dev`

      可以直接在测试的时候，配置传入命令行参数，这是在idea中的`edit configurations`中搞的

   3. 虚拟机参数

      ![image-20200919223122553](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200919223122553.png)

### 六、配置文件加载位置

![image-20200919223159303](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200919223159303.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201107163044407.png" style="zoom:67%;" />

不要看这个1234哈，不准确哈

`SpringBoot`会从这四个位置全部加载主配置文件；**互补配置**

**我们还可以通过spring.config.location来改变默认的配置文件位置,**

项目打包好以后，我们可以使用命令行参数的形式，启动项目的时候来指定配置文件的新位置，指定配置文件和默认加载的这些文件共同起作用形成互补配置*

> 我顺便再来说下我是怎么理解这个的，优先级最高的是最后执行的，你看四个路径，可以理解为就近查找，找不到翻文件夹，再找不到到更大的地方找，找不到找内部，直到找到为止。
>
> 理解下互补，就是都会在这四个地方找，优先级只是用于替代的，在其他文件没有的就可以形成互补的情况

### 七、外部配置加载顺序

![image-20200920235404000](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200920235404000.png)

![image-20200920235420560](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200920235420560.png)





![image-20201107165222020](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201107165222020.png)

外部配置的话就是当你的工程打成jar包的时候你在同级目录下搞个配置文件后的顺序

> 这个真的太多太杂了，等以后有需要我再继续看。
>
> 那你怎么理解的，我还是反着来，优先级最低的是最快加载的，所以的话才是先再jar包内部找，再去外部寻找，先从简单的找再去难的找，这里为什么说外部配置，我觉得是和外部配置结合再一起看，之前单纯只是再idea里面操作而已





### 8、自动配置原理

配置文件到底能写什么？怎么写？自动配置原理：

配置文件能配置的参照文档

**自动配置原理**：

1. SpringBoot启动的时候加载主配置类，开启了自动配置功能`@EnableAutoConfiguration`

2. `@EnableAutoConfiguration`作用：

   - 利用`EnableAutoConfigurationImportSelector`给容器中导入一些组件？

   - 可以查看selectImports()方法的内容

   - `StringUtils.toStringArray(autoConfigurationEntry.getConfigurations());`获取候选的配置

     - ```java
       SpringFactoriesLoader.loadFactoryNames()
           扫描所有jar包类路径下 META-INF/spring.factories
           把扫描到的这些的文件内容包装成properties对象
           从properties中获取到EnableAutoConfiguration.class类(类名)对应的值，然后把他们添加在容器中
       ```

       将类路径下META-INF/spring.factories里面配置的所有`EnableAutoConfiguration`的值添加到了容器中

       每一个这样的`xxxAutoConfiguration`类都是容器中的一个组件，都加入到容器中；用他们来做自动配置

3. 每一个自动配置类进行自动配置功能；

4. 以`HttpEncodingAutoConfiguration`为例解释自动配置原理; 

   ```java
   @Configuration(
       proxyBeanMethods = false
   )//表示这是一个配置类，以前编写的配置文件一样，也可以给容器中添加组件
   @EnableConfigurationProperties({ServerProperties.class})//启动指定类的ConfigurationProperties功能;将配置文件中对应的值和HttpEncodingProperties绑定起来；
   //并把HttpEncodingProperties加入到ioc容器中
   
   @ConditionalOnWebApplication(//Spring底层@Conditional注解，根据不同的条件，如果满足指定的条件，整个配置类里面的配置就会生效；  判断当前应用是否是web应用，如果是，当前配置类生效
       type = Type.SERVLET
   )
   @ConditionalOnClass({CharacterEncodingFilter.class})//判断当前项目有没有这个类CharacterEncodingFilter;SpringMVC中进行乱码解决的过滤器;
   @ConditionalOnProperty(//判断配置文件中是否存在某个配置，如果不存在，判断也是存在的
       //即使我们配置文件中不配置，也是默认生效的
       prefix = "server.servlet.encoding",
       value = {"enabled"},
       matchIfMissing = true
   )
   
   public class HttpEncodingAutoConfiguration {
       //已经和SpringBoot配置文件映射了
       private final Encoding properties;
   
       //只有一个有参构造器的情况下，参数的值就会从容器中拿
       public HttpEncodingAutoConfiguration(ServerProperties properties) {
           this.properties = properties.getServlet().getEncoding();
       }
    @Bean //给容器中添加一个组件,这个组件的某些值需要从properties中获取
       @ConditionalOnMissingBean
       public CharacterEncodingFilter characterEncodingFilter() {
           CharacterEncodingFilter filter = new OrderedCharacterEncodingFilter();
           filter.setEncoding(this.properties.getCharset().name());
           filter.setForceRequestEncoding(this.properties.shouldForce(org.springframework.boot.web.servlet.server.Encoding.Type.REQUEST));
           filter.setForceResponseEncoding(this.properties.shouldForce(org.springframework.boot.web.servlet.server.Encoding.Type.RESPONSE));
           return filter;
       }
   }
   ```

   根据当前不同的条件判断，决定这个配置类是否生效？

   一旦这个配置类生效；这个配置类就会给容器中添加各种组件，这些属性是从对应的properties类中的文件获取的，这些类里面的每一个属性又是和配置文件绑定的

5. 所有在配置文件中能配置的属性都是在xxxxProperties类中封装着；配置文件能配置什么就可以参照某个功能对应的这个属性类

   ```java
   @ConditionalOnProperty(
       prefix = "server.servlet.encoding",
       value = {"enabled"},
       matchIfMissing = true
   )
   ```





**精髓**

1. SpringBoot启动会加载大量的自动配置类
2. 我们看我们需要的功能有没有SpringBoot默认写好的自动配置类
3. 我们再来看这个自动配置类中到底配置了哪些组件；(只要我们要用的组件有，我们就不需要再来配置了)
4. 给容器中自动配置类添加组件的时候，会从properties类中获取某些属性，我们就可以在配置文件中指定这些属性的值

`xxxAutoConfiguration`:自动配置类；

给容器中添加组件

`xxxProperties:`封装配置文件中相关属性

> 怎么说呢这里是springboot的核心，自动配置，就是省去了配置文件，改成配置类来完成扫描组件和加入组件的工作，扫描组件的话就直接扫描就好了，主要还是加入组件比较复杂，这里的话我感觉我好像觉得没有那么多疑问？
>
> 首先有自己写的bean或者像`mvc:annotation`的组件，自己写的bean的话就是有自己的属性的，属性怎么拿呢？就要去一个xxxProperties的类中，一般这个xxxProperties的类就有指定属性，然后你在外面的properties文件就可以配置，但是呢你想一般一个完整的功能把，就可能不止一个配置文件这么简单，还有适用情境啊，各种别的东西合在一起。

### 细节

1. `@Conditional派生注解`(Spring注解版原生的@Conditional 作用)

   作用：必须是`@Conditional`指定的条件成立，才给容器中添加组件，配置里面的所有内容才生效

   ![image-20200923222722284](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200923222722284.png)

   自动配置类必须在一定的条件下才能生效：

   我们可以通过启用 `debug=true`属性，来让控制台打印自动配置报告,这样我们就可以很方便地知道哪些自动配置类生效;



## 三、日志

### 1.日志框架

小张；开发一个大型系统；

1. `System.out.println("")`:将关键数据打印在控制台上；去掉？写在一个文件？

2. 框架来记录系统的一些运行时信息；日志框架：zhanglogging.jar;

3. 高大上的功能？异步模式？自动归档？xxxx？zhanglogging-good.jar>

4. 将以前框架卸下来？换下新的框架，重新修改之前相关的`API`;zhanglogging-perfect.jar

5. JDBC-数据库驱动；

   写了一个统一的接口层；日志门面（日志的一个抽象层）；logging-abstract.jar给项目中导入具体的日志实现就行了；我们之前日志框架都是实现抽象层

市面上的日志框架：

`JUL JCL Jboss-logging logback log4j`

![image-20200924001335307](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200924001335307.png)

左边选一个门面(抽象层) 右边来选一个实现

日志门面(抽象层)，右边来选一个实现

日志门面：`SLG4j`

日志实现：`Logback`

SpringBoot:底层是Spring框架，Spring默认使用是`JCL`;

SpringBoot选用`SLF4j和Logback`

### 2.SFL4j使用

#### 	1. 如何在系统中使用SFL4j

以后开发的时候，日志记录方法的调用，不应该来直接调用日志的实现类，而是调用日志抽象层里面的方法

给系统里面导入slf4jj和logback的实现jar

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class HelloWorld{
    public static void main(String[] args){
        Logger logger  = LoggerFactory.getLogger(HelloWorld.class);
        logger.info("Hello World");
    }
}
```

![image-20200924205945661](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200924205945661.png)

> 怎么理解这个呢，我认为呢是实现类和接口的关系嘛，就接口给你定义好该怎么写，然后大家统一用这种方法 写，就可以不同的实现框架使用一个抽象层，但是呢为什么会用到适配器呢？当实现类比抽象框架早出现的时候，没有按照后来抽象框架的要求去做，所以的话中间需要一个适配器。让调用接口方法的时候实际上调用的是实线框自己的方法

每一个日志的实现框架都有自己的配置文件，使用slf4j以后，**配置文件还是做成日志实现框架本身的配置文件**

##### 遗留问题

`a(slf4j+logback):Spring(commons-logging) Hibernate(jboss-logging) Mybatis xxx`

统一日志记录，即使是别的框架和我一起统一使用slf4j进行输出？

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201107210632586.png)

**如何让系统中所有的日志都统一到slf4j**：

1. 将系统中其他日志框架先排除出去；
2. 用中间包来替换原有的日志框架；
3. 我们导入slf4j其他的实现

> 其实也蛮好理解的，实际上就是把他本来用的框架用jar包代替掉，其实还是一层装饰器哈，就也没多大区别。

### 3.SpringBoot日志关系

```xml
<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>
```

SpringBoot使用它来做日志功能

```xml
<dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-logging</artifactId>
        </dependency>
```

底层依赖关系

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201107192405315.png)

总结：

1. SpringBoot底层也时使用`slf4j+logback`的方式进行日志记录

2. SpringBoot也把其他的日志都替换成了slf4j；

3. 中间替换包？

   ![image-20200925084916124](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200925084916124.png)

   ![image-20201107192352776](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201107192352776.png)

4. 如果我们要引入其他框架？一定要把这个框架的默认日志依赖移除掉？

   因为转换包和原包是同名的，不排除的话不知道用哪个jar包(但不确定现在还是不是这样，因为弹幕里面讲现在不是了)

   Spring框架用的是`commons-logging`

   ![image-20200925085459333](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200925085459333.png)

   SpringBoot自动适配所有的日志，而底层使用`slf4j+logback`的方式记录日志，引入其他框架的时候，只需要把这个框架依赖的日志框架排除掉。

   > 看了下弹幕，基本上说SpringBoot2.0不是这样子的，底层变了好多，但是又又什么办法呢





### 4.日志使用

1. 默认配置

```java
  //记录器
    Logger logger = LoggerFactory.getLogger(getClass());


    @Test
    void contextLoads() {
//        System.out.println();
        //日志的级别：
        //由低到高 trace<debug<info<warn<error
        //可以调整输出的日志级别，日志就只会在这个级别以后的高级别生效
       logger.trace("这是trace日志..");
       logger.debug("这是debug日志");
       //SpringBoot默认给我们使用的是info级别，没有指定级别就用SpringBoot默认的级别:root级别
       logger.info("这是info日志");
       logger.warn("这是warn日志");
       logger.error("这是error日志...");


    }
```

![image-20200925092922279](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200925092922279.png)

> 这个file和path可以互相用好像，但如果都用的话是以file为准的

![image-20200925093901353](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200925093901353.png)

SpringBoot修改日志的默认配置

```properties
logging.level.com.zbr=trace
# 不指定路径在当前项目下生成springboot.log日志
# 可以指定完整的路径：
#logging.file.name=D:/maven/springboot.log
# 在当前磁盘的根路径下创建spring文件夹和里面的Log文件夹，使用spring.log作为默认文件
logging.file.path=/spring/log
# 在控制台输出的日志的格式
logging,pattern.console=
# 指定文件中日志输出的格式
logging.pattern.file=

```

2. 自定义配置

   给类路径下放上每个日志框架自己的配置文件即可：SpringBoot就不使用它默认配置的了

   ![image-20200925095505208](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200925095505208.png)

   logback.xml:直接被日志框架识别到了

   logback-spring.xml:日志框架就不直接加载日志的配置项，由SpringBoot解析日志配置，可以使用SpringBoot的高级Profile功能

   ```xml
   <springProfile name="staging">
   <!-- configuration to be enabled when the "staging" profile is active-->
       可以指定某段配置只在某个环境下生效
   </springProfile>
   ```

   否则

   ```
   no application action for [springProfile]
   ```

   ![image-20200927215041609](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200927215041609.png)

### 5.切换日志框架

可以按照slf4j的日志适配图，进行相关日志的切换；

slf4j+log4j的方式

![image-20200927221356756](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200927221356756.png)

![image-20200927221741185](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200927221741185.png)

额，这个有点迷茫把，他主要想说的应该是换成log4j2日志的方式，就是有给你提供两种一个是默认的logback,另外一种就是log4j2，如果想用后面这种，就需要人为排掉这个依赖

## 四、Web开发

使用SpringBoot：

1. 创建SpringBoot应用，选中我们需要的模块
2. SpringBoot已经默认将这些场景配置好了，只需要在配置文件中指定少量配置就可以运行出来
3. 自己编写业务代码

**自动配置原理**？

这个SpringBoot帮我们配置了什么？能不能修改？能修改哪些配置？能不能扩展？xxx

```
xxxxAutoConfiguration:帮我们给容器自动装配组件
xxxxProperties:配置类来封装配置文件的内容
```

### SpringBoot对静态资源的映射规则:

```java
@ConfigurationProperties(
    prefix = "spring.resources",
    ignoreUnknownFields = false
)
public class ResourceProperties {
    //可以设置和资源有关的参数,缓存时间
```



```java
public void addResourceHandlers(ResourceHandlerRegistry registry) {
            if (!this.resourceProperties.isAddMappings()) {
                logger.debug("Default resource handling disabled");
            } else {
                Duration cachePeriod = this.resourceProperties.getCache().getPeriod();
                CacheControl cacheControl = this.resourceProperties.getCache().getCachecontrol().toHttpCacheControl();
                if (!registry.hasMappingForPattern("/webjars/**")) {
                    this.customizeResourceHandlerRegistration(registry.addResourceHandler(new String[]{"/webjars/**"}).addResourceLocations(new String[]{"classpath:/META-INF/resources/webjars/"}).setCachePeriod(this.getSeconds(cachePeriod)).setCacheControl(cacheControl));
                }

                String staticPathPattern = this.mvcProperties.getStaticPathPattern();
                if (!registry.hasMappingForPattern(staticPathPattern)) {
                    this.customizeResourceHandlerRegistration(registry.addResourceHandler(new String[]{staticPathPattern}).addResourceLocations(WebMvcAutoConfiguration.getResourceLocations(this.resourceProperties.getStaticLocations())).setCachePeriod(this.getSeconds(cachePeriod)).setCacheControl(cacheControl));
                }

            }
        }
//配置欢迎页映射
@Bean
        public WelcomePageHandlerMapping welcomePageHandlerMapping(ApplicationContext applicationContext, FormattingConversionService mvcConversionService, ResourceUrlProvider mvcResourceUrlProvider) {
            WelcomePageHandlerMapping welcomePageHandlerMapping = new WelcomePageHandlerMapping(new TemplateAvailabilityProviders(applicationContext), applicationContext, this.getWelcomePage(), this.mvcProperties.getStaticPathPattern());
            welcomePageHandlerMapping.setInterceptors(this.getInterceptors(mvcConversionService, mvcResourceUrlProvider));
            welcomePageHandlerMapping.setCorsConfigurations(this.getCorsConfigurations());
            return welcomePageHandlerMapping;
        }

```

1. 所有`/webjars/**`,都去`classpath:/META-INF/resources/webjars/`找资源

   webjars:以jar包的方式引入静态资源

   ![image-20200928204651307](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200928204651307.png)

   `localhost:8080/webjars/jquery/3.3.1/jquery.js`

   ```xml
          <!--        引入jquery-webjar,在访问的时候只需要写webjars下面资源的名称即可-->
           <dependency>
               <groupId>org.webjars</groupId>
               <artifactId>jquery</artifactId>
               <version>3.3.1</version>
           </dependency>
   ```

2. "/**"访问当前项目的任何资源(静态资源的文件夹)，

   ```java
   "classpath:/META-INF/resources/", 
   "classpath:/resources/",
   "classpath:/static/",
   "classpath:/public/"
    "/":当前项目的根路径
   ```

3. 欢迎页：静态资源文件夹下的所有index.html的页面：被"/**"映射；

   `localhost:8080/`找index页面

4. 所有的`**/favicon.ico`都是在静态资源文件下找；(这是网页的图标哈，好像2.xx的配置不一样了，但我不知道，我和老师用的是1.5.9的)



### 模板引擎

![image-20200929094522758](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200929094522758.png)

> 把数据填充到里面去，因为我们要用到的是html，而不是jsp

1. 引入thymeleaf:，

   ```xml
   <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter-test</artifactId>
               <scope>test</scope>
           </dependency>
   
   切换thymeleaf版本
   <properties>
    <thymeleaf.version>3.0.9.RELEASE</thymeleaf.version>
   <!--        布局功能的支持程序 thymeleaf3主程序 layout2以上版本-->
   <!--        thymeleaf2 layout1-->
           <thymeleaf-layout-dialect.version>2.2.2</thymeleaf-layout-dialect.version>
       </properties>
   ```

2. Thymeleaf使用&语法

   ```java
   @ConfigurationProperties(
       prefix = "spring.thymeleaf"
   )
   public class ThymeleafProperties {
       private static final Charset DEFAULT_ENCODING;
       public static final String DEFAULT_PREFIX = "classpath:/templates/";
       public static final String DEFAULT_SUFFIX = ".html";
       //只要我们把html页面放在classpath:/templates/,thymeleaf就能帮我们自动渲染了，而且好像还是视图解析器的前缀和后缀？应该是把，毕竟你把静态资源放那里他就帮你渲染，那肯定是需要访问 的，那视图解析器也一起把
   ```

   只要我们把HTML页面放在`classpath:/templates/,thymeleaf`就自动渲染

   使用：

   1. 导入thymeleaf的名称空间

      ```xml
      <html lang="en" xmlns:th="http://www.thymeleaf.org">
      ```

   2. 使用thymeleaf语法

      ```html
      <!DOCTYPE html>
      <html lang="en" xmlns:th="http://www.thymeleaf.org">
      <head>
          <meta charset="UTF-8">
          <title>Title</title>
      </head>
      <body>
      <h1>成功!</h1>
      <!--th:text 将div里面的文本内容设置为-->
      <div id="div01" class="myDiv" th:id="${hello}" th:class="${hello}" th:text="${hello}">这是显示欢迎信息</div>
      <hr/>
      <div th:text="${hello}"></div>
      <div th:utext="${hello}"></div>
      <hr/>
      <!--th:each每次遍历都会生成当前这个标签-->
      <!--3个h4-->
      <h4 th:text="${user}" th:each="user:${users}"></h4>
      <hr/>
      
      <h4>
      <!--    这里怎么理解呢，就是th:each遍历的标签每次都会生成当前的标签，然后的参数是你每次要遍历的内容，顺便可以取个别名
              th:text 的话就是你该标签下的内容了，你可以直接用th:text 也可以想着以前用jsp的时候${},但是这里的话要用另外一种代替，就是[[${user}]]
      -->
          <span th:each="user:${users}"> [[${user}]] </span>
      </h4>
      </body>
      </html>
      ```

3. 语法规则

   1. `th:text`:改变当前元素里面的文本内容；

      `th:任意html属性;来替换原生属性的值`

      

      ![image-20200929113356192](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200929113356192.png)

      ​	

   2. 表达式?

      ```properties
      Simple expressions:（表达式语法）
          Variable Expressions: ${...}：获取变量值；OGNL；
          		1）、获取对象的属性、调用方法
          		2）、使用内置的基本对象：
          			#ctx : the context object.
          			#vars: the context variables.
                      #locale : the context locale.
                      #request : (only in Web Contexts) the HttpServletRequest object.
                      #response : (only in Web Contexts) the HttpServletResponse object.
                      #session : (only in Web Contexts) the HttpSession object.
                      #servletContext : (only in Web Contexts) the ServletContext object.
                      
                      ${session.foo}
                  3）、内置的一些工具对象：
      #execInfo : information about the template being processed.
      #messages : methods for obtaining externalized messages inside variables expressions, in the same way as they would be obtained using #{…} syntax.
      #uris : methods for escaping parts of URLs/URIs
      #conversions : methods for executing the configured conversion service (if any).
      #dates : methods for java.util.Date objects: formatting, component extraction, etc.
      #calendars : analogous to #dates , but for java.util.Calendar objects.
      #numbers : methods for formatting numeric objects.
      #strings : methods for String objects: contains, startsWith, prepending/appending, etc.
      #objects : methods for objects in general.
      #bools : methods for boolean evaluation.
      #arrays : methods for arrays.
      #lists : methods for lists.
      #sets : methods for sets.
      #maps : methods for maps.
      #aggregates : methods for creating aggregates on arrays or collections.
      #ids : methods for dealing with id attributes that might be repeated (for example, as a result of an iteration).
      
          Selection Variable Expressions: *{...}：选择表达式：和${}在功能上是一样；
          	补充：配合 th:object="${session.user}：
         <div th:object="${session.user}">
          <p>Name: <span th:text="*{firstName}">Sebastian</span>.</p>
          <p>Surname: <span th:text="*{lastName}">Pepper</span>.</p>
          <p>Nationality: <span th:text="*{nationality}">Saturn</span>.</p>
          </div>
          
          Message Expressions: #{...}：获取国际化内容
          Link URL Expressions: @{...}：定义URL；
          		@{/order/process(execId=${execId},execType='FAST')}
          Fragment Expressions: ~{...}：片段引用表达式
          		<div th:insert="~{commons :: main}">...</div>
          		
      Literals（字面量）
            Text literals: 'one text' , 'Another one!' ,…
            Number literals: 0 , 34 , 3.0 , 12.3 ,…
            Boolean literals: true , false
            Null literal: null
            Literal tokens: one , sometext , main ,…
      Text operations:（文本操作）
          String concatenation: +
          Literal substitutions: |The name is ${name}|
      Arithmetic operations:（数学运算）
          Binary operators: + , - , * , / , %
          Minus sign (unary operator): -
      Boolean operations:（布尔运算）
          Binary operators: and , or
          Boolean negation (unary operator): ! , not
      Comparisons and equality:（比较运算）
          Comparators: > , < , >= , <= ( gt , lt , ge , le )
          Equality operators: == , != ( eq , ne )
      Conditional operators:条件运算（三元运算符）
          If-then: (if) ? (then)
          If-then-else: (if) ? (then) : (else)
          Default: (value) ?: (defaultvalue)
      Special tokens:
          No-Operation: _ 
      ```

4. SpringMVC自动配置

   https://docs.spring.io/spring-boot/docs/1.5.10.RELEASE/reference/htmlsingle/#boot-features-developing-web-applications

   1. Spring MVC auto-configuration

   Spring Boot 自动配置好了SpringMVC

   以下是SpringBoot对SpringMVC的默认配置:**==（WebMvcAutoConfiguration）==**

   - Inclusion of `ContentNegotiatingViewResolver` and `BeanNameViewResolver` beans.

     - 自动配置了ViewResolver（视图解析器：根据方法的返回值得到视图对象（View），视图对象决定如何渲染（转发？重定向？））
     - ContentNegotiatingViewResolver：组合所有的视图解析器的；
     - ==如何定制：我们可以自己给容器中添加一个视图解析器；自动的将其组合进来；==

   - Support for serving static resources, including support for WebJars (see below).静态资源文件夹路径,webjars

   - Static `index.html` support. 静态首页访问

   - Custom `Favicon` support (see below).  favicon.ico

     

   - 自动注册了 of `Converter`, `GenericConverter`, `Formatter` beans.

     - Converter：转换器；  public String hello(User user)：类型转换使用Converter
     - `Formatter`  格式化器；  2017.12.17===Date；

   ```java
   		@Bean
   		@ConditionalOnProperty(prefix = "spring.mvc", name = "date-format")//在文件中配置日期格式化的规则
   		public Formatter<Date> dateFormatter() {
   			return new DateFormatter(this.mvcProperties.getDateFormat());//日期格式化组件
   		}
   ```

   ​	==自己添加的格式化器转换器，我们只需要放在容器中即可==

   - Support for `HttpMessageConverters` (see below).

     - HttpMessageConverter：SpringMVC用来转换Http请求和响应的；User---Json；

     - `HttpMessageConverters` 是从容器中确定；获取所有的HttpMessageConverter；

       ==自己给容器中添加HttpMessageConverter，只需要将自己的组件注册容器中（@Bean,@Component）==

       

   - Automatic registration of `MessageCodesResolver` (see below).定义错误代码生成规则

   - Automatic use of a `ConfigurableWebBindingInitializer` bean (see below).

     ==我们可以配置一个ConfigurableWebBindingInitializer来替换默认的；（添加到容器）==

     ```
     初始化WebDataBinder；
     请求数据=====JavaBean；
     ```

   **org.springframework.boot.autoconfigure.web：web的所有自动场景；**

   If you want to keep Spring Boot MVC features, and you just want to add additional [MVC configuration](https://docs.spring.io/spring/docs/4.3.14.RELEASE/spring-framework-reference/htmlsingle#mvc) (interceptors, formatters, view controllers etc.) you can add your own `@Configuration` class of type `WebMvcConfigurerAdapter`, but **without** `@EnableWebMvc`. If you wish to provide custom instances of `RequestMappingHandlerMapping`, `RequestMappingHandlerAdapter` or `ExceptionHandlerExceptionResolver` you can declare a `WebMvcRegistrationsAdapter` instance providing such components.

   If you want to take complete control of Spring MVC, you can add your own `@Configuration` annotated with `@EnableWebMvc`.

   2. 扩展SpringMVC

      ```xml
      <mvc:view-controller path="/hello" view-name="success1"/>
          <mvc:interceptors>
              <mvc:interceptor>
                  <mvc:mapping path="/hello"/>
                  <bean></bean>
              </mvc:interceptor>
          </mvc:interceptors>
      ```

      编写一个配置类(@Configuration),是`WebMvcConfigurerAdapter`类型；还不能标注`EnableWebMvc`

      既保留了所有的自动配置，也能用我们扩展的配置

      ```java
      //实现WebMvcConfigurer可以来扩展SpringMvc的功能
      @Configuration
      public class MyMvcConfig implements WebMvcConfigurer {
      
          @Override
          public void addViewControllers(ViewControllerRegistry registry) {
              //浏览器发送 /zbr 请求来到success
              registry.addViewController("/zbr").setViewName("success1");
          }
      }
      
      ```

      原理：

      1. `WebMvcAutoConfiguration`是SpringMvc的自动配置类

      2. 在做其他自动配置时会导入;`@Import(EnableWebMvcConfiguration.class)`

         ```java
          @Configuration(
                 proxyBeanMethods = false
             )
             public static class EnableWebMvcConfiguration extends DelegatingWebMvcConfiguration implements ResourceLoaderAware {
                 
                  private final WebMvcConfigurerComposite configurers = new WebMvcConfigurerComposite();
         
             public DelegatingWebMvcConfiguration() {
             }
         
              //从容器中获取所有的WebMvcConfigurer   
             @Autowired(
                 required = false
             )
             public void setConfigurers(List<WebMvcConfigurer> configurers) {
                 if (!CollectionUtils.isEmpty(configurers)) {
                     this.configurers.addWebMvcConfigurers(configurers);
                //一个参考实现；将所有的WebMvcConfigurer相关配置都来一起调用
                    // @Override
                      // public void addViewControllers(ViewControllerRegistry registry) {
                       //    for (WebMvcConfigurer delegate : this.delegates) {
                        //       delegate.addViewControllers(registry);
                        //   }
                 }
         
             }
         ```

      3. 容器中所有的`WebMvcConfigurer`都会一起起作用；包括我们自己写的

      4. 我们的配置类也会被调用

      效果：`SpringMvc`的自动配置和我们的扩展配置都会起作用

   3. 全面接管SpringMvc

      SpringBoot对SpringMvc的自动配置不需要了，所有都是我们自己配，所有的SpringMVC的自动配置都失效

      我们需要在配置类中添加`@EnableWebMvc`即可

      ```java
      //实现WebMvcConfigurer可以来扩展SpringMvc的功能
      @EnableWebMvc
      @Configuration
      public class MyMvcConfig implements WebMvcConfigurer {
      
          @Override
          public void addViewControllers(ViewControllerRegistry registry) {
              //浏览器发送 /zbr 请求来到success
              registry.addViewController("/zbr").setViewName("success1");
          }
      }
      
      ```

      原理：

      为什么`@EnableWebMvc`自动配置就失效了？

      1. `EnableWebMvc`的核心

         ```java
         @Import(DelegatingWebMvcConfiguration.class)
         public @interface EnableWebMvc{}
         ```

      2. ```java
         @Configuration
         public class DelegatingWebMvcConfiguration extends WebMvcConfigurationSupport{}
         ```

      3. ```java
         @Configuration(
             proxyBeanMethods = false
         )
         @ConditionalOnWebApplication(
             type = Type.SERVLET
         )
         @ConditionalOnClass({Servlet.class, DispatcherServlet.class, WebMvcConfigurer.class})
         //容器中没有这个组件的时候，这个自动配置类才生效
         @ConditionalOnMissingBean({WebMvcConfigurationSupport.class})
         @AutoConfigureOrder(-2147483638)
         @AutoConfigureAfter({DispatcherServletAutoConfiguration.class, TaskExecutionAutoConfiguration.class, ValidationAutoConfiguration.class})
         public class WebMvcAutoConfiguration {
         ```

      4. `@EnableWebMvc`将`WebMvcConfigurationSupport`组件导入尽量

      5. 导入的`WebMvcConfigurationSupport`只是SpirngMVC最基本的功能

   

5. 如何修改SpringBoot的默认配置

   模式

   1. SpringBoot在自动配置很多组件的时候，先看看容器中有没有用户自己配置的(@Bean @Component)如果有就用用户配置的，如果没有，才自动配置；如果有些组件可以有多个(ViewResolver)将用户配置和自己默认的组合起来
   2. 在SpringBoot中会有非常多的`xxxConfigurer`帮助我们进行扩展配置

6. RestfulCRUD

   1. 默认访问首页

      但是如果你在配置中加了个基础路径的话，`server.servlet.context-path=/crud`,那`thymeleaf`这个模板引擎是有渲染的，意思是视图解析器也是有的，他会默认加上的，但是如果你用一些静态资源比如说图片的时候你直接写`     <link href="asserts/css/signin.css" rel="stylesheet" th:href="@{/asserts/css/signin.css}">`,你用的是相对路径，那肯定是不保险的，在某些情况下是用不了的，但如果是用了`th:href`的话就会自动帮你渲染帮你加上去变为根目录，这就是用`thymeleaf`的好处

      ----------------------------anki到这里呀 2020.11.8------------------------

   2. 国际化
   
      1. 编写国际化配置文件
   2. 使用`ResourceBundleMessageSource`管理国际化资源文件
      3. 在页面使用`fmt:message`取出国际化内容

      步骤：

      1. 编写国际化配置文件，抽取页面需要显示的国际化消息

         ![image-20201003172258348](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201003172258348.png)

      2. SpringBoot自动配置好了管理国际化资源文件的组件
   
         ```java
         @ConfigurationProperties(prefix = "spring.messages")
         public class MessageSourceAutoConfiguration {
             
             /**
         	 * Comma-separated list of basenames (essentially a fully-qualified classpath
         	 * location), each following the ResourceBundle convention with relaxed support for
         	 * slash based locations. If it doesn't contain a package qualifier (such as
         	 * "org.mypackage"), it will be resolved from the classpath root.
         	 */
         	private String basename = "messages";  
             //我们的配置文件可以直接放在类路径下叫messages.properties；
             
             @Bean
         	public MessageSource messageSource() {
         		ResourceBundleMessageSource messageSource = new ResourceBundleMessageSource();
         		if (StringUtils.hasText(this.basename)) {
                     //设置国际化资源文件的基础名（去掉语言国家代码的）
         			messageSource.setBasenames(StringUtils.commaDelimitedListToStringArray(
         					StringUtils.trimAllWhitespace(this.basename)));
         		}
         		if (this.encoding != null) {
         			messageSource.setDefaultEncoding(this.encoding.name());
         		}
         		messageSource.setFallbackToSystemLocale(this.fallbackToSystemLocale);
         		messageSource.setCacheSeconds(this.cacheSeconds);
         		messageSource.setAlwaysUseMessageFormat(this.alwaysUseMessageFormat);
         		return messageSource;
      	}
         ```

      3. 去页面获取国际化的值

         ![image-20201003214532809](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201003214532809.png)

         设置全局的配置
   
         ```html
         <!DOCTYPE html>
         <html lang="en" xmlns:th="http://www.thymeleaf.org">
         	<head>
         		<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
         		<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
         		<meta name="description" content="">
         		<meta name="author" content="">
         		<title>Signin Template for Bootstrap</title>
         		<!-- Bootstrap core CSS -->
         		<link href="asserts/css/bootstrap.min.css" th:href="@{/webjars/bootstrap/4.0.0/css/bootstrap.css}" rel="stylesheet">
         		<!-- Custom styles for this template -->
         		<link href="asserts/css/signin.css" rel="stylesheet" th:href="@{/asserts/css/signin.css}">
         <!--		<link href="asserts/css/signin.css" rel="stylesheet" >-->
         	</head>
         
         	<body class="text-center">
         		<form class="form-signin" action="dashboard.html">
         			<img class="mb-4" th:src="@{/asserts/img/bootstrap-solid.svg}" src="asserts/img/bootstrap-solid.svg" alt="" width="72" height="72">
         			<h1 class="h3 mb-3 font-weight-normal" th:text="#{login.tip}">Please sign in</h1>
         			<label class="sr-only" th:text="#{login.username}">Username</label>
         			<input type="text" class="form-control" placeholder="Username" th:placeholder="#{login.username}" required="" autofocus="">
         			<label class="sr-only" th:placeholder="#{login.password}">Password</label>
         			<input type="password" class="form-control" placeholder="Password" th:placeholder="#{login.password}" required="">
         			<div class="checkbox mb-3">
         				<label>
                   <input type="checkbox" value="remember-me" > [[#{login.remember}]]
                 </label>
         			</div>
         			<button class="btn btn-lg btn-primary btn-block" type="submit" th:text="#{login.btn}">Sign in</button>
         			<p class="mt-5 mb-3 text-muted">© 2017-2018</p>
         			<a class="btn btn-sm">中文</a>
         			<a class="btn btn-sm">English</a>
         		</form>
         
         	</body>
         
      </html>
         ```

         效果：根据浏览器语言设置的信息切换了国际化；

         原理：

         ​	国际化Locale(区域信息对象)；`LocaleResolver`(获取区域信息对象)
   
         ```java
         		@Bean
         		@ConditionalOnMissingBean
         		@ConditionalOnProperty(prefix = "spring.mvc", name = "locale")
         		public LocaleResolver localeResolver() {
         			if (this.mvcProperties
         					.getLocaleResolver() == WebMvcProperties.LocaleResolver.FIXED) {
         				return new FixedLocaleResolver(this.mvcProperties.getLocale());
         			}
         			AcceptHeaderLocaleResolver localeResolver = new AcceptHeaderLocaleResolver();
         			localeResolver.setDefaultLocale(this.mvcProperties.getLocale());
         			return localeResolver;
         		}
      默认的就是根据请求头带来的区域信息获取Locale进行国际化
         ```

      4. 点击链接切换国际化
   
         ```java
         /**
          * 可以在链接上携带Locale信息
          */
         public class MyLocaleResolver implements LocaleResolver {
             @Override
             public Locale resolveLocale(HttpServletRequest httpServletRequest) {
                 String l = httpServletRequest.getParameter("l");
                 Locale locale = Locale.getDefault();
                 if(!StringUtils.isEmpty(l)){
                     String[] split = l.split("_");
                      locale = new Locale(split[0], split[1]);
         
                 }
                 return locale;
             }
         
             @Override
             public void setLocale(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Locale locale) {
         
             }
         }
         
         //这是在MyMvcConfig中的
         @Bean
             public LocaleResolver localeResolver(){
                 return new MyLocaleResolver();
          }
         ```

         然后加到容器中就可以了`MyMvcConfig`

   3. 登录

      模板引擎页面修改以后，要实时生效

      1. 禁用模板引擎的缓存

         

      2. 页面修改完以后`ctrl+f9`：重新编译

         登录错误消息的显示
   
         ```html
      	<p style="color: red" th:text="${message}" th:if="${not #strings.isEmpty(message)}"></p>
         ```

   4. 拦截器进行登录检查

      拦截器
   
      ```java
      /**
       * 登陆检查，
       */
      public class LoginHandlerInterceptor implements HandlerInterceptor {
          //目标方法执行之前
          @Override
          public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
              Object user = request.getSession().getAttribute("loginUser");
              if(user == null){
                  //未登陆，返回登陆页面
                  request.setAttribute("msg","没有权限请先登陆");
                  request.getRequestDispatcher("/index.html").forward(request,response);
                  return false;
              }else{
                  //已登陆，放行请求
                  return true;
              }
      
          }
      
          @Override
          public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
      
          }
      
          @Override
          public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
      
          }
      }
   
      ```

      

      注册拦截器
   
      ```java
        //所有的WebMvcConfigurerAdapter组件都会一起起作用
          @Bean //将组件注册在容器
          public WebMvcConfigurerAdapter webMvcConfigurerAdapter(){
              WebMvcConfigurerAdapter adapter = new WebMvcConfigurerAdapter() {
                  @Override
                  public void addViewControllers(ViewControllerRegistry registry) {
                      registry.addViewController("/").setViewName("login");
                      registry.addViewController("/index.html").setViewName("login");
                      registry.addViewController("/main.html").setViewName("dashboard");
                  }
      
                  //注册拦截器
                  @Override
                  public void addInterceptors(InterceptorRegistry registry) {
                      //super.addInterceptors(registry);
                      //静态资源；  *.css , *.js
                      //SpringBoot已经做好了静态资源映射
                      registry.addInterceptor(new LoginHandlerInterceptor()).addPathPatterns("/**")
                              .excludePathPatterns("/index.html","/","/user/login");
                  }
              };
              return adapter;
       }
      ```

   5. CRUD-员工列表

      实验要求：

      1. RestfulCRUD:CRUD满足Rest风格

         URI:`/资源名称/资源标识`  HTTP请求方式区分对资源CRUD操作
   
         |      | 普通CRUD(uri来区分操作) | ResufulCRUD       |
         | ---- | ----------------------- | ----------------- |
         | 查询 | getEmp                  | emp---GET         |
         | 添加 | addEmp?xxx              | emp---POST        |
      | 修改 | updateEmp?id=xxx&xxx=xx | emp(id)---PUT     |
         | 删除 | deleteEmp?id=1          | emo/(id)---DELETE |

      2. 实验的请求架构
   
         |                                    | 请求URI  | 请求方式 |
         | ---------------------------------- | -------- | -------- |
         | 查询所有员工                       | emps     | GET      |
         | 查询某个员工                       | emp/{id} | GET      |
         | 来到添加页面                       | emp      | GET      |
         | 添加员工                           | emp      | POST     |
         | 来到修改页面(查出员工进行信息回显) | emp/{id} | GET      |
      | 修改员工                           | emp      | PUT      |
         | 删除员工                           | emp/{id} | DELETE   |

         

      4. 员工列表

         ##### thymeleaf公共页面元素抽取
   
         ```html
         1.抽取公共片段
         1、抽取公共片段
         <div th:fragment="copy">
         &copy; 2011 The Good Thymes Virtual Grocery
         </div>
         
         2、引入公共片段
         <div th:insert="~{footer :: copy}"></div>
         ~{templatename::selector}：模板名::选择器
         ~{templatename::fragmentname}:模板名::片段名
         
         3、默认效果：
         insert的公共片段在div标签中
         如果使用th:insert等属性进行引入，可以不用写~{}：
      行内写法可以加上：[[~{}]];[(~{})]；
         ```
   
         三引入公共片段的th属性 
         
         **th:insert**:将公共片段整个插入到声明引入的元素中
         
         **th:replace**:将声明引入的元素替换为公共片段
         
         **th:include**：将被引入的片段的内容包含进这个标签中
         
         ```html
         <footer th:fragment="copy">
         &copy; 2011 The Good Thymes Virtual Grocery
         </footer>
         
         引入方式
         <div th:insert="footer :: copy"></div>
         <div th:replace="footer :: copy"></div>
         <div th:include="footer :: copy"></div>
         
         效果
         <div>
             <footer>
             &copy; 2011 The Good Thymes Virtual Grocery
             </footer>
         </div>
         
         <footer>
         &copy; 2011 The Good Thymes Virtual Grocery
         </footer>
         
         <div>
         &copy; 2011 The Good Thymes Virtual Grocery
         </div>
         ```
         
         引入片段的时候传入参数：
         
         ```html
         <nav class="col-md-2 d-none d-md-block bg-light sidebar" id="sidebar">
             <div class="sidebar-sticky">
                 <ul class="nav flex-column">
                     <li class="nav-item">
                         <a class="nav-link active"
                            th:class="${activeUri=='main.html'?'nav-link active':'nav-link'}"
                            href="#" th:href="@{/main.html}">
                             <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-home">
                                 <path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path>
                                 <polyline points="9 22 9 12 15 12 15 22"></polyline>
                             </svg>
                             Dashboard <span class="sr-only">(current)</span>
                         </a>
                     </li>
         
         <!--引入侧边栏;传入参数-->
         <div th:replace="commons/bar::#sidebar(activeUri='emps')"></div>
         ```
      
   6. CRUD---员工添加
   
      添加页面
   
      ```html
      <form>
          <div class="form-group">
              <label>LastName</label>
              <input type="text" class="form-control" placeholder="zhangsan">
          </div>
          <div class="form-group">
              <label>Email</label>
              <input type="email" class="form-control" placeholder="zhangsan@atguigu.com">
          </div>
          <div class="form-group">
              <label>Gender</label><br/>
              <div class="form-check form-check-inline">
                  <input class="form-check-input" type="radio" name="gender"  value="1">
                  <label class="form-check-label">男</label>
              </div>
              <div class="form-check form-check-inline">
                  <input class="form-check-input" type="radio" name="gender"  value="0">
                  <label class="form-check-label">女</label>
              </div>
          </div>
          <div class="form-group">
              <label>department</label>
              <select class="form-control">
                  <option>1</option>
                  <option>2</option>
                  <option>3</option>
                  <option>4</option>
                  <option>5</option>
              </select>
          </div>
          <div class="form-group">
              <label>Birth</label>
              <input type="text" class="form-control" placeholder="zhangsan">
          </div>
          <button type="submit" class="btn btn-primary">添加</button>
      </form>
      ```
   
      提交的数据格式不对：生日:日期;
   
      `2017-12-12;2017/12/12;2017.12.12`
   
      日期的格式化；SpringMvc将页面提交的值需要转为指定的类型
   
      `2017.12.12`---Date:类型转换、格式化
   
      默认日期是按照`/`的方式；
   
      > 我在想一个问题，员工那里的，因为添加和修改都共用一个页面，而且还是转发，这样的话参数不会共享吗？但是我觉得这里没有是因为用的是`/`，而不是`?`来搞参数的
   
   7. CRUD-员工修改
   
      修改二合一表单
   
      ```html
      <!DOCTYPE html>
      <!-- saved from url=(0052)http://getbootstrap.com/docs/4.0/examples/dashboard/ -->
      <html lang="en"  xmlns:th="http://www.thymeleaf.org">
      
      	<head>
      		<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
      		<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
      		<meta name="description" content="">
      		<meta name="author" content="">
      
      		<title>Dashboard Template for Bootstrap</title>
      		<!-- Bootstrap core CSS -->
      		<link href="../../static/asserts/css/bootstrap.min.css" th:href="@{/webjars/bootstrap/4.0.0/css/bootstrap.css}" rel="stylesheet">
      
      		<!-- Custom styles for this template -->
      		<link href="../../static/asserts/css/dashboard.css" th:href="@{/asserts/css/dashboard.css}" rel="stylesheet">
      		<style type="text/css">
      			/* Chart.js */
      			
      			@-webkit-keyframes chartjs-render-animation {
      				from {
      					opacity: 0.99
      				}
      				to {
      					opacity: 1
      				}
      			}
      			
      			@keyframes chartjs-render-animation {
      				from {
      					opacity: 0.99
      				}
      				to {
      					opacity: 1
      				}
      			}
      			
      			.chartjs-render-monitor {
      				-webkit-animation: chartjs-render-animation 0.001s;
      				animation: chartjs-render-animation 0.001s;
      			}
      		</style>
      	</head>
      
      	<body>
      <!--		引入抽取的topbar-->
      <!--		模板名：会使用thymeleaf的前后缀配置规则进行解析-->
      			<div th:replace="commons/bar::topbar"></div>
      
      
      		<div class="container-fluid">
      			<div class="row">
      <!--				引入侧边栏-->
      				<div th:replace="commons/bar::#sidebar(activeUri='emps')"></div>
      
      				<main role="main" class="col-md-9 ml-sm-auto col-lg-10 pt-3 px-4">
      <!--					需要区分是员工修改还是员工添加-->
      					<form th:action="@{/emp}" method="post">
      <!--						发送put请求修改员工数据-->
      <!--						1.SpringMvc中配置HiddenHttpMethodFilter(SpringBoot自动配好的)
      							2.页面创建一个post表单
      							3.创建一个input项，name="_method";值就是我们指定的请求方式(为什么要转，因为表单只支持post和get)
      -->
      
      						<input type="hidden" name="_method" value="put" th:if="${emp!=null}">
      <!--						这个th:if的意思是判断正确了才会生成这个标签-->
      						<input type="hidden" name="id" th:value="${emp.id}" th:if="${emp!=null}">
      						<div class="form-group">
      							<label>LastName</label>
      							<input name="lastName" type="text" class="form-control" placeholder="zhangsan" th:value="${emp!=null}?${emp.lastName}">
      						</div>
      						<div class="form-group">
      							<label>Email</label>
      							<input name="email" type="email" class="form-control" placeholder="zhangsan@atguigu.com" th:value="${emp!=null}?${emp.email}">
      						</div>
      						<div class="form-group">
      							<label>Gender</label><br/>
      							<div class="form-check form-check-inline">
      								<input class="form-check-input" type="radio" name="gender"  value="1" th:checked="${emp!=null}?${emp.gender==1}">
      								<label class="form-check-label">男</label>
      							</div>
      							<div class="form-check form-check-inline">
      								<input class="form-check-input" type="radio" name="gender"  value="0" th:checked="${emp!=null}?${emp.gender==0}">
      								<label class="form-check-label">女</label>
      							</div>
      						</div>
      						<div class="form-group">
      							<label>department</label>
      <!--							提交的是部门的id-->
      							<select class="form-control" name="department.id">
      								<option th:selected="${emp!=null}?${dept.id == emp.department.id}" th:each="dept:${depts}" th:text="${dept.departmentName}" th:value="${dept.id}">1</option>
      							</select>
      						</div>
      						<div class="form-group">
      							<label>Birth</label>
      							<input name="birth" th:value="${emp!=null}?${#dates.format(emp.birth,'yyyy-MM-dd HH:mm')}" type="text" class="form-control" placeholder="zhangsan">
      						</div>
      						<button type="submit" class="btn btn-primary" th:text="${emp!=null}?'修改':'添加'">添加</button>
      					</form>
      
      				</main>
      			</div>
      		</div>
      
      		<!-- Bootstrap core JavaScript
          ================================================== -->
      		<!-- Placed at the end of the document so the pages load faster -->
      		<script type="text/javascript" src="asserts/js/jquery-3.2.1.slim.min.js" th:src="@{/webjars/jquery/3.3.1/jquery.js}"></script>
      		<script type="text/javascript" src="asserts/js/popper.min.js" th:src="@{/webjars/popper.js/1.11.1/dist/popper.js}"></script>
      		<script type="text/javascript" src="asserts/js/bootstrap.min.js" th:src="@{/webjars/bootstrap/4.0.0/js/bootstrap.js}"></script>
      
      		<!-- Icons -->
      		<script type="text/javascript" src="asserts/js/feather.min.js" th:src="@{/asserts/js/feather.min.js}"></script>
      		<script>
      			feather.replace()
      		</script>
      
      		<!-- Graphs -->
      		<script type="text/javascript" src="../../static/asserts/js/Chart.min.js" th:src="@{/asserts/js/Chart.min.js}"></script>
      		<script>
      			var ctx = document.getElementById("myChart");
      			var myChart = new Chart(ctx, {
      				type: 'line',
      				data: {
      					labels: ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"],
      					datasets: [{
      						data: [15339, 21345, 18483, 24003, 23489, 24092, 12034],
      						lineTension: 0,
      						backgroundColor: 'transparent',
      						borderColor: '#007bff',
      						borderWidth: 4,
      						pointBackgroundColor: '#007bff'
      					}]
      				},
      				options: {
      					scales: {
      						yAxes: [{
      							ticks: {
      								beginAtZero: false
      							}
      						}]
      					},
      					legend: {
      						display: false,
      					}
      				}
      			});
      		</script>
      
      	</body>
      
      </html>
      ```
   
      > 说明一下，要想修改表单提交方式的话要在`application`资源文件中改一个属性
      >
      > ```properties
      > 
      > server.servlet.context-path=/crud
      > # 禁用缓存
      > spring.thymeleaf.cache=false
      > # 为什么要设置这个，因为默认他国际化文件是从类路径下的properties文件中找的，因为我们这里没按规定的要求放，所以就需要自己设置路径
      > spring.messages.basename=i18n/login
      > 
      > # 在这里说下我之前好像说明白了properties那里的setting,首先改为utf-8指的是我们要用utf-8来解码和编码文件，那转为ascii码啥意思，我认为是把整个文件都保存为ascii码，那在哪里打开都不会报错哈？？？
      > # 好像又不懂了，那中文咋地搞？
      > 
      > # 这个是能以什么方式接受Date,这个就是设定好为我们常用的，而不是Date默认的
      > spring.mvc.format.date=yyyy-MM-dd
      > # 可以在input框的hidden中带上要用的方法
      > spring.mvc.hiddenmethod.filter.enabled=true
      > ```
   
   8. CRUD-员工删除
   
      ```html
      <tr th:each="emp:${emps}">
       	<td th:text="${emp.id}"></td>
          <td>[[${emp.lastName}]]</td>
          <td th:text="${emp.email}"></td>
          <td th:text="${emp.gender}==0?'女':'男'"></td>
          <td th:text="${emp.department.departmentName}"></td>
          <td th:text="${#dates.format(emp.birth, 'yyyy-MM-dd HH:mm')}"></td>
          <td>
              <a class="btn btn-sm btn-primary" th:href="@{/emp/}+${emp.id}">编辑</a>
              <button th:attr="del_uri=@{/emp/}+${emp.id}" class="btn btn-sm btn-danger deleteBtn">删除</button>
          </td>
      </tr>
      
      <script>
      		$('.deleteBtn').click(function () {
      			//删除当前员工,这个因为如果每个button都有表单的话就太冗余了,所以干脆绑定js事件，然后现在的问题就是uri的问题，可以在button那里自定义，然后再把这个自定义的属性加到表单里面去就可以了
      			$('#deleteEmpForm').attr("action",$(this).attr("del_uri")).submit();
      			return false;
      		});
      		</script>
      ```
   
7. 错误处理机制

   1. SpringBoot默认的错误处理机制

      默认效果:

      1. 浏览器，返回一个默认的错误页面

         

         ![image-20201005163138145](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201005163138145.png)

         浏览器发送请求的请求头：![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201005174740425.png)

      2. 如果是其他客户端，默认响应一个json数据

         ![image-20201005164817181](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201005164817181.png)

         ![image-20201005174752140](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201005174752140.png)

      原理：

      ​	可以参照`ErrorMvcAutoConfiguration`;错误处理的自动配置

      ​	给容器中添加了以下组件

      1. DefaultErrorAttributes

         ```java
         帮我们在页面共享信息；
         @Override
         	public Map<String, Object> getErrorAttributes(RequestAttributes requestAttributes,
         			boolean includeStackTrace) {
         		Map<String, Object> errorAttributes = new LinkedHashMap<String, Object>();
         		errorAttributes.put("timestamp", new Date());
         		addStatus(errorAttributes, requestAttributes);
         		addErrorDetails(errorAttributes, requestAttributes, includeStackTrace);
         		addPath(errorAttributes, requestAttributes);
         		return errorAttributes;
         	}
         ```

         

      2. BasicErrorController:处理默认/error请求

         ```java
         @Controller
         @RequestMapping("${server.error.path:${error.path:/error}}")
         public class BasicErrorController extends AbstractErrorController {
            @RequestMapping(produces = "text/html")//产生html类型的数据；浏览器发送的请求来到这个方法处理
         	public ModelAndView errorHtml(HttpServletRequest request,
         			HttpServletResponse response) {
         		HttpStatus status = getStatus(request);
         		Map<String, Object> model = Collections.unmodifiableMap(getErrorAttributes(
         				request, isIncludeStackTrace(request, MediaType.TEXT_HTML)));
         		response.setStatus(status.value());
                 
                 //去哪个页面作为错误页面；包含页面地址和页面内容
         		ModelAndView modelAndView = resolveErrorView(request, response, status, model);
         		return (modelAndView == null ? new ModelAndView("error", model) : modelAndView);
         	}
         
         	@RequestMapping
         	@ResponseBody    //产生json数据，其他客户端来到这个方法处理；
         	public ResponseEntity<Map<String, Object>> error(HttpServletRequest request) {
         		Map<String, Object> body = getErrorAttributes(request,
         				isIncludeStackTrace(request, MediaType.ALL));
         		HttpStatus status = getStatus(request);
         		return new ResponseEntity<Map<String, Object>>(body, status);
         	}
         ```

         

      3. ErrorPageCustomizer

         ```java
         //这个Value里面的东西的意思是从error.path中取，如果没有的话就用/error,所以${v1:v2}的意思就是先v1，v1没有再用v2
         @Value("${error.path:/error}")
         private String path = "/error";系统出现错误以后来到error请求进行处理；web.xml定制错误页面
         ```

         

      4. DefaultErrorViewResolver

         ```java
         @Override
         	public ModelAndView resolveErrorView(HttpServletRequest request, HttpStatus status,
         			Map<String, Object> model) {
         		ModelAndView modelAndView = resolve(String.valueOf(status), model);
         		if (modelAndView == null && SERIES_VIEWS.containsKey(status.series())) {
         			modelAndView = resolve(SERIES_VIEWS.get(status.series()), model);
         		}
         		return modelAndView;
         	}
         
         	private ModelAndView resolve(String viewName, Map<String, Object> model) {
                 //默认SpringBoot可以去找到一个页面？  error/404
         		String errorViewName = "error/" + viewName;
                 
                 //模板引擎可以解析这个页面地址就用模板引擎解析
         		TemplateAvailabilityProvider provider = this.templateAvailabilityProviders
         				.getProvider(errorViewName, this.applicationContext);
         		if (provider != null) {
                     //模板引擎可用的情况下返回到errorViewName指定的视图地址,这段话我不是很明白？意思是如果有使用模板引擎的话就会直接返回模板引擎提供的？没有的话就直接去静态资源中找，但是问题是如果静态资源中也无怎么办？难道会有一个默认的？
         			return new ModelAndView(errorViewName, model);
         		}
                 //模板引擎不可用，就在静态资源文件夹下找errorViewName对应的页面   error/404.html
         		return resolveResource(errorViewName, model);
         	}
         ```

         

      步骤：

      ​	一旦系统出现了4xx或5xx之类的错误，`ErrorPageCustomizer`就会生效(定制错误的响应规则)，就会来到`/error`请求,就会被BasicErrorController处理

      1. 响应页面：去哪个页面是由`DefaultErrorViewResolver`决定的

         ```java
         protected ModelAndView resolveErrorView(HttpServletRequest request,
               HttpServletResponse response, HttpStatus status, Map<String, Object> model) {
             //所有的ErrorViewResolver得到ModelAndView
            for (ErrorViewResolver resolver : this.errorViewResolvers) {
               ModelAndView modelAndView = resolver.resolveErrorView(request, status, model);
               if (modelAndView != null) {
                  return modelAndView;
               }
            }
            return null;
         }
         ```

         

   2. 如何定制错误响应

      1. 如何定制错误的页面

         1. 有模板引擎的情况下：`error/状态码`,将错误页面命名为错误状态码.html放在模板引擎文件夹里面的error文件夹下，发生

            此状态码的错误就会来到对应的页面

            我们可以使用4xx和5xx作为错误页面的文件夹来匹配这种类型的所有错误，精确优先(优先寻找精确的状态码.html);

            页面能获取的信息

            - timestamp:时间戳
            - status:状态码
            - error:错误提示
            - exception:异常对象
            - message:异常消息
            - errors:JSR303数据校验的错误都在这里

         2. 没有模板引擎(模板引擎找不到这个错误页面)，静态资源文件夹下找

         3. 以上都没有错误页面，默认来到SpringBoot默认的错误提示页面

         >  我感觉我大概明白了啥意思，发生错误的时候会在三种情况下去找页面，第一如果有模板引擎解析的那就直接用，没有的话就去静态资源文件夹下面找，再没有的话就用SpringBoot默认提供的。那以上的操作是怎么完成的呢？
>
         > 1. 首先错误被拦截下来，去到了`ErrorPageCustomizer`,定制规则？怎么个定制法我也不大清楚，接下来就是控制器`BasicErrorController`的流程了，跟别的请求无太大区别
         > 2. 但是问题是你怎么知道去哪个页面？那些错误信息你怎么去解析的？这时候就到了剩余几个组件的使用了，就像是你把一个东西给别人处理，先给别人老大，老大再交给小弟处理，老大就是`DefaultErrorViewResolver`,处理好之后他一并把所有结果返回给你。
         > 3. 说说老大这里搞什么，控制器的返回无非就是`ModelAndView`,那这里问题是你`ModelAndView`是怎么搞到的，这需要老大这边出面了，老大这边需要一些信息，才能搞吗，首先你的请求给我，状态码给我，map封装的数据给我，因为是我给你数据和视图，所以都由我来组装创建就可以了。
         > 4. 拿到信息之后，就让小弟去忙了，小弟的话就拿到了一些东西，拼接一下地址啥的，反正就是返回了哈，帮你搞定好之后你就按照老大这边的要求去做去放资源就可以了。
         
         

         

         

      2. 如何定制错误的json数据

         1. 自定义异常处理&返回定制的json数据

            ```java
      @ControllerAdvice
            public class MyExceptionHandler {
            //浏览器和客户端返回的都是json,自适应页面得首先你要去的是自定制的错误页面才可以自适应，因为返回json还是html
                @ResponseBody
                @ExceptionHandler(UserNotExistException.class)
                public Map<String,Object> handleException(Exception e){
                    Map<String,Object> map = new HashMap<>();
                    map.put("code","user.notexist");
                    map.put("message",e.getMessage());
                    return map;
            
                }
            }
            //没有自适应效果
            ```
      
            然后结果是postman和浏览器都是返回json数据了，我觉得把哈，这个发到自己定制的错误页面的前提是你没有自己在后台搞？就像`ConditionalMissingBean`一样，然后有个优先级关系？自己搞了json,那就后面的error也不看了？

         2. 转发到/error自适应响应效果处理

            ```java
      @ExceptionHandler(UserNotExistException.class)
                public String handleException(Exception e, HttpServletRequest request){
                    Map<String,Object> map = new HashMap<>();
                    //传入我们自己的错误状态码 4xx 5xx否则默认是200啦，就是状态码出错啦
                    /**
                     * Integer statusCode = (Integer) request.getAttribute("javax.servlet.error.status_code")
                     */
                    request.setAttribute("javax.servlet.error.status_code",400);
                    map.put("code","user.notexist");
                    map.put("message",e.getMessage());
            //转发到/error
                    //但是呢浏览器返回的不是json了，但是不是出现我们定制的页面，是因为不是4xx 5xx的状态码，而是2xx的，
                 //200的意思是成功处理了请求，而不是错误的状态码，意思就是我们成功处理了exception的请求，然后呢？跟正常的返回一个视图没什么两样的
                    return "forward:/error";
            
                }
            ```
            
         3. 将我们的定制数据携带出去;
         
            出现错误以后，会来到`/error`请求，会被`BasicErrorController`处理,响应出去可以获取的数据是由`getErrorAttributes`得到的是`AbstractErrorController(ErrorController)`规定的方法
         
            1. 完全编写一个`ErrorController`的实现类(或者是编写AbstractErrorController的子类)，放在容器中
         
            2. 页面上能用的数据，或者是json返回能用的数据都是通过`errorAttributes.getErrorAttributes`得到的
         
               容器中`DefaultErrorAttributes.getAttributes`默认进行数据处理的
         
            自定义`ErrorAttributes`
         
            ```java
            
            //但说实话我不是很明白这里，因为你看有的组件是加到MyMvcConfig里面的，但是这里的话就是搞到@Component里面去的，这到底区别是什么？
            //给容器中加入我们自己定义的ErrorAttributes
            @Component
            public class MyErrorAttributes
                    extends DefaultErrorAttributes {
            
                //返回的map就是页面和json能获取的所有字段
                @Override
                public Map<String, Object> getErrorAttributes(WebRequest webRequest, ErrorAttributeOptions options) {
                    Map<String, Object> map = super.getErrorAttributes(webRequest, options);
                    map.put("company","atguigu");
                    //我们的异常处理器携带的数据，这里有两个参数，第二个参数代表你是从request还是从session中取Attribute的
                    Map<String,Object> ext = (Map<String, Object>) webRequest.getAttribute("ext",0);
                    map.put("ext",ext);
                    return map;
                }
            }
            
            
            ```
         
            最终的效果：相应是自适应的，可以通过定制`ErrorAttribute`的内容
   
   ## 
   
   
   
   
   
   ## 
   
   ​				