#### 1.SELECT

we soecify the columns that we want to retrieve

all columns using asterisk `*`

```mysql
SELECT *
FROM customers//挑选
WHERE customer_id=1 // find the data of the 1 
```

![image-20200324213505964](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200324213505964.png)

```mysql
SELECT *
From customers
ORDER BY first_name//排序方式
-- WHere customer_id=1 //这个是mysql的注释
```

#### 2.MySql--三种注释写法



需要特别注意  --  这种注释后面要加一个空格

\#DELETE FROM SeatInformation  

 /*DELETE FROM SeatInformation */
 -- DELETE FROM SeatInformation





line breaks white spaces and tabs are ignored when executing 

but each line is better



```mysql
SELECT first_name,last_name,points +10
 From customers
-- WHERE customer_id=1
-- ORDER BY first_name
```

![image-20200324214554592](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200324214554592.png)

注意到没，这个point+10

#### 3.变成了名字，但这不是我们想要的，所以我们可以改名字

![image-20200324215020812](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200324215020812.png)

```mysql
SELECT first_name,
last_name,
points,
points *10+10 As discount_factor-- points *10+10 As 'discount factor' 有空格了
 From customers
```

改好了



如果你要对数据进行改动的话你可以直接改动，

[^APPLY AND REVERT]: NOTHING

![image-20200324215631261](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200324215631261.png)

右下角看到没有





#### 4.如果你不想要duplicate的话你可以用、

```mysql
SELECT DISTINCT state//这个distinct
From customers
```



SELECT 也算一种filter 但是呢只是在概念上进行filter

但是where 的话是在有目标的数值上进行filter



#### 5.!= <>  same then

大写小写 也是same的

```mys

```



#### 6.![image-20200324222000808](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200324222000808.png)





#### 7.SELECT FORM WHERE 的终极奥秘

今天老是搞错，那我来讲到底是什么吧

SELECT 是选的columns ，选输出的时候你要展现那些column

From 选的是哪个文件的

WHERE选的是 columns 值对应的 范围





#### 8.AND OR OPERATOR

#### 9.IN

```mysql
USE sql_store;
SELECT *
FROM Customers
WHERE state IN('VA','GA','FA')
-- or or or 一个意思
```

代表 equal 也行，就表示你的值在里面就ok



#### 10.between

就是代表了 >= <= 的符号 很有用的哈

```mysql
BETWEEN 1000 AND 49999
```



#### 11.LIKE

##### 1.%

```mysql
USE sql_store;
SELECT *
FROM customers
WHERE last_name LIKE 'B%'
```

![image-20200324230457618](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200324230457618.png)

代表长的像 的哈，% 代表无论你后面有多少个，q**其实代表的是省略号的意思啦**，

```mysql
USE sql_store;
SELECT *
FROM customers
WHERE last_name LIKE '%b%'
WHERE address LIKE '%TRAIL%'OR address LIKE'%AVENUE%'  -- 如果是或的话两边一起写
```

代表之间有一个B 就OK了



##### 2，_

```mysql
USE sql_store;
SELECT *
FROM customers
WHERE last_name LIKE '_y' -- _表示一个character ，代表名字符合有两个字符 最后一个是y的
WHERE last_name LIKE '____Y'
```



##### 3.REGEXP(regular expression)

像是用来代替% **功能更强大**

1. $

2. ^

3. |
4. []
5. [a-h]//表示 a到h 不用一个一个打出来



```mysql
USE sql_store;
SELECT *
FROM customers
-- WHERE address LIKE '%TRAIL%'OR address LIKE'%AVENUE%'//这个怎么想还是太麻烦了吧，
-- WHERE phone LIKE '%9'
WHERE last_name REGEXP 'field'
    WHERE last_name REGEXP '^b'//表示第一个字母为b
    WHERE last_name REGEXP 'h$' -- represents the end of the string
     WHERE last_name REGEXP 'mac|field'-- 强大的功能
     -- 不用像上面一样用的那么麻烦哈
```

```mysql
 WHERE last_name REGEXP '[gim]e'-- 酷炫的又来了 
 -- 表示的是 ge,ie,me both ok
```



#### 12. IS NULL||is not null

```mysql
USE sql_store;
SELECT *
FROM customers
-- WHERE address LIKE '%TRAIL%'OR address LIKE'%AVENUE%'
-- WHERE phone LIKE '%9%8%'
 WHERE PHONE IS NULL -- is not null 也可以用
```

![image-20200325000755109](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325000755109.png)

判断是否为空



#### 13.ORDER

有分为**natrual order 和 primary order**， 一般有默认排序的，但是你可以自己改

```mysql
ORDER BY first_name 
ORDER BY first_name DESC -- 降序
```

不过要注意一下，character 的排序实际上是一个字母一个字母排的

```mysq
ORDER BY first_name,last_name
```

![image-20200325002106068](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325002106068.png)

发现没有，反而D的在上面，说明排序不是像你想象中的那样哈，那如果我想那样呢？ 暂时还不知道



```mysql
USE sql_store;
SELECT first_name,last_name,10 AS points
FROM customers
-- WHERE address LIKE '%TRAIL%'OR address LIKE'%AVENUE%'
-- WHERE phone LIKE '%9%8%'
ORDER BY points

```

你还可以加一些无关的东西进去![image-20200325002422712](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325002422712.png)

然后多了一行



**calling** 

```mysql
USE sql_store;
SELECT first_name,last_name,10 AS points
FROM customers
-- WHERE address LIKE '%TRAIL%'OR address LIKE'%AVENUE%'
-- WHERE phone LIKE '%9%8%'
ORDER BY 1,2 -- 指的是 first_name ,last_name easy 
```

但是可能会produce unexpected results ，因为 当你插入或删除的时候 位置可能会改变

所以不推荐这种方法



#### 14.LIMIT

当你只想得到一段数据的时候

```mysql
USE sql_store;
SELECT *
FROM customers
LIMIT 4
```

![image-20200325003124388](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325003124388.png)

想要中间的数据呢

```mysql
USE sql_store;
SELECT *
FROM customers
LIMIT 4,3 -- 表示 去掉前四个，要接下来的三个
```



#### 15. 与其他表格联系在一起

```mysql
USE sql_store;
SELECT *
FROM orders
JOIN customers ON orders.customer_id=customers.customer_id
```

![image-20200325151548069](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325151548069.png)

意思是和其他表格的内容联系在一起，联系的依据就是这个id，orders 先出来的所以这里也是orders 先出来



```mysql
USE sql_store;
SELECT order_id,customer_id,first_name,last_name
FROM orders
JOIN customers ON orders.customer_id=customers.customer_id
```

![image-20200325152739074](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325152739074.png)

出现了一个error，这个customer_id有点模糊？ 但是他两不是一样的吗(算了机器可能不了解把)

修改的方法就是你在前面加`customer.customer_id` 就好了



##### 改进方法，那些东西太麻烦了

```mysql
USE sql_store;
SELECT order_id,o.customer_id,first_name,last_name
FROM orders o -- 变成缩写，说明这个mysql 不是一行一行进行的
JOIN customers c
ON o.customer_id=c.customer_id
```

大家都缩写的话那就都要进行下去哦

##### 2.与自己的表格联系在一起

```mysql
USE sql_hr;
SELECT e.employee_id,e.first_name,m.first_name
FROM employees e
JOIN employees m
ON m.employee_id=e.reports_to
```



![image-20200325163823941](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325163823941.png)

先看原来的表。就是select * 的

![image-20200325163856789](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325163856789.png)



很神奇是不是，这个要求时把employee 的manager 找出来 

那这个时候就要区分JOIN 和 From 到底是怎么回事

首先说下这个表，联系起来的表一般都分为两部分，前面的比较好理解时因为ON 的相同的东西，但是这里不是了，前面的表对应的是from 所以说from保持原样，join 进行改变 on的内容进行匹配然后差不多就是这样了



```mysql
USE sql_hr;
SELECT e.employee_id,e.first_name,m.first_name AS manager	
FROM employees e
JOIN employees m
ON m.employee_id=e.reports_to
```

![image-20200325165935598](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325165935598.png)

改进





##### 3. 把几个table 合成起来

```mysql
SELECT o.order_id,order_date,first_name,last_name,os.name AS status
FROM orders o
JOIN customers c
ON o.customer_id=c.customer_id
JOIN order_statuses os
ON os.order_status_id=o.status
```

![image-20200325171719177](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325171719177.png)

主要还是呢，**用两个JOIN on 就好了，像我还想一起join on 呢**

调换顺序无关系



你可以ON 几个条件进来，

JOIN 

ON 

AND 

可以了





#### implicit join syntax

```mysql
SELECT *
FROM orders o,customers c
WHERE o.customer_id=c.customer_id
```

这种也算的

看起来感觉一样把

**如果漏掉一行WHERE呢？**

就变成了cross turn？ 这啥？？？？

![image-20200325193535299](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325193535299.png) 

![image-20200325193548182](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200325193548182.png)

order前十行对应的是customer 的第一行？？？怎么回事

然后10x10=100 一共有这么多行？？ 迷茫

所以最好不用



#### 16. outer join

##### 1.两种join： left join and right join 

> 为什么需要Outer join

**因为遇到了一个问题，不是所有customer 都order了，**

你打出这个table的条件是 `c.customer_id =o.customer_id`

那既然有一方的值为空，就不符合条件，那这时候就需要outer join

```mysql
SELECT c.customer_id,first_name,order_id
FROM customers
left JOIN    corders o
	ON o.customer_id=c.customer_id
    order by c.customer_id
```

原理是什么？
from 后接的是左

JOIN 后接的是右

你可以想象成先把左的打印出来，然后让右边进行比对，就算右边有空值也要进行下去

**所以select那里还是有讲究的，不能乱select，**



##### 2. multiple join

要记住要统一right left 最好都使用left

```mysql
SELECT 
	o.order_id,
    c.first_name,
    sh.name AS shipper
    FROM orders o
    JOIN customers c
		USING (customer_id) -- c.customer_id=o.customer_id
	 LEFT JOIN shippers sh
    USING (shipper_id)
```

如果两行的名字完全一样的话可以简化成`using` 

如果有多个比较的话

不用on 记住了刚刚就搞错了



#### 17. natural join

不推荐

```mysql
SELECT 
o.order_id,
c.first_name
FROM orders o
NATURAL JOIN customers c
```

就没有on了， 这代表你让系统去猜相同的地方



#### 18. cross join 

前面有提到过了，那什么时候用到呢， 当你需要combine 的时候了

```mysql
SELECT 
c.first_name AS customer,
p.name AS product
FROM customers c
CROSS JOIN products p -- 前面的用法是 FROM customers c,products p 这样的，但是最好用前面这种，清楚
ORDER BY c.first_name

```





#### 19.插入

```mysql
Insert INTO `database1`.`employee table`(
`employee id`,`first_name`,`last_name`,`age`) VALUES('104','DOE','Jane','30'),( );-- 可以插入多行！
```

注意哪几个符号的使用

```mysql
CREATE SCHEMA `database`
```

创建数据库



![image-20200326111417163](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200326111417163.png)

每次用完一个程序 这种大写的都要分号哈

![image-20200326112856343](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200326112856343.png)

![image-20200326113059946](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200326113059946.png)

增加一行代表的意思是

DECIMAL 代表一共几位数，小数点后几位

![image-20200326113420717](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200326113420717.png)

你也可以丢掉一列



![image-20200326114537743](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200326114537743.png)

如果有null

![image-20200326124404906](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200326124404906.png)

表示的意思是特别的，不能重复



像其他的一样，这个也可以有默认值，所以呢就

**``` INSERT INTO `student` VALUES(5,'Claire',default);**



#### 20.UPDATE

```mysql
UPDATE `student` 
SET major = 'Computer Science'
WHERE major = 'CS';
```

之前



alter都是修改属性的，这个可以修改内容 了



```mysql
UPDATE `student` 
SET major = 'Computer Science'
 -- 意思是所有人的major都是cs
```



```mysql
delete
实际上drop 也是指 属性的
delete 才是删掉内容
```





#### 21. UNION

```mysql
如何将行合并在一起，

SELECT 
	order_id,
    order_date,
    'Active' AS status -- 然后这个可以手动添加，之前还不咋知道
FROM orders
WHERE order_date >= '2019-01-01'
UNION
SELECT 
	order_id,
    order_date,
    'Archived' AS status
FROM orders
WHERE order_date < '2019-01-01'
-- 其实这个首先是选出上面的一部分，然后UNION 是作为拼接的，所以这种可以用作自定义排序里面



不同表的拼接
SELECT first_name
FROM customers
UNION 
SELECT name
FROM shippers 名字不一样也是ok的，以上面的为准
可以多个进行拼接 is ok

```



![image-20200327095944985](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200327095944985.png)

```mysql
那个AI 就是auto incremental
```



#### 22. LAST_INSERT_ID

```mysql
SELECT LAST_INSERT_ID
可以获得最近插入的id，注意，应该是一个主键，这时候应该是作为外键使用的。
这个有什么用呢？
因为有蛮多表格是联系在一起的，也算是父类与子类所以的话
在某一个表格增加了一个值，那对应另外一个表格也要增加一个值，所以的话，就用到了，不用再去看多麻烦啊


```

![image-20200327175547438](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200327175547438.png)

![image-20200327175625397](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200327175625397.png)

![image-20200327175639893](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200327175639893.png)

这时候插进去的反而是一个11，不是这个customer_id



#### 23. copy data

这里直接是创建一个table copy data 的

![image-20200327180728607](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200327180728607.png)

```mysql
你可以创一个table copy 另外table的值，
CREATE TABLE orders_archived AS
 SELECT * FROM orders;
 
 CREATE TABLE 和SELECT 结合在一起
 问题是copy 后的表是没有主键 也没有 AI 的所以要注意啦
```

Insert data 批量来的

```mysql
 INSERT INTO orders_archived
 SELECT *
 FROM orders
 WHERE order_date < '2019-01=01'
```

我以为肯恩更需要AS 像上面一样 然后好像不用，其实上面也可以不用，刚刚试了一下，但最好要，表示这里和select 是区分开来的

> 在项目中时，把审核好的用户插入到用户表中就可以进行，就你不用再取出来了，你只需要copy data 就可以 了

#### 24. 清空表格

直接找到table 右键  

truncate ok 就好了 没别的事情



#### 25. trigger

```mysql
DELIMITER $$
CREATE 
	TRIGGER my_trigger BEFORE  INSERT
    ON student 
    FOR EACH ROW BEGIN
	INSERT INTO trigger_test VALUES('add new student');
	END$$
DELIMITER ; -- 改变终止符的意思啦
有什么用呢，感觉像是个消息提醒吧，每当你insert 进去 ，都会trigger 'add new student'出来，算是一种记录吧，但是为什么要 delimiter 因为上面需要一个;  然后你要在下面改变终止符的符号
```

![image-20200328093147485](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200328093147485.png)



![image-20200328093229015](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200328093229015.png)

要在这里进行哈，因为在work bench 里面改变并不了 DELIMITER

##### 2.你可以看下

```mysql
你说我不想只加 'add messages '，我想有对应的，就是把修改的人民加进去 那怎么搞，
NEW.name ok
表示最新插入进去的哪一行对应的名字

DELIMITER $$
CREATE 
	TRIGGER my_trigger_1 BEFORE  INSERT
    ON student 
    FOR EACH ROW BEGIN INSERT INTO trigger_test VALUES(NEW.name);
	END$$
DELIMITER ;
如果前面有Trigger 的话会叠加在一起
```



#### 26. AGGREGATE FUNCTION

总数的function

only include non null value，duplicate 

```mysql
SELECT MAX(invoice_total) AS highest,
	MIN(invoice_total) AS lowest,
    AVG(invoice_total) AS average,
    SUM(invoice_total) AS total,
    COUNT(invoice_total) AS number_of_invoices
        COUNT(payment_date) AS count_of_payments,
    COUNT(*) AS total_records -- 这个算的是total 的table 里面的行,如果没有限制的话
FROM invoices
```

![image-20200328112815009](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200328112815009.png)

![image-20200328113044180](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200328113044180.png)

还可以限制条件 在里面搞expression 也可以，duplicate

```mysql
SELECT 
	client_id,
    SUM(invoice_total) AS total_sales,
    count(*) AS number_of_invoices -- 这个到底是什么？看下面怎么跟不一样的？
    实际上是符合 having 的条件后去计算的，对应的你一个client 开了多少条发票
    FROM invoices
    GROUP BY client_id
    having total_sales > 500;
```

![image-20200328125935773](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200328125935773.png)

与其他的进行合并

```mysql
SELECT 
	'First half of 2019' AS date_range,
    SUM(invoice_total) AS total_sales,
    SUM(payment_total) AS total_payments,
    SUM(invoice_total - payment_total) AS what_we_expected
    FROM invoices
    WHERE invoice_date BETWEEN '2019-01-01' AND '2019-06-30'
UNION
SELECT 
	'SECOND half of 2019' AS date_range,
    SUM(invoice_total) AS total_sales,
    SUM(payment_total) AS total_payments,
    SUM(invoice_total - payment_total) AS what_we_expected
    FROM invoices
    WHERE invoice_date BETWEEN '2019-07-01' AND '2019-12-31'
    
```

![image-20200328114358002](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200328114358002.png)

加一行。怎么加之前也有加过，但是有点忘记了



###### 1. aggregate 好像里面只允许用 sum 啥的，如果你要加一个别的东西，要用group by

```mysql
SELECT 
	client_id,
    SUM(invoice_total) AS total_sales
    FROM invoices
    GROUP BY client_id
	ORDER BY total_sales DESC
```

![image-20200328120720976](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200328120720976.png)

###### 2.join

```mysql
SELECT 
	p.date AS date,
    pm.name AS payment_method,
    SUM(amount) AS total_payments
    FROM payments p
    JOIN payment_methods pm
    ON p.payment_method = pm.payment_method_id
    group by date,payment_method
    ORDER BY date;
```



```mysql
SELECT 
	client_id,
    SUM(invoice_total) AS total_sales
    FROM invoices
     WHERE client_id >2
    GROUP BY client_id -- 说明这个group 原来是client——id 所在的地方
    被group 的是 aggregate 
    
    ？？如果你想要total_sales 用where 限制呢？ 你的where 是在from 后面的，但是你现在又在from的前面，所以你限制不了啊，怎么办。看接下来的have
```

![image-20200328123724153](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200328123724153.png)



###### 3. having

相当于where 的作用，但是where 要在from 后面，group 前面，那这时候就产生了一个新的关键词

having

```mysql
SELECT 
	client_id,
    SUM(invoice_total) AS total_sales
    FROM invoices
    GROUP BY client_id
    having total_sales > 500;
   -- HAVING name Like 'b%'  可不可以，不行，having 只能对select进行限制，因为这个表 是合成的，与原表无关，但是where 不一样，where 可以是原表的
```



###### 4.rollup

```mysql
SELECT 
	state,
    city,
	SUM(invoice_total) AS total_sales
    From invoices
    JOIN clients c USING(client_id)
    GROUP BY state,city WITH ROLLUP
    ;
```

![image-20200328133951952](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200328133951952.png)



可以对aggregate 的最后进行相加 很有趣把

##### ！！！注意一点，group 里面不能用别名

```mysql
 SELECT
	pm.name AS payment_method,
    SUM(amount) AS total
    FROM payments p
    JOIN payment_methods pm
    ON p.payment_method = pm.payment_method_id
    GROUP BY pm.name with rollup
```

这个才是可以的

#### 26. subqueries

其实这才是我们正常用到的情况，不是一上来就知道具体数据的

```mysql
SELECT *
FROM products
WHERE unit_price > (
	select unit_price
    FROM products
    WHERE product_id =3
) 
```



```mysql
-- 找没有被订购的物品，其实还可以用join，哪个更好嗯，子查询的话通常会把两个表合起来会有多余 的东西，前面的时候看要求，但是用子查询的话很有可能会变得复杂，所以还是要视情况而定
USE sql_store;
SELECT  *
FROM products
WHERE product_id NOT IN (
	SELECT DISTINCT product_id
    FROM order_items
)

SELECT 
customer_id,
first_name,
last_name
FROM customers
WHERE customer_id IN (
	SELECT customer_id
    FROM orders -- 其实这里可以用join
    WHERE order_id IN(
		SELECT order_id
        FROM order_items
        WHERE product_id =3
        )
    );

SELECT 
	customer_id,
    first_name,
    last_name
    FROM customers c
    JOIN orders o
    USING(customer_id)
	JOIN order_items
    USING(order_id)
    WHERE product_id =3

怎么说呢，你选择哪个，可能后面哪个更可读把
```



#### 27. ALL KEYWORD

![image-20200328162725809](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200328162725809.png)

差不多就是这个意思 了，当你被比较的有一堆数的时候，感觉和MAX 有点像呢，但是MAX 是用在select里面的好像哈，不过也可以有两种方法，一个是拿值与最大值比，一个是拿值与全部进行比，就是all，但是all 的话可以与table ，list 比较



#### 28: any keyword

```mysql
SELECT *
FROM clients
WHERE client_id IN(  -- where client_id = any() ok 都是意昂的
	SELECT client_id
    FROM invoices
    GROUP BY client_id
    HAVING COUNT(*) >=2  -- 所以这个count 代表又是什么，最终说一遍就是每一行出现的次数！！！！
)
```



#### 29. correlation

??? 就很懵逼

```mysql
SELECT *
FROM employees e
WHERE salary > (
	SELECT AVG(salary)
    FROM employees
    WHERE office_id = e.office_id  这个实在搞啥， 可以执行多行
)
```



![image-20200329010310076](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200329010310076.png)



![image-20200329010316919](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200329010316919.png)



![image-20200329010331117](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200329010331117.png)





#### 30. 刚刚搞的有点久是因为 exist 的关系， exist 和in的区别



![image-20200329100313898](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200329100313898.png)

这个实际上也用到了correlated subquery

主要的区别是，比较的内容， 像老师和学生进行比较，如果一个老师教好多学生，有些老师可能不教，那你要找出教了学生的老师怎么找，如果用in的话就直接是把学生对应的老师id 列出来，然后把老师的id 去里面一个个比对，这样的话就很慢，当你面对一大堆数据的时候，那你用exist的好处是比较的对象改变了，

为什么呢，你看上面，先执行括号里的东西， 其实括号里的select 没有什么用处，因为最后return 的是true or false， 从学生的角度去找，到老师的数据里面找，这时候找的就是老师的个数了，这明显是比学生小的，所以呢，就这样吧，然后exist 还可以比对空值，你应该知道的，因为in 的话有涉及一个中间过程，可能有些东西没有id，但是你的条件又符合，所以不可以哈



Exist的话实际上是因为select那里减少时间的，因为select那里这里对应的是老师，本来就是少的地方，每个老师的返回是正确或错误，所以的话就是这样减少时间的哈

```mysql
SELECT *
FROM products p
WHERE not EXISTS(
	SELECT product_id 
    FROM order_items
    WHERE product_id = p.product_id
)
```





#### 31. select in subquery

```mysql
SELECT 
	invoice_id,
    invoice_total,
    (SELECT AVG(invoice_total)
    FROM invoices) AS invoice_average,
      invoice_total - (SELECT invoice_average) AS difference
FROM invoices
```

就是select 在里面咯，但是呢，记住不可以直接用名字，会报错的，所以要select invoice_average

```mysql
SELECT 
	client_id,
    name,
    (SELECT SUM(invoice_total)
    FROM invoices
    WHERE client_id = c.client_id) AS total_sales,
    (SELECT AVG(invoice_total) FROM invoices) AS average,
    (SELECT total_sales - average)
    FROM clients c
```

看看这个很有趣的东西，当你想与另外的表连起来，得到另外的表中的AVG 时，你要怎么做，我暂时是不知道其他的，join啥的不会，只好这样，因为这样的话你可以对应(比如说一个人有多笔订单，你就可以在这堆订单中找到对应该人数值的平均值)，很好用，**而且提醒一点，你自己重新得到的AVG 是不可以直接用的，为啥，直接用的话之前有一个例子是大家都得是相同的，但是实际上大家不是，各有各的avg，而且要注意from，你直接用就代表的column 是来自对应table的，但实际上是自己新建出来的**





#### 32. round()，ceiling,florr,truncate,ABS

```mysql
   select round(2.73,1) -- 保留小数点后一位，四舍五入数字
 
      select TRUNCATE(3.2,1) --3.2 为啥，这是只保留小数点后一位，然后其他全部remove的
      select Ceiling(3.2)
      select FLOOR(3.2)
      select ABS(-3.2)
         select RAND() -- 产生[0,1]的float
         SELECT LENGTH('SKY');  长度3
		SELECT LOWER('SKY') -- sky
		SELECT LTRIM('       sky'); -- sky sure have RTRIM trim  any
		SELECT LEFT('KINDERGATEN',4) --KIND 表示输出左边几个数字
		SELECT SUBSTRING('KINDERGATEN',4,4) -- DERG 表示从第四个开始，输出四个字符
		-- 最后一个可以忽略，然后就是从第四个开始后面的全部 了
		SELECT LOCATE('n','Kindergarten') -- 3 找出n的位置
		SELECT REPLACE('kindergarten','garten','garden')-- kindergarden
		select CONCAT('FIRST','LAST') --FIRSTLAST combine to 1 string -- '' 表示文本，大家都一样的
select 
	concat(first_name,' ',last_name) AS name, -- 一般来说要这样子
    IFNULL(phone , 'Unknown') AS phone
from customers
```





#### 33. DATE FUNCTION

```MYSQL
SELECT NOW(),curdate(),curtime();
```

![image-20200330132901725](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330132901725.png)

对应的精确时间，精确日期，和时间

```MYSQL
SELECT MONTH(NOW());
```

![image-20200330133043555](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330133043555.png)

这算是extract 出来的意思 没错了，YEAR ,DAY 都ok把,HOUR,MIN,SEC

```mysql
SELECT DAYNAME(NOW());
```

![image-20200330133301735](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330133301735.png)

变成了一个String了

```mysql
SELECT * 
FROM orders
WHERE YEAR(order_date) = Year(NOW()) 判断是否一个年的

select date_format(NOW(),'%y')  小写的话对于年代表 20(指的是后面的那个)，大写代表2020
select date_format(NOW(),'%M %D %Y')
select date_format(NOW(),'%H:%i')
```

![image-20200330135035526](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330135035526.png)

![image-20200330135124888](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330135124888.png)

这样你就可以输出一些人性化的东西了，可以只要求hour 和min 这些都是可以的，大写小写可能会有所不同，所以要注意一下



```MYSQL
SELECT DATE_ADD(NOW(),INTERVAL 1 DAY) -- 可以进行加减了！！
SELECT DATE_sub(NOW(),INTERVAL 1 HOUR)
SELECT datediff('2019-01-05','2019-01-02') -- 只能减day 顺序跟平常减的顺序是一样的
select time_to_sec('09:03') -  TIME_TO_sec('09:02') 减秒

```

![image-20200330135455566](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330135455566.png)



#### 34. ifnull coalesce

```mysql
SELECT
	order_id,
    IFNULL(shipper_id, 'NOT ASSIGNED') AS shipper
    FROM orders
啥意思，就是把空值代替一下，说明一下
```

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330140236432.png" alt="image-20200330140236432" style="zoom:50%;" />

```mysql
SELECT
	order_id,
    COALESCE(shipper_id,comments, 'NOT ASSIGNED') AS shipper
    FROM orders
```

![image-20200330140610303](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200330140610303.png)

这个可以有多重保障(感觉很实用)，如果shipper_id 没有， 看看有没有comment(说明情况)，如果没有，还可以继续往下，然后把有的放到shipper 里面，这个真的有趣

#### 35. if statement

```mysql
SELECT 
	order_id,
    order_date,
    IF(
		YEAR(order_date) = 2019, -- 条件
        'Active', -- true
        'Archived' -- false
    ) AS year
    From orders
```



#### 36. case

```mysql

    SELECT 
		order_id,
        CASE
			WHEN YEAR(order_date) = YEAR(NOW())-1 THEN 'Active'
            WHEN YEAR(order_date) = YEAR(NOW())-2 THEN 'LAST YEAR'
            WHEN YEAR(order_date) < YEAR(NOW())-3 THEN 'Archived'
            ELSE 'Future'
		END AS category -- 不同点是有when then end
	FROM orders
	
	
	SELECT 
		order_id,
        CASE
			WHEN YEAR(order_date) = YEAR(NOW())-1 THEN 'Active'
            WHEN YEAR(order_date) = YEAR(NOW())-2 THEN 'LAST YEAR'
            WHEN YEAR(order_date) < YEAR(NOW())-3 THEN 'Archived'
            ELSE 'Future'
		END AS category
	FROM orders;跟之前的 相比，不用 UNION 进行拼接 会好很多
```



#### 37. view

```mysql
CREATE VIEW BALANCE AS -- or replace  这个的作用是什么，实际上是如果没有的话就建，有的话就replace
SELECT 
	client_id,
    name,
    (SELECT SUM(invoice_total - payment_total) 
		FROM invoices
		WHERE clients.client_id = invoices.client_id
     )AS balance
    from clients 
   
```

what is thats exactly

其实你的很多表是分开的，你每次想去合并看一个表的话每次都要重写就很麻烦，所以你可以创建一个 view 来让别人看到你的表，其实你也给可以更改一个表，他对应的真实的表也会改变的 ？？ 存疑不确定 我自己搞了一个会变的



然后呢 update delete 啥的差不多都是相同的

emem好像懂了，updatable view 实际上指的是可以对原表进行修改说明你的view 有很多限制，你可以加一列啥的在原基础的，等会也会改啊？

那到底要这个updated 的表干啥子哦？？？

![image-20200331135243187](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331135243187.png)

![image-20200331135248539](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200331135248539.png)

这里是限制哈





##### with check option?

实际上你insert 或update 的时候一些会没有，而且插不进去 check opTION

的话用在如果插入不进去的话就不让你搞

1. 提高了重用性，就像一个函数。如果要频繁获取user的name和goods的name。就应该使用以下sql语言。
2. 对数据库重构，却不影响程序的运行。
3. 提高了安全性能。可以对不同的用户，设定不同的视图。



#### 38. procedure

我现在还是没那个搞清楚这个和view 之间到底有什么关系哈，无语

都是可以加密嘛，限制访问嘛，然后呢？

反正这里用到了DELIMITER

```mysql
DELIMITER $$
CREATE PROCEDURE get_clients()
begin 
SELECT * FROM clients;
END $$
DELIMITER ;

call sql_invoicing.get_clients();
DROP PROCEDURE IF EXISTS get_clients 这样就不会出现error 虽然我也不知道有啥用哈
```

简单来create 不想用上面的话可以直接点右键 create store procedure then you're done

```mysql
DELIMiTER $$
CREATE PROCEDURE get_clients_by_state (state CHAR(2))
BEGIN
SELECT *
FROM clients c
WHERE c.state = state;
END$$
DELIMITER ;

call get_clients_by_state('CA');
```

有parameter 的，有什么用的呢，感觉像函数诶，这其实可以不用写sql code 在java里面但是到底怎么用我还不咋知道



可以

可以有default 值的，一般是在无法识别的情况(NULL)，不是说有值不存在的情况

```mysql
DROP Procedure  get_clients_by_state;  -- 如何drop
DELIMiTER $$
CREATE PROCEDURE get_clients_by_state (state CHAR(2))
BEGIN
IF state IS NULL THEN
	SET state = 'CA'; --这里就是了
    END IF;
SELECT *
FROM clients c
WHERE c.state = state;
END$$
DELIMITER ;

call get_clients_by_state(NULL);
```

```mysql
CREATE PROCEDURE get_clients_by_state (state CHAR(2))
BEGIN
SELECT *
FROM clients c
WHERE c.state = IFNULL(state,c.state);
END$$
DELIMITER ;
这个是什么意思呢，就是如果为NULL，的话就直接把整个表扔给你哈
```

