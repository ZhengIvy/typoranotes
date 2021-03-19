## Servlet 的各个方法，生命周期



![image-20200525105610635](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200525105610635.png)

![image-20200525105621253](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200525105621253.png)

![image-20200525110024964](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200525110024964.png)



![image-20200525110212321](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200525110212321.png)

无语了。

意思是只有初始化一次，相当于单例模式，多线程运行的话会有线程的安全问题，所以一般不会共享变量

### 1. init

> 目前来看，跟构造器的有点像，为什么这么讲，因为你再用一次这个servlet ，打印出来的就只有service方法了，其他的都没有



### 2.destroy

> 清理善后工作

![image-20200525105848066](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200525105848066.png)

destory 方法在什么时候使用呢，在停止服务器的时候，没有跑服务器的时候就可以啦

![image-20200525110024964](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200525110024964.png)

### 3.ServletConfig(配置信息)



![image-20200525110801472](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200525110801472.png)

有没有发现init那里需要传入一个ServletConfig 的参数，不过其实这个是tomcat启动的时候就帮你传好了的，所以呢，你就没有必要再传了，还有一个ServletConfig需要进行专门获取config的把



![image-20200525111716263](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200525111716263.png)

![image-20200525112533880](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200525112533880.png)

![image-20200525112724329](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200525112724329.png)

#### servletconfig功能：

1. 获取servlet 的别名
2. 获取servlet的初始化参数
3. 获取ServletContext对象，代表servlet的上下文，代表当前web项目的信息

### 4.ServletContext 

#### 作用：

1. 是什么？代表一个web应用对应一个ServletContext
2. 功能：
   1. 获取web配置信息，获取web的初始化参数 parameter
   2. web项目路径
   3. 获取真实路径
   4. 可以作为最大的域对象共享数据 application

> 这个原本是从ServletConfig 那里来的

```java
ServletContext context = config.getServletContext();
String path = context.getContextPath();// /ServletdDemo 就是这个哈
```

![image-20200526145155042](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200526145155042.png)

这个是虚拟路径，指的是网络上的路径，就是 服务器/项目/资源 这样子一步一步获取的

所以你是可以获取真实路径的

![image-20200526145636140](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200526145636140.png)

```JAVA
String realPath = servletContext.getRealPath("/index.html");
System.out.println(realPath);
```

### 5.路径问题

**一般情况下都推荐使用绝对路径，原因？等会写给你看**

如果 浏览器的话就是tomcat 的根目录，如果是内部资源的话就是项目的根目录

![image-20200526151638654](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200526151638654.png)

总的来说，通过url传的都是从服务器根目录开始的，所以使用绝对路径的时候是需要把项目名加上

eg：

1. a标签
2. location 啥的
3. 重定向

那从项目根目录的有？

1. 转发

一般呢 绝对路径和相对路径的区别就是在那条

/ 这里，有了这个就是绝对路径了

#### 所以为什么不能用相对路径？？

> 因为跳转的时候，相对的是你该地的资源，那个同个文件下的资源，所以如果你跳转到别的地方的时候就相对的是他的路径下的了。



```java
Web

  	file

​		 	123.html
    		test.js

<a href="file/123.html"></a>
//引入js文件    
    request.getRequestDispatcher("/file/123.html").forward(request,response);
```

然后你发现了下面这种情况，看到没有，资源无法加载了

![image-20200527125923115](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200527125923115.png)

![image-20200527130600526](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200527130600526.png) 

所以你就可以用这个

但是呢，base标签还是不好，如果有服务器的话，你的base标签实际上不是？？ 那个整个端口都不是的把？

![image-20200530123129420](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200530123129420.png)

所以要动态获取咧，用这几个就可以动态获取哈，就ok了

```java
request.getScheme()
request.getServerName()
request.getServerPort()
request.getConextPath()
```

> 我感觉我这里没说好，导致我回顾起来还蒙蒙的
>
> 首先明白需求是什么，第一，遇到 了相对路径转发的缺陷
>
> 第二，如何有效地用base标签进行拼接，要静态写吗？ 很麻烦把？
>
> 所以可以动态地拼接，现在的方法就是把他放到base.jsp里面去，然后让众多jsp去include 就差不多了

### 6.BaseDao

![image-20200527143935664](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200527143935664.png)



![image-20200527144117235](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200527144117235.png)

![image-20200527144219079](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200527144219079.png)

![image-20200527144725234](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200527144725234.png)

![image-20200527144937588](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200527144937588.png)

这边整理一下，怎么说呢。

他呢，sql语句照样写，但是那些关于jdbc的操作都放在了，增删查改都整合在了basedao里面。 如上图

不过呢，我感觉还是不够完美，感觉每要一个，都写一个impl 就有一些麻烦。不过现在是一个比较完美的方案了，

不过那个反射的用到了我不懂的东西，我觉得我明天还是什么时候可以去改下我的dao层代码



### 7.jsp标签

`isErrorPage=true` : 表示一个错误页面

`ErrorPage`  : 指定页面发生错误去向的页面

如果你被指定的页面没有写 true 的话你是不可以get到Exception 的具体内容的

**动态包含和静态包含**

> 有什么区别吗，就是静态页面和动态页面的区别把，我们一般需要的是

![image-20200529103653867](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200529103653867.png)

#### 2. jsp foward

![image-20200529104753291](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200529104753291.png)

这样就完事了，不过呢，转页面的话是不改变url的

那这样有啥用呢？？？

1. `<jsp:forward>`动作指令之后的代码是不会执行的。
2. 使用动作指令跳转的页面，浏览器的地址还是跳转之前的页面地址





#### 3. 四大域对象

![image-20200529111215896](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200529111215896.png)



![image-20200529111056495](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200529111056495.png)

![image-20200529111730784](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200529111730784.png)

> 总的来说，四大域对象就是这些pageContext request session application

其他都还好，主要是pageContext 的意思是本页面的意思，数据只在本页面中共享，然后呢，也可以setAttribute 在本页面内，这个attribute只能在本页面里面共享，然后就大概是这样子了 

#### 4.确认的表单

![image-20200605231447593](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200605231447593.png)

我之前一直不会写，这次的话这个是

对应list 里面的  -> td -> tr 的第几个 对应的内容哈，confirm 这里的这个表格说实话我还没咋见过

### 8.  BeanUtils

原理还是利用了反射

populate 可以用到parametermap里面去![image-20200601003900083](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200601003900083.png)

BeanUtils 看的是getter setter实际上，但到底他是怎么拼接上的挺好奇，所以呢我挺像看看源码的

至于我之前提到的为什么好像又有field 那你怎么搞，因为实际上还是用了BeanUtils 不算是自己写的把。

### 9.EL

#### a.Http协议

![image-20200601115852782](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200601115852782.png)

这个我就不是很清楚了只接触过param 和paramValues

后面一个数组哈，所以就进行遍历就好了



然后el拼base标签的时候你老是request request 就麻烦了，你可以直接把request 的值set到attribute 里面变得简短一点

#### b. out set

#### ![image-20200604000019575](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200604000019575.png)

```
这个呢，这个out我没怎么用到诶，但是可以了解。default 当没有值的时候，后面的转义看识别不识别escapeXml
```

![image-20200604003035545](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200604003035545.png)

![image-20200604003404449](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200604003404449.png)

```
感觉蛮好用，可以用到session 啊 request 里面了 因为之前在session 好像设置不了
这个修改的目前只是在bean中看到，target指的bean类，property 就是field

明白什么意思了
var scope value 一起的 代替 request.setAttribute("key") 这个样子哈
但是呢 property target 和 value 就是在bean 里面的
```

#### c. remove

```java
<c:remove var="" scope=""> 就这样 蛮简单的
```

#### d.if

![image-20200604203223979](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200604203223979.png)

1. 可以把判断后的结果放到scope里面的var 中，可以以后取出来用





#### e.switch case

因为你的if里面是没有else 的，所以的话就只能一个个写，这里引进了一个choose when otherwise

![image-20200604203925695](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200604203925695.png)

#### f. forEach

![image-20200604205422956](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200604205422956.png)

![image-20200604205620859](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200604205620859.png)

### 10. cookie 登录

cookie 登录实际上我的难点就在于发送了cookie 之后怎么取出来

但实际上很简单哈

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200607195308191.png" alt="image-20200607195308191" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200715102932325.png" alt="image-20200715102932325" style="zoom:80%;" />

用jstl  el？ 就可以咯

![image-20200607201355459](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200607201355459.png)

为什么会失效，失效的原因是session 实际上是用jessionId 去判断个体的，想起来了一些东西。   

![image-20200607205159170](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200607205159170.png)

实际上就是一个用户一个jessionid 的因为被禁用的关系 ，所以才会不断获得新的jessionid 如果被禁用的话 你可以直接在url 上进行url 重写

![image-20200607210735302](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200607210735302.png)

如果没被禁用是不会带上jessionid 的

### 11. get post 编码问题

##### 1. 地址栏编码

直接输中文的话是根据浏览器不同的判断而定的 有些用的是utf-8 有的用的是gbk

> IE：使用GB2312；
>
>   FireFox：使用GB2312；
>
>   Chrome：使用UTF-8；

#### 2. post 编码

**注意一下表单里面的提交post 是可以加参数的，不可以加的是get，因为会覆盖掉**

因为post的参数是在请求体中

默认是`ISO-8859-1` 来解码，所以你有中文的话就是`request.setCharacterEncoding(“utf-8”);`

##### b.使用post编码的几种方式

###### application/x-www-form-urlencoded

```

	这应该是最常见的 POST 提交数据的方式了。浏览器的原生 <form> 表单，如果不设置 enctype 属性，那么最终就会以 application/x-www-form-urlencoded 方	式提交数据。请求类似于下面这样（无关的请求头在本文中都省略掉了）：
	BASHPOST http://www.example.com HTTP/1.1
	Content-Type: application/x-www-form-urlencoded;charset=utf-8

	title=test&sub%5B%5D=1&sub%5B%5D=2&sub%5B%5D=3
	首先，Content-Type 被指定为 application/x-www-form-urlencoded；其次，提交的数据按照 key1=val1&key2=val2 的方式进行编码，key 和 val 都进行了 	 URL 转码。大部分服务端语言都对这种方式有很好的支持。例如 PHP 中，$_POST['title'] 可以获取到 title 的值，$_POST['sub'] 可以得到 sub 数组。
	很多时候，我们用 Ajax 提交数据时，也是使用这种方式。例如 JQuery 和 QWrap 的 Ajax，Content-Type 默认值都是「application/x-www-form-			urlencoded;charset=utf-8」。
```

###### multipart/form-data

```

这又是一个常见的 POST 数据提交的方式。我们使用表单上传文件时，必须让 <form> 表单的 enctype 等于 multipart/form-data。直接来看一个请求示例：
BASHPOST http://www.example.com HTTP/1.1
Content-Type:multipart/form-data; boundary=----WebKitFormBoundaryrGKCBY7qhFd3TrwA

------WebKitFormBoundaryrGKCBY7qhFd3TrwA
Content-Disposition: form-data; name="text"

title
------WebKitFormBoundaryrGKCBY7qhFd3TrwA
Content-Disposition: form-data; name="file"; filename="chrome.png"
Content-Type: image/png

PNG ... content of chrome.png ...
------WebKitFormBoundaryrGKCBY7qhFd3TrwA--
这个例子稍微复杂点。首先生成了一个 boundary 用于分割不同的字段，为了避免与正文内容重复，boundary 很长很复杂。然后 Content-Type 里指明了数据是以 multipart/form-data 来编码，本次请求的 boundary 是什么内容。消息主体里按照字段个数又分为多个结构类似的部分，每部分都是以 --boundary 开始，紧接着是内容描述信息，然后是回车，最后是字段具体内容（文本或二进制）。如果传输的是文件，还要包含文件名和文件类型信息。消息主体最后以 --boundary-- 标示结束。关于 multipart/form-data 的详细定义，请前往 rfc1867 查看。
这种方式一般用来上传文件，各大服务端语言对它也有着良好的支持。
上面提到的这两种 POST 数据的方式，都是浏览器原生支持的，而且现阶段标准中原生 <form> 表单也只支持这两种方式（通过 <form> 元素的 enctype 属性指定，默认为 application/x-www-form-urlencoded。其实 enctype 还支持 text/plain，不过用得非常少）。
随着越来越多的 Web 站点，尤其是 WebApp，全部使用 Ajax 进行数据交互之后，我们完全可以定义新的数据提交方式，给开发带来更多便利。
```

###### **application/json**

```
application/json 这个 Content-Type 作为响应头大家肯定不陌生。实际上，现在越来越多的人把它作为请求头，用来告诉服务端消息主体是序列化后的 JSON 字符串。由于 JSON 规范的流行，除了低版本 IE 之外的各大浏览器都原生支持 JSON.stringify，服务端语言也都有处理 JSON 的函数，使用 JSON 不会遇上什么麻烦。
JSON 格式支持比键值对复杂得多的结构化数据，这一点也很有用。记得我几年前做一个项目时，需要提交的数据层次非常深，我就是把数据 JSON 序列化之后来提交的。不过当时我是把 JSON 字符串作为 val，仍然放在键值对里，以 x-www-form-urlencoded 方式提交。
Google 的 AngularJS 中的 Ajax 功能，默认就是提交 JSON 字符串。例如下面这段代码：
JSvar data = {'title':'test', 'sub' : [1,2,3]};
$http.post(url, data).success(function(result) {
    ...
});
最终发送的请求是：
BASHPOST http://www.example.com HTTP/1.1 
Content-Type: application/json;charset=utf-8

{"title":"test","sub":[1,2,3]}
这种方案，可以方便的提交复杂的结构化数据，特别适合 RESTful 的接口。各大抓包工具如 Chrome 自带的开发者工具、Firebug、Fiddler，都会以树形结构展示 JSON 数据，非常友好。但也有些服务端语言还没有支持这种方式，例如 php 就无法通过 $_POST 对象从上面的请求中获得内容。这时候，需要自己动手处理下：在请求头中 Content-Type 为 application/json 时，从 php://input 里获得原始输入流，再 json_decode 成对象。一些 php 框架已经开始这么做了。
当然 AngularJS 也可以配置为使用 x-www-form-urlencoded 方式提交数据。如有需要，可以参考这篇文章。
```

###### **text/xml**

ps: 这个并不知道是什么。。

```html
我的博客之前提到过 XML-RPC（XML Remote Procedure Call）。它是一种使用 HTTP 作为传输协议，XML 作为编码方式的远程调用规范。典型的 XML-RPC 请求是这样的：
HTMLPOST http://www.example.com HTTP/1.1 
Content-Type: text/xml

<?xml version="1.0"?>
<methodCall>
    <methodName>examples.getStateName</methodName>
    <params>
        <param>
            <value><i4>41</i4></value>
        </param>
    </params>
</methodCall>
XML-RPC 协议简单、功能够用，各种语言的实现都有。它的使用也很广泛，如 WordPress 的 XML-RPC Api，搜索引擎的 ping 服务等等。JavaScript 中，也有现成的库支持以这种方式进行数据交互，能很好的支持已有的 XML-RPC 服务。不过，我个人觉得 XML 结构还是过于臃肿，一般场景用 JSON 会更灵活方便。
```





#### 3.url

通过页面传输数据给服务器时，如果包含了一些特殊字符是无法发送的。这时就需要先把要发送的数据转换成URL编码格式，再发送给服务器。
其实需要我们自己动手给数据转换成URL编码的只有GET超链接，因为表单发送数据会默认使用URL编码，也就是说，不用我们自己来编码。
例如：“传智”这两个字通过URL编码后得到的是：“%E4%BC%A0%E6%99%BA”。URL编码是先需要把“传智”转换成字节，例如我们现在使用UTF-8把“传智”转换成字符，得到的结果是：“[-28,-68, -96, -26, -103, -70]”，然后再把所有负数加上256，得到[228, 188, 160,
 230, 153, 186]，再把每个int值转换成16进制，得到[E4, BC, A0, E6, 99, BA]，最后再每个16进制的整数前面加上“%”。
通过URL编码，把“传智”转换成了“%E4%BC%A0%E6%99%BA”，然后发送给服务器！服务器会自动识别出数据是使用URL编码过的，然后会自动把数据转换回来。

当然，在页面中我们不需要自己去通过上面的过程把“传智”转换成“%E4%BC%A0%E6%99%BA”，而是使用Javascript来完成即可。当后面我们学习了JSP后，就不用再使用Javascript了。

  <script type="text/javascript">  	function _go() {  		location = "/day05_2/AServlet?name=" + encodeURIComponent("传智+播客");  	}  </script><a href="javascript:_go();">链接</a>

因为URL默认只支持ISO-8859-1，这说明在URL中出现中文和一些特殊字符可能无法发送到服务器。
所以我们需要对包含中文或特殊字符的URL进行URL编码。
服务器会自动识别数据是否使用了URL编码，如果使用了服务器会自动把数据解码，无需我们自己动手解码。

> 然后我观察了一下，谷歌和百度搜索中文时url上面显示的是不同的
>
> 谷歌是![image-20200715121000652](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200715121000652.png)
>
> 直接显示中文
>
> 百度是？ or 还是ie 的问题？
>
> ![image-20200715121036761](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200715121036761.png)
>
> 已经是编码的状态了



#### 4. 响应

> 今天试验了下发现呢，get中文过来是可以的，我觉得是我当时有设置个utf-8，post过来不行，因为是请求体，请求体是经过服务器的啦，感觉呢，还是有一点懵逼的哈

通常用到的就是 

响应：服务器发送给客户端数据！响应是由response对象来完成，如果响应的数据不是字符数据，那么就无需去考虑编码问题。当然，如果响应的数据是字符数据，那么就一定要考虑编码的问题了。
`response.getWriter().print(“传智”);`
上面代码因为没有设置repsonse.getWriter()字符流的编码，所以服务器使用默认的编码（`ISO-8859-1`）来处理，因为ISO-8859-1不支持中文，所以一定会出现编码的。
所以在使用response.getWriter()发送数据之前，一定要设置`response.getWriter()`的编码，这需要使用`response.setCharacterEncoding()`方法设置服务器的编码方式，
`response.setCharacterEncoding(“utf-8”);`
`response.getWriter().print(“传智”);`
上面代码因为在使用response.getWriter()输出之前已经设置了编码，所以输出的数据为utf-8编码。但是，因为没有告诉浏览器使用什么编码来读取响应数据，所以很可能浏览器会出现错误的解读，那么还是会出现乱码的。
当然，通常浏览器都支持来设置当前页面的编码，如果用户在看到编码时，去设置浏览器的编码，如果设置的正确那么乱码就会消失。但是我们不能让用户总去自己设置编码，而且应该直接通知浏览器，服务器发送过来的数据是什么编码，这样浏览器就直接使用服务器告诉他的编码来解读！这需要使用content-type响应头。
`response.setContentType(“text/html;charset=utf-8”);`
`response.getWriter().print(“传智”);`
　　上面代码使用setContentType()方法设置了响应头content-type编码为utf-8，这不只是在响应中添加了响应头，还等于调用了一次`response.setCharacterEncoding(“utf-8”)`，也就是说，通过我们只需要调用一次`response.setContentType(“text/html;charset=utf-8”)`即可，而无需再去调用`response.setCharacterEncoding(“utf-8”)了。`

在静态页面中，使用<meta>来设置content-type响应头，例如：
`<meta http-equiv="content-type" content="text/html;charset=UTF-8">`

差不多就是这样了吧，感觉了解了蛮多的，而且纠正了之前理解上的一个错误哈





### 12.session

> 重新看一遍之后还是觉得懵逼把？
>
> 1. session钝化的用处？ 意思是需要序列化才能钝化吗？
> 2. 不是说session不随浏览器的关闭而消失吗？ 但是session又依赖于cookie，cookie默认情况下关闭后就消失了？ 到底是怎么回事呢？（其实你看后面发现一点都不矛盾啦，的确是依赖关系，只不过你重新打开之后就不是同一个jsessionid了，那你的数据也就不同了，相当于就没了，解决方法就是把cookie的时间给设置长，那我觉得我需要把登录界面给改了啊，想改成正常淘宝那样子，不需要每次一按就登录，有session的话可以直接登录那种的。而且呢，session钝化的用处是关于在服务器重启前后的状态，那跟淘宝有什么关系呢，那之间是差不多让服务器断开了？？？？？？？？？？看看吧，晚上的任务就是修修搞搞session的事情）
> 3. 但是服务器关闭和重新开启的话是不会变的，jsessionid哈

**为何关闭浏览器后，再次访问会觉得session失效了呢，这里的失效意思是session的数据丢失了？**

其实这里session数据并没有丢失，只是关闭浏览器后，因为默认的cookie生命周期为浏览器的内存，即关掉浏览器之后cookie就失效了，此时JSESSIONID也就没有了。再次访问后，服务器又生成一个新的JSESSIONID，此时request.getSession()通过JSESSIONID获取到的session就不是之前的session了。

解决：设置客户端 JSESSIONID  cookie的时间  

```java
        Cookie[] cookies = request.getCookies();
        Cookie cookie = CookieUtils.findCookieByName(cookies, "JSESSIONID");
        cookie.setMaxAge(60*60);
        response.addCookie(cookie);
```
1. 活化和钝化

   - 活化：服务器再启动时，把之前序列化好的文件加载进来。就会再次加载之前保存的session

     SESSION.ser 包含了session域中的所有内容。

   - 钝化：服务器关闭之后，会将session保存硬盘中。

   这个的原因是因为session有保存的时间哈

2. 关于session的序列化问题

   之前一直只知道session 关闭浏览器之后不会失效，但具体能不能再用我是不知道的所以我在这里告诉你是不ok 的，因为存到ser 里面 的东西必须经过序列化 否则无法保存下去

   比如![image-20200610000348272](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200610000348272.png)

   这个从user里面取东西的时候就刚好需要啊，但是你这个user没序列化呢，这时候就需要你的user去实现序列化的接口就ok了，没序列化是没结果 的，保存不了数据。

   ![image-20200715221138467](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200715221138467.png)
   
   ![image-20200715222051709](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200715222051709.png)
   
   详情请查看[序列化博客](https://blog.csdn.net/eson_15/article/details/51423300 "序列化")

>  最后总结一下：     
>
>    1. 容关闭后session并没有消失，而是被持久化到了硬盘里；   
>
>          2. 如果项目中的POJO实现了Serializable接口，那么会跟着session一起被持久化到硬盘，在反序列化的时候会成功还原；
>         3.  要想服务器重启后，还是原来的session，还继续紧接着原来的页面操作的话，就需要实例化项目中的POJO。
>         

#### ![image-20200610204928336](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200610204928336.png)

#### 2.关闭浏览器保留session

![image-20200610205532017](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200610205532017.png)

我上面搞的是在关闭服务器后如何把session存到硬盘中，这里倒是不一样 了哈，还好我点开了，不然还以为是一样的东西呢。

所以是啥呢，因为你想想，session是cookie带来的实际上，默认情况下，你浏览器关掉，cookie就没了，所以就要把cookie中带有JESSIONID的时间延长

大概是这样子，不过有什么用呢？ 我目前好像还没有考虑到。和之前的项目比起来，感觉还是蛮有用的，我等会想想哈，因为我的确蛮多功能没有考虑到的害







诶，我觉得我需要在后面的时候加一个这个功能，因为真的需要考虑到

补充：欲哭无泪，因为eclipse 和idea 是不一样的，所以你要去context.xml 文件中搞一个东西出来这样才能成功哈。成功啦哈哈，关闭浏览器保持session 也成功了，另外说一点，关于序列化的问题，String这种是已经implements 序列化了，所以只有自己的pojo需要implements 这样子



### 13.表单重复提交

![image-20200615191126488](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200615191126488.png)

![image-20200716154203603](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200716154203603.png)

![image-20200716160139006](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200716160139006.png)

> 感觉终于明白了到底啥是表单重复提交了。之前看黑马的时候只有一个模糊的概念，现在明白了，对于我那种情况就是返回到页面的时候重复注册，一个角色重复注册，那你的数据库 一下就爆了哈，那你咋搞，就要防止啊。而且如果你是转发的话，你的url地址还不变，所以的话你转到另外一个页面后刷新，那照样是一样的结果，说实话，学到了蛮多东西的
>
> **2020.07.16**补充：
>
> 1. 为什么说get会这样呢，你看上面那张图，还是以表单的url转发的，所以你直接刷新就相当于重复提交表单了 **所以这是get+转发的结果**
>
> 2. 要了解一下post后的url到底是什么样的，如图就是UserServlet ，直接以Servlet为url，而这个就是 **post+转发**的结果，如果是重定向的话就是到
>
> **success.jsp**里面去 ，所以转发影响的是get的表单，post也有，只要返回去再刷新就可以了
>
> 3. 然后视频里面没说对，最后面，重定向可以解决get表单直接重复刷新的问题，但问题是如果你get表单再返回一次的话，你照样是可以重复提交的，所以基本上没什么区别哈



现象：

1. 不断刷新重复提交表单(表单为get)
2. 网慢，用户反复点
3. 用户成功后，点击后退，再次提交

危害

 	1. 数据库多次保存相同的数据
 	2. 安全问题(如果遇到支付宝啊，啥的，别人给你设置个东西，就不断扣钱啦)
 	3. 服务器性能(超多个表单提交诶，你服务器跑得不好啊)

以上以上会发生这些东西的原因是：

HTTP 无状态协议（无法识别你的请求是否是同一个）

因为，每次HTTP请求的时候都会过来创建一个TCP（一个通道罢了） HTTP1.0 的时候就会每次请求完连接通道关掉，那当你要用很多的时候服务器就会爆掉？ HTTTP1.1 现在是，有些改善把，会给你停留一会。但是为啥呢？？？ 这个有点自相矛盾的感觉了

简单的解决方法：

	1. 如果是第一种和第三种现象的话就可以在页面防止重复？ 好像不是很可以，所以的话就可以在前端表单上进行操控一下

![image-20200616192431567](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200616192431567.png)

是按钮disabled ，不能再点

针对第一种的话，用重定向就ok可以解决了，但是第三种没法子吼

----------------------------------------------------------------------------------重新回顾笔记一遍之后有了新的问题-----------------------------------------------------------------------------------

1. 为什么post不会重复提交？
2. 这里的转发和重定向？？

-------------------------------------------------------------------------------------解决了，看上面补充-----------------------------------------------------------------------------------------------------



#### token

> 用于解决第三种的问题，返回后还可以提交，其实也算是所有把，基本上没有能解决到这种问题的

![image-20200716170732746](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200716170732746.png)

![image-20200716171031664](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200716171031664.png)

有点奇怪这里

的确我猜的没错，他们的确是一样的，所以这里就是先给你讲一种可能，然后发现实施不了

![image-20200716171823159](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200716171823159.png)

但是有一种，你可以把session里面的uuid 给变了就行

![image-20200716171949695](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200716171949695.png)

你也可以直接把服务器的令牌移除掉 

![image-20200716172719555](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200716172719555.png)

![image-20200716173648830](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200716173648830.png)

基本上的话就是这个原理了啦

总结来说，token是可以解决以上的三种问题的

### 14.验证码

![image-20200717093358196](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200717093358196.png)

验证码的原理其实不难，实际上就是和token机制一样的，你在session中存入正确的值，然后后台进行比对，然后清空这样子

![image-20200717094540299](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200717094540299.png)

![image-20200717110558006](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200717110558006.png)

可以 对一些参数进行设置，比如说字体什么的

![image-20200717123142115](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200717123142115.png)

这个是要点击验证码就可以刷新的，但是有个问题哈，好像有些浏览器里点了不行，不知道为什么，主要是一些浏览器会默认为同一个请求，所以的话就要改变一些东西![image-20200717124330437](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200717124330437.png)

![image-20200717124527374](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200717124527374.png)

![image-20200717124916407](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200717124916407.png)

校验的话都要到后端来验，因为万一前端禁用js的话，那你的验证码填不填都无所谓了哈

>
>
>ps: 改的时候遇到了点麻烦，关于判断密码错误啊，什么东西的，不用一个个写true 啥的，直接返回一个信息，统一放在一个地方就好了，不然超麻烦的

重复提交优于验证码验证哈

总的来说也没有什么稀奇的，大概就是这样吧



### 15. Filter

> 这个我很清楚地明白我只学了一个大概，只会用一种而已，学的不全
>
> 这次我重看的收获是：filter像一个地铁的检票机，不仅拦进还拦出！ 是的，我一直都是只拦过进从来都没有拦过出的哈

![image-20200717153358599](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200717153358599.png)



![image-20200717154141650](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200717154141650.png)

![image-20200717154213844](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200717154213844.png)

> 一个奇怪的点在于我之前接触到的filter中的request 和response 有转的这一步

![image-20200717163239939](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200717163239939.png)

虽然是不知道为什么要这样子，看起来不用转？不行，还是得转，不然那个 `servletRequest`里面没有`getSession`这种东西哈 

![image-20200717164249024](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200717164249024.png)

![image-20200717164300046](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200717164300046.png)

> 这里是一个重要的点，当你doFilter之后你后面再加一句话就是“我是请求放行之后“，你发现他是在被拦截的页面之后输出的，也就是如上图请求拦截一次，响应拦截一次

![image-20200717164932220](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200717164932220.png)

![image-20200717164942275](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200717164942275.png)

> 这里比较有趣 的点是，你的response是相当于追加的，而不是替代关系，就你跟在`response.sendRedirect`后面加一句`System.out.println`一样的

#### filter的生命周期

![image-20200718115708618](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200718115708618.png)

> 与servlet的生命周期不同，servlet是在用到的时候才开始init，但是这个是在服务器启动的时候就开始了，当然，还是没能超过构造器哈

![image-20200718120715333](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200718120715333.png)

![image-20200718122242313](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200718122242313.png)

总而言之，就只能这三种拦，等会再来补充下哈，下午试下ok不ok

> 什么意思呢，就是你拦截资源时有三种拦法，第一种是以精确的拦，
>
> 第二种可以说是拦所有，
>
> 第三种是以后缀形式拦，only `*.jsp`这样子
>
> 一般从`/` 开始的都是路径哈，eme这种的话是类型，把所以不用加
>
> 但是呢，我们就不用用web.xml啦，直接`@WebFilter`就好了

**但是呢？如果你想拦某个文件夹下的jsp怎么办？ 你不能用/page/*.jsp 是不行的，因为不符合上面三种的任意一种哈**

所以你的解决方法是在filter里面自己筛选

```java
@WebFilter("/pics/*")
public class HelloFilter implements Filter {
    public void destroy() {
    }

    public void doFilter(ServletRequest req, ServletResponse resp, FilterChain chain) throws ServletException, IOException {
        HttpServletRequest request = (HttpServletRequest) req;
        HttpServletResponse response = (HttpServletResponse) resp;
        
        String uri = request.getRequestURI();
        StringBuffer url = request.getRequestURL();
        
        System.out.println("uri是" + uri);
        System.out.println("url是" + url);
        System.out.println("我在Filter中啦");
        
        if (uri.endsWith("jsp")) {

        } else {
            chain.doFilter(req, resp);
        }
    }

    public void init(FilterConfig config) throws ServletException {

    }
}


// uri是/mymymy/pics/my.html
//url是http://localhost:8080/mymymy/pics/my.html
//我在Filter中啦

```

#### Filter 放行之前写中文乱码的原因

> 诶，我还没尝试过在`doFilter`前来`response.getWriter`，然后发现乱码了
>
> 注意：如果是在`doFilter`后面写的话就不会这样子哈

![image-20200718155009252](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200718155009252.png)

![image-20200718155536426](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200718155536426.png)

你好可以显示诶

![image-20200718191457236](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200718191457236.png)

这个就是问题哈

> 说下如果是servlet中搞的话你已经sendRedirect后再来，response.getWriter.println 是不显示的哈，那为什么因为filter有呢，因为是有响应之后也有经过这哈

![image-20200718200859143](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200718200859143.png)

> 什么意思呢？ 首先大家的response都是一样的，意味着你的编码情况也是一样的，因此呢，如果你开始编码设置好了那基本上后面在设置 那没有用了，那这里的关键在于doFilter 他的意思就是转到jsp页面嘛，jsp页面是已经设置好编码的情况了，所以你在他之前就response那么意味着你的编码情况没有设置，因此呢你的响应状态也是乱码的，那基本上就是这样了

#### FilterChain

> 当有多个filter拦截一个的时候，你的顺序又是怎么样的？

![image-20200719110732965](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200719110732965.png)

![image-20200719110810905](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200719110810905.png)

#### Dispatcher

> 发现一个问题哈，我们一般被filter拦是因为我们在前端就要求去了，如果我们这时候通过Servlet去要求到目的的页面呢？会不会出现被拦截的问题？

事实是看情况，filter拦截怎么看？看到实际上是你的url呀，如果你的url想到目的的页面那filter就会出动

所以有个点，如果我url不变转到 目的页面呢？ 也就是用转发进行，对吧，转发又不用改变url，因此`request.sendRedirect`是不行的

现在有个解决方法是用`dispatcher`进行的

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200719121023569.png)

有这四种类型哈

1. 

> FORWARD: 拦转发的，所以你上面的 `requestDispatcher`就不起作用了

所以如果你又想要request被ban又想要转发被ban 那两个都写上去ok

2. 

```java
@WebFilter(value = "/test.jsp",dispatcherTypes={DispatcherType.FORWARD,DispatcherType.REQUEST} )
```

3. 

这里的include是动态包含

动态包含和静态包含的区别什么

>![image-20200719163344457](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200719163344457.png)
>
>上面静态，下面动态
>
>静态就相当于复制粘贴罢了
>
>动态呢还要加载，所以去别又是啥？先保留一下。。

4. ERROR

这个error不是你想的那种errorpage转过去，因为errorpage实际上是转发的，所以他可被转发类型拦截



> 有趣的东西来了，error的作用就体现再这里哈，就是我们一般遇到404 500 时候每个浏览器返回的页面就不同嘛，因为是自己设置 的，所以呢这里的error就是设置全局错误页面，如果发生了404 500 错误返回自己设置的页面啦

![image-20200719165324506](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200719165324506.png)

### 16. ajax请求解决缓存问题？

但他那种形式比较古老，在我这里好像不是很常见诶，所以呢，缓存问题跟那个验证码点了不能刷新是一样的，但是我这里没有地方给你输入url，后面看下有没有改进的方法把

### 17. json

![image-20200720103835570](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200720103835570.png)

> 总的来说就是和普通的js对象区别就是属性有加双引号，这是必须要求的。

![image-20200720105045473](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200720105045473.png)

> 这里的话是教你如何在object和string中转换，之前一直用jar包的，所以还没有考虑过。
>
> 还有的是如何从obj里面取出值来

![image-20200720112926926](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200720112926926.png)

？？？？

> 这里讲的是如何在java中 json格式和原来格式的互相转换？ 这是为什么？
>
> 然后呢，不过有一点说下，我的json那里明明传来的是json，但拿到的却是object的格式了
>
> 我是真tmd不明白哈
>
> 不过感觉跟他设置的格式有关？？ 我看到后面的时候再继续看下

**补充：是的哈，是因为设置的type的问题，这里的type指的是响应转换成的数据 ，然后默认设置为text形式，但是我的设置是json的形式，因此我就自动转为json需要的了，而text只是个string罢了**

![image-20200720153459394](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200720153459394.png)

> 还感受到了一些区别啊哈，就是你观察那些谷歌啊，啥的浏览器里面，那些,method 都显示得清清楚楚的，然后呢，所以我可以改进一下，不用每次都把method啥的藏到请求体里面，不需要啊哈

![image-20200720154553215](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200720154553215.png)

> get post的缺点在于传的参数很固定，就四个，如果要想完成更多的东西需要求助于ajax，他是属于比较底层的，getJson代表人性化了，你不用每次都写type:Json
>
> 

怎么说呢， ajax要习惯和session结合，不要动不动就去数据库里面找东西，比如说翻页的时候记录的总数是不变的把，你从哪里取呢？ 我从session中取哈

### 18. 监听器

![image-20200721163051278](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200721163051278.png)

> ServletRequest 请求对象
>
> ServletContext 代表当前整个web应用，一个就ServletContext
>
> HttpSession session 对象

一共有八个监听器

三大类：

 1. 生命周期监听器，监听三个对象的生命周期（创建到销毁）

    - `SevletRequestListener`：requestDestroyed,requestInitialized

    > 实际上是请求开始到响应结束就是一个生命周期
    >
    > <img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200721170435198.png" alt="image-20200721170435198" style="zoom:67%;" />
    >
    > 也没啥，基本上就是这样了

    - `ServletContextListener`：contextInitialized，contextDestroyed 

    > 跟上面的其实也差不多的，也是生命周期的东西，web应用开启就初始化，关闭就没了

    - `HttpSessionListener`:新会话进来的时候创建对象（第一次拿到session的时候把就这样子），session失效销毁（过期，invalidate）

 2. 属性监听器。监听三个对象。监听域对象中属性的增（setAttribute()）删(removeAttribute())改(setAttribute())

    - `SevletRequestAttributeListener`:attributeAdded,attributeRemoved,attributeReplaced

    String getName()

    Object getValue

    > 就是监听你request里面属性的值增加，替换 or 移除,后面基本上就是一样的了

    - `ServletContextAttributeListener`
    - `HttpSessionAttributeListener`

 3. session 固有的（**特殊，不需要配置**）

    - `HttpSessionActivationListener` 监听session活化钝化（服务器的开启和关闭）
    
  >  监听session对象的钝化和活化，注意是对象哦，所以这个可以让你被监听的对象implements 接口的

~~~java

  public class Student implements Serializable, HttpSessionActivationListener {
     private String name;
  
      public Student(String name) {
          this.name = name;
      }
  
      public Student() {
      }
  
      @Override
      public String toString() {
          return "Student{" +
                  "name='" + name + '\'' +
                  '}';
      }
  
      @Override
      public void sessionWillPassivate(HttpSessionEvent se) {
          System.out.println("我和session要一起钝化啦");
  
      }
  
      @Override
      public void sessionDidActivate(HttpSessionEvent se) {
          System.out.println("我和session要一起活化了");
          HttpSession session = se.getSession();
          Object attribute = session.getAttribute("stu");
          System.out.println(attribute);
      }
  }
  
  ```
~~~


​      
​    
    - ``HttpSessionBindingListener` 监听 一个对象是否绑定在session中（保存到session中）
    
      > 绑定：保存在session中就叫绑定 `valueBound`
      >
      > 解绑：session中移除就叫解绑  `valueUnBound`
    
    本质上就是session是否有被利用，还有影响session使用的因素

(然后你发现这恰好是四大域对象中的其中三个，另外一个是`pageContext`)，说明监听器是不监听page的

> 以上都是接口

### 19. i18n

internationlization 从i到n有十八个字母，所以简化成这样子

目的是让网站识别多种语言

主要是利用java的三个类

1. ResourceBundle:资源绑定，管理资源文件（要动态获取的内容）

   >管理所有国际化资源文件
   >
   >
   >
   >![image-20200722210152547](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200722210152547.png)

   ```java
   public void test2(){
           //写资源文件ResourceBundle 来管理的。可以根据不同国家获取不同的值
           //.properties 文件名：基础名_语言_国家.properties
           //如果是中国 i18n_zh_CN.properties
           //如果是美国 i18n_en_US.properties
           //将要显示的信息放在这些文件中，然后通过文件动态获取。这些文件放在类路径下（src）
           Locale china = Locale.CHINA;
           ResourceBundle bundle = ResourceBundle.getBundle("i18n", china);
           String string = bundle.getString("login");
           System.out.println(string);
       }
   ```

   > 思路呢是利用ResourceBundle去管理所有的国际化资源文件，首先得通过locale去获取才行，然后对应的找你要的bundle，再对bundle进行取值进行输出就可以了

   然后说下国际版java，就是像你去那些页面一样显示中因为跟切换的，首先有个浏览器默认，但我觉得直接在那里写java代码感觉也不是很好的样子，大概这样子把，留了点模糊的印象

2. Locale：代表区域（中国）

```java
 @Test
    public void test(){
        //获取默认区域信息zh_CN en_US
        // 一个Locale由 语言_国家
        //Locale本身储存一些区域
        Locale locale = Locale.getDefault();
        System.out.println(locale);
    }
//en_US
```

```java
public void test(){
        //获取默认区域信息zh_CN en_US
        // 一个Locale由 语言_国家
        //Locale本身储存一些区域
        Locale us = Locale.US;
        Locale cn = Locale.CHINA;
        System.out.println(us);

        DateFormat dateInstance = DateFormat.getDateInstance(DateFormat.FULL, cn);
        String format = dateInstance.format(new Date());
        System.out.println(format);
    }

//2020年7月22日星期三
//如果是us的话输出结果是 Wednesday, July 22, 2020
```



1. XXXFormat

   1. DateFormat：日期格式化

      ```java
      public void test(){
              //获取默认区域信息zh_CN en_US
              // 一个Locale由 语言_国家
              //Locale本身储存一些区域
              Locale us = Locale.US;
              Locale cn = Locale.CHINA;
              System.out.println(us);
      
      
              DateFormat dateInstance1 = DateFormat.getDateInstance(DateFormat.FULL, cn);
              DateFormat dateInstance2 = DateFormat.getDateInstance(DateFormat.LONG, cn);
      
              DateFormat dateInstance3 = DateFormat.getDateInstance(DateFormat.MEDIUM, cn);
              DateFormat dateInstance4 = DateFormat.getDateInstance(DateFormat.SHORT, cn);
              DateFormat dateInstance5 = DateFormat.getDateInstance(DateFormat.DEFAULT, cn);
              String format1 = dateInstance1.format(new Date());
              String format2 = dateInstance2.format(new Date());
      
              String format3 = dateInstance3.format(new Date());
      
              String format4 = dateInstance4.format(new Date());
      
              String format5 = dateInstance5.format(new Date());
      
      
              System.out.println(format1);
              System.out.println(format2);
              System.out.println(format3);
              System.out.println(format4);
              System.out.println(format5);
          }
      }
      //		  2020年7月22日星期三 FULL
      //        2020年7月22日 LONG
      //        2020年7月22日 MEDIUM
      //        2020/7/22 SHORT
      //        2020年7月22日 DEFAULT
      // 但是跟视频上的有些不一样？
      
      ```

      ![image-20200722183306901](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200722183306901.png)

### 20.文件上传

1. 上传用户图像
2. 