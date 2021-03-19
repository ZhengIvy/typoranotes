下半的笔记

## 8.配置嵌入式Servlet容器

SpringBoot默认使用的是嵌入的Servlet容器(Tomcat)

![image-20201006222426481](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201006222426481.png)

问题？

### 1.如何定制和修改Servlet容器的相关配置

1. 修改和server有关的配置(ServerProperties也是`EmbeddedServletContainerCustomer`)

   ```properties
   server.port=8081
   server.context-path=/crud
   
   server.tomcat.uri-encoding=UTF-8
   # 通用的Servlet容器设置
   server.xxx
   # Tomcat的设置
   server.tomcat.xxx
   ```

2. 编写一个`EmbeddedServletContainerCustomizer`:嵌入式的Servlet容器的定制器；来修改Servlet容器的配置

   ```java
    @Bean
               public WebServerFactoryCustomizer<ConfigurableWebServerFactory> webServerFactoryCustomizer(){
                   return new WebServerFactoryCustomizer<ConfigurableWebServerFactory>() {
   
                       //定制嵌入式的Servlet容器相关的规则,但是为什么我的什么都没有显示出来，端口号没变啊
                       @Override
                       public void customize(ConfigurableWebServerFactory factory) {
                           factory.setPort(8083);
                       }
                   };
               }
   ```

### 2.注册Servlet三大组件【Servlet、Filter、Listener】

由于SpringBoot默认是以jar包的方式启动嵌入式的Servlet容器来启动SpringBoot的web应用，没有web.xml文件

注册三大组件用一下方式

`ServletRegistrationBean`

```java
 //注册三大组件
    @Bean
    public ServletRegistrationBean myServlet(){

        ServletRegistrationBean<MyServlet> registrationBean = new ServletRegistrationBean<>(new MyServlet(),"/myServlet");
        return registrationBean;

    }
```



`FilterRegistrationBean`

```java
  @Bean
    public FilterRegistrationBean filterRegistrationBean(){
        FilterRegistrationBean<MyFilter> filterRegistrationBean = new FilterRegistrationBean<>();
        filterRegistrationBean.setFilter(new MyFilter());
        filterRegistrationBean.setUrlPatterns(Arrays.asList("/hello","/myServlet"));
        return filterRegistrationBean;
    }
```

![image-20201112192349257](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112192349257.png)

这是个很实际的问题啊！然后它这里是这么搞的hh

`ServletListenerRegistrationBean`

注意关闭项目的时候不再是按上面的红色方块了哈，你这个就相当于一个电脑，那你就是拔电源了，但是你想看输出结果啊，所以应该是退出一个应用

```java
  @Bean
    public ServletListenerRegistrationBean myListener(){
        ServletListenerRegistrationBean<MyListener> listenerRegistrationBean = new ServletListenerRegistrationBean<>(new MyListener());
        return listenerRegistrationBean;


    }
```

SpringBoot帮我们自动配置SpringMvc的时候，自动注册SpringMvc的前端控制器：DispatcherServlet；

DispatcherServletAutoConfiguration中：

```java
@Bean(name = DEFAULT_DISPATCHER_SERVLET_REGISTRATION_BEAN_NAME)
@ConditionalOnBean(value = DispatcherServlet.class, name = DEFAULT_DISPATCHER_SERVLET_BEAN_NAME)
public ServletRegistrationBean dispatcherServletRegistration(
      DispatcherServlet dispatcherServlet) {
   ServletRegistrationBean registration = new ServletRegistrationBean(
         dispatcherServlet, this.serverProperties.getServletMapping());
    //为什么不拦截jsp呢，这实际上是dispactherServlet里面的url-pattern，如果用的是 / 的话就是defaultServlet处理，所以会把静态资源给拦了，然后我查了一下(之前用springmvc的时候也的确没拦jsp)，jsp是有专门的servlet来对付，额，反正就是拦不到把
    //默认拦截： /  所有请求；包静态资源，但是不拦截jsp请求；   /*会拦截jsp
    //可以通过server.servletPath来修改SpringMVC前端控制器默认拦截的请求路径
    
   registration.setName(DEFAULT_DISPATCHER_SERVLET_BEAN_NAME);
   registration.setLoadOnStartup(
         this.webMvcProperties.getServlet().getLoadOnStartup());
   if (this.multipartConfig != null) {
      registration.setMultipartConfig(this.multipartConfig);
   }
   return 
       registration;
}

```

SpringBoot能不能支持其他的Servlet容器

### 3.替换为其他嵌入式Servlet容器

![image-20201007220214971](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201007220214971.png)

默认支持

- Tomcat(默认使用)

  ```xml
  <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-web</artifactId>
     引入web模块默认就是使用嵌入式的Tomcat作为Servlet容器；
  </dependency>
  ```

  

- Jetty

  ```xml
  <!-- 引入web模块 -->
  <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-web</artifactId>
     <exclusions>
        <exclusion>
           <artifactId>spring-boot-starter-tomcat</artifactId>
           <groupId>org.springframework.boot</groupId>
        </exclusion>
     </exclusions>
  </dependency>
  
  <!--引入其他的Servlet容器-->
  <dependency>
     <artifactId>spring-boot-starter-jetty</artifactId>
     <groupId>org.springframework.boot</groupId>
  </dependency>
  ```

  

- Undertow

  ```xml
  <!-- 引入web模块 -->
  <dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-web</artifactId>
     <exclusions>
        <exclusion>
           <artifactId>spring-boot-starter-tomcat</artifactId>
           <groupId>org.springframework.boot</groupId>
        </exclusion>
     </exclusions>
  </dependency>
  
  <!--引入其他的Servlet容器-->
  <dependency>
     <artifactId>spring-boot-starter-undertow</artifactId>
     <groupId>org.springframework.boot</groupId>
  </dependency>
  ```

### 4.嵌入式Servlet容器自动配置的原理

EmbeddedWebServerFactoryCustomizerAutoConfiguration:嵌入式的Servlet容器自动配置

```java
@Configuration(
    proxyBeanMethods = false
)
@ConditionalOnWebApplication
@EnableConfigurationProperties({ServerProperties.class})
public class EmbeddedWebServerFactoryCustomizerAutoConfiguration {
	 @Configuration(
        proxyBeanMethods = false
    )
    @ConditionalOnClass({Tomcat.class, UpgradeProtocol.class})//判断当前是否引入了tomcat依赖
    public static class TomcatWebServerFactoryCustomizerConfiguration {
        public TomcatWebServerFactoryCustomizerConfiguration() {
        }
        @Bean
        public TomcatWebServerFactoryCustomizer tomcatWebServerFactoryCustomizer(Environment environment, ServerProperties serverProperties) {
            return new TomcatWebServerFactoryCustomizer(environment, serverProperties);
        }
    }
}
    //别的类中的，因为这个2.x和1.x的源码不一样了
  @Configuration(
        proxyBeanMethods = false
    )
    @ConditionalOnClass({Servlet.class, Tomcat.class, UpgradeProtocol.class})
    @ConditionalOnMissingBean(
        value = {ServletWebServerFactory.class},
        search = SearchStrategy.CURRENT
    )//判断当前容器中是否有ServletWebServerFactory：嵌入式的Servlet容器工厂：创建嵌入式的Servlet容器
    static class EmbeddedTomcat {
        EmbeddedTomcat() {
        }
    }
```

额，上面是2.x的，但是老师讲的是1.x的，那还是按老师的来吧

@AutoConfigureOrder(Ordered.HIGHEST_PRECEDENCE)
@Configuration
@ConditionalOnWebApplication
@Import(BeanPostProcessorsRegistrar.class)
//导入BeanPostProcessorsRegistrar：Spring注解版；给容器中导入一些组件
//导入了EmbeddedServletContainerCustomizerBeanPostProcessor：
//后置处理器：bean初始化前后（创建完对象，还没赋值赋值）执行初始化工作
public class EmbeddedServletContainerAutoConfiguration {
    
```java
@Configuration
@ConditionalOnClass({ Servlet.class, Tomcat.class })//判断当前是否引入了Tomcat依赖；
@ConditionalOnMissingBean(value = EmbeddedServletContainerFactory.class, search = SearchStrategy.CURRENT)//判断当前容器没有用户自己定义EmbeddedServletContainerFactory：嵌入式的Servlet容器工厂；作用：创建嵌入式的Servlet容器
public static class EmbeddedTomcat {

	@Bean
	public TomcatEmbeddedServletContainerFactory tomcatEmbeddedServletContainerFactory() {
		return new TomcatEmbeddedServletContainerFactory();
	}

}

/**
 * Nested configuration if Jetty is being used.
 */
@Configuration
@ConditionalOnClass({ Servlet.class, Server.class, Loader.class,
		WebAppContext.class })
@ConditionalOnMissingBean(value = EmbeddedServletContainerFactory.class, search = SearchStrategy.CURRENT)
public static class EmbeddedJetty {

	@Bean
	public JettyEmbeddedServletContainerFactory jettyEmbeddedServletContainerFactory() {
		return new JettyEmbeddedServletContainerFactory();
	}

}

/**
 * Nested configuration if Undertow is being used.
 */
@Configuration
@ConditionalOnClass({ Servlet.class, Undertow.class, SslClientAuthMode.class })
@ConditionalOnMissingBean(value = EmbeddedServletContainerFactory.class, search = SearchStrategy.CURRENT)
public static class EmbeddedUndertow {

	@Bean
	public UndertowEmbeddedServletContainerFactory undertowEmbeddedServletContainerFactory() {
		return new UndertowEmbeddedServletContainerFactory();
	}

}
```
1）、EmbeddedServletContainerFactory（嵌入式Servlet容器工厂）

```java
public interface EmbeddedServletContainerFactory {

   //获取嵌入式的Servlet容器
   EmbeddedServletContainer getEmbeddedServletContainer(
         ServletContextInitializer... initializers);

}
```

![](D:/BaiduNetdiskDownload/网课/源码、资料、课件/源码、资料、课件/文档/Spring Boot 笔记/images/搜狗截图20180302144835.png)

2）、EmbeddedServletContainer：（嵌入式的Servlet容器）

![](D:/BaiduNetdiskDownload/网课/源码、资料、课件/源码、资料、课件/文档/Spring Boot 笔记/images/搜狗截图20180302144910.png)



3）、以**TomcatEmbeddedServletContainerFactory**为例

```java
@Override
public EmbeddedServletContainer getEmbeddedServletContainer(
      ServletContextInitializer... initializers) {
    //创建一个Tomcat
   Tomcat tomcat = new Tomcat();
    
    //配置Tomcat的基本环节
   File baseDir = (this.baseDirectory != null ? this.baseDirectory
         : createTempDir("tomcat"));
   tomcat.setBaseDir(baseDir.getAbsolutePath());
   Connector connector = new Connector(this.protocol);
   tomcat.getService().addConnector(connector);
   customizeConnector(connector);
   tomcat.setConnector(connector);
   tomcat.getHost().setAutoDeploy(false);
   configureEngine(tomcat.getEngine());
   for (Connector additionalConnector : this.additionalTomcatConnectors) {
      tomcat.getService().addConnector(additionalConnector);
   }
   prepareContext(tomcat.getHost(), initializers);
    
    //将配置好的Tomcat传入进去，返回一个EmbeddedServletContainer；并且启动Tomcat服务器
   return getTomcatEmbeddedServletContainer(tomcat);
}
```

4）、我们对嵌入式容器的配置修改是怎么生效？

```
ServerProperties、EmbeddedServletContainerCustomizer
```



**EmbeddedServletContainerCustomizer**：定制器帮我们修改了Servlet容器的配置？

怎么修改的原理？

5）、容器中导入了**EmbeddedServletContainerCustomizerBeanPostProcessor**

```java
//初始化之前
@Override
public Object postProcessBeforeInitialization(Object bean, String beanName)
      throws BeansException {
    //如果当前初始化的是一个ConfigurableEmbeddedServletContainer类型的组件
   if (bean instanceof ConfigurableEmbeddedServletContainer) {
       //
      postProcessBeforeInitialization((ConfigurableEmbeddedServletContainer) bean);
   }
   return bean;
}
private void postProcessBeforeInitialization(
			ConfigurableEmbeddedServletContainer bean) {
    //获取所有的定制器，调用每一个定制器的customize方法来给Servlet容器进行属性赋值；
    for (EmbeddedServletContainerCustomizer customizer : getCustomizers()) {
        customizer.customize(bean);
    }
}
private Collection<EmbeddedServletContainerCustomizer> getCustomizers() {
    if (this.customizers == null) {
        // Look up does not include the parent context
        this.customizers = new ArrayList<EmbeddedServletContainerCustomizer>(
            this.beanFactory
            //从容器中获取所有这葛类型的组件：EmbeddedServletContainerCustomizer
            //定制Servlet容器，给容器中可以添加一个EmbeddedServletContainerCustomizer类型的组件
            .getBeansOfType(EmbeddedServletContainerCustomizer.class,
                            false, false)
            .values());
        Collections.sort(this.customizers, AnnotationAwareOrderComparator.INSTANCE);
        this.customizers = Collections.unmodifiableList(this.customizers);
    }
    return this.customizers;
}

ServerProperties也是定制器
```

步骤：

1）、SpringBoot根据导入的依赖情况，给容器中添加相应的EmbeddedServletContainerFactory【TomcatEmbeddedServletContainerFactory】

2）、容器中某个组件要创建对象就会惊动后置处理器；EmbeddedServletContainerCustomizerBeanPostProcessor；

只要是嵌入式的Servlet容器工厂，后置处理器就工作；

3）、后置处理器，从容器中获取所有的**EmbeddedServletContainerCustomizer**，调用定制器的定制方法

> 在这里说一下，虽然说真的超多东西，但是并没有那么难，主要就是一下几点，`Factory`工厂生产一个商品，就是一个容器，那你这个容器毕竟也是要使用的嘛，其实真的就很像aop哈，后置处理器就来了，他工作的时间点就是赋值前后，所以你才可以改变端口等的各种值，然后后置处理器就去调用定制的方法，然后这个对象也就创建了
>
> 看下包是哪个的包，tomcat，jetty还是另外一个，然后返回的是对应的内置容器，进入到内置容器，发现他们是统一实现了一个接口的，然后分别重写那个接口，就在这里面创建一个与tomcat等等其他的东西，然后启动tomcat，并返回了一个嵌入的tomcat

-------------------anki 2020.11.12---------------------------------------------------------

### 5.嵌入式Servlet容器启动原理

什么时候创建嵌入式的Servlet容器工厂？什么时候获取嵌入式的Servlet容器并启动tomcat？

获取嵌入式的Servlet容器工厂：

1. SpringBoot应用启动运行run方法

2. `refreshContext(context)`:SpringBoot刷新IOC容器(创建IOC容器对象并初始化容器，创建容器中的每一个组件)；如果是web应用创建**AnnotationConfigEmbeddedWebApplicationContext**，否则：**AnnotationConfigApplicationContext**

3. refresh(context);**刷新刚才创建好的ioc容器；**

   ```java
   public void refresh() throws BeansException, IllegalStateException {
      synchronized (this.startupShutdownMonitor) {
         // Prepare this context for refreshing.
         prepareRefresh();
   
         // Tell the subclass to refresh the internal bean factory.
         ConfigurableListableBeanFactory beanFactory = obtainFreshBeanFactory();
   
         // Prepare the bean factory for use in this context.
         prepareBeanFactory(beanFactory);
   
         try {
            // Allows post-processing of the bean factory in context subclasses.
            postProcessBeanFactory(beanFactory);
   
            // Invoke factory processors registered as beans in the context.
            invokeBeanFactoryPostProcessors(beanFactory);
   
            // Register bean processors that intercept bean creation.
            registerBeanPostProcessors(beanFactory);
   
            // Initialize message source for this context.
            initMessageSource();
   
            // Initialize event multicaster for this context.
            initApplicationEventMulticaster();
   
            // Initialize other special beans in specific context subclasses.
            onRefresh();
   
            // Check for listener beans and register them.
            registerListeners();
   
            // Instantiate all remaining (non-lazy-init) singletons.
            finishBeanFactoryInitialization(beanFactory);
   
            // Last step: publish corresponding event.
            finishRefresh();
         }
   
         catch (BeansException ex) {
            if (logger.isWarnEnabled()) {
               logger.warn("Exception encountered during context initialization - " +
                     "cancelling refresh attempt: " + ex);
            }
   
            // Destroy already created singletons to avoid dangling resources.
            destroyBeans();
   
            // Reset 'active' flag.
            cancelRefresh(ex);
   
            // Propagate exception to caller.
            throw ex;
         }
   
         finally {
            // Reset common introspection caches in Spring's core, since we
            // might not ever need metadata for singleton beans anymore...
            resetCommonCaches();
         }
      }
   } 
   ```

   

4.  onRefresh(); web的ioc容器重写了onRefresh方法

5. webioc容器会创建嵌入式的Servlet容器；**createEmbeddedServletContainer**();

6. **获取嵌入式的Servlet容器工厂：**EmbeddedServletContainerFactory containerFactory = getEmbeddedServletContainerFactory();从ioc容器中获取EmbeddedServletContainerFactory 组件；**TomcatEmbeddedServletContainerFactory**创建对象，后置处理器一看是这个对象，就获取所有的定制器来先定制Servlet容器的相关配置；

7. **使用容器工厂获取嵌入式的Servlet容器**：this.embeddedServletContainer = containerFactory      .getEmbeddedServletContainer(getSelfInitializer());

8. 嵌入式的Servlet容器创建对象并启动Servlet容器；

   **先启动嵌入式的Servlet容器，再将ioc容器中剩下没有创建出的对象获取出来；**

   **==IOC容器启动创建嵌入式的Servlet容器==**

> 感觉总的思路就是创建对应的ioc容器，ioc容器去创建对象+初始化，那就搞到了一个factory，factory创建好之后来了后置处理器去拿到所有的定制器，factory创建相应的servlet容器，创建好返回之后就会启动这个容器了，就是启动了tomcat



## 9.使用外置的Servlet容器

嵌入式Servlet容器：应用打成可执行的jar

优点：简单、便携

缺点：默认不支持JSP(？？？之前说的只是jetty还是undertow不支持而已啊)、优化定制比较复杂(使用定制器【ServerProperties】，【EmbeddedServletContainterCustomizer】,自己编写嵌入式Servlet容器的创建)

外置的Servlet容器：外面安装Tomcat---应用war方式打包

![image-20201008142304738](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201008142304738.png)

步骤：

1. 必须创建一个war项目（利用idea创建好目录结构）

2. 将嵌入式的tomcat指定为provided

3. 

   ```xml
    <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter-tomcat</artifactId>
               <scope>provided</scope>
           </dependency>
   ```

   这个的意思是打包的时候带上，为什么不带呢，因为这个用的是外置的tomcat，要发布的时候直接放到外面的tomcat上就行了，内置的话就需要随身带着

4. 必须编写一个SpringBootInitializer的子类，并调用configure方法

   ```java
   //自动生成的
   public class ServletInitializer extends SpringBootServletInitializer {
   
       @Override
       protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
           //传入SpringBoot应用的主程序
           return application.sources(SpringBoot04WebJspApplication.class);
       }
   
   }
   ```

5. 启动服务器就可以使用

### 原理：

jar包：执行SpringBoot主类的main方法；启动ioc容器，创建嵌入式的Servlet容器	

war包：启动服务器，**服务器启动springboot应用**【SpringBootServletInitializer】，启动ioc容器；

servlet3.0（Spring注解版）：

8.2.4 Shared libraries / runtimes pluggability：

规则：

​	1）、服务器启动（web应用启动）会创建当前web应用里面每一个jar包里面ServletContainerInitializer实例：

​	2）、ServletContainerInitializer的实现放在jar包的META-INF/services文件夹下，有一个名为javax.servlet.ServletContainerInitializer的文件，内容就是ServletContainerInitializer的实现类的全类名

​	3）、还可以使用@HandlesTypes，在应用启动的时候加载我们感兴趣的类；A

流程：

1）、启动Tomcat

2）、org\springframework\spring-web\4.3.14.RELEASE\spring-web-4.3.14.RELEASE.jar!\META-INF\services\javax.servlet.ServletContainerInitializer：

Spring的web模块里面有这个文件：**org.springframework.web.SpringServletContainerInitializer**

3）、SpringServletContainerInitializer将@HandlesTypes(WebApplicationInitializer.class)标注的所有这个类型的类都传入到onStartup方法的Set<Class<?>>；为这些WebApplicationInitializer类型的类创建实例；

4）、每一个WebApplicationInitializer都调用自己的onStartup；

![](D:/BaiduNetdiskDownload/网课/源码、资料、课件/源码、资料、课件/文档/Spring Boot 笔记/images/搜狗截图20180302221835.png)

5）、相当于我们的SpringBootServletInitializer的类会被创建对象，并执行onStartup方法

6）、SpringBootServletInitializer实例执行onStartup的时候会createRootApplicationContext；创建容器

```java
protected WebApplicationContext createRootApplicationContext(
      ServletContext servletContext) {
    //1、创建SpringApplicationBuilder
   SpringApplicationBuilder builder = createSpringApplicationBuilder();
   StandardServletEnvironment environment = new StandardServletEnvironment();
   environment.initPropertySources(servletContext, null);
   builder.environment(environment);
   builder.main(getClass());
   ApplicationContext parent = getExistingRootWebApplicationContext(servletContext);
   if (parent != null) {
      this.logger.info("Root context already created (using as parent).");
      servletContext.setAttribute(
            WebApplicationContext.ROOT_WEB_APPLICATION_CONTEXT_ATTRIBUTE, null);
      builder.initializers(new ParentContextApplicationContextInitializer(parent));
   }
   builder.initializers(
         new ServletContextApplicationContextInitializer(servletContext));
   builder.contextClass(AnnotationConfigEmbeddedWebApplicationContext.class);
    
    //调用configure方法，子类重写了这个方法，将SpringBoot的主程序类传入了进来
   builder = configure(builder);
    
    //使用builder创建一个Spring应用
   SpringApplication application = builder.build();
   if (application.getSources().isEmpty() && AnnotationUtils
         .findAnnotation(getClass(), Configuration.class) != null) {
      application.getSources().add(getClass());
   }
   Assert.state(!application.getSources().isEmpty(),
         "No SpringApplication sources have been defined. Either override the "
               + "configure method or add an @Configuration annotation");
   // Ensure error pages are registered
   if (this.registerErrorPageFilter) {
      application.getSources().add(ErrorPageFilterConfiguration.class);
   }
    //启动Spring应用
   return run(application);
}
```

7）、Spring的应用就启动并且创建IOC容器

```java
public ConfigurableApplicationContext run(String... args) {
   StopWatch stopWatch = new StopWatch();
   stopWatch.start();
   ConfigurableApplicationContext context = null;
   FailureAnalyzers analyzers = null;
   configureHeadlessProperty();
   SpringApplicationRunListeners listeners = getRunListeners(args);
   listeners.starting();
   try {
      ApplicationArguments applicationArguments = new DefaultApplicationArguments(
            args);
      ConfigurableEnvironment environment = prepareEnvironment(listeners,
            applicationArguments);
      Banner printedBanner = printBanner(environment);
      context = createApplicationContext();
      analyzers = new FailureAnalyzers(context);
      prepareContext(context, environment, listeners, applicationArguments,
            printedBanner);
       
       //刷新IOC容器
      refreshContext(context);
      afterRefresh(context, applicationArguments);
      listeners.finished(context, null);
      stopWatch.stop();
      if (this.logStartupInfo) {
         new StartupInfoLogger(this.mainApplicationClass)
               .logStarted(getApplicationLog(), stopWatch);
      }
      return context;
   }
   catch (Throwable ex) {
      handleRunFailure(context, listeners, analyzers, ex);
      throw new IllegalStateException(ex);
   }
}
```

**==启动Servlet容器，再启动SpringBoot应用==**

> 总结一下，觉得难理解吗，其实也还行吧，能看得懂，但那种精髓应该是掌握不到的，
>
> 首先呢说的是我们是先启动Servlet容器。再启动SpringBoot应用的，所以问题是你怎么在启动Servlet的时候去启动SpringBoot的，值得一说的是这里是有一个ServletInitializer，所以应该是从这里再去启动SpringBoot，因为这个东西里面也有传入那个SpringBootApplication的类文件，那这里的说法是服务器启动的时候，会创建当前web应用的每一个jar包里面ServletContainerInitializer,然后你还可以加一些别的东西进去嘛，别的星球的人来逃难，你说可以的哈，然后创建实例后，会执行onStartup方法，然后就起飞了，到达逃难的星球后，用了Builder的方法，把自己的文明再生根发芽，创建了原先的文明在另外的地球上
>
> 不过这是1.x的源码，虽然2.x可能不会差太多，但是的话俺觉得差不多就ok，虽然的话我觉得这个源码的部分后面使需要再来看一遍的



-----------------------------------------2020/11/14 anki----------------------------------------

## 五、Docker

### 1. 简介

Docker使一个开源的应用容器引擎

![image-20201009084900672](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009084900672.png)

![image-20201009084923464](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201009084923464.png)

> 个人理解的话它是一开始想解决的问题是，每个人不需要重复的安装一样的东西，比如装系统，要装好多的东西，为了简单的话，就只装一个，然后让别人用它的镜像就可以了，突然想到了阿里云镜像

### 2.核心概念

docker主机(Host):安装了Docker程序的机器(Docker直接安装再操作系统之上)

docker客户端(Cilent):连接docker主机进行操作

docker仓库(Registry):用来保存各种打包好的软件镜像

docker镜像(Images):软件打包好的镜像，放在docker仓库中

docker容器(Container):镜像启动后的实例称为一个容器，容器时独立运行的一个或一组应用

使用步骤：

1. 安装Docker
2. 去Docker仓库找到这个软件对应的镜像
3. 使用Docker运行这个镜像，这个镜像就会生成一个Docker容器
4. 对容器的启动停止就是对软件的启动停止

> 个人理解：比如说麦当劳，在每个国家都会因地制宜改变菜单，但基本东西时不会变的，就是一些口味上会有区别，所以的话就引进了麦当劳，麦当劳的这个实体店时一个主机，然后那些专业人员在背后也就是在客户端里面对菜单进行操作，他们就从仓库拿来一些东西，把他们安装好的东西直接拿过来，然后这边的话再本地生根发芽，我猜这里面有一些配置要改，需要自己搞，所以镜像启动后的实例就是一个容器(本土化的麦当劳)，然后你这个本土化停了，那你麦当劳也就没了哈

### 3.安装Docker

#### 1. 安装虚拟机

1. VMWARE,VirtualBox
2. 导入虚拟机文件
3. 双击启动linux虚拟机；使用root登录
4. 使用客户端连接

![image-20201026215244002](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201026215244002.png)

#### 2. 在linux虚拟机上安装docker

步骤：

```shell
1、检查内核版本，必须是3.10及以上
uname -r
2、安装docker
yum install docker
3、输入y确认安装
4、启动docker
[root@localhost ~]# systemctl start docker
[root@localhost ~]# docker -v
Docker version 1.12.6, build 3e8e77d/1.12.6
5、开机启动docker
[root@localhost ~]# systemctl enable docker
Created symlink from /etc/systemd/system/multi-user.target.wants/docker.service to /usr/lib/systemd/system/docker.service.
6、停止docker
systemctl stop docker
```

--------------------------------------------------anki 11.16-----------------------------------------------------

### 4. Docker 常用命令&操作

#### 1. 镜像操作

| 操作 | 命令                                            | 说明                                                     |
| ---- | ----------------------------------------------- | -------------------------------------------------------- |
| 检索 | docker  search 关键字  eg：docker  search redis | 我们经常去docker  hub上检索镜像的详细信息，如镜像的TAG。 |
| 拉取 | docker pull 镜像名:tag                          | :tag是可选的，tag表示标签，多为软件的版本，默认是latest  |
| 列表 | docker images                                   | 查看所有本地镜像                                         |
| 删除 | docker rmi image-id                             | 删除指定的本地镜像                                       |

https://hub.docker.com/

#### 2. 容器操作

软件镜像（QQ安装程序）----运行镜像----产生一个容器（正在运行的软件，运行的QQ）；

步骤：

````shell
1、搜索镜像
[root@localhost ~]# docker search tomcat
2、拉取镜像
[root@localhost ~]# docker pull tomcat
3、根据镜像启动容器
docker run --name mytomcat -d tomcat:latest
4、docker ps  
查看运行中的容器
5、 停止运行中的容器
docker stop  容器的id
6、查看所有的容器
docker ps -a
7、启动容器
docker start 容器id
8、删除一个容器
 docker rm 容器id
9、启动一个做了端口映射的tomcat
[root@localhost ~]# docker run -d -p 8888:8080 tomcat
-d：后台运行
-p: 将主机的端口映射到容器的一个端口    主机端口:容器内部的端口

10、为了演示简单关闭了linux的防火墙
service firewalld status ；查看防火墙状态
service firewalld stop：关闭防火墙
11、查看容器的日志
docker logs container-name/container-id

更多命令参看
https://docs.docker.com/engine/reference/commandline/docker/
可以参考每一个镜像的文档

````

感觉有点不一样吼，他这个可以一次性搞多个tomcat，俺们好像不行，映射多个端口过来，nb哈

### 关于docker run 和 docker start 的区别

![image-20201030120003975](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201030120003975.png)

我个人理解镜像就是一个`exe`,然后run是重新搞一个exe生成一个容器，start就是在已有容器上打开而已

#### 3.安装mysql示例

```
docker pull mysql
```

##### 连navicat过程中遇到的问题

1. 老是出错，![image-20201031094755417](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201031094755417.png)

   然后我`systemctl restart docker`就好了

   ![image-20201031094835028](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201031094835028.png)

2. 搞好后去navicat那边连接发现

   <img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201031094908105.png" alt="image-20201031094908105" style="zoom:50%;" />

   确认之后呢出现了1251的错误，什么`authentication error`,

   然后发现是加密的问题？？

![image-20201031094556243](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201031094556243.png)





错误的启动

```shell
[root@localhost ~]# docker run --name mysql01 -d mysql
42f09819908bb72dd99ae19e792e0a5d03c48638421fa64cce5f8ba0f40f5846

mysql退出了
[root@localhost ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                           PORTS               NAMES
42f09819908b        mysql               "docker-entrypoint.sh"   34 seconds ago      Exited (1) 33 seconds ago                            mysql01
538bde63e500        tomcat              "catalina.sh run"        About an hour ago   Exited (143) About an hour ago                       compassionate_
goldstine
c4f1ac60b3fc        tomcat              "catalina.sh run"        About an hour ago   Exited (143) About an hour ago                       lonely_fermi
81ec743a5271        tomcat              "catalina.sh run"        About an hour ago   Exited (143) About an hour ago                       sick_ramanujan


//错误日志
[root@localhost ~]# docker logs 42f09819908b
error: database is uninitialized and password option is not specified 
  You need to specify one of MYSQL_ROOT_PASSWORD, MYSQL_ALLOW_EMPTY_PASSWORD and MYSQL_RANDOM_ROOT_PASSWORD；这个三个参数必须指定一个
```

正确的启动

```shell
[root@localhost ~]# docker run --name mysql01 -e MYSQL_ROOT_PASSWORD=123456 -d mysql
b874c56bec49fb43024b3805ab51e9097da779f2f572c22c695305dedd684c5f
[root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
b874c56bec49        mysql               "docker-entrypoint.sh"   4 seconds ago       Up 3 seconds        3306/tcp            mysql01
```

做了端口映射

```shell
[root@localhost ~]# docker run -p 3306:3306 --name mysql02 -e MYSQL_ROOT_PASSWORD=123456 -d mysql
ad10e4bc5c6a0f61cbad43898de71d366117d120e39db651844c0e73863b9434
[root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
ad10e4bc5c6a        mysql               "docker-entrypoint.sh"   4 seconds ago       Up 2 seconds        0.0.0.0:3306->3306/tcp   mysql02
```



几个其他的高级操作

```
docker run --name mysql03 -v /conf/mysql:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag
把主机的/conf/mysql文件夹挂载到 mysqldocker容器的/etc/mysql/conf.d文件夹里面
改mysql的配置文件就只需要把mysql配置文件放在自定义的文件夹下（/conf/mysql）

docker run --name some-mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql:tag --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
指定mysql的一些配置参数
```

## 六、SprigBoot与数据访问

1. JDBC

```xml
<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-jdbc</artifactId>
		</dependency>
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<scope>runtime</scope>
		</dependency>
```

`application.yml`中配置的

```yaml
spring:
  datasource:
    username: root
    password: 123456
    url: jdbc:mysql://192.168.100.129:3306/jdbc
    driver-class-name: com.mysql.cj.jdbc.Driver
```

效果：

默认使用的是`class com.zaxxer.hikari.HikariDataSource`,额，和1.x 的不一样哈

数据源相关的配置都在`DataSourceProperties`里面

自动配置原理：

`org.springframework.boot.autoconfigure.jdbc`:

1. 参考`DataSourceConfiguration`,根据配置创建数据源，默认使用hikari(2.x之后)连接池，可以使用`spring.datasource.type`指定自定义的数据类型

2. springboot默认支持：

   ```
   org.apache.tomcat.jdbc.pool.DataSource、HikariDataSource、BasicDataSource、
   ```

3. 自定义数据源类型

   ```java
    @Configuration(
           proxyBeanMethods = false
       )
       @ConditionalOnMissingBean({DataSource.class})
       @ConditionalOnProperty(
           name = {"spring.datasource.type"}
       )
       static class Generic {
           Generic() {
           }
   
           @Bean
           DataSource dataSource(DataSourceProperties properties) {
               //使用DataSourceBuilder创建数据源，利用反射创建响应type的数据源，并且绑定相关属性
               return properties.initializeDataSourceBuilder().build();
           }
       }
   ```

4. DataSourceInitializer：ApplicationListener:

   这个实际上就是短暂时间的建表操作，就是你项目停了你这个~~表就没了~~，~~所以感觉后面是不是会加强一下这个功能，因为是通过springboot来帮你建表的~~，不是的，我试了一下，不会没有，还是保持原来的状态，所以的话这个建表其实算是重新建表，但不会起冲突的那种。

   作用：

   1. `runSchemaScripts():运行建表语句`
   2. `runDataScripts:运行插入数据的 sql语句`

   默认只需要将文件命名为：

   ```properties
   schema-*.sql、data-*.sql
   默认规则：schema.sql，schema-all.sql；
   可以使用   
   	schema:
         - classpath:department.sql
         指定位置
   ```

5. 操作数据库：自动配置了JdbcTemplate操作数据库

### 整合Druid数据源

```java
导入druid数据源
@Configuration
public class DruidConfig {

    @ConfigurationProperties(prefix = "spring.datasource")
    @Bean
    public DataSource druid(){
       return  new DruidDataSource();
    }
    //配置Druid的监控
    //1、配置一个管理后台的Servlet
    @Bean
    public ServletRegistrationBean statViewServlet(){
        ServletRegistrationBean bean = new ServletRegistrationBean(new StatViewServlet(), "/druid/*");
        Map<String,String> initParams = new HashMap<>();

        //这个应该是给servlet的参数
        initParams.put("loginUsername","admin");
        initParams.put("loginPassword","123456");
        initParams.put("allow","");//默认就是允许所有访问
        initParams.put("deny","192.168.15.21");

        bean.setInitParameters(initParams);
        return bean;
    }
    //2、配置一个web监控的filter
    @Bean
    public FilterRegistrationBean webStatFilter(){
        FilterRegistrationBean bean = new FilterRegistrationBean();
        bean.setFilter(new WebStatFilter());
        //给Filter的参数
        Map<String,String> initParams = new HashMap<>();
        initParams.put("exclusions","*.js,*.css,/druid/*");
        bean.setInitParameters(initParams);
        bean.setUrlPatterns(Arrays.asList("/*"));
        return  bean;
    }
}
```

![image-20201031210452755](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201031210452755.png)

nb啊，原来那个servlet是搞这个的啊，我还以为啥呢

![image-20201031210548065](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201031210548065.png)

这个也是可以查得出来的哦

### 整合mybatis

```xml
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>2.1.3</version>
</dependency>
```

![image-20201031212808554](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201031212808554.png)

#### 注解版

```java
package com.zbr.springboot.mapper;

import com.zbr.springboot.bean.Department;
import org.apache.ibatis.annotations.*;

//这里用的是注解版的哦，动力节点教的是xml的
//操作数据库的
@Mapper
public interface DepartmentMapper {

    //天哪，这个那边也没教，看起来好方便哦,但是感觉只适用于简单的项目，高级的操作还是在xml这边
    @Select("select * from department where id=#{id}")
    public Department getDeptById(Integer id);

    @Delete("delete from department where id = #{id}")
    public int deleteDeptById(Integer id);

    @Insert("insert into department(departmentName) values(#{departmentName})  ")
    public int insertDept(Department department);

    @Update("update department set departmentName=#{departmentName} where id=#{id}")
    public int updateDept(Department department);

}

```

问题：
自定义MyBatis的配置规则:给容器中添加一个ConfigurationCustomizer:

```java
@org.springframework.context.annotation.Configuration
public class MyBatisConfig {
    @Bean
    public ConfigurationCustomizer configurationCustomizer(){

        return new ConfigurationCustomizer(){

            @Override
            public void customize(Configuration configuration) {
                //数据库中的下划线字转换为实体中的驼峰命名变量，这个是个很实用也是我们经常考虑到的问题
                configuration.setMapUnderscoreToCamelCase(true);
            }
        };
    }
}
```

```java
@MapperScan(value = "com.zbr.springboot.mapper")
@SpringBootApplication
public class SpringBoot06DataMybatisApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringBoot06DataMybatisApplication.class, args);
    }
}
```

#### 配置文件版

```yml
mybatis:
  config-location: classpath:mybatis/mybatis-config.xml  指定全局配置文件的位置
  mapper-locations:
    - classpath:mybatis/mapper/*.xml 指定sql映射文件的位置
```

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201104210152815.png" alt="image-20201104210152815" style="zoom:50%;" />

有点奇怪的是，xml文件没和接口搞在一个文件夹里，我一会看看啊哈

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <settings>
    这个就是解决了数据库和idea这里的命名格式要求不一样的问题，就可以自动转换，很好哈
        <setting name="mapUnderscoreToCamelCase" value="true"/>
    </settings>

</configuration>
```

### @Mapper 和 @MapperScan

记住哈，重要的，之前没搞懂上面的@Mapper 和 @MapperScan 的意思

```java
@Mapper
@Component
public interface EmployeeMapper {

    public Employee getEmpById(Integer id);

    public void insertEmp(Employee employee);
}

```

这里的Mapper代表的意思是生成接口对应的实现类而已，我们之前是用哪个动态代理来着忘记了，mybatis是用别的方法来的，问题不大，所以这个注解是注解版和配置文件版都需要的，@Mapper是在每一个dao上面都要的哈



所以问题来了，如果你有很多dao，那这样写不是很麻烦吗？的确，所以我们有了@MapperScan

```java
@MapperScan(value = "com.zbr.springboot.mapper")
@SpringBootApplication
public class SpringBoot06DataMybatisApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringBoot06DataMybatisApplication.class, args);
    }

}
```

会去扫描每一个并直接生成，就很方便。



还有的问题是，你对应的xml文件放哪啊？springboot里面教的时候不把他和mapper放在一起诶

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201117090748653.png" alt="image-20201117090748653" style="zoom:50%;" />

```yml
mybatis:
  mapper-locations:
    - classpath:mybatis/mapper/*.xml
```

这里啦，这个是指定xml文件的，所以必须加上噢

---------------------------------------------------------anki 11.17------------------------------------

## 七、启动配置原理

几个重要的事件回调机制

配置在META-INF/spring.factories

**ApplicationContextInitializer**

**SpringApplicationRunListener**



只需要放在ioc容器中

**ApplicationRunner**

**CommandLineRunner**



启动流程：

### **1、创建SpringApplication对象**

```java
initialize(sources);
private void initialize(Object[] sources) {
    //保存主配置类
    if (sources != null && sources.length > 0) {
        this.sources.addAll(Arrays.asList(sources));
    }
    //判断当前是否一个web应用
    this.webEnvironment = deduceWebEnvironment();
    //从类路径下找到META-INF/spring.factories配置的所有ApplicationContextInitializer；然后保存起来
    setInitializers((Collection) getSpringFactoriesInstances(
        ApplicationContextInitializer.class));
    //从类路径下找到ETA-INF/spring.factories配置的所有ApplicationListener
    setListeners((Collection) getSpringFactoriesInstances(ApplicationListener.class));
    //从多个配置类中找到有main方法的主配置类
    this.mainApplicationClass = deduceMainApplicationClass();
}
```

![](D:/BaiduNetdiskDownload/网课/源码、资料、课件/源码、资料、课件/文档/Spring Boot 笔记/images/搜狗截图20180306145727.png)

![](D:/BaiduNetdiskDownload/网课/源码、资料、课件/源码、资料、课件/文档/Spring Boot 笔记/images/搜狗截图20180306145855.png)

> 怎么说呢，我也不是说能懂他具体为什么这么操作，我觉得我懂的是一些比较片面的东西，就是其实像一个发射器？你在发射之前要去填充一些燃料之类的。那这个applicationContext是全局的配置把。listener再搞点监听器？

### 2、运行run方法

```java
public ConfigurableApplicationContext run(String... args) {
   StopWatch stopWatch = new StopWatch();
   stopWatch.start();
   ConfigurableApplicationContext context = null;
   FailureAnalyzers analyzers = null;
   configureHeadlessProperty();
    
   //获取SpringApplicationRunListeners；从类路径下META-INF/spring.factories
   SpringApplicationRunListeners listeners = getRunListeners(args);
    //回调所有的获取SpringApplicationRunListener.starting()方法
   listeners.starting();
   try {
       //封装命令行参数
      ApplicationArguments applicationArguments = new DefaultApplicationArguments(
            args);
      //准备环境
      ConfigurableEnvironment environment = prepareEnvironment(listeners,
            applicationArguments);
       		//创建环境完成后回调SpringApplicationRunListener.environmentPrepared()；表示环境准备完成
       
      Banner printedBanner = printBanner(environment);
       
       //创建ApplicationContext；决定创建web的ioc还是普通的ioc
      context = createApplicationContext();
       
      analyzers = new FailureAnalyzers(context);
       //准备上下文环境;将environment保存到ioc中；而且applyInitializers()；
       //applyInitializers()：回调之前保存的所有的ApplicationContextInitializer的initialize方法
       //回调所有的SpringApplicationRunListener的contextPrepared()；
       //
      prepareContext(context, environment, listeners, applicationArguments,
            printedBanner);
       //prepareContext运行完成以后回调所有的SpringApplicationRunListener的contextLoaded（）；
       
       //s刷新容器；ioc容器初始化（如果是web应用还会创建嵌入式的Tomcat）；Spring注解版
       //扫描，创建，加载所有组件的地方；（配置类，组件，自动配置）
      refreshContext(context);
       //从ioc容器中获取所有的ApplicationRunner和CommandLineRunner进行回调
       //ApplicationRunner先回调，CommandLineRunner再回调
      afterRefresh(context, applicationArguments);
       //所有的SpringApplicationRunListener回调finished方法
      listeners.finished(context, null);
      stopWatch.stop();
      if (this.logStartupInfo) {
         new StartupInfoLogger(this.mainApplicationClass)
               .logStarted(getApplicationLog(), stopWatch);
      }
       //整个SpringBoot应用启动完成以后返回启动的ioc容器；
      return context;
   }
   catch (Throwable ex) {
      handleRunFailure(context, listeners, analyzers, ex);
      throw new IllegalStateException(ex);
   }
}
```

## 





我 看到这后面的源码的话等我熟悉了一些东西的时候再回来看吧