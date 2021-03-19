## 1. String的特性

- `String` 是一个`final`类，不可再继承，代表不可变的字符序列。
- 字符串是常量，用双引号表示。他们的值在创建之后不能更改。
- `String`对象的字符内容是存储在一个数组的`byte value[]`中的

```java
/**
 * String:字符串，用一对"”表示
 * 1.String声明为final的，不可被继承
 * 2.String实现了Serializable接口：表示字符串是支持序列化的
 *          实现了Comparable接口，表示String是可以比大小的
 * 3.String内部定义了final byte[] value用于存储字符串数据
 * 4.String：代表不可变的字符序列，简称：不可变性
 *          体现：1.当对字符串重新赋值时，需要重新指定内存区域赋值，不能使用原有的value及进行赋值
 *               2.当对现有字符串及进行连接操作时，也需要重新指定内存区域赋值，不能使用原有的区域
 *               3.当调用String的replace()方法修改指定字符和字符串时，也需要重新指定内存区域赋值。
 * 5.通过字面量的方式(区别于new)给一个字符串赋值，此时的字符串值声明在字符串常量池中
 * 6.字符串常量池是不会有存储相同内容的字符串的
 */
public class Test1 {
    @Test
    public void test1(){
        //字面量
        String s1 = "abc";
        String s2 = "abc";
//        s1 = "hello";

        //比较s1和s2地址值
        System.out.println(s1 == s2);

        System.out.println(s1);
        System.out.println(s2);

        System.out.println("*****************");

        String s3 = "abc";
        s3 += "def";
        System.out.println(s3);
        System.out.println(s2);

        System.out.println("******************");

        String s4 = "abc";
        String s5 = s4.replace('a', 'm');
        System.out.println(s4);
        System.out.println(s5);
    }
}
```



![image-20200727105030230](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200727105030230.png)

> 1. 字符串常量池在方法区当中
> 2. 当没有`abc`的时候会新开辟一个地址存abc，有的话就直接用

**所以不可变性是什么？**

> 指的是不可以在原有的数组value上重新赋值，因为你也已经规定好了(根据final)，你这个数组有多少格，所以接下来就是重新开辟一块区域来
>
> 总的来说就是不能修改







![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200727111557503.png)

![image-20200727111029492](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200727111029492.png)

> 对于`new String("abc"); ` 这种地址值指向的是堆，那堆中的存的又是什么？是方法区常量池那块区域的地址

## 2. String之间相加的问题

```java
public void test3(){
        String s1 = "javaEE";
        String s2 = "hadoop";

        String s3 = "javaEEhadoop";
        String s4 = "javaEE" + "hadoop";
        String s5 = s1 + "hadoop";
        String s6 = "hadoop" + s2;

        System.out.println(s3 == s4);//true
        System.out.println(s3 == s5);//false
        System.out.println(s3 == s6);//false
        System.out.println(s5 == s6);//false
		
      	String s8 = s5.intern();
        System.out.println(s3 == s8);//true
    }
```

> 为什么是false？
>
> 对于上述情况，拼接时需要额外创建一个`StringBuffer（或StringBuilder），之后将StringBuffer`转换为String,在此处new了一个对象，因此实在堆区中进行的

> 结论：
>
> 1. 常量于常量的拼接结果在常量池。且常量池中不会存在相同内容的常量
> 2. 只要其中有一个是变量，结果就在堆中
> 3. 如果拼接的结果调用`intern()`方法，返回值就在常量池中

### 与String 有关的一道面试题

```java
public class Test7{
    String str = new String("good");
    public void change(String str){
        String string = "good";
        str = "test ok";
        System.out.println(str);
    }

    public static void main(String[] args) {
        Test7 ex = new Test7();
        ex.change(ex.str);
        String string = "good";
        System.out.println(ex.str);//输出的是什么？
    }
}
```

答案是：`good`

> 首先有一点需要知道
>
> 基本数据类型传参--传的是**常量在常量池中的地址**
>
> 引用数据类型传参--传的是**对象在堆内存中的地址**

还有

```java
 @Test
    public void test6(){
        String str = new String("hello");
        String str1 = "world";
        System.out.println(str == str1);//false
        str = "world";
        System.out.println(str1 == str);//true
        System.out.println(str);
    }
//这意味着先new后再重新赋值，这时候str储存的是常量池里面的地址，相当于new就没有了。
```

> 所以上面相当于放了一个地址进去，然后他们把这个地址抛弃了，但我输出的时候还是以该地址指向的值来输出，所以没有变化。

### JVM?

![image-20200727160958251](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200727160958251.png)

我了解到有几个路程 方法区(永久代)->堆->方法区(元空间) 1.6->1.7->1.8

### String常用方法

![image-20200727165034645](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200727165034645.png)

```java
@Test
    public void test1(){
        String s1 = "helloWorld";
        System.out.println(s1.length());
        System.out.println(s1.charAt(0));
        System.out.println(s1.charAt(9));
        System.out.println(s1.isEmpty());

        String s2 = s1.toLowerCase();
        System.out.println(s1);//s1不可以变，仍然为原来的情况
        System.out.println(s2);//改为全部小写

        String s3 = "he llo world";
        String s4 = s3.trim();
        System.out.println("------"+s3 + "-------");
        System.out.println(s4);

        String s5 = "abc";
        String s6 = "abe";
        System.out.println(s5.compareTo(s6));//-2,一个个去比，不过c和e差了俩，所以呢就是-2
        //涉及到字符串排序

        String s7 = "北京尚硅谷教育";
        String s8 = s7.substring(2);
        System.out.println(s8);
        //尚硅谷教育

        String s9 = s7.substring(2, 5);
        //左闭右开，尚硅谷
    }
```

![image-20200727165100130](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200727165100130.png)

![image-20200727170239620](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200727170239620.png)

分为以下三种：替换，匹配，切片

![image-20200727171044337](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200727171044337.png)

![image-20200727171221363](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200727171221363.png)

```java
@Test
    public void test3(){
        //原有的不会改变
        String str1 = "北京尚硅谷教育北京";
        //东京尚硅谷教育东京
        String str2 = str1.replace('北', '东');
    }
```

![image-20200727171637537](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200727171637537.png)

#### String 与 char[]之间的转换

```java
/**
     * String 与 char[]之间的转换
     * String --> char[] ：调用String 的toCharArray方法
     * char[] --> String : 调用String 的构造器
     */
    @Test
    public void test4(){
    String str1 = "abc123";
        char[] chars = str1.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            System.out.println(chars[i]);
        }

        char[] arr = new char[]{'h','e','l','l','o'};
        String s1 = new String(arr);
        System.out.println(arr);
    }
```

#### String 与 byte[]之间的转换

```java
 /**
     * String 与 byte[] 之间的转换
     * 编码： String-> byte[]：调用String的getBytes()
     * 解码： byte[] --> String：调用String的构造器
     *
     * 编码： 字符串 --> 字节(看得懂--> 看不懂)
     * 解码： 编码的逆过程 字节 --> 字符串 (看不懂的二进制数据--> 看得懂)
     * 说明： 解码时，要求解码使用的字符集必须与编码时使用的字符集一致，否则会出现乱码。
     * @throws UnsupportedEncodingException
     */
    @Test
    public void test5() throws UnsupportedEncodingException {
    String str1 = "abc123中国";
    byte[] bytes = str1.getBytes();//使用默认的字符集，进行转换
        System.out.println(Arrays.toString(bytes));

        byte[] gbks = str1.getBytes("gbk");//使用gbk编码集进行编码
        System.out.println(Arrays.toString(gbks));

        String str2 = new String(bytes);//使用默认的字符集，进行解码
        System.out.println(str2);

        String str3 = new String(gbks);
        System.out.println(str3);//出现乱码，原因：编码集和解码集不一致

        String str4 = new String(gbks, "gbk");
        System.out.println(str4);//没有出现乱码，原因：编码集和解码集一致
    }
```

![image-20200727221151841](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200727221151841.png)

#### +final后变true 的问题

![image-20200727221930228](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200727221930228.png)

加上final后实际就变为常量了 

## 3. `String` `StringBuilder` 和 `StringBuffer`的异同

```java
 /*    String、StringBuffer、StringBuilder三者异同
        String：不可变的字符序列 底层使用char[]存储(现在的jdk应该改成byte[]了)
        StringBuffer：可变的字符序列；线程安全，效率低，`StringBuffer 默认创建一个 长度为16的数组
        StringBuilder：jdk5.0新增的 可变的字符序列;线程不安全的，效率高 `StringBuilder	 默认创建一个 长度为16的数组
     */
@Test
    public void test() {
        StringBuffer sb1 = new StringBuffer("abc");
        sb1.setCharAt(0,'m');//返回值为空，所以不是重新再把值赋给一个新的，直接自己就改变了
        System.out.println(sb1);//mbc
        // 所以猜猜，刚开始的数组长度不是固定的把？
    }
```



 ![image-20200728091421397](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200728091421397.png)

> `StringBuffer 和 StringBuilder`都是默认创建一个 长度为16的数组
>
> 如果不是空的话，再在额外多个16

![image-20200728091833553](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200728091833553.png)

> 注意这里的再多16是指你在构造器中输值的基础上，所以当你直接append的话就不算了

```java
//源码分析:
String str = new String();//byte[] value = new byte[16];
String str1 = new String("abc");// byte[] value = new byte[]{'a','b','c'}

StringBuffer sb1 = new StringBuffer();//byte[] value = new byte[16];
sb1.append('a');//value[0] = 'a';
sb1.append('b');//value[1] = 'b';

StringBuffer sb2 = new StringBuffer();
System.out.println(sb2.length());//多少？ 0 or 16 当然是0，这里的length()被重写了，和String的表示不一样，是计算append的数的
```

> 问题2：扩容问题: 如果要添加的数据底层数组盛不下了，那就需要扩容底层的数组
>
> 默认的情况下，扩容为原来容量的2倍+2，同时将原有数组中的元素赋值到新的数组中。
>
> 指导意义：开发中建议使用：`StringBuffer(int capacity)` builder也一样，不要让数组进行赋值，效率不高

#### StringBuffer 的常用方法

![image-20200728095257037](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200728095257037.png)

![image-20200728095244198](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200728095244198.png)

> 总结：
>
> - 增：`append(xxx)`
>
> - 删：`delete(int start, int end)`
> - 改：`setCharAt(int n, char ch)/replace(int start,int end,String str)`
> - 查：`charAt(int n)`
> - 插：`insert(int offset,xxx)`
> - 长度：`length()`
> - 遍历:`for() + charAt()`/`toString()`
>
> `StringBuilder`也差不多是这些方法

**对比String、`StringBuilder` 和 `StringBuffer`三者的效率:**

从高到低排列：`StringBuilder` > `StringBuffer` > `String`

## 日期和时间的API

![image-20200728102451830](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200728102451830.png)

```java

/**
 * java.util.Date类
 *        --- java.sql.Date类
 * 1. 两个构造器的使用
 *      > 构造器一：Date()：创建一个对应当前时间的Date对象
 *      >构造器二：创建指定毫秒数的Date对象
 * 2.两个方法的使用
 *      >toString():显示当前的年、月、日、时、分、秒
 *      >getTime():获取当前Date对象对应的毫秒数(时间戳)
 */
public class DateTest {

    @Test
    public void test(){
        //构造器一：Date()：创建一个对应当前时间的Date对象
        Date date1 = new Date();
        //Tue Jul 28 10:30:11 CST 2020
        System.out.println(date1.toString());

        //1595903411149 毫秒数，与currentTimeMillis()那个差不多
        System.out.println(date1.getTime());

        //构造器二：创建指定毫秒数的Date对象
        Date date2 = new Date(1595903411149L);
        //Tue Jul 28 10:30:11 CST 2020
        System.out.println(date2);

        //如何将java.util.Date对象转换为java.sql.Date对象，前者是父类，后者是子类，数据库时需要用到
        //情况1：
        Date date4 = new java.sql.Date(2323232332L);
        java.sql.Date date5 = (java.sql.Date) date4;

        //情况二：
        Date date6 = new Date();
//        java.sql.Date date7 = (java.sql.Date) date6;,这个可以吗？不行啊，运行的时候是会报错的，回忆一下，比如一个Person转成Student，你的属性都不一样，怎么强转啊
        //正确操作
        java.sql.Date date7 = new java.sql.Date(date6.getTime());//直接按毫秒来就好啦
    }
}

```

## 4. String 的常见算法题目

```java
public class StringDemo {

    /**
     * 将一个字符串进行反转。将字符串中指定部分进行反转。如"abcdefg"反转为"abfdcg"
     * <p>
     * 这是我写的
     */
    public String reverse(String str, int startIndex, int endIndex) {
        String sub = str.substring(startIndex, endIndex + 1);
        System.out.println(sub);
        char[] arr = str.toCharArray();
        for (int i = startIndex; i < endIndex; i++) {
            char c = arr[endIndex - (i - startIndex)];
            arr[endIndex - (i - startIndex)] = arr[i];
            arr[i] = c;
        }
        System.out.println(arr);
        return null;
    }

    @Test
    public void test1() {
        String str = "abcdefg";
        reverse(str, 2, 5);

    }
    /**
     * 这是视频里写的
     * 方式一：转换为char[]
     */
    public String reverse2(String str, int startIndex, int endIndex) {
        if (str != null) {
            char[] arr = str.toCharArray();
            for (int x = startIndex, y = endIndex; x < y; x++, y--) {
                char temp = arr[x];
                arr[x] = arr[y];
                arr[y] = temp;
            }
            return new String(arr);
        }
        return null;
    }
    /**
     * 方式二：使用String的拼接
     * 感觉跟我写的有点像，但不同的地方在于我没有拆开来
     */
    public String reverse3(String str, int startIndex, int endIndex) {
        if (str != null) {
            //第一部分
            String reverseStr = str.substring(0, startIndex);
            //第二部分
            for (int i = endIndex; i >= startIndex; i--) {
                reverseStr += str.charAt(i);

            }
            //第三部分
            reverseStr += str.substring(endIndex + 1);

            return reverseStr;
        }
        return null;
    }
    /**
     * 方式二的迭代，更高效
     */
    //方式三：使用StringBuffer/StringBuilder替换String
    public String reverse4(String str,int startIndex,int endIndex) {
        if (str != null) {
            StringBuilder builder = new StringBuilder(str.length());
            //第一部分
            builder.append(str.substring(0, startIndex));
            //第二部分
            for (int i = endIndex; i >= startIndex; i--) {
                builder.append(str.charAt(i));
            }
            //第三部分
            builder.append(str.substring(endIndex + 1));

            return builder.toString();
        }
        return null;
    }
}
```

```java
/**
 * 获取一个字符串在另一个字符串中出现的次数
 * 比如： 获取"ab" 在"abkkcadkabkebfkabkskab"中出现的次数
 */
public class StringDemo2 {


    public int getCount(String mainStr, String subStr) {
        int mainLength = mainStr.length();
        int subLength = subStr.length();
        int count = 0;
        int index = 0;
        if(mainLength >= subLength){
//            方式一：
//            while((index = mainStr.indexOf(subStr)) != -1){
//                count ++;
//                mainStr = mainStr.substring(index + subStr.length());
//            }
//            方式二：对方式一的改进
            while ((index = mainStr.indexOf(subStr,index)) != -1){
                count ++;
                //但是有个问题，不能计算出重复的，aaa就是两个，你怎么搞？
                index +=subLength;
            }
            return count;
        }else {
            return 0;
        }
    }
}
```



![image-20200805132308293](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200805132308293.png)

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200805161918436.png)

![image-20200805162027467](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200805162027467.png)

```java
public class StringDemo3 {
    //前提：两个字符串中只有一个最大相同子串
    public String getMaxSameString(String str1,String str2){
        if(str1 != null && str2 != null) {
            String maxStr = (str1.length() >= str2.length()) ? str1 : str2;
            String minStr = (str1.length() < str2.length()) ? str1 : str2;
            int length = minStr.length();

            for (int i = 0; i < length; i++) {
                for (int x = 0, y = length - i; y <= length; x++, y++) {
                    String subStr = minStr.substring(x, y);
                    if (maxStr.contains(subStr)) {
                        return subStr;
                    }
                }
            }
        }
        return null;
    }
    @Test
    public void testGetMaxSameString(){
        String str1 = "abcwerthelloyuiodefabcdef";
        String str2 = "cvhellohnmabcde";
        String maxSameString = getMaxSameString(str1, str2);
        System.out.println(maxSameString);
    }
}
```

> 讲讲这道题的思路，感觉效率还是不够，但暂且就这样子吧，他是怎么找的，有分长度小一点和长度大一点的，拿长度小的作为标准去比，就不断削小的，看长度大的是否包含，所以整个程序中长度大的是几乎不动的。
>
> 如何削长度小的呢？拿abc举例子，
>
> 首先是 abc->ab->bc->c，所以第二层for循环就是不断在往后移，举个更明显的例子吧，就是abcde 中已经被削去两个字母了 在第二层中表现为 abc ->bcd->cde 
>
> 我觉得我解释了差不多了，但是这个方法有一个缺点就是你只能有一个长度最大的，如果有多个的话参照上面截图的做法 

![image-20200807125405550](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200807125405550.png)

> 这个啥意思？怎么变成4了？ 还是要从源码看起
>
> 因为append的时候会判断是否为null，为null就appendnull 意思就是直接append  "null"，长度就变为4了，但是如果你直接在构造器里面放null的话，就会报空指针异常，因为会用到`str.length()`

![image-20200807125541072](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200807125541072.png)

![image-20200807125557839](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200807125557839.png)

![image-20200807125615370](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200807125615370.png)