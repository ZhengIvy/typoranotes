![image-20200330010624061](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330010624061.png)![image-20200329010410461](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200329010410461.png)

![image-20200329010416347](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200329010416347.png)

![image-20200329010422319](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200329010422319.png)

servlet到底是啥，实际上是 server component 你要怎么搞呢，

当他请求一个html 过来的时候，如果是本地有的话，你可直接发回给他，但如果没有的话就需要自己去建哈，这时候就需要了一个 web container 里面有 web.xml 呵 servlet 

web.xml 算是个媒介把，

今天学到了什么呢

今天很可惜还是用eclipse，我先把知识搞懂把，就是按键的区别罢了，我目前还是搞不上，就真的烦，明天再试试吧，然后我学到了doget dopost

目前了解到的就是doget实际上是fetch data，一般是static 的不变的，像textbook 一样，安全性就比较低，而且有变量多少的 限制，一般默认method 是 get

post 的话就是upload data ，可以在服务器中改变，最后上传的是一个page，没有长度的限制， 差不多就是这样了，然**后service中包含了这两个方法，不过呢，我也不知道要不要用这些东西哈，并不知道啥时候用啥时候不要用**，这是我想解决的一点，然后呢，

![image-20200330010529627](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330010529627.png)

![image-20200330010537428](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330010537428.png)

![image-20200330010544888](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330010544888.png)

![image-20200330010550516](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330010550516.png)

![image-20200330010557127](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330010557127.png)

![image-20200330010605204](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330010605204.png)	

![image-20200330010613471](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330010613471.png)

![image-20200330010619235](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330010619235.png)

![image-20200330010627987](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330010627987.png)

![image-20200330010633836](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330010633836.png)

#### api 

到底是什么， application programming interface 可以说是  class interface 和  guide的集合，可以是class 可以是 interface 也可以是guide，怎么说呢就是 他有很多中作用，跟jdbc 很像

像有servlet的class 也有使用servlet的接口，反正都可以进行。

#### 那你觉得call a servlet from a sevlet 是干嘛呢？

因为前面讲到有servlet class，所以我认为是不同class 有不同的作用才要call 的没错就是这样哈





#### 2.sendredirect

![image-20200330091543723](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330091543723.png)

![image-20200330091558075](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330091558075.png)![image-20200330091626514](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330091626514.png)

就你md神奇<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330130713614.png" alt="image-20200330130713614" style="zoom:33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330130719829.png" alt="image-20200330130719829" style="zoom:33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330130725952.png" alt="image-20200330130725952" style="zoom: 33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330130754087.png" alt="image-20200330130754087" style="zoom:33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330130806600.png" alt="image-20200330130806600" style="zoom:33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330130815294.png" alt="image-20200330130815294" style="zoom:33%;" />



今天学到了什么？ sendredirect 是一种方式，在进行转页面的时候会用到，因为当你直接用requestdispatcher的时候呢，request response 都是同一个object ，当你response 的时候你分不清到底是哪个页面给你返回的，那么这个时候会用到sendredirect 告诉他，嘿，你的这个request实际上要传给第二个servlet 那第一个servelt有用吗，当然有用了不过这个等会再说，首先讲最开始怎么把第一个servlet算出来的值传给第二个servlet呢，通过urlrewriting 把url 重写一下，但是这个就牵扯到了一个问题，这种方法能传输的东西很有限，而且不安全，而且在servlet中dopost 不可以用，因为之前就提到了区别说是dopost 的 parameter come from body,doget parameter come from url，而且用的时候getParameter后面有key 和value哈。

那session 用来干嘛的之前提到过用urlrewriting的方法但是不是很好哈，因为不能真正起到share的作用，session 才可以，相当于一个sharing，里面提到的一个例子是去超市买东西但是双方都没有零钱，那这时候就需要一个凭证，否则他不知道是你要钱，所以大概就是这样的作用吧。

#### 3. session and cookie

```java
public class AddServlet extends HttpServlet{
	public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException, ServletException {
		int i = Integer.parseInt(req.getParameter("num1"));
		int j = Integer.parseInt(req.getParameter("num2"));
		int k = i + j;
//		req.setAttribute("k", k);
		
		HttpSession session = req.getSession(); -- 这里
		session.setAttribute("k", k);
		res.sendRedirect("sq");
//		RequestDispatcher rd = req.getRequestDispatcher("sq");
//		rd.forward(req, res);
	}
}


public class SqServlet extends HttpServlet {
	public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
		HttpSession session = req.getSession();
        //session.removeAttribute("k"); 可以把session里面的东西remove掉
		int k =  (int) session.getAttribute("k");  -- 这里
		k = k*k;
		PrintWriter out = res.getWriter();
		out.println("Result is " + k);
		System.out.println("sq called");
	}
}
```

session 和 cookie 实际上好像是联系在一起的。首先举个例子，我去星巴克点单，正常来说我点的单都不会被记住，每次要进行重点，因为普通的http 是stateless ，session 和cookie 可以让变成stable，记住你的订单啥的，cookie 是从client side的，可以说是一张id卡，每次进行出示可以验证你的身份，session 其实也可以在client side，但是内存很小，session 的话在server side 的话就估计和cookie 一起作用，session去database 进行check 或者其他的东西，目前了解的就是这个样子把。然后cookie现在估计比较老了，不是很行，现在用的json好像比较多，怎么说呢，session 比较适用于browser。



```java
public class AddServlet extends HttpServlet{
	public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException, ServletException {
		int i = Integer.parseInt(req.getParameter("num1"));
		int j = Integer.parseInt(req.getParameter("num2"));
		int k = i + j;
//		req.setAttribute("k", k);
		
		Cookie cookie = new Cookie("k",k + "");
		res.addCookie(cookie);
		res.sendRedirect("sq");
//		RequestDispatcher rd = req.getRequestDispatcher("sq");
//		rd.forward(req, res);
	}
}

public class SqServlet extends HttpServlet {
	public void doGet(HttpServletRequest req, HttpServletResponse res) throws IOException {
		int k =  0;
		Cookie []cookies = req.getCookies(); // 是个array 哈，可以有很多cookie
		for(Cookie c : cookies) {
			if(c.getName().equals("k")) { //这是之前输进的key
				k = Integer.parseInt(c.getValue());
			}
		}
		k = k*k;
		PrintWriter out = res.getWriter();
		out.println("Result is " + k);
		System.out.println("sq called");
	}
}
可以add cookies
```





#### 4. ServletContext ServletConfig

就目前了解的知道是 

前者可以公用，但是后者一个servlet只能有一个，不能公用

这样做的原因是什么？

实际上是为了parameter好initialize？

不然每次去各个servlet 找就很麻烦了，直接可以在里面搞哈

```html
 <context-param>
  	<param-name>name</param-name>
  	<param-value>Ivy</param-value>
  </context-param>   <!-->基本上就是这样把，一个是key 一个是value </!-->
```

![image-20200331012941918](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331012941918.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331012948209.png" alt="image-20200331012948209" style="zoom:33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331012956412.png" alt="image-20200331012956412" style="zoom:33%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331013005018.png" alt="image-20200331013005018" style="zoom:33%;" />

#### 5.Annotation

![image-20200331013049889](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331013049889.png)

哪个@就是了 不过要记得加一个/"/add" 正确





#### 6. servlet jsp

jsp 是啥，java server pages

就是html java 结合在一起，虽然说你可以直接在java里面写html 但是就很麻烦啊，所以你就需要这个来进行，有几个特点：

1. 不需要object initialize 对于 session request response 这些是不需要的哈
2. 然后有一些符号，<% %> 关于这种的各有各的不同 但是我有疑问  如果有class 呢，他好像没有提到欸

![image-20200331013517412](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331013517412.png)

![image-20200331013522335](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331013522335.png)

jsp 上的可以被translate到java code中哈。





#### 7. JSP tags

1. sciptlet <%   %>
2. declearation <%! %>
3. directive `<%@ page import="java.util.Scanner" %>`

4. expression

![image-20200331135146943](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331135146943.png)

![image-20200331135151383](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331135151383.png)

![image-20200331135155008](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331135155008.png)

![image-20200331135200177](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331135200177.png)

![image-20200331135205373](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331135205373.png)

![image-20200331135209049](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331135209049.png)

![image-20200331135216837](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331135216837.png)

![image-20200331163734072](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331163734072.png)

终于知道怎么导入html 了，首先是要在同一个web 中哈，所以呢就这样，jsp 啥的都可以导入，就是引用别的

![image-20200331170848783](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331170848783.png)

这个是啥？？？？？？、



#### 8. exception handling in jsp

![image-20200401001400096](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200401001400096.png)

 注意那个 要加一个isErrorPage ![image-20200401001528761](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200401001528761.png)

这是主的jsp的，就是把exception 都交给上面的那个page，然后呢，那个page 要确定自己是不是 errorpage 哈



#### 9. MVC 架构

其实这个我实际上也有想到了嘻嘻，就是在找你目前学到的东西的关系罢了

其实这个也是你

![image-20200401005723510](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200401005723510.png)

![image-20200401005735683](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200401005735683.png)

就是简单的一个用户登录的过程，首先对于用户来说，他只要view，不管 what's going on behind the scene.

那这个view 提供的就是jsp 可以有静态的也可以以有动态的，像Html就是静态的，但是我觉得html 在这里也有用。html可以提供静态的部分，然后数据谁送呢？ controller 里面就是servlet 只负责response request的指令，那这两者之间由谁送的呢， pojo plain old java object 就是以object 的形式送的，反正到后面都是以 object的形式去送的，那谁写 business language呢，就是一些class 了，前面的pojo的可能只是媒介把，

那数据哪来呢。数据库嘛，通过jdbc的dao形式传来的，感觉有点像吼， 但是后面的class 可能包括的是method 啥的，前面的object可能就是个整合罢了





#### 10. jstl

这是个什么东西呢

```java
<%String name = request.getAttribute("label").toString();
  out.print(name);


  %>
      
      same as ${label} 
```

然后今天犯了一个很蠢的错误是没有把普通 的class 变成servlet 无语了，但是依然在idea 上跑不了，无语了，因为那个部署的问题是真的无语，为什么要这样搞呢



```jsp
<%@ page import="org.w3c.dom.ls.LSOutput" %><%--
  Created by IntelliJ IDEA.
  User: zbr
  Date: 2020/3/31
  Time: 8:03
  To change this template use File | Settings | File Templates.
--%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="sql" uri="http://java.sun.com/jsp/jstl/sql" %>
<%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions" %>
<%--<%@ page import="static com.zbr.com.FunUtils.makeItLower" %>--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%--<%@page errorPage="fun.jsp" %>--%>
<html>
  <head>
    <title>PLAY PLAY PLAY</title>
  </head>
  <body>
// 下面是与sql相连用到的，感觉var的话是name把
<%--<sql:setDataSource var="db" driver="com.mysql.cj.jdbc.Driver" url="jdbc:mysql://localhost:3306/database1?&useSSL=false&serverTimezone=UTC" user="root" password="zbr84521051.."/>--%>
<%--<sql:query var="rs" dataSource="${db}">select * from student</sql:query>--%>
<%--<c:forEach items="${rs.rows}" var="students">--%>
<%--  <br/><c:out value="${students.student_id}"></c:out> : <c:out value="${students.name}"></c:out>--%>
<%--</c:forEach>--%>
<%--  ${label} <br>--%>
<c:set var = "str" value="Ivy Martin"/>
    //这里用function了
Length : ${fn:lenth(str)}
  <c:out value="Hello World"/>
  hello
  </body>
</html>

```





每天都是心累的，一下这里异常 一下那里异常，反正就不知道为什么哈

所以今天学了什么呢，一直在跟着他那个的操作系统进行log in log out welcome 其实也没有什么难度的，然后呢，后面又学了一个问题，反正我刚刚没打出来，就是要注意到logout之后呢再返回的话会出现问题h差不多就这样子

然后我刚刚又出现了一个问题，login页面卡在那里不动，不知道又是啥出了问题，心累了。

cache file.

session invalidate dao 这些我还要去搞，没学点皮毛无语，上次dao就搞不了的。



#### 11. login

怎么 说呢就是，这个东西感觉不好记录啊，反正就是差不多那些东西

log in log out

没搞啥 就感觉搞了挺久这个的，感觉也没学啥知识无语，不过学了一个md5 一个加密的东西，就差不多这样了

还有login 的构造 ，一个jsp

一个controller 一个 connection 一个 dao 就这样的配置哈，然后配上mysql就好了 差不多就是这样

事实证明我不会搞重复的





#### 12.继续LOG IN AND LOG OUT

今天的进度是搞了个弹窗，还搞了一些啥？ 弄了好久的链栈，没想到真正的链栈是这个样子的，无语，所以其实还是挺简单的哈，我觉得，就是清空那里要注意一下，还有呢就是不知道为啥case 里面第一行不能定义。不懂哈

然后现在呢就是这样呢，主要是不是很熟 然后把modify 再连在一起就可以了哈，然后其他的问题是忘记的话你要验证吧，你拿啥验证呢？ 邮箱吧？ 账号注销也差不多也可以搞，搞在很多界面都行的，然后call一个function 就好了，我还差注册成功的提醒，没写，这个怎么写呢等会想想哈





#### 13. 搞定啥 count session的好像

不过我也真是不咋会，![image-20200410005120177](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410005120177.png)

好像是application 的=可以换界面罢了，在不同的浏览器上



```java
//package password;

import javax.crypto.Cipher;
import javax.crypto.spec.SecretKeySpec;

//import com.mysql.cj.protocol.Message;
//
//    import javax.servlet.ServletException;
//import javax.servlet.ServletOutputStream;
//import javax.servlet.annotation.WebServlet;
//    import javax.servlet.http.HttpServlet;
//import javax.servlet.http.HttpServletRequest;
//import javax.servlet.http.HttpServletResponse;
//import java.io.IOException;
//import java.io.PrintWriter;
//    import java.security.MessageDigest;
//    import java.security.NoSuchAlgorithmException;
//
//    public class Helloworld {
//        public static String hashPassword(String password) throws NoSuchAlgorithmException {
//            MessageDigest md = MessageDigest.getInstance("md5");
//            md.update(password.getBytes());
//            byte[] b = md.digest();
//            StringBuffer sb = new StringBuffer();
//            for(byte b1:b){
//                sb.append(Integer.toHexString(b1& 0xff).toString());
//            }
//            return sb.toString();
//        }
//        public static void main(String[] args) throws NoSuchAlgorithmException {
//            String password = "password";
//            System.out.println(hashPassword(password));
//        }
//    }
//

//    public static String encrypt(String strClearText, String strKey) throws Exception {
//        String strData = "";
//        try {
//            SecretKeySpec skeyspec = new SecretKeySpec(strKey.getBytes(), "Blowfish");
//            Cipher cipher = Cipher.getInstance("Blowfish");
//            cipher.init(Cipher.ENCRYPT_MODE, skeyspec);
//            byte[] encrypted = cipher.doFinal(strClearText.getBytes());
//            strData = new String(encrypted);
//        } catch (Exception e) {
//            e.printStackTrace();
//            throw new Exception(e);
//        }
//        return strData;
//    }
//}
//    public static String decrypt(String strEncrypted,String strKey) throws Exception{
//        String strData="";
//        try {
//            SecretKeySpec skeyspec=new SecretKeySpec(strKey.getBytes(),"Blowfish");
//            Cipher cipher=Cipher.getInstance("Blowfish");
//            cipher.init(Cipher.DECRYPT_MODE, skeyspec);
//            byte[] decrypted=cipher.doFinal(strEncrypted.getBytes());
//            strData=new String(decrypted);
//        } catch (Exception e) {
//            e.printStackTrace();
//            throw new Exception(e);
//        }
//        return strData;
//    }
```





#### 14.setContentType

目前了解的就是resp 的时候你可能有好几种类型啦，一般认为的话是html 然后你可以改变嘛 就其他类型都是ok 的哈

<img src="D:\tim\1097641461\FileRecv\MobileFile\IMG_4640.PNG" alt="IMG_4640" style="zoom:33%;" />

<img src="D:\tim\1097641461\FileRecv\MobileFile\IMG_4639.PNG" alt="IMG_4639" style="zoom: 33%;" />

<img src="D:\tim\1097641461\FileRecv\MobileFile\IMG_4638.PNG" alt="IMG_4638" style="zoom:33%;" />

<img src="D:\tim\1097641461\FileRecv\MobileFile\IMG_4637.PNG" alt="IMG_4637" style="zoom:33%;" />