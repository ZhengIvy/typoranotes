## 1. var

throughout your program



let in the scope



## 2. console.log

```javascript
console.log(myName);

var a = "Ada";
var length = 0;
length = a.length;
console.log(length); //算length 是这样的哈
```

这就是输出



## 3.array

```javascript
var array = ["Ivy","J","cat"];
array.push(["happy","joy"]);
```

不同点 没有[] 不是{} 而是[]

还可以进行push 相加哈



```javascript
var array = ["Ivy","J","cat"];
array.push(["happy","joy"]);
array.unshift("happy"); // 和push差不多，不过是在最前面罢了

var remove = array.pop();
console.log(remove);
var remove = array.shift();
```

还可以pop  掉最后面的一个哈

shift是前面的，pop前面的罢了





```javascript
function nextLine(arr,item){// 发现没有 不需要定义var什么的
return item;
}

var testArr = [1,2,3,4,5];

console.log(JSON.stringify(testArr));
console.log(nextLine(testArr,6));
console.log(JSON.stringify(testArr));
```

我怎么就遇到json了？？迷茫

好想直接输出数组需要json诶

```javascript
var ourDog = {
  "name" : "Camper",
  "legs" : 4
};
var name = ourDog.name;
console.log(name);

var ourDog = {
  "my name" : "Camper", // 如果你的object 名字中间有个空格的话那就需要 
  "legs" : 4
};
var name = ourDog["my name"];
console.log(name);
```

这个是object  虽然还不知道有啥子用吼

![image-20200428003040600](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200428003040600.png) 

## 4. let

不能定义两次 在同一个域内 是不行的哈

var globally

let was restricted 所以let的话是根据block来的

然后很多不一样的东西就来了，~~像我们有分局部变量啥的，那这个就不会有哈~~，所以var在一个block里面定义后，还可以在外面继续定义哈

```javascript
function checkBox(){
  var i ="function scope";//let same
if(true){
   i = "block scope";
  console.log(i);
}
  console.log(i);
  return i;
}

checkBox();
```

![image-20200428084250457](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200428084250457.png)

真的是没有全局变量和局部变量这回事的哈

## 5. const

这个还是可以改的哈，如果array的话

```javascript
const SENTENCE = [1,2,3];
SENTENCE[0] = 5;
```

## 6. hello world

loosely type

dynamic type

```html
<!DOCTYPE html>
<html>
<head>
	<title>My title</title>
	<script type="text/javascript">
		document.write("<h1>Heading 1</h1>	");
	</script>
</head>
<body>

</body>
</html>

<script type="text/javascript" >
	function myfunction(){
		var1 = "tammy";//global variable
		document.write(var1);
		var a = 5;
		document.write(a);
	}
	myfunction();
	document.write(var1);
</script>
```

我之前学的到底是什么？？？

靠 我终于学到想要的东西了	![image-20200428173127213](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200428173127213.png)

![image-20200428173359201](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200428173359201.png)

![image-20200428173425450](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200428173425450.png)

![image-20200428173432701](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200428173432701.png)

所以呢type of 的话就是用来判断类型 判断不出来的都为object

所以这时候需要instanceof 判断到底是不是个对象哈





## 7. object

有点不一样啊

```html
<script type="text/javascript" >
	function abc(car_name,car_size){
		this.car_name = car_name;//this 竟然可以这样子用
		this.car_name = car_name;
		document.write(car_name);
		document.write(car_size);
	}
	var my_car = abc("aaa",3);然后这时候就是一个object了
</script>
```

new keyword create object

```html
<script type="text/javascript" >
	var car = {
		car_brand : "Tesla",
		car_price : 12333,
		car_mode : 3
	}
	car.fueltype = "electric";
	delete car.car_mode;//可以delete
	document.write(typeof(car.car_mode));//delete
</script>
```

```html
<!DOCTYPE html>
<html>
<head>
	<title>My title</title>
	<script type="text/javascript" >
	function buttonClick(){//终于知道click button了哈哈
		alert("button clicked");
	}
	// buttonClick();
</script>
	</head>
</head>
<body>
<button onclick="buttonClick()">Click me</button>
<h2 id="heading2">Some Random Text</h2>
</body>
</html>

function buttonClick(){
		// alert("button clicked");
		var str =document.getElementById("heading2").innerHTML;//这个代表的意思是获得其中的东西，你也可以去change文本
		alert(str);
	}
	// buttonClick();
```

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200428181627661.png" alt="image-20200428181627661" style="zoom:33%;" />

```html
<!DOCTYPE html>
<html>
<head>
	<title>My title</title>
	<script type="text/javascript" >
	function fn1(){
		var password = document.getElementById("text2").value;
		if(password != "my"){
			alert("wrong password");
		}
	}
	// buttonClick();
</script>
	</head>
</head>
<body>
<input id="text1" placeholder="username">
<input id="text2" placeholder="username" type="password">
<br>
<button id="btn1" onclick="fn1()">Click me</button>
</body>
</html>
```

这就是我们之前遇到的东西了哈，啥呢，判断你输入的东西正不正确哈

<input name="grp1" type="radio" value="Simple Snippets">Simple Snippets</input><br>

<input name="grp2" type="radio" value="Telusko Learnings">Telusko Learnings</input>

<br>

<button>Click me</button>

多选的情况，这样就可以多选哈，当时不同值的时候





<!DOCTYPE html>

```html
<!DOCTYPE html>
<html>
<head>
	<title>My title</title>
	<script type="text/javascript" >
	function fn1(){
		var rd1 = document.getElementById("rd1");
		var rd2 = document.getElementById("rd2");

		if(rd1.checked == true){// 代表你有没有选上哈
			alert("The channel selected is "+rd1.value);}
			else if(rd2.checked == true){
				alert("The channel selected is "+rd2.value);
			}
			else{
				alert("No channel selected");
			}
		}
	
	// buttonClick();
</script>
	</head>
</head>
<body>
<!-- <input id="text1" placeholder="username">
<input id="text2" placeholder="username" type="password">
<br>
<button id="btn1" onclick="fn1()">Click me</button> -->
<input id="rd1" name="grp1" type="radio" value="Simple Snippets">Simple Snippets</input><br>
<input name="grp1" id="rd2" type="radio" value="Telusko Learnings">Telusko Learnings</input>
<br>
<button onclick="fn1()">Click me</button>
</body>
</html>
```

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200428200611797.png" alt="image-20200428200611797" style="zoom:50%;" />

这个是啥子哦，这个就是选了可以判断你选的是啥

但我更想要的是与后端的交接想要的是那种确认的弹框，不知道行不行哈，等会去找找哈，



## 8. selectbox

```html
<!DOCTYPE html>
<html>
    <head>
        <script type="text/javascript">
            function fn1(){
                var select = document.getElementById("selectbox");
                // alert(select.options[select.selectedIndex].value);
                alert(select.value);
            }
        </script>
    </head>
    <body>
        <select name="name" id="selectbox">
            <option value="Telusko Learnings">Telusko Learnings</option>
            <option value="Simple Snippets">Simple Snippets</option>
        </select>
        <button onclick="fn1()">Click me</button>
    </body>
</html>
```

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200428201829944.png" alt="image-20200428201829944" style="zoom:33%;" />

这个就是你选了哪个然后告诉你选了啥，不过还是达不到我想要的效果后面看一下哈



### getElementsByTagName

```html
<!DOCTYPE html>
<html>
<head>
	<title>My title</title>
	<script type="text/javascript" >
	function changeStyling(){
		var para = document.getElementsByTagName("p");
		para[2].style.fontSize = "25px";
	}
	
</script>
	
</head>
<body>
	<p >This is paragraph</p>
	<p>This is paragraph 2</p>
	<p>This is paragraph 3</p>
	<p>This is paragraph 4</p>
	<p>This is paragraph 5</p>
	<button onclick="changeStyling()">Click me</button>

</body>
</html>
```

## 9. login

```html
<!DOCTYPE html>
<html>
<head>
	<title>My title</title>
	<script type="text/javascript" >
	function validate(){
		var userName = document.getElementById("userName").value;
		var password = document.getElementById("password").value;
// var regx = /[^a-x]mple/i;//正则表达，这个表示不可以是这些范围哈
		var regx = /^[5-9][0-9]{8}[7-9]$///限制电话号码的一般{表示个数}
		if( regx.test(userName)==false||userName.trim()=="" ){
			alert("Blank username");
			document.getElementById("valid").style.visibility="visible";
			return false;
		}
		else if(password.value.trim()){
			alert("Blank password");
			return false;
		}
		else if(password.value.trim.length<5){
			alert("Password too short");
			return false;
		}
		else{
			return true;
		}
	}
</script>
	
</head>
<body>
	<form action="aaa.html" onsubmit="return validate()">
	<input type="text" id="userName" placeholder="userName"/>
	<label id="valid" style="color: red;visibility: hidden;">Invalid</label>
	<input type="password" name="" id="password">
	<button type="submit">Submit</button>
	</form>
</body>
</html>
```

目前最intuitive的

![image-20200428214353302](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200428214353302.png)

1. 限制长度
2. 不让空格
3. invalid 显示能让用户体验更加好
4. 感觉在我的返回失败中有了信心，今晚可以试试哈

![image-20200428231552006](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200428231552006.png)

正则表达

![image-20200428232650188](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200428232650188.png)

这个好像之前没接触过诶，不知道在数据库中是不是这样的那个方法哈

![image-20200429002854865](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200429002854865.png)

点号用处很大

![image-20200429003913715](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200429003913715.png)

如果\号的话基本上代表失去功能了吧





## 10. debug

在谷歌上可以debug 的，console log debug 在谷歌上，而且也可以用debugger哈，我觉得我之前用debugger 的方法可能错误了。。





## 11. timeout

```html
<!DOCTYPE html>
<html>
    <head>
     <script type="text/javascript">
     var ID=0;
     var seconds = 0;
function printMsg(){
    // document.getElementById("op").innerHTML="5 seconds has passed";
    document.getElementById("op").innerHTML= seconds + "seconds";
    seconds++;

}
function start(){
   
    // ID = window.setTimeout(printMsg,5000); 这个是你开始之后就会有一个ID，过了这么多时间后就会提醒出现，使用那个function
    ID = window.setInterval(printMsg,1000);// 这个就是时间段，每隔一定的时间进行变化
}

function stop(){
    window.clearInterval(ID);// 这个就是stop了哈
}

    </script>   
        
    </head>
        <body>
       <button onclick="start()" id="btnAdd">Start</button> 
       <h2 id="op">Some text</h2>
       <button onclick="stop()" id="btnStop">Stop</button>
    </body>
    </html>
```





## 12. JQuery

<html>

  <head></head>

  <body>

​    <h2 id="heading1">Setting up jquery</h2>

​    <button id="btn1" onclick="fn1()">Click me</button>

  </body>   

    <script src="jquery/jquery-3.4.1.js"></script>

    <script>

​    function fn1(){

​      $("#heading1").fadeToggle(); //这个就是jquery ，这个selector 是和css 一样的，直接用library完成就ok

​    }

  </script>

</html>





```html
<html>
    <head>
        <link rel="stylesheet" href="style2.css">
    </head>
    <body>
       <div id="firstdiv" class="mydivs">
           <p>This is first paragraph</p>
           <p>This is second paragraph</p>
       </div>
       <div id="seconddiv" class="mydivs">
        <p>This is what?</p>   
       </div>
       <div id="thirddiv" class="mydivs">
           <ul>
               <li>List item1</li>
               <li>List item2</li>
           </ul>
       </div>
        <button id="btn1" onclick="fn1()">Click me</button>
    </body>     
    <script src="jquery/jquery-3.4.1.js"></script>
    <script>
        function fn1(){
            $("#firstdiv,p,li").fadeToggle(); div: first div p
        }
    </script>
</html>
```

然后这里就跟css差不多了



```html
<html>
    <head>
        <link rel="stylesheet" href="style2.css">
    </head>
    <body>
       <div id="firstdiv" class="mydivs">
           <p>This is first paragraph</p>
           <p>This is second paragraph</p>
       </div>
       <div id="seconddiv" class="mydivs">
        <p>This is what?</p>   
       </div>
       <div id="thirddiv" class="mydivs">
           <ul>
               <li>List item1</li>
               <li>List item2</li>
           </ul>
       </div>
        <button id="btn1" >Click me</button>
    </body>     
    <script src="jquery/jquery-3.4.1.js"></script>
    <script>
        $(document).ready(function(){//when the page is loaded because sometimes when a page is heavy with stuff,you can't execute the funtion
        $("button").click(fn1);//onclick 到这来了哈
        $("button").mouseenter(fn1);
        $("button").mouseleave(fn2);//可以用于预览的差不多哈
        $("button").hover(fn1,fn2);//把两个功能整在一起，我就不用写那么多了
        function fn1(){
            $("#firstdiv,p,li").fadeOut();
        }
        function fn2(){
            $("#firstdiv,p,li").fadeIn();
        }
    });
    </script>
</html>
```



```html
<html>
    <head>
        <link rel="stylesheet" href="style2.css">
    </head>
    <body>
       <div id="firstdiv" class="mydivs">
           <p>This is first paragraph</p>
           <p>This is second paragraph</p>
       </div>
       <div id="seconddiv" class="mydivs">
        <p>This is what?</p>   
       </div>
       <div id="thirddiv" class="mydivs">
           <ul>
               <li>List item1</li>
               <li>List item2</li>
           </ul>
       </div>
        <button id="btn1" >Click me</button>
        <button id="btn2">Click me</button>
    </body>     
    <script src="jquery/jquery-3.4.1.js"></script>
    <script>
        $(document).ready(function(){//when the page is loaded because sometimes when a page is heavy with stuff,you can't execute the funtion
        $("#btn1").click(function(){
            $("#firstdiv").hide();
        });
        $("#btn2").click(function(){
            $("#firstdiv").show();
        });
    });
    </script>
</html>
```

callback 就是在执行完之后才会出现 的东西

```javascript
 $(document).ready(function(){
           $("#btn1").click(function(){
               var txt = $('#p1').text();
               alert(txt);
           });
       });// 这个是在js中换了种方式call 就是简略了getelementid


 alert($('#p1').attr("value")); 拿到你那个id里的attr
```

text(),html(),attr(),css()

css就是拿到css的东西

html和text区别是html能识别text里面的html word

```javascript
 $(document).ready(function(){
           $("#btn1").click(function(){
            //    $('#p1').text();
               $("#p1").attr("class","p1class");//把attrclass换成p1class 之前是p1
               反正js一点都不严谨把，经不得推敲
              css也能改的这样子
           });
           $("#btn2").click(function(){
               alert($("#p1").attr("class"));
           })
       });
```

关于那个日期的可以用jquery 诶，但是列，你怎么retrievedate呢，就不是date的format了，是text的format

![image-20200429115733471](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200429115733471.png)

![image-20200429115738590](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200429115738590.png)

### Jquery UI

```html
<html>
    <head>
        <link rel="stylesheet" href="jqueryui/jquery-ui.css">
        <link rel="stylesheet" href="jqueryui/jquery-ui.structure.css">
        <link rel="stylesheet" href="jqueryui/jquery-ui.theme.css">
    </head>
    <body>
       <div id="mydiv">
           <h3>Introduction to jQuery UI</h3>
           <input type="text" id="dateinput">
       </div>
    </body>
    <script src="css/jquery/jquery-3.4.1.js"></script>
    <script src="jqueryui/jquery-ui.js"></script>
    <script>
        $("#dateinput").datepicker({
            numberOfMonths:1,
            changeYear:true,
            changeMonth:true,
            showWeek:true,
            weekHeader:"wk no",
            showOtherMonths:true,
            minDate: new Date(2017,0,1),
            maxDate: new Date(2020,0,1)
        });
    </script>
</html>
```

这个上面的结果哈

```html
<img src="images/showcase.jpg" width="200px" title="beauty" id="myimg">

$("img").tooltip({
            track:true,
            content: "Telusko is the best",//一定要有title，即使是空
            show:{effect:"pulsate",duration:3000}
            //hightlight bounce explode blind
        });
```

![image-20200429121635260](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200429121635260.png)

```html
 <div id="mydiv">
           <h3>Introduction to jQuery UI</h3>
           <!-- <img src="images/showcase.jpg" width="200px" title="beauty" id="myimg"> -->
           <!-- <input type="text" id="dateinput"> -->
      <p>Telusko learnings is one of the largest tech</p>
        <h3>Learnings</h3>
        <p>Simple Snippets</p> 
        <p>dada</p>   
    </div>



$("#mydiv").accordion({
            collapsible:true,
            event:"click",
            active:1,//show up automatically
            heightStyle:true   //height based on the content
        });
```

![image-20200429123929073](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200429123929073.png)

MessageBox

```html
<html>
    <head>
        <link rel="stylesheet" href="jqueryui/jquery-ui.css">
        <link rel="stylesheet" href="jqueryui/jquery-ui.structure.css">
        <link rel="stylesheet" href="jqueryui/jquery-ui.theme.css">
    </head>
    <body>
        <h2>Introduction to jQuery UI</h2>
        <div id="messagebox" title="Messagebox" class="mydivs">
            <h3>This is just a dummy title</h3>
            <img src="images/showcase.jpg" width="200px">
            <br><button id="btn1">Click me</button>
        </div>
    </body>
    <script src="css/jquery/jquery-3.4.1.js"></script>
    <script src="jqueryui/jquery-ui.js"></script>
    <script>
       $("#btn1").click(function(){

            // alert("Button clicked");
            $("#messagebox").dialog({
                title:"Custom MessageBox",
                draggable:false,
                resizable:true,//modify size
                height:300,
                width:300,
                modal:true,//can't do anything in the page
                buttons:[{
                    text:"Close",
                    icon:"ui-icon-heart",
                    click:function(){
                        $(this).dialog("close");
                    }
                },
                {
                    text:"ok",
                    icon:"ui-icon-heart",
                    click: function(){
                        alert("hello")
                    }
                }
                ]
            });
       });
    </script>
</html>
```

![image-20200429125849581](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200429125849581.png)

fucking cool