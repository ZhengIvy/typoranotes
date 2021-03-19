<!DOCTYPE html>
<html>
	<head>
		<title>HTML  Cheat Sheet</title>
	</head>
	<body>
		<!-- Headings -->
		<h1>Heading One</h1>
		<h2>Heading Two</h2>
		<h3>Heading Three</h3>
		<h4>Heading Four</h4>
		<h5>Heading Five</h5>
		<h6>Heading Six</h2>
        <p>
            虽然你你不知道在list中会放进什么类型的元素，<strong>但list是一种原始类型，你随意放进一些不同类型的元素可能会破坏这个<em>list</em>里面元素的类型，</strong>但比如说是可能你想要一个Integer的list 但是因为这是原始类型你还可以输进别的类型的元素，这就破坏了本意。
            </p>
       <ul>
			<li>List Item1</li>
			<li>List Item2</li>
			<li>List Item3</li>
			<li>List Item4</li>
		</ul>
        <ol> 
			<li>List Item1</li>
			<li>List Item2</li>
			<li>List Item3</li>
			<li>List Item4</li>
		</ol>
        <!-- Table -->
		<table>
			<thead>
				<tr>
					<th>Name</th>
					<th>Email</th>
					<th>Age</th>
				</tr>
			</thead>
		</table>
        <div style="margin-top:"500px;" ></div>
</body>






so cool 原来 markdown 的是这么酷的

```html
<strong>
Welcome to my house
</strong>

<em>
    italic
</em>

<a href="https://www.baidu.com/">
			 	This is a link
			 </a>


 <a href="https://www.baidu.com/" target="_blank">
			 	This is a link 可以转到下个窗口，否则会在本窗口中打开
			 </a>
<ul>
			<li>List Item1</li>
			<li>List Item2</li>  // 表示无序
			<li>List Item3</li>
			<li>List Item4</li>
		</ul>
        <ol> 
			<li>List Item1</li>
			<li>List Item2</li>  // 表示有序
			<li>List Item3</li>
			<li>List Item4</li>
		</ol>
<img src = "https://github.com/Ivy0700/Figurebed/raw/main/img/20210306161511.png"/>
<!-- Table -->
		<table>
			<thead>
				<tr>
					<th>Name</th>
					<th>Email</th>
					<th>Age</th>
				</tr>
			</thead>
		</table>
关于如何搞一个table就ok了
```

![image-20200407093839195](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200407093839195.png)

<ul>
    <li> we can
    </li>
    <li> my name
    </li>
    <img src="https://github.com/Ivy0700/Figurebed/blob/main/img/2019-07-24%20081953.jpg"/>
</ul>


<footer>
    <p>Copyright &copy; 2017, My website </p>    
</footer>



这就是哈

```css
<style type="text/css">
		#main-header{
			text-align: center;
			background-color: black;
			color: white;
			padding: 10px;
		}
	</style>
```

这实际上是css 那个main header 是标签来着的，

![image-20200423101934578](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200423101934578.png)

变成这样了哈



```css
<!DOCTYPE html>
<html>
<head>
	<title>CSS Cheat Sheet</title>
</head>
<body>
<h1 style="color:red">Hello World</h1> // 这是inlined 的不推荐这样子使用哈
</body>
</html>


<!DOCTYPE html>
<html>
<head>
	<title>CSS Cheat Sheet</title>
	<link rel="stylesheet" type="text/css" href="css/style.css">
</head>
<body>
<h1 >Hello World</h1>
</body>
</html>

h1{
	color: green;
}
```

![image-20200423104312877](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200423104312877.png)

这种external 是最好的，直接link过去了哈





Selector

`element class id inlined style`

这是顺序，其实就是specific的程度