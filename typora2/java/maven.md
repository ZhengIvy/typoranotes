## 1. maven的作用

![image-20200805095524932](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200805095524932.png)

> 看来还有很多功能是我不了解的，比如说2,5,7,8 就没有接触过
>
> 编译不止这些，还可以把resources下的文件拷贝过去，然后resources的文件没了
> 打包只打包src/main下的，压缩成jar或war在target文件夹下，打包这里不操作什么，容易搞混的是compile这里，等会再细讲

![image-20200805100425947](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200805100425947.png)

![image-20200805100512734](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200805100512734.png)

![image-20200805100906968](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200805100906968.png)

## 2. maven约定的目录结构

> 算是大家都会遵循的规定，文件如何放置

![image-20200805104511781](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200805104511781.png)

![image-20200805105940184](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200805105940184.png)

## 3. 修改maven的仓库地址

他说首先是备份？？我的就没有备份诶，我觉得我的仓库地址有问题，因为我记得我当时导入包然后用不了，可能有些东西没有配好，后面再继续看下

![image-20200805115550091](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200805115550091.png)

![image-20200805120354635](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200805120354635.png)

## 总结：

![image-20200805120555656](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200805120555656.png)





## 4.仓库

### 	(1).仓库是什么？

存放东西的，存放maven使用的jar和我们项目使用的jar

- maven使用的插件(各种jar)

- 我项目使用的jar(第三方工具)

  

  

  ### (2).仓库的分类

  - 本地仓库：个人计算机上的文件夹，存放各种jar
  - 远程仓库： 互联网上的，使用网络才能使用的仓库
    1. 中央仓库：最权威的，所有开发人员都共享使用的一个集中仓库
    2. 中央仓库的镜像：中央仓库的备份，在各大洲，重要的城市都有镜像
    3. 私服，在公司内部，在局域网中使用的，不是对外使用的。



### 	(3).仓库的使用

​		maven仓库的使用不需要人为参与

​		开发人员需要使用mysql 驱动 --->maven 首先查看本地仓库 ---> 私服 --->镜像--->中央仓库

## 5. pom文件

​	`pom`即`Project Object Model` 项目对象模型，maven把一个项目的结构和内容抽象成一个模型，	在xml文件中进行声明，以方便进行构建和描述，`pom.xml`是maven的灵魂。所以，maven环境搭建	好之后，所有的学习和操作都是关于`pom.xml` 的

### 1> 坐标：唯一值，在互联网中唯一表示一个项目的（gav）

```html
<groupId>公司域名的倒写</groupId>
<artifactId>自定义项目名称</artifactId>
<version>项目版本号</version>
```

`www.mvnrepository.com`：搜索使用的中央仓库，使用`groupId`或者`artifactid`作为搜索条件

### 2> packaging

打包后压缩文件的扩展名，默认是`jar`，web 应用是`war`

packaging可以不写，默认是jar

### 3> 依赖

`dependencies` 和`dependency`

你的项目中要使用各种资源说明，比如我项目要使用`mysql`驱动,相当于java的 import

```html
<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependecies>
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>8.0.17</version>
</dependency>
    </dependecies>

```

> 这个在仓库中的文件夹如何显示的？
>
> `groupId`
>
> ​			`artifactId`
>
> ​								`version`



### 4> properties: 设置属性

![image-20200805172927949](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200805172927949.png)



### 5> build

maven在进行项目的构建时，配置信息，例如指定编译java代码使用的jdk版本



## 6. maven的生命周期，maven的命令，maven的插件

### 1>. maven的生命周期

是maven构建项目的过程，清理，编译，测试，报告，打包，安装，部署

### 2> maven 的命令

maven 独立使用，通过命令，完成maven的生命周期的执行。

maven可以使用命令，完成项目的清理，编译，测试等等

![image-20200805173259344](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200805173259344.png)

> 只要执行其中一个命令，就会把前面的命令执行一遍
>
> - `mvn compile执行后`
>
>   编译`main/java/`目录下的`java`为`class`文件，同时把`class`拷贝到`target/classes`目录下，还把`main/resources目录下的所有文件都拷贝到target/classes目录下`
>
> - `mvn test-compile执行后`
>
>   和上面是差不多一样的把，就是目录变成了`target/test-classes目录下`
>
> - `mvn test` 执行的时候会把前面的步骤再执行一遍所以就直接一步到位就可以了
>
> - `mvn package`  就是打包压缩成jar文件或war 在`target`文件夹中，名字的话你可以在依赖那里设置，但只打包`src/main/下的文件`，无test，class文件都无
>
> - `mvn install`  这个的话就是把工程依靠工程的坐标保存到本地仓库中，这样别的项目就可以从本地仓库中取来用，直接写坐标就好了，如果自己有写工具类的话算是可以直接导入进去。
>
> 注意：编译和运行是有区别的
>
> 编译是将java代码交给编译器进行语法检查，如果没有错误就生成.class文件
>
> 运行是将字节码文件交给java虚拟机执行，如果没有逻辑错误，就成功出现结果

### 3>. maven的插件

maven命令执行时，真正完成功能的是插件，插件就是一些jar文件，一些类

在idea中的`pom.xml`可以直接删掉，不影响，因为照样会有



#### a.单元测试

> 使用的是`junit`，`junit`是一个专门测试框架(工具)。
>
> `junit`测试的内容：测试的是类中的方法，每一个方法都是独立测试的。方法是测试的基本单位
>
> maven借助单元测试，批量的测试类中的大量方法是否符合预期

#### b. 使用步骤

1. 加入依赖在 `pom.xml`加入单元测试依赖

2. 在maven项目中 的`src/test/java`目录下，创建测试程序。

   推荐的创建类和方法的提示：

   1. 测试类的名称 是 `Test+你要测试的类名`
   2. 测试的方法名称是：`Test+方法名称`

   例如你要测试`HelloMaven`,

   创建测试类`TestHelloMaven`

   测试方法的定义规则

   	1. 方法时候public的，必须的
    	2. 方法没有返回值，必须的
    	3. 方法名称是自定义的，推荐 `Test+方法名称`
    	4. 在方法的上面加入`@Test`

### 4> build 的使用

![image-20200805205840176](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200805205840176.png)

编译插件配置

这里的话就是告诉编译的环境，指定一些信息

## 7. 在idea中设置maven

> 在idea中内置了maven，一般不使用内置的，因为修改设置不方便
>
> 使用自己安装的maven，需要覆盖idea中的默认设置，让idea知道maven位置的信息
>
> - 配置的入口1 :配置当前工程的设置`file---settings---Build,Execution,Deployment--Build Tools--Maven` 
>
>   `Maven home directory:maven的安装目录`
>
>   `User Settings File:就是maven安装conf/setting.xml配置文件`
>
>   `Local Repository:本机仓库的目录位置`
>
>   `--Build Tools--Maven--Runner`
>
>   ​	`VM Options:-DarchetypeCatalog=internal,maven的项目创建时会联网下载一个模板文件，比较大，使用这个后就不用下载，创建maven项目速度快`
>
>   ​	`JRE:你项目的jdk`
>
> - 配置的入口2  配置以后新建工程的设置 `file-other settings--Settings for New Project` 
>
>   其他就和上面的一样了

### 1> 使用模板创建项目	

1.  `maven-archetype-quickstart:普通的java项目`
2. `maven-arhchetype-webapp:web工程`

### 2> 导入modules

如何导入工程？

1. ![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200806090316755.png)

2. ![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200806090425242.png)

之后进行导入工程

3. ![image-20200806090515510](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200806090515510.png)

点击确定后

4. ![image-20200806090536088](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200806090536088.png)

进行如下选择后Finish

5. ![image-20200806090614150](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200806090614150.png)

选择性修改jdk版本。

6. 点击 apply 后就成功了

## 8. maven的依赖范围

> 使用scope表示，默认是compile
>
> - compile：所有阶段都要使用到这个jar包，如果范围是compile的话意味着打包的时候这个jar包也一起加过去了
> - test：只有测试阶段使用到jar包
> - provided：因为在打包，部署的时候jar包已经给提供了(tomcat)，所以可以使用到的阶段是 编译和测试阶段
>
> `scope:`表示依赖使用的范围，也就是在maven构建项目的那些阶段中起作用。
>
> maven构建项目的过程有清理，编译，测试，打包，安装，部署

```html
<dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.11</version>
      <scope>test</scope>
    </dependency>
   <!-- 像这里的junit的依赖范围就是test，只有在测试功能时才起作用，的确试了一下，在java代码里面编译不通过--> 
```

![image-20200806091925353](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200806091925353.png)

## 9. maven的常用操作

### 1> maven的属性设置

`<properties>:设置maven的常用属性`

### 2> maven的全局变量

自定义属性

1. 在`<properties>`通过自定义标签声明变量(标签名就是变量名)
2. 在`pom.xml`文件中的其他位置使用`${标签名}`使用变量的值

自定义全局变量一般是定义依赖的版本号，当你项目中要使用多个相同的版本号，先使用全局变量定义，再使用`${标签名}`

```html
<dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>${spring-version}</version>  
    <!-- 就是这样的全局变量，修改方便，可以进行统一管理-->
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>${spring-version}</version>
    </dependency>

 <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
<!--    编译代码使用的jdk版本-->
    <maven.compiler.source>1.8</maven.compiler.source>
<!--    运行程序时使用的jdk版本-->
    <maven.compiler.target>1.8</maven.compiler.target>
    <spring-version>5.2.5</spring-version>
  </properties>
```

### 3>  资源插件

![image-20200806101358561](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200806101358561.png)

![image-20200806102035120](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200806102035120.png)

![image-20200806105129156](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200806105129156.png)