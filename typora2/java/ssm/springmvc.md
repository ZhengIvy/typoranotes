## springmcv是啥？

> 是基于spring的一个框架，实际上就是spring的一个模块，专门是做web开发的。理解是servlet一个升级.
>
> web开发底层是servlet，框架是在servlet基础上面加入一些功能，让你做web开发方便
>
> springmvc就是一个spring，spring是容器，ioc能够管理对象，使用<bean>,@Component,@Repository,@Service,@Controller
>
> springmcv能够创建对象，放入到容器中(SpringMVC容器)，springmvc容器中放的是控制器对象
>
> 我们要做的是使用 `@Controller`创建控制器对象，把对象放入到springmvc容器中，把创建的对象作为控制器使用，这个控制器对象能够接收用户的请求，显示处理结果，就当做是一个servlet使用。
>
> 使用@Controller注解创建的是一个普通类对象，不是servlet，springmvc赋予了控制器对象一些额外的功能。(就是当做一个servlet，但实际上不是servlet)

那在springmvc里的逻辑是啥？

> web开发层是servlet，springmvc中有一个对象是servlet：`DispatcherServlet`(中央调度器),他是负责接收用户的所有请求，用户把请求给了`DispatcherServlet`，之后`DispatcherServlet`把请求转发给我们的Controller对象，最后是Controller对象处理请求
>
> index.jsp-----`DispatcherServlet(Servlet)-----转发，分配给---Controller对象，(@Controller注解创建的对象)`

## 第一个springmvc项目

### 需求

用户在页面发起一个请求，请求发给springmvc的控制器对象，并显示请求的处理结果(在结果页面显示一个欢迎语句)

### 实现步骤

1. 新建web maven工程

2. 加入依赖

   spring-webmvc 依赖，间接把spring的依赖都加入到项目中

   jsp，servlet依赖

3. 重点：在web.xml中注册springmvc框架的核心对象`DispatcherServlet`

   1. `DispatcherServlet`叫做中央调度器，是一个servlet，它的父类时继承`HttpServlet`
   2. `DispatcherServlet`页叫做前端控制器(front controller)
   3. `DispatcherServlet`负责接收用户提交的请求，调用其他的控制器对象，并把请求的处理结果显示给用户

4. 创建一个发起请求的页面 index.jsp

5. 创建控制器类

   1. 在类的上面加入`@Controller注解，创建对象，并放入到springmvc容器中`
   2. 在类中的方法上面加入`@RequestMapping注解`

6. 创建作为结果的jsp，显示请求的处理结果

7. 创建springm的配置文件(spring的配置文件)

   1. 声明组件扫描器，指定`@Controller`注解所在的包名
   2. 声明视图解析器，帮助处理视图的





### springmvc 处理请求的流程

1. 发起`some.do`---
2. `tomcat`(`web.xml`--`url-pattern`知道`*.do给DispatcherServlet`)-----
3. `Dispatcher(根据springmvc.xml配置知道some.do---doSome())----`
4. `DispatcherServlet把some.do焕发给MyController.doSome()方法`
5. 框架执行doSome()把得到的`ModelAndView进行处理，转发到show.jsp`

上面的过程简化方式

`some.do---DispatcherServlet----MyController`

![image-20200818174306620](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200818174306620.png)

### springmvc 执行过程中源代码的分析

1. tomcat启动，创建容器的过程

   通过`load-on-start`标签指定的1，创建`DispactherServlet`对象，

   `DispactherServlet`它的父类是继承`HttpSevlet`，它是一个servlet，在被创建时，会执行`init()`方法

   在init()方法中

   ```java
   //创建容器，读取配置文件
       WebApplicationContext ctx = new ClassPathXmlApplicationContext("springmvc.xml");
       //把容器对象放入到ServletContext中
       getServletContext.setAttribute(key,ctx);
   }
   ```

   上面创建容器作用：创建`@Controller注解所在的类的对象`，创建`MyController对象`，这个对象那个放入到`springmvc的容器中`，容器时map，类似于`map.put("myController",MyController对象)`

2. 请求的处理过程

`protected void service(HttpServletRequest request, HttpServletResponse response)`

`protected void doService(HttpServletRequest request, HttpServletResponse response)`

`DispactherServlet.doDispatch(request,response){`

调用`MyController的.doSome方法`

`}`

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200819163705038.png" alt="image-20200819163705038" style="zoom:67%;" />

把一些jsp放到`WEB-INF`的好处是可以使得用户无法直接访问一些页面，确保了安全性

1. springmvc.xml

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

<!--   声明 组件扫描器-->
    <context:component-scan base-package="com.zbr.controller"/>
<!--    声明 springmvc框架中的视图解析器，帮助开发人员设置 视图文件的路径，不用重复下相同的

-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
<!--        前缀：视图文件的路径-->
        <property name="prefix" value="/WEB-INF/view/"/>
<!--        后缀：视图文件的扩展名-->
        <property name="suffix" value=".jsp"/>
    </bean>
</beans>
```

2. web.xml

   ```html
   <?xml version="1.0" encoding="UTF-8"?>
   <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
            version="4.0">
   
   <!--    声明，注册springmvc的核心对象DispatcherServlet
           我们需要在tomcat服务器启动后，创建DispatcherServlet对象的实例。
           为什么要创建DispatcherServlet对象的实例呢？
           因为DispatcherServlet在他的创建过程中，会同时创建springmvc容器对象，
           入去springmvc的配置文件，把这个配置文件中的对象都创建好，当用户发起请求时就可以
           直接使用对象了
   
           servlet的初始化会执行init()方法，DispatcherServlet在init()中{
               //创建容器，读取配置文件
               WebApplicationContext ctx = new ClassPathXmlApplicationContext("springmvc.xml");
               //把容器对象放入到ServletContext中
               getServletContext.setAttribute(key,ctx);
           }
   
           顺便说下我在纠结监听器的问题，但是算了，毕竟我对这个DispatcherServlet了解的也不深，所以也不大清楚了
           我纠结的点在于是利用监听器在tomcat一启动就创建对象，而这里的话创建servlet和监听器之间的关系？？？？(spring容器和springmvc容器是分开的，所			以这个问号可以去掉了)
   
           启动tomcat报错，读取这个文件  /WEB-INF/springmvc-servlet.xml
           springmvc创建容器对象时，读取的配置文件默认是/WEB-INF/<servlet-name>-servlet.xml
   
   -->
       <servlet>
           <servlet-name>myweb</servlet-name>
           <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
   
   <!--        自定义springmvc读取的哦配置文件的位置-->
           <init-param>
   <!--            springmvc的配置文件的位置的属性-->
               <param-name>contextConfigLocation</param-name>
   <!--           指定自定义文件的位置-->
               <param-value>classpath:springmvc.xml</param-value>
           </init-param>
           <!--        在tomcat启动后，创建servlet对象
               load-on-startup:表示tomcat启动后创建对象的顺序。它的值是整数，数值越小，tomcat创建对象的时间越早
               大于等于0的整数
   -->
           <load-on-startup>1</load-on-startup>
       </servlet>
       
       <servlet-mapping>
           <servlet-name>myweb</servlet-name>
   <!--
           使用框架的时候，url-pattern可以使用两种值
           1.使用扩展名，语法 *.xxxx, xxxx是自定义扩展名 常用的方式 *.do, *.action,*.mvc等等
               http://localhost:8080/myweb/some.do
               //但是没这样用过欸，jsp一般不都以jsp结尾，哪还有哪些可以用到
   
           2.使用斜杠 "/"
   
   -->
   
           <url-pattern>*.do</url-pattern>
       </servlet-mapping>
   </web-app>
   ```

   3. index.jsp

      ```html
      <%@ page contentType="text/html;charset=UTF-8" language="java" %>
      <html>
      <head>
          <title>Title</title>
      </head>
      <body>
      <p>第一个springmvc项目</p>
      <p><a href="some.do">发起some.do请求</a></p>
      <p><a href="other.do">other.do请求</a></p>
      </body>
      </html>
      ```

3. controller

   ```java
   /**
    * @Controller: 创建处理器对象，对象放在springmvc容器中
    * 位置：在类上面
    * 和Spring中讲的@Service,@Component
    *
    * 能处理请求的都是控制器(处理器): MyController能处理请求，
    * 叫做后端控制器(back controller)
    */
   @Controller
   public class MyController {
       /*
       处理用户提交的请求，springmvc是使用方法来处理的，
       方法是自定义的，可以有多种返回值，多种参数，方法名称自定义
        */
   
       /**
        * 准备doSome 方法处理some.do请求
        * @RequestMapping:请求映射，作用是把一个请求地址和一个方法绑定在一起
        *                  一个请求指定一个方法处理
        *         属性： 1.value 是一个String，表示请求的uri地址的(some.do)
        *                  value的值必须是唯一的，不能重复，在使用时，推荐地址以"/"
        *         位置：1.在方法的上面，常用的
        *              2.在类的上面
        *   说明：使用RequestMapping修饰的方法叫做处理器方法或者控制器方法
        *   使用@RequestMapping修饰的方法可以处理请求的，类似Servlet中的doGet，doPost
        *   (但是我有疑问，那这样就相当于把Controller层和Servlet层放在一起了，就比较奇怪的感觉)
        *
        *   返回值:ModelAndView 表示本次请求的处理结果
        *   Model:数据，请求处理完成后，要显示给用户的数据（request.setAttribute()）
        *   View：视图。比如说jsp等等
        */
       @RequestMapping(value= {"/some.do","/first.do"})
       public ModelAndView doSome(){//doGet()---service请求处理
           //处理some.do请求 相当于service调用处理完成
           ModelAndView mv = new ModelAndView();
           //添加数据,框架在请求的最后把数据放入到request作用域
           //request.setAttribute("msg","欢迎使用springmvc做web开发");
           mv.addObject("msg","欢迎使用springmvc做web开发");
           mv.addObject("fun","执行的是doSome方法 ");
   
           //指定视图,指定视图的完整路径
           //框架对视图执行的forward操作，request.getRequestDispatcher("/show.jsp").forward(...)
   //        mv.setViewName("/show.jsp");
   //        mv.setViewName("WEB-INF/view/show.jsp");
   
           //当配置了视图解析器，可以使用逻辑名称(文件名)，指定视图
           //框架会使用视图解析器的前缀 + 逻辑名称 + 后缀 组成完整路径，这里就是字符串连接操作
           // /WEB-INF/view/ + show +.jsp
           mv.setViewName("show");
           //返回mv
           return mv;
       }
   
       @RequestMapping(value= {"/other.do","/second.do"})
       public ModelAndView doOther(){//doGet()---service请求处理
           ModelAndView mv = new ModelAndView();
           mv.addObject("msg","======欢迎使用springmvc做web开发");
           mv.addObject("fun","执行的是doSome方法 ");
           mv.setViewName("other");
           //返回mv
           return mv;
       }
   }
   ```

### requestMapping 的使用

其他的配置都和上面的一样，不同点在于`MyController`

```java
/**
 * @RequestMapping
 *      value: 所有请求地址的公共部分，叫做模块名称
 *      位置：放在类的上面
 */
@Controller
@RequestMapping("/test")
public class MyController {
    /**
     * @RequestMapping :请求映射
     *                  属性： method，表示请求的方式，它的值RequestMethod类枚举值
     *                      例如表示get请求方式，RequestMethod.GET
     *                          post,RequestMethod.POST
     *
     *  你不用
     */
    //指定some.do使用get请求方式
    @RequestMapping(value= "/some.do",method = RequestMethod.GET)
    public ModelAndView doSome(){//doGet()---service请求处理
        ModelAndView mv = new ModelAndView();
        mv.addObject("msg","欢迎使用springmvc做web开发");
        mv.addObject("fun","执行的是doSome方法 ");
        mv.setViewName("show");
        return mv;
    }
    //指定other.do 是post请求方式
    @RequestMapping(value= "/other.do",method = RequestMethod.POST)
    public ModelAndView doOther(){//doGet()---service请求处理
        ModelAndView mv = new ModelAndView();
        mv.addObject("msg","======欢迎使用springmvc做web开发");
        mv.addObject("fun","执行的是doSome方法 ");
        mv.setViewName("other");
        //返回mv
        return mv;
    }
    //不指定请求方式，没有限制,get post都可以啊，这个之前在servlet好像就没这样的
    @RequestMapping(value= "/first.do")
    public ModelAndView doFirst(HttpServletRequest request,
                                HttpServletResponse response,
                                HttpSession session){
        ModelAndView mv = new ModelAndView();
        mv.addObject("msg","======欢迎使用springmvc做web开发"+request.getParameter("name"));
        mv.addObject("fun","执行的是doFirst方法 ");
        mv.setViewName("other");
        //返回mv
        return mv;
    }
}

```



## springmvc接受参数

1. 接受请求参数，使用的处理器方法的形参

   1. `HttpServletRequest`
   2. `HttpServletResponse`
   3. `HttpSession`
   4. 用户提交的数据

2. 接受用户提交的参数：

   1. 逐个接收
   2. 对象接收

3. 注意：在提交请求参数时，get请求方式中文没有乱码 

   使用post方式提交请求，中文有乱码，需要使用过滤器处理乱码问题

   过滤器可以自定义，也可使用框架中提供的过滤器 `CharacterEncodingFilter`

4. 代码部分

   `MyController`

   ------------------------------------------------------------2020.8.22 anki在这！-------------------------------------------------------------------------------------------------------------
   
   ```java
   /**
    * @RequestMapping
    *      value: 所有请求地址的公共部分，叫做模块名称
    *      位置：放在类的上面
    */
   @Controller
   public class MyController {
   
   
       /**
        * 逐个接受请求参数：
        *  要求：处理器(控制器)方法的形参名和请求中参数名必须一致
        *       同名的请求参数赋值给同名的形参
        *
        *  框架接受请求参数
        *   1.使用request对象接受请求参数
        *      String strName = request.getParameter("name");
        *      String  strAge = request.getParameter("age");
        *   2.springmvc框架通过DispatcherServlet 调用 MyController的doSome()方法
        *      调用方法时，按名称对应，把接受的参数赋值给形参
        *      doSome(strName,Integer.valueOf(strAge))
        *      框架会提供类型转换的功能，能把String转为 int, long, float等
        *
        *  400状态码时客户端错误，表示请求参数过程中，发生了错误
        */
       @RequestMapping(value= "/receiveproperty.do")
       public ModelAndView doSome(String name, Integer age){//doGet()---service请求处理
           System.out.println("doSome,name="+name+"    age="+age);
          //可以直接在方法中直接使用name，age
           ModelAndView mv = new ModelAndView();
           mv.addObject("myname",name);
           mv.addObject("myage",age);
           mv.setViewName("show");
           return mv;
       }
   
       /**
        * 请求中参数名和处理器方法的形参名不一样
        * @RequestParam : 逐个接受请求参数中，解决请求中参数名形参名不一样的问题
        *      属性：1.value 请求中的参数名称
        *           2. required 表示请求中必须包含此参数，默认是true（这和参数为空和无参数是有区别的，前者只是空没填，后者连空都没有）
        *      位置： 在处理器方法的形参定义的前面
        * 然后我测试了一下，如果没有用RequestParam 的话 required 的默认是false把，没有报错
        */
       @RequestMapping(value= "/receiveparam.do")
       public ModelAndView receiveParam(@RequestParam(value = "rname") String name, @RequestParam("rage") Integer age){//doGet()---service请求处理
           System.out.println("doSome,name="+name+"    age="+age);
           //可以直接在方法中直接使用name，age
           ModelAndView mv = new ModelAndView();
           mv.addObject("myname",name);
           mv.addObject("myage",age);
           mv.setViewName("show");
           return mv;
       }
   
       /**
        * 处理器方法形参是java对象，这个对象的属性名和请求参数名一样的
        * 框架会创建形参的java对象，给属性赋值，请求中的参数时name，框架会调用setName()
        */
       @RequestMapping(value= "/receiveobject.do")
       public ModelAndView receiveObject(Student myStudent){
           System.out.println("doSome,name="+myStudent.getName()+"    age="+myStudent.getAge());
           //可以直接在方法中直接使用name，age
           ModelAndView mv = new ModelAndView();
           mv.addObject("myname",myStudent.getName());
           mv.addObject("myage",myStudent.getAge());
           mv.addObject("mystudent",myStudent);
           mv.setViewName("show");
           return mv;
       }
   
   }

   ```

   student 对象就不写了，就是有一个name 和age值而已

   `web.xml`

   多了个监听器
   
   ```html
   <?xml version="1.0" encoding="UTF-8"?>
   <web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
            version="4.0">
   
   
       <servlet>
           <servlet-name>myweb</servlet-name>
           <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
   
   <!--        自定义springmvc读取的哦配置文件的位置-->
           <init-param>
   <!--            springmvc的配置文件的位置的属性-->
               <param-name>contextConfigLocation</param-name>
   <!--           指定自定义文件的位置-->
               <param-value>classpath:springmvc.xml</param-value>
           </init-param>
           <!--        在tomcat启动后，创建servlet对象
               load-on-startup:表示tomcat启动后创建对象的顺序。它的值是整数，数值越小，tomcat创建对象的时间越早
               大于等于0的整数
   -->
           <load-on-startup>1</load-on-startup>
       </servlet>
       
       <servlet-mapping>
           <servlet-name>myweb</servlet-name>
   <!--
           使用框架的时候，url-pattern可以使用两种值
           1.使用扩展名，语法 *.xxxx, xxxx是自定义扩展名 常用的方式 *.do, *.action,*.mvc等等
               http://localhost:8080/myweb/some.do
               //但是没这样用过欸，jsp一般不都以jsp结尾，哪还有哪些可以用到
   
           2.使用斜杠 "/"
   
   -->
   
           <url-pattern>*.do</url-pattern>
       </servlet-mapping>
   
   <!--    注册声明过滤器，解决post请求乱码的问题-->
       <filter>
           <filter-name>characterEncodingFilter</filter-name>
           <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
   <!--        设置项目中使用的字符编码-->
           <init-param>
               <param-name>encoding</param-name>
               <param-value>utf-8</param-value>
           </init-param>
   <!--        强制请求对象(HttpServletRequest)使用encoding编码的值-->
           <init-param>
               <param-name>forceRequestEncoding</param-name>
               <param-value>true</param-value>
           </init-param>
   <!--        强制应答对象(HttpServletResponse)使用encoding编码的值-->
           <init-param>
               <param-name>forceResponseEncoding</param-name>
               <param-value>true</param-value>
           </init-param>
       </filter>
   
       <filter-mapping>
           <filter-name>characterEncodingFilter</filter-name>
   <!--
           /*:表示强制所有的请求先通过过滤器处理
   -->
           <url-pattern>/*</url-pattern>
       </filter-mapping>
   </web-app>
   ```

## 处理器方法的返回值

![image-20200819164302028](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200819164302028.png)

### 1. ModelAndView:

有数据和视图，对视图执行forward

### 2.String：表示视图，可以逻辑名称，也可以是完整视图路径

不过这个是建立在有在springmvc.xml配视图路径的情况下

```java
    /**
     * 处理器方法返回String--表示逻辑视图名称，需要配置视图解析器
     */
    @RequestMapping(value = "/returnString-view.do")
    public String doReturnView(HttpServletRequest request, String name, Integer age) {//doGet()---service请求处理
        System.out.println("doReturnView,name=" + name + "    age=" + age);
        //可以自己手动添加数据到request作用域
        request.setAttribute("myname", name);
        request.setAttribute("myage", age);
        //show：逻辑视图名称，项目中配置的视图解析器
        //框架对视图执行forward
        return "show";
    }

   
```



### 3.返回void

不能表示数据，也不能表示视图

在处理ajax的时候，可以使用void返回值。通过`HttpServletResponse`输出数据，响应ajax请求

ajax请求数据端返回的就是数据，和视图无关。

```java
 //处理器方法返回void，相应ajax请求
    //手工实现ajax，json数据：代码有重复的 1.java对象转为json； 2.通过HttpServletResponse输出数据
    @RequestMapping(value = "/returnVoid-ajax.do")
    public void doReturnVoidAjax(HttpServletResponse response, String name, Integer age) throws IOException {//doGet()---service请求处理
        System.out.println("doReturnVoidAjax,name=" + name + "    age=" + age);
        //处理ajax，使用json做数据的格式
        //service调用完成啦，使用Student表示处理结果
        Student student = new Student();
        student.setAge(age);
        student.setName(name);

        String json = "";
        //把结果的对象转为json格式的数据
        if (student != null) {
            ObjectMapper om = new ObjectMapper();
            json = om.writeValueAsString(student);
            System.out.println("student转换的json====" + json);
        }
        //输出数据，相应ajax请求
        response.setContentType("application/json;charset=utf-8");
        PrintWriter pw = response.getWriter();
        pw.println(json);
        pw.flush();
        pw.close();
    }
```



### 4.返回值Object

![image-20200819181232000](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200819181232000.png)

> 所以返回数据基本上在servlet直接的不行，要的话得借助AJAX

例如`String,Integer,Map,List,Student等等都是对象，对象有属性，属性就是数据，所以返回Object表示数据，和视图无关，可以使用对象表示的数据，响应ajax请求`

现在做ajax，主要使用json的数据格式，实现步骤：

1. 加入处理json的工具库的依赖，springmvc默认使用的jackson

2. 在springmvc配置文件中加入<mvc:annotation-driven>注解驱动

   ```java
   json = om.writeValueAsString(student);
   ```

3. 在处理器方法的上面加入`@ResponseBody`注解

   ```java
   response.setContentType("application/json;charset=utf-8");
   PrintWriter pw = response.getWriter();
   pw.println(json);
   ```

springmvc处理器方法返回Object,转为json输出到浏览器，响应ajax的内容原理

1. <mvc:annotation-driven>注解驱动

   注解驱动实现功能是 完成java对象到json，xml，text，二进制等数据格式的转换

   <mvc:annotation-driven> 在加入到springmvc配置文件中，会自动创建`HttpMessageConverter`接口的7个实现类对象，包括 `MappingJackson2HttpMessageConverter`(使用jackson工具库中的`ObjectMapper`实现java对象json字符串)

   <img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200819214450870.png" alt="image-20200819214450870" style="zoom:67%;" />

   主要是红线的两个

   ![image-20200819215632344](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200819215632344.png)

   > 这个看了这么久源码的目的就在说明，加入注解之后创建的`HttpMessageConverter`的实现类可以把Object转化成json格式的了，就不需要我们手动写

   `HttpMessageConverter`接口：消息转换器

   功能：定义了java对象转为json，xml等数据格式的方法，这个接口有很多的实现类，这些实现类完成java对json，xml，二进制数据的转换

   下面两个方法是控制器类把结果输出给浏览器时使用的

   ```java
   boolean canWrite(Class<?> var1, @Nullable MediaType var2);
   
   void write(T var1, @Nullable MediaType var2, HttpOutputMessage var3);
   ```

   1. canWrite 作用检查处理器方法的返回值，能不能转为var2表示的数据格式

      例如处理器方法

      ```java
      @RequestMapping(value= "/returningString.do")
      public Student deReturnView2(HttpServletReqeust request,String name,Integer age){
      	Student student = new Student();
          student.setName("lisi");
          student.setAge(20);
          return student;
      }
      ```

      检查student(lisi,20)能不能转为var2表示的格式，如果检查能转为json，canWrite返回true

      `MediaType`:表示数据格式的，例如json，xml等等

   2. write：把处理器方法的返回值对象，调用jackson中的`ObjectMapper`转为json字符串

2. `@ResponseBody`注解

   放在处理器方法的上面，通过`HttpServletResponse`输出数据相应ajax请求的。



```java
/**
     * 处理器方法返回一个Student，通过框架转为json，响应ajax请求
     *  @ResponseBody
     *      作用：把处理器方法返回对象转为json后，通过HttpServletResponse输出给浏览器
     *      位置：方法的定义上面，和其他注解没有先后顺序的关系
     *  返回对象框架的处理流程：
     *  1.框架会把返回Student类型，调用框架中的ArrayList<HttpMessageConverter>
     *      中的每个类的canWrite()方法，检查那个HttpMessageConverter接口的实现类能处理Student类型的数据--MappingJackson2HttpMessageConverter
     *
     *  2.框架会调用实现类的write()，MappingJackson2HttpMessageConverter的write方法
     *  把李四同学的student对象转为json，调用Jackson的ObjectMapper实现转为json
     *
     *  3.框架会调用@ResponseBody 把2 的结果数据输出到浏览器，ajax请求处理完成
     */
    @RequestMapping(value = "/returnStudentJson.do")
    @ResponseBody
    public Student doStudentJsonObject( String name, Integer age){
        //调用service，获取请求结果数据,Student对象表示结果数据
        Student student = new Student();
        student.setName("李四同学");
        student.setAge(20);
        return student;
    }

    /**
     * 处理器方法返回List<Student>
     *返回对象框架的处理流程：
     *  1.框架会把返回List<Student>类型，调用框架中的ArrayList<HttpMessageConverter>
     *       中的每个类的canWrite()方法，检查那个HttpMessageConverter接口的实现类能处理Student类型的数据--MappingJackson2HttpMessageConverter
     *
     *  2.框架会调用实现类的write()，MappingJackson2HttpMessageConverter的write方法
     *   把李四同学的student对象转为json，调用Jackson的ObjectMapper实现转为json array
     *
     *  3.框架会调用@ResponseBody 把2 的结果数据输出到浏览器，ajax请求处理完成
     */
    @RequestMapping(value = "/returnStudentJsonArray.do")
    @ResponseBody
    public List<Student> doStudentJsonObjectArray(String name, Integer age){
        List<Student> list = new ArrayList<>();
        //调用service，获取请求结果数据,Student对象表示结果数据
        Student student = new Student();
        student.setName("李四同学");
        student.setAge(20);
        list.add(student);

        student = new Student();
        student.setName("张三");
        student.setAge(28);
        list.add(student);
        return list;
    }
   
```





### 5.返回值是String

是否加上了@RequestBody

```java
 /**
     * 处理器方法返回的时String，String表示数据的，不是视图
     * 区分返回值String时数据，还是视图，看有没有@ResponseBody注解
     * 如果又@Response注解，返回String就是数据，反之就是视图
     *
     * 在返回的过程中，由于(默认???)content-Type是json格式的，String传过去的话转不成json？？(但我之前又学过String转json)，导致你点击
     * 按钮无变化，所以要在dataType那里设置为文本格式的(那这时候感觉就有两个方向？一个response content-Type,和ajax接受的数据类型dataType)
     * 相当于双方一个要求json,另外一个要求text，那没办法，你的text格式只好使用默认的ISO-8859-1所以会有乱码啦
     * 默认使用"text/plain;charset=ISO-8859-1"作为contentType,导致中文又乱码,所以你想用不乱码的编码的话，那你就自己设置咯
     * 解决方案：给RequestMapping增加一个属性produces,使用这个属性指定新的contentType
     * (不过我以为会在ResponseBody这里设置的)
     *
     * 返回对象框架的处理流程：
     *      *  1.框架会把返回String类型，调用框架中的ArrayList<HttpMessageConverter>
     *      *       中的每个类的canWrite()方法，检查那个HttpMessageConverter接口的实现类能处理String类型的数据--StringHttpMessageConverter
     *      *
     *      *  2.框架会调用实现类的write()，StringHttpMessageConverter的write方法
     *      *   把字符串按照指定的编码处理
     *      *
     *      *  3.框架会调用@ResponseBody 把2 的结果数据输出到浏览器，ajax请求处理完成
     */
    @RequestMapping(value = "/returnStringData.do",produces = "text/plain;charset=utf-8")
    @ResponseBody
    public String doStringData(String name,Integer age){
        return "Hello SpringMVC 返回对象，表示数据";
    }
```

关于springmvc中的返回值String想被框架转为json而失败

## url-pattern

**注意：会有下面的问题的前提是你的urlpattern配的是"/"**

发起的请求是由那些服务器程序处理的

`http://localhost:8080/ch05_url_pattern/index.jsp`:tomcat（jsp会转为servlet）

`http://localhost:8080/ch05_url_pattern/js/jquery-3.4.1.js`:tomcat

`http://localhost:8080/ch05_url_pattern/pics/2019-07-24%20081953.jpg`:tomcat

`http://localhost:8080/ch05_url_pattern/some.do`:`DispactherServlet`(springmvc框架处理的)

tomcat本身能处理静态资源的访问，像html，图片，js文件都是静态资源

tomcat的`web.xml`文件有一个servlet，名称是default，在服务器启动时创建。

```html
<servlet>
    <servlet-name>default</servlet-name>
    <servlet-class>org.apache.catalina.servlet.DefaultServlet</servlet-class>
    <init-param>
    	<param-name>debug</param-name>
        <param-value>0</param-value>
    </init-param>
    <init-param>
    <param-name>listings</param-name>
        <param-value>false</param-value>
       
    </init-param>
    <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
	<servlet-name>default</servlet-name>
    <url-pattern>/</url-pattern>
    <!--表示静态资源和未映射的请求都给这个default处理 -->
</servlet-mapping>
```

default这个servlet的作用

1. 处理静态资源
2. 处理未映射到其他servlet的请求

### 第一种方式

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       https://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">

<!--   声明 组件扫描器-->
    <context:component-scan base-package="com.zbr.controller"/>
<!--    声明 springmvc框架中的视图解析器，帮助开发人员设置 视图文件的路径，不用重复下相同的

-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
<!--        前缀：视图文件的路径-->
        <property name="prefix" value="/WEB-INF/view/"/>
<!--        后缀：视图文件的扩展名-->
        <property name="suffix" value=".jsp"/>
    </bean>
<!--    default-servlet-handler 和 @RequestMapping注解有冲突，需要加入annotation-driven 解决问题，
        因为默认全部都会转发给这个defaultServlet 
-->
    <mvc:annotation-driven/>

<!--    第一种处理静态资源的方式:
        需要在springmvc配置文件加入 <mvc:default-servlet-handler>
        原理是：加入这个标签后，框架会创建控制器对象DefaultServletHttpRequestHandler(类似我们自己创建的MyController)
        DefaultServletHttpRequestHandler这个对象可以把接受的请求转发给tomcat的defaultServlet
-->
    <mvc:default-servlet-handler/>
</beans>
```

```html
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">


    <servlet>
        <servlet-name>myweb</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>

<!--        自定义springmvc读取的哦配置文件的位置-->
        <init-param>
<!--            springmvc的配置文件的位置的属性-->
            <param-name>contextConfigLocation</param-name>
<!--           指定自定义文件的位置-->
            <param-value>classpath:springmvc.xml</param-value>
        </init-param>
        <!--        在tomcat启动后，创建servlet对象
            load-on-startup:表示tomcat启动后创建对象的顺序。它的值是整数，数值越小，tomcat创建对象的时间越早
            大于等于0的整数
-->
        <load-on-startup>1</load-on-startup>
    </servlet>
    
    <servlet-mapping>
        <servlet-name>myweb</servlet-name>
<!--
        使用框架的时候，url-pattern可以使用两种值
        1.使用扩展名，语法 *.xxxx, xxxx是自定义扩展名 常用的方式 *.do, *.action,*.mvc等等
            http://localhost:8080/myweb/some.do
            //但是没这样用过欸，jsp一般不都以jsp结尾，哪还有哪些可以用到

        2.使用斜杠 "/"
        当你的项目中使用了"/",它会替代tomcat中的default
        导致所有的静态资源都给DispatcherServlet处理，默认情况下DispatcherServlet没有处理静态资源的能力
        没有控制器对象能处理静态资源的访问，所以静态资源(html,js,图片,css)都是404

        动态资源some.do是可以访问的，因为我们程序中有MyController对象，能处理some.do请求
-->

        <url-pattern>/</url-pattern>
    </servlet-mapping>

<!--    注册声明过滤器，解决post请求乱码的问题-->
    <filter>
        <filter-name>characterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
<!--        设置项目中使用的字符编码-->
        <init-param>
            <param-name>encoding</param-name>
            <param-value>utf-8</param-value>
        </init-param>
<!--        强制请求对象(HttpServletRequest)使用encoding编码的值-->
        <init-param>
            <param-name>forceRequestEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
<!--        强制应答对象(HttpServletResponse)使用encoding编码的值-->
        <init-param>
            <param-name>forceResponseEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
    </filter>

    <filter-mapping>
        <filter-name>characterEncodingFilter</filter-name>
<!--
        /*:表示强制所有的请求先通过过滤器处理
-->
        <url-pattern>/*</url-pattern>
    </filter-mapping>


</web-app
```



### 第二种方式

![image-20200820112359488](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200820112359488.png)

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       https://www.springframework.org/schema/context/spring-context.xsd
       http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">

<!--   声明 组件扫描器-->
    <context:component-scan base-package="com.zbr.controller"/>
<!--    声明 springmvc框架中的视图解析器，帮助开发人员设置 视图文件的路径，不用重复下相同的

-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
<!--        前缀：视图文件的路径-->
        <property name="prefix" value="/WEB-INF/view/"/>
<!--        后缀：视图文件的扩展名-->
        <property name="suffix" value=".jsp"/>
    </bean>
<!--    default-servlet-handler 和 @RequestMapping注解有冲突，需要加入annotation-driven 解决问题，
        因为默认全部都会转发给这个defaultServlet
        第二种方式mvc resources 也有冲突
-->
    <mvc:annotation-driven/>

<!--第二种处理静态资源的方式
    mvc:resources 加入后框架会创建 ResourceHttpRequestHandler 这个处理器对象
    让这个对象处理静态资源的访问，不依赖tomcat服务器
    mapping：访问静态资源的uri地址，使用通配符 **
    location:静态资源在你的项目中的目录位置

    /pics/** ：表示 /pics/p1.jpg, /pics/user/log.gif
-->
    <mvc:resources mapping="/pics/**" location="/pics/"/>
    <mvc:resources mapping="/html/**" location="/html/"/>
    <mvc:resources mapping="/js/**" location="/js/"/>
<!--    使用一个配置语句，指定多种静态资源的访问-->
<!--    <mvc:resources mapping="/static/**" location="/static/"/>-->
</beans>
```

web.xml的东西和上面的是一样的

### 总结下:

>会出现这两种的问题是在于，你的urlpattern被设置为"/"的意思是全部的访问我的中央调度器都接受，就覆盖了本来处理静态资源的servlet，但是中央调度器没有这个能力啊！所以两种方式就出现了

## jsp页面的路径问题！！！！！！！！

在jsp，html中使用的地址，都是在前端页面的地址，都是相对地址

地址分类：

1. 绝对地址，带有协议名称的是绝对地址,<htp://www.baidu.com>

2. 相对地址，没有协议开头的，例如 `user/some.do`,`/user/some.do`

   相对地址不能独立使用，必须有个参考地址，通过参考地址+相对地址本身才能指定资源。

   张三同学，1班有张三，2班有张三

3. 参考地址

   在你的页面中，访问地址不加 "/"

   访问的是：`http://localhost:8080/ch06_path/index.jsp`

   路径：`http://localhost:8080/ch06_path/`

   资源 index.jsp

   在`index.jsp`发起`test/some.do`请求，访问地址变为`http://localhost:8080/ch06_path/test/some.do`

   当你的地址没有斜杠开头，例如`test/some.do`当你点击链接时，访问的是当前页面的地址加上的地址。

   `http://localhost:8080/ch06_path/` + `test/some.do`

   ---------------------------------------------------------------------------

   index.jsp 访问 test/some.do,返回后现在的地址

   `http://localhost:8080/ch06_path/test/some.do`

   路径：`http://localhost:8080/ch06_path/test/`

   资源:`some.do`

   在index.jsp 再次点击`test/some.do`，就变成了`http://localhost:8080/ch06_path/test/test/some.do`

4. 在你的页面中，访问地址加"/"

   访问的是`http://localhost:8080/ch06_path/index.jsp`

   路径`http://localhost:8080/ch06_path/`

   资源index.jsp

   点击`/test/some.do`,访问地址变为``http://localhost:8080/test/some.do`,出错了，访问失败

   解决方案：

   1. 加入`${pageContext.request.contextPath}`(不用相对路径了)

   2. 加入base标签,是html语言中的标签，表示当前页面中访问地址的基地址

      你的页面中所有  没有"/"开头的地址，都是以base标签中的地址为参考地址，使用base中的地址+ `test/some.do`地址

   参考的是服务器地址，也就是``http://localhost:8080`

   如果你的资源不能访问，加入`${pageContext.request.contextPath}`

   `<a href="`${pageContext.request.contextPath}`/test/some.do">`发起`test/some.do`的get请求`</a>`

   如果你的资源不能访问：加入`${pageContext.request.contextPath}`

   ### 总结：

> 总结来说就是几点
>
> 1. 前端的根路径是啥？`http://localhost:8080/`就是这个了，所以直接上`/show.jsp`类似的话直接和根目录拼接，这样的话就肯定找不到
>
> 2. 后台的根路径是啥？ `http://localhost:8080/ch06_path/`这个，加上了项目路径，所以在后台基本上都可以直接"/index.jsp","/WEB-INF/show.jsp"，而且是最好直接根目录来，不然的话会被搞成相对路径会报错，访问不到页面，就是`/test/index.jsp`这样子
>
> 3. 还有一种比较显在的错误是，比如从index.jsp->test/some.do->index.jsp->test/some.do，使用转发的方式，所以的话`http//localhost:8080/ch06_path/index.jsp`->`http//localhost:8080/ch06_path/test/doSome`->`http//localhost:8080/ch06_path/test/doSome`->
>
>    `http://localhost:8080/ch06_path/test/test/some.do`，因为相对路径是相对当前的，就有可能相对在test/目录下，可这可是servlet的路径啊，所以就会出错。
>
> 4. 解决方法：两种哈，base or `pageContext`， 很明显base更好还只用写一次
>
>    ```html
>    <%@ page contentType="text/html;charset=UTF-8" language="java" %>
>    <%
>        String basePath = request.getScheme() + "://" +
>                    request.getServerName() + ":" +request.getServerPort()+
>                    request.getContextPath() + "/";
>    %>
>    <html>
>    <head>
>        <title>Title</title>
>        <base href="<%=basePath%>"/>
>    </head>
>    <body>
>    <p>第一个springmvc项目</p>
>    <p><a href="test/some.do">发起test/some.do的get请求</a></p>
>    
>    <br>
>    ```
>
>    

------------------------------------------------------------------------------2020.8.24 anki在这---------------------------------------------------------------------------------------------------------

## ssm整合开发

>SSM: `SpringMVC +Spring +Mybatis`
>
>`SpringMVC`:视图层，界面层，负责接收请求，显示处理结果的
>
>`Spring:业务层，管理service，dao，工具类对象的`
>
>`MyBatis:持久层，访问数据库的`
>
>用户发起请求---SpringMVC接收--Spring中的Service对象--MyBatis处理数据
>
>SSM整合也叫做SSI(IBatis 也就是mybatis的前身),整合中有容器
>
>1. 第一个容器时SpringMVC容器，管理Controller控制器对象的
>2. 第二个容器Spring容器，管理Service，Dao工具类对象的
>
>我们要做的是把使用的对象交给合适的容器创建，管理，把Controller还有web开发的相关对象交给springmvc容器，这些web用的对象写在springmvc配置文件中
>
>service，dao对象定义在spring的配置文件中，让spring管理这些对象
>
>springmvc容器和spring容器是有关系的，关系已经确定好了
>
>springmvc容器时spring容器的子容器，类似java中的继承，子可以访问父的内容
>
>在子容器中的Controller可以访问父容器中的Service对象，就可以实现controller使用service对象
>
>实现步骤：
>
>0. 使用springdb的mysql库，表使用student（id auto_increment,name,age）
>
>1. 新建maven web项目
>
>2. 加入依赖
>
> `springmvc,spring,mybatis,三个框架依赖,jackson依赖，mysql驱动，druid连接池，jsp，servlet依赖`
>
>3. 写web.xml
>
> 4. 注册`DispatcherServlet`，目的：1. 创建springmvc容器对象，才能创建Controller类对象 2. 创建的是Servlet，才能接受用户请求
> 5. 注册spring的监听器：`ContextLoaderListener`，目的：创建spring的容器对象，才能创建service，dao等对象。
> 6. 注册字符集过滤器，解决post请求乱码的问题
>
>7. 创建包，Controller包，service，dao实体类名创建好
>
>8. 写springmvc，spring，mybatis的配置文件
>
> 9. springmvc配置文件
> 10. spring文件
> 11. mybatis主配置文件
> 12. 数据库的属性配置文件
>
>13. 写代码，dao接口和mapper文件，service和实现类，controller，实体类
>
>14. 写jsp页面

等等，好像明白为什么两个容器时独立的了，有两个不同的容器，一个负责Controller,一个负责service和dao，我之前不理解是因为我把两个容器合为一起了

`pom.xml`

```html
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.zbr</groupId>
  <artifactId>ch07-ssm</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>war</packaging>


  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>1.8</maven.compiler.source>
    <maven.compiler.target>1.8</maven.compiler.target>
  </properties>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
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
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>5.2.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>5.2.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-tx</artifactId>
      <version>5.2.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-core</artifactId>
      <version>2.9.0</version>
    </dependency>
    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>2.9.0</version>
    </dependency>
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis-spring</artifactId>
      <version>1.3.1</version>
    </dependency>
    <dependency>
      <groupId>org.mybatis</groupId>
      <artifactId>mybatis</artifactId>
      <version>3.5.1</version>
    </dependency>
    <dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.19</version>
    </dependency>
    <dependency>
      <groupId>com.alibaba</groupId>
      <artifactId>druid</artifactId>
      <version>1.1.23</version>
    </dependency>
    <dependency>
      <groupId>javax.annotation</groupId>
      <artifactId>javax.annotation-api</artifactId>
      <version>1.3.2</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <version>5.2.5.RELEASE</version>
    </dependency>
  </dependencies>

  <build>
    <resources>
      <resource>
        <directory>src/main/java</directory>
        <includes><!-- 包括目录下的.properties.xml文件都会被扫描到-->
          <include>**/*.properties</include>
          <include>**/*.xml</include>
        </includes>
        <filtering>false</filtering>
      </resource>
    </resources>
    <plugins>
      <plugin>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.1</version>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>

```



`applicationContext.xml`

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <!--spring配置文件： 声明service，dao，工具类等对象-->

    <context:property-placeholder location="classpath:conf/jdbc.properties" />

    <!--声明数据源，连接数据库-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource"
          init-method="init" destroy-method="close">
        <property name="url" value="${jdbc.url}" />
        <property name="username" value="${jdbc.username}" />
        <property name="password" value="${jdbc.password}" />
    </bean>

    <!--SqlSessionFactoryBean创建SqlSessionFactory-->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <property name="dataSource" ref="dataSource" />
        <property name="configLocation"  value="classpath:conf/mybatis.xml" />
    </bean>

    <!--声明mybatis的扫描器，创建dao对象-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory" />
        <property name="basePackage" value="com.zbr.dao" />
    </bean>

    <!--声明service的注解@Service所在的包名位置-->
    <context:component-scan base-package="com.zbr.service" />

    <!--事务配置：注解的配置， aspectj的配置-->
</beans>
```

`dispatcherServlet.xml`是springmvc的

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">
<!--springmvc配置文件，声明controller和其他web相关的对象-->
<context:component-scan base-package="com.zbr.controller"/>
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsp/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
    <mvc:annotation-driven/>
<!--
    1.相应ajax请求，返回json
    2.解决静态资源访问问题
-->
</beans>
```

`jdbc.properties`就不放了没啥好放的

`mybatis.xml`还是老样子

```html
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>


<!--    <settings>-->
<!--        &lt;!&ndash;        设置mybatis输出日志&ndash;&gt;-->
<!--        <setting name="logImpl" value="STDOUT_LOGGING"/>-->
<!--    </settings>-->
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


    </mappers>
</configuration>
```

`web.xml`也是老样子

```html
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

<!--注册中央调度器-->
    <servlet>
        <servlet-name>myweb</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>


        <init-param>

            <param-name>contextConfigLocation</param-name>

            <param-value>classpath:conf/dispatcherServlet.xml</param-value>
        </init-param>

        <load-on-startup>1</load-on-startup>
    </servlet>
    
    <servlet-mapping>
        <servlet-name>myweb</servlet-name>


        <url-pattern>*.do</url-pattern>
    </servlet-mapping>
<!--    注册监听器-->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath:conf/applicationContext.xml</param-value>
    </context-param>
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>
<!--    注册字符集过滤器-->
    <filter>
        <filter-name>characterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>utf-8</param-value>
        </init-param>
        <init-param>
            <param-name>forceRequestEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
        <init-param>
            <param-name>forceResponseEncoding</param-name>
            <param-value>true</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>characterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
</web-app>
```

给你看个Controller把，不过也没啥好看的额

```java
@Controller
@RequestMapping("/student")
public class StudentController {
    @Resource
    private StudentService studentService;
    //注册学生
    @RequestMapping("/addStudent.do")
    public ModelAndView addStudent(Student student){
        ModelAndView mv = new ModelAndView();
        String tips = "注册失败";
        //调用service处理student
        int nums = studentService.addStudent(student);
        if( nums > 0){
            //注册成功
            tips = "学生【"+student.getName()+"】注册成功";
        }
        //指定结果页面
        mv.addObject("tips",tips);
        //指定结果页面
        mv.setViewName("result");
        return mv;
    }

    //处理查询，相应ajax
    @RequestMapping("/queryStudent.do")
    @ResponseBody
    public List<Student> queryStudent(){
        //参数检查，简单的数据处理
        List<Student> students = studentService.findStudents();
        return students;
    }
}

```

给你看个如何输出list集合，需要掌握啊

```html
<%--
 不过这个项目可以好好看，关于整合 的
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%
    String basePath = request.getScheme() + "://" +
            request.getServerName() + ":" +request.getServerPort()+
            request.getContextPath() + "/";
%>
<html>
<head>
    <title>查询学生ajax</title>
    <base href="<%=basePath%>>">
    <script type="text/javascript" src="js/jquery-3.4.1.js"></script>
    <script type="text/javascript">
        $(function(){
            //在当前页面dom对象加载后，执行loadStudentData()
            loadStudentData();
            $('#btnLoader').click(function () {
                loadStudentData();
            })
        })
        
        function loadStudentData() {
            $.ajax({
                url:"student/queryStudent.do",
                type:"get",
                dataType:"json",
                success:function (data) {

                    //清楚旧数据
                    $('#info').html("");
                    $.each(data,function (i,n) {
                        $('#info').append("<tr>")
                            .append("<td>"+n.id+"</td>")
                            .append("<td>"+n.name+"</td>")
                            .append("<td>"+n.age+"</td>")
                            .append("</tr>")
                    })
                }
            })
        }
    </script>
</head>
<body>
<div align="center">
    <table>
        <thead>
        <tr>
            <td>学号</td>
            <td>姓名</td>
            <td>年龄</td>
        </tr>
        </thead>
        <tbody id="info">
        
        </tbody>
    </table>
    <input type="button" id="btnLoader" value="查询数据">
</div>
</body>
</html>

```









## 转发和重定向

![image-20200821161240247](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200821161240247.png)

> forward和redirect都是关键字，有一个共同的特点是不合视图解析器一同工作

配置文件基本上和上面的没区别，所以这里集中写有区别的东西

```java
@Controller
public class MyController {


    /**
     * 处理器方法返回ModelAndView，实现转发forward
     * 语法:setViewName("forward:视图文件完整路径")
     * forward特点：不合视图解析器一起使用，就当项目中没有视图解析器
     * 所以有个作用，当你的资源不在你的视图解析器指定的目录下时候可以用forward来转发
     * 就是因为他不受视图解析器的限制
     */
    @RequestMapping(value= "/doForward.do")
    public ModelAndView doSome(){//doGet()---service请求处理
        ModelAndView mv = new ModelAndView();
        mv.addObject("msg","欢迎使用springmvc做web开发");
        mv.addObject("fun","执行的是doSome方法 ");
        mv.setViewName("forward:/WEB-INF/view/show.jsp");
        return mv;
    }

    /**
     * 处理器方法返回ModelAndView,实现重定向redirect
     * 语法:setViewName("redirect:视图的完整路径")
     * redirect特点：不合视图解析器一起使用，就当项目中没有视图解析器
     * 框架对重定向的操作:
     * 1. 框架会把Model中的简单类型数据，转为string使用，作为hello.jsp的get请求参数使用
     *      目的是在doRedirect.do 和 hello.jsp两次请求之间传递数据
     *      ！！这里很不一样诶，主要是我有些忘记如何从request.getParameter取参的el表达式了
     *  2.在目标hello.jsp页面可以使用参数集合对象${param}获取请求参数值
     *      ${param.myname}
     *  3.重定向不能访问/WEB/INF资源
     */
    @RequestMapping(value= "/doRedirect.do")
    public ModelAndView doWithRedirect(String name,Integer age){//doGet()---service请求处理
        ModelAndView mv = new ModelAndView();
        //数据放入到request作用域
        mv.addObject("myname",name);
        mv.addObject("myage",age);
       //重定向
//        mv.setViewName("redirect:/hello.jsp");
        //http://localhost:8080/ch08_forward_redirect/hello.jsp?myname=lisi&myage=123

        //重定向不能访问/WEB/INF资源
        mv.setViewName("redirect:/WEB-INF/view/show.jsp");
        return mv;
    }

}

```

> 这里forward没啥特别的，主要是这个重定向框架还赋予了一个功能，这个是没有想到的，所以取参的时候的方式也有所区别

## 异常处理

> 很多代码抛差不多的异常，很多代码，比较凌乱，所以出现了一个集中异常处理的方式
>
> springmvc框架采用的是统一，全局的异常处理，把controller中的所有异常处理都集中到一个地方，采用的是aop的思想，把业务逻辑和异常处理代码分开，解耦合。
>
> 使用两个注解
>
> 1. `@ExceptionHandler`
> 2. `@ControllerAdvice`
>
> 异常处理步骤:
>
> 1. 新建maven web项目
> 2. 加入依赖
> 3. 新建自定义异常类 `MyUserException`,再定义它的子类`NameException`,`AgeException`
> 4. 在controller抛出`NameException,AgeException`
> 5. 创建一个普通类，作为全局异常处理类
>    1. 在类的上面加入`@ControllerAdvice`
>    2. 在类中定义方法,在方法的上面加入`@ExceptionHandler`
> 6. 创建处理异常的视图页面
> 7. 创建springmvc的配置文件
>    1. 组件扫描器，扫描`@Controller`注解
>    2. 组件扫描器，扫描`@ControllerAdvice`所在的包名
>    3. 声明注解驱动

代码部分

![image-20200822211357570](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200822211357570.png)

`springmvc.xml`

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd http://www.springframework.org/schema/mvc https://www.springframework.org/schema/mvc/spring-mvc.xsd">

<!--   声明 组件扫描器-->
    <context:component-scan base-package="com.zbr.controller"/>
<!--    声明 springmvc框架中的视图解析器，帮助开发人员设置 视图文件的路径，不用重复下相同的

-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
<!--        前缀：视图文件的路径-->
        <property name="prefix" value="/WEB-INF/view/"/>
<!--        后缀：视图文件的扩展名-->
        <property name="suffix" value=".jsp"/>
    </bean>

<!--    处理异常需要的两步-->
    <context:component-scan base-package="com.zbr.handler"/>
<!--    这个真的用到了很多地方额，三个作用了，json那里，在aop中直接就是aspectj，那这里就是annotation-driven了-->
    <mvc:annotation-driven/>
</beans>
```

`MyController`

```java
@Controller
public class MyController {



    @RequestMapping(value= "/some.do")
    public ModelAndView doSome(String name,Integer age) throws MyUserException {
        ModelAndView mv = new ModelAndView();
//        try {
            //根据请求参数抛出异常
            if (!"zs".equals(name)) {
                throw new NameException("姓名不正确");
            }
            if (age == null || age > 80) {
                throw new AgeException("年龄比较大");
            }
//        }catch (Exception e){
//            e.printStackTrace();
//        }

        mv.addObject("myname",name);
        mv.addObject("myage",age);
        mv.setViewName("show");
        return mv;
    }



}

```

`exception`

```java
public class MyUserException extends Exception{

    public MyUserException() {
        super();
    }

    public MyUserException(String message) {
        super(message);
    }
}



//当年龄有问题时，抛出的异常
public class AgeException extends MyUserException{
    public AgeException() {
        super();
    }

    public AgeException(String message) {
        super(message);
    }
}


//表示当用户的姓名有异常，抛出NameException
public class NameException extends MyUserException{
    public NameException() {
        super();
    }

    public NameException(String message) {
        super(message);
    }
}

```

`handler`

```java
/**
 * @ControllerAdvice : 控制器增强（控制器类增加功能-----异常处理功能）
 *                  位置:在类的上面
 *   特点:必须让框架知道这个注解所在的包名，需要在springmvc配置文件中声明组件扫描器
 *   指定@ControllerAdvice所在的包名
 */
@ControllerAdvice
public class GlobalExceptionHandler {
    //定义方法，处理发生的异常
    /*
    处理异常的方法和控制器方法的定义一样，可以有多个参数，可以有ModelAndView，
    String，void，对象类型的返回值
    (我以为是跟通知一样的，但是考虑到要转到视图的页面，那就行不通，估计是专门搞了个处理异常的代理)

    形参: Exception,表示controller中抛出的异常对象
    通过形参可以获取发生的异常信息

    @ExceptionHandler(异常的class):表示异常的类型，当发生此类型异常时，
    由当前方法处理
     */
        @ExceptionHandler(value = NameException.class)
        public ModelAndView doNameException(Exception ex){
            //处理NameException的异常
            /*
            异常发生处理逻辑：
            1.需要把异常记录下来，记录到数据库，日志文件
                记录日志发生的时间，哪个方法发生的，异常错误内容
            2.发送通知，把异常的信息通过邮件，短信，微信发送给相关人员。
            3.给用户友好的提示。
             */
            ModelAndView mv = new ModelAndView();
            mv.addObject("msg","姓名必须是zs，其他用户不能访问");
            mv.addObject("ex",ex);
            mv.setViewName("nameError");
            return mv;
        }
    //处理AgeException
    @ExceptionHandler(value = AgeException.class)
    public ModelAndView doAgeException(Exception ex){
        //处理AgeException的异常
            /*
            异常发生处理逻辑：
            1.需要把异常记录下来，记录到数据库，日志文件
                记录日志发生的时间，哪个方法发生的，异常错误内容
            2.发送通知，把异常的信息通过邮件，短信，微信发送给相关人员。
            3.给用户友好的提示。
             */
        ModelAndView mv = new ModelAndView();
        mv.addObject("msg","你的年龄不能大于80");
        mv.addObject("ex",ex);
        mv.setViewName("ageError");
        return mv;
    }

    //处理其他异常，NameException,AgeException以外，不知类型的异常,相当于if-else中的else，只能有一个
    @ExceptionHandler
    public ModelAndView doOtherException(Exception ex){
        //处理其他类型异常

        ModelAndView mv = new ModelAndView();
        mv.addObject("msg","姓名必须是zs，其他用户不能访问");
        mv.addObject("ex",ex);
        mv.setViewName("defaultError");
        return mv;
    }
}

```

> 这个思路就是异常进行统一的处理哈，如果有别的异常也可以转到指定的页面去

--------------------------------------------------------------8.26 anki 在这里---------------------------------------------------------------------------------------------

## 拦截器

> 1. 拦截器是springmvc中的一种，需要实现`HandlerInterceptor`接口
>
> 2. 拦截器和过滤器类似，功能方向侧重点不同，过滤器是用来过滤请求参数，设置编码 字符集等工作，拦截器是拦截用户请求的，对请求做判断处理。
>
> 3. 拦截器是全局的，可以对多个`Controller`做拦截。
>
>    一个项目可以有0个或多个拦截器，他们在一起拦截用户请求。
>
>    拦截器常用在：用户登录处理，权限检查，记录日志
>
> 拦截器的使用步骤：
>
> 1. 新建maven web项目
> 2. 加入依赖
> 3. 创建Controller类
> 4. 创建一个普通类，作为拦截器使用
>    1. 定义类实现`HandlerInterceptor`接口
>    2. 实现接口中的三个方法
> 5. 创建show.jsp
> 6. 创建springmvc配置文件
>    1. 组件扫描器，扫描`@Controller`注解
>    2. 声明拦截器，并制定拦截的请求uri地址
>
> 拦截器的执行时间
>
> 1. 在请求处理之前，也就是controller类中的方法执行之前先被拦截
> 2. 在控制器方法执行之后也会执行拦截器
> 3. 在请求处理完成后也会执行拦截器

```java
//拦截器类：拦截用户的请求。
public class MyInterceptor implements HandlerInterceptor {

    private long btime = 0;
    /**
     * preHandle叫做预处理方法
     *  重要:是整个项目的入口，门户，当preHandle返回true请求可以被处理
     *      返回false，请求方法到此就截止了
     * 参数：
     *  Object handler: 
     *  返回值boolean
     *  true：请求是通过拦截器的验证，可以执行处理器方法
     *  拦截器的MyInterceptor的preHandle()
     * ========执行MyController中的doSome方法=========
     * 拦截器的MyInterceptor的postHandle()
     * 拦截器的MyInterceptor的afterCompletion()
     *  false：请求没有通过拦截器的验证，请求到达拦截器就停止了，请求没有被处理
     *  拦截器的MyInterceptor的preHandle()
     *
     *  特点：
     *  1.方法在控制器方法(MyController的doSome)之前先执行的
     *      用户的请求首先到达此方法
     *
     *  2.在这个 方法中可以获取请求的信息，验证是否符合要求
     *      可以验证用户是否登录，验证用户是否有权限某个连接地址(url)。
     *      如果验证失败，可以截断请求，请求不能被处理
     *      如果验证成功，可以放行请求，此时控制器方法才能执行
     */
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
      btime = System.currentTimeMillis();
        System.out.println("拦截器的MyInterceptor的preHandle()");
        //计算的业务逻辑，根据计算结果，返回true or false
        //给浏览器一个返回结果
//        request.getRequestDispatcher("/tips.jsp").forward(request,response);
        return true;
    }

    /*
    postHandle：后处理方法。
    参数：
     Object handler：被拦截的处理器对象MyController
     ModelAndView mv:处理器方法的返回值

     特点:
        1. 在处理器方法之后执行的(MyController.doSome())
        2.能够获取到处理器方法的返回值ModelAndView,可以修改ModelAndView中的
        数据和视图，可以影响到最后的执行结果
        3.主要是对原来的执行结果做二次修正。(环绕通知把)
        (所以返回值不是ModelAndView咋办)
        (个人觉得是把ModelAndView搞完之后再给的)
     */
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("拦截器的MyInterceptor的postHandle()");

        //对原来的doSome执行结果，进行调整
        if(modelAndView != null){
          //修改数据
            modelAndView.addObject("mydate",new Date());
            //修改视图
            modelAndView.setViewName("other");
        }
    }

    /*
     * afterCompletion:最后执行的方法
     * 参数：
     *  Object handler: 被拦截的处理器对象
     *  Exception ex:程序中发生的异常
     * 特点:
     * 1.在请求处理完成后执行的。框架中规定当你的视图处理完成后，对视图执行了forward，就认为请求处理完成
     * 2.一般是做资源回收工作的，程序请求过程中创建了一些对象，在这里可以删除，把占用的内存回收。(还是通知，忘记叫啥了，也是资源关闭的)
     */
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("拦截器的MyInterceptor的afterCompletion()");
        long etime = System.currentTimeMillis();
        System.out.println("计算从preHandle到请求处理完成的时间：" + (etime - btime));
    }
}

```

```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
         https://www.springframework.org/schema/context/spring-context.xsd
          http://www.springframework.org/schema/mvc
           https://www.springframework.org/schema/mvc/spring-mvc.xsd">

<!--   声明 组件扫描器-->
    <context:component-scan base-package="com.zbr.controller"/>
<!--    声明 springmvc框架中的视图解析器，帮助开发人员设置 视图文件的路径，不用重复下相同的

-->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
<!--        前缀：视图文件的路径-->
        <property name="prefix" value="/WEB-INF/view/"/>
<!--        后缀：视图文件的扩展名-->
        <property name="suffix" value=".jsp"/>
    </bean>

<!--声明拦截器:拦截器可以有0个或多个-->
<mvc:interceptors>
<!--    声明第一个拦截器-->
<mvc:interceptor>
<!--    指定拦截的请求uri地址
        path:就是uri地址，可以使用通配符 **
        **:表示任意的字符，文件或者多级目录和目录中的文件
        http://localhost:8080/myweb/user/listUser.do

-->
    <mvc:mapping path="/**"/>
<!--    声明拦截器对象-->
    <bean class="com.zbr.handler.MyInterceptor"/>
</mvc:interceptor>
</mvc:interceptors>
</be
```

> 这个是框架给的，而且没用注解，直接就实现类了，之前蛮多都是有用注解的

### 多个拦截器

1. #### 第一个拦截器`preHandle=true`,第二个`preHandle=true`

```
1111111拦截器的MyInterceptor的preHandle()
2222222拦截器的MyInterceptor的preHandle()
========执行MyController中的doSome方法=========
222222拦截器的MyInterceptor的postHandle()
111111拦截器的MyInterceptor的postHandle()
22222拦截器的MyInterceptor的afterCompletion()
11111拦截器的MyInterceptor的afterCompletion()
```

![image-20200822110017642](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200822110017642.png)

![image-20200822113630335](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200822113630335.png)

#### 2. 第一个拦截器为`preHandle=true`,第二个拦截器`preHandle=false`

```
1111111拦截器的MyInterceptor的preHandle()
2222222拦截器的MyInterceptor的preHandle()
11111拦截器的MyInterceptor的afterCompletion()
```

> 理解为只要preHandle为true，则一定会有个`afterCompletion`，因为在这中间内你能否成功，是凭你自身的，但是我不管，我最后等你结果出来后我就是会执行

#### 3.第一个拦截器为`preHandle=false拦截器`preHandle=false|true`

```
1111111拦截器的MyInterceptor的preHandle()
```

 

> 这个还是蛮好理解的吼，跟filter的那个链感觉差不多，把他想成一个四方形的拦截就好。

## 拦截器和过滤器的区别

1. 过滤器是servlet中的对象，拦截器是框架中的对象

2. 过滤器实现Filter接口的对象，拦截器是实现`HandlerInterceptor`

3. 过滤器是用来设置`request,response`的参数，属性，侧重于对数据过滤

   拦截器是用来验证请求的，能截断请求

4. 过滤器在拦截器之前先执行的(想象成一个美好的世界，拦人先看有没有带不该带的东西，而不是先看他是哪里人)

5. 过滤器是tomcat服务器创建的对象(所以过滤器比拦截器先)

   拦截器是springmvc容器中 创建的对象

6. 过滤器是一个执行时间点。

   拦截器有三个执行时间点

7. 过滤器可以处理jsp，js,html等等

   拦截器是侧重拦截对`Controller`的对象，如果你的请求不能被`DispatcherServlet`接受，这个请求不会执行拦截器内容(所以这就是过滤器先的原因之2，过滤器完之后才能给servlet啊，可拦截器是servlet给的诶，所以明白了吧)

8. 拦截器拦截普通类(Controller)方法执行，过滤器过滤servlet请求响应

## 权限拦截器举例

![image-20200822115916951](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200822115916951.png)

使用拦截器检查登录的用户是不是能访问系统

实现步骤

1. 新建maven

2. 修改`web.xml`注册中央调度器

3. 新建index.jsp发起请求

4. 创建MyController 处理请求

5. 创建结果show.jsp

6. 创建login.jsp 模拟登录(把用户的信息放入到session中)

   创建jsp,logout.jsp,模拟退出系统(从session中删除数据)

7. 拦截器，从session中获取用户登录的数据，验证能否访问系统

8. 创建一个验证的jsp，如果验证视图，给出提示

9. 创建spring.mvc 配置文件

   声明组件扫描器

   声明拦截器



代码也没啥特别的把

```java
//拦截器类：拦截用户的请求。
public class MyInterceptor implements HandlerInterceptor {


    //验证登录的用户信息，正确return true，其他 return false
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {

        System.out.println("1111111拦截器的MyInterceptor的preHandle()");
        String loginName = "";
        //从session中获取name的值
        Object arr = request.getSession().getAttribute("name");
        if(arr != null){
            loginName = (String) arr;
        }
        //判断登录的账户，是否符合要求
        if(!"zs".equals(loginName)){
            //不能访问系统
            //给用户提示
            request.getRequestDispatcher("/tips.jsp").forward(request,response);
            return false;
        }
        //zs 登录
        return true;
    }



}

```

真没啥特别的，一般要求掌握`preHandle`就基本差不多了



## springmvc内部请求处理流程

![image-20200822172122262](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200822172122262.png)

> 也就是springmvc接受请求，到处理完成的过程
>
> 1. 用户发起请求some.do
>
> 2. `DispatcherServlet`接受请求some.do,把请求转交给处理器映射器
>
>    处理器映射器:springmvc 框架中的一种对象，框架把实现了`HandleMapping`接口的类都叫做映射器(多个)
>
>    处理器映射器作用: 
>
>    1. 根据请求，从springmvc容器对象中获取处理器对象(`MyController controller = ctx.getBean("some.do")`)
>
>    2. 框架把找到的处理器对象放到一个叫做处理器执行链(`HandlerExecutionChain`)的类保存
>
>    `HandlerExecutionChain`：类中保存着:1. 处理器对象 2.项目中的所有拦截器`List<HandlerInterceptor>`
>
> 3. `DispatcherServlet`把2中的`HandlerExecutionChain`中的处理器对象交给了处理器适配器(多个)
>
>    处理器适配器：springmvc框架中的对象，需要实现`HandlerAdapter`接口
>
>    处理器适配器作用: 执行处理器方法(调用MyController的doSome方法得到返回值`ModelAndView`)
>
> 4. `DispatcherServlet`把3中获取的`ModelAndView`交给了视图解析器对象。视图解析器：springmvc中的对象，需要实现`ViewResolver接口(可以有多个？没尝试过诶)`
>
>    视图解析器:组成视图完整路径，使用前缀，后缀，并创建view对象
>
>    View是一个接口，表示视图，在框架中`jsp,html不是String表示的`而是使用View和他的实现类表示视图的
>
>    `InternalResourceView`:视图类，表示jsp文件，视图解析器会创建`InternalResourceView`类对象，这个对象的里面，有一个属性`url=/WEB-INF/view/show.jsp`
>
> 5. `DispatcherServlet`把4步骤中创建的View对象获取到，调用View类自己的方法，把Model数据放入到request域中，执行对象视图的forward，请求结束



没有注解之前，需要实现各种不同的接口才能做控制器使用

> 如何理解呢？怪不得叫中央调度器，之前还有点懵，不知道为啥。
>
> 中央调度器获得请求，解析下地址，看要去哪个Controller，就是交给了处理器映射器处理，这时候也已经创建好了对象，就取出来对象，交给处理器执行链中保存再去把拦截器一起拉上来，这个处理器执行链就一起返回给中央调度器，下一步就是把这个链交给下一步的处理器适配器处理(拿到对应处理器方法，然后这时候拦截器就开始起作用了)，处理完之后从处理器对象拿到了`ModelAndView`再返回给中央调度器，中央调度器再拿到视图解析器那儿去(我觉得可以把jsp缩小成一个对象，就像一张纸揉成一团一样，你要从数据和jsp中拿到jsp把他两分开)，拿到view之后再传回去，然后就让view自己去执行了。