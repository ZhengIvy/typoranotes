## 1.File类的使用

![image-20200728145417335](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200728145417335.png)

![image-20200728145704175](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200728145704175.png)

![image-20200728150202917](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200728150202917.png)

```java
/**
 * 1. File类的一个对象，代表一个文件或一个文件目录（俗称：文件夹）
 * 2. File类声明在java.io包下
 * 3. 路径分隔符
 *      windows:\\
 *      unix:/
 */
public class FileTest {
    /*
    *   1. 如何创建File类的实例
    *   File(String filePath)
    *   File(String parentPath,String childPath)
    *   File(File parentFile, String childPath)
    * 相对路径：相较于某个路径下，指明的路径。
    * 绝对路径：包含盘符在内的文件或文件目录的路径
    *
    *
     */
    @Test
    public void test1(){
        //构造器1
        File file1 = new File("hello.txt");//相对于当前module
        File file2 = new File("D:\\javathread\\he.txt");
       //hello.txt
        System.out.println(file1);
        //D:\javathread\he.txt
        System.out.println(file2);

        //构造器2
        File file3 = new File("D:\\","javathread");
        //D:\javathread,就相当于在文件夹里面选目录，感觉在需要选目录中可以用到
        System.out.println(file3);

        //构造器3
        File file4 = new File(file3,"hi.txt");
        System.out.println(file4);
    }
}

```

> File和我之前记住的有些偏差，因为我以为直接回创建文件的，但是并没有哈，这是第一点，然后直接输出file 返回的是文件的路径，第三点，还有一个是可以通过父子的路径进行操作，所以这里可以再展开两个，直接输入路径，或直接把file放进去，不过你看上面，是有一个顺序在里面，所以我们通常可以把要使用的路径直接file一下，如果需要在某路径下文件的话就可以直接输入路径就可以了

### File常用方法

![image-20200728162948038](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200728162948038.png)

```java
 @Test
    public void test2(){
        File file1 = new File("hhh.txt");
        File file2 = new File("D:\\javathread\\eee.txt");

        //D:\javathread\hhh.txt
        System.out.println(file1.getAbsoluteFile());
        //hhh.txt
        System.out.println(file1.getPath());
        //hhh.txt  这个是根据你自己输入的路径来看的
        System.out.println(file1.getName());
        //null 这也是同样，根据你输入的路径来看，因为是相对路径，所以无parent
        System.out.println(file1.getParent());
        //0
        System.out.println(file1.length());
        //0
        System.out.println(file1.lastModified());

        System.out.println();

        //D:\javathread\eee.txt
        System.out.println(file2.getAbsoluteFile());
        //D:\javathread\eee.txt
        System.out.println(file2.getPath());
        //eee.txt
        System.out.println(file2.getName());
        //D:\javathread
        System.out.println(file2.getParent());
        //0
        System.out.println(file2.length());
        //0
        System.out.println(file2.lastModified());
    }

    @Test
    public void test3(){
        File file = new File("D:\\javathread");
        String[] list = file.list();
        //输出的是相对路径
        //.idea
        //out
        //src
        //thread1.iml
        for (String s: list
             ) {
            System.out.println(s);
        }
        System.out.println();
        File[] files = file.listFiles();
        //输出的是绝对路径
        //D:\javathread\.idea
        //D:\javathread\out
        //D:\javathread\src
        //D:\javathread\thread1.iml
        for (File f: files
             ) {
            System.out.println(f);
        }
    }

    /**
     * public boolean renameTo(File dest):把文件重命名为指定的文件路径
     *  比如：file1.renameTo(file2)为例：
     *      要想保住返回true、需要file1在硬盘中是存在的，且file2不能再硬盘中存在。
     *      相当于移动 + 改名
     */
        @Test
        public void test4(){
            File file1 = new File("hello.txt");
            File file2 = new File("D:\\javathread\\hi.txt");

            boolean renameTo = file1.renameTo(file2);
            System.out.println(renameTo);
        }
}

```

![image-20200729092044912](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200729092044912.png)

![image-20200729092509406](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200729092509406.png)

```java
/**
     * File类的一个对象，代表一个文件或文件目录(俗称文件夹)
     * 2.File类声明在java.io包下
     * 3.File类涉及到关于文件或文件目录的创建、删除、重命名、修改时间、文件大小等方法
     *  并未涉及到写入或读取文件内容的操作。如果需要读取或写入文件内容，必须使用IO流来完成。
     * 4.后续File类的对象常会作为参数传递到流的构造器中，指明读取或写入的“终点”
     */
        @Test
        public void test6(){
            File file1 = new File("hello.txt");

            System.out.println(file1.isDirectory());
            System.out.println(file1.isFile());
            System.out.println(file1.exists());
            System.out.println(file1.canRead());
            System.out.println(file1.canWrite());
            System.out.println(file1.isHidden());


        }

        @Test
        public void test7() throws IOException {
            File file1 = new File("hi.txt");
             if(!file1.exists()){
                 file1.createNewFile();
                 System.out.println("创建成功");
             }else{
                 file1.delete();
                 System.out.println("删除成功");
             }


        }

        @Test
        public void test8(){
            //文件目录的创建
            File file1 = new File("d:\\javathread\\io1\\io3");

            boolean mkdir = file1.mkdir();
            if (mkdir){
                System.out.println("创建成功");
            }else{
                System.out.println("失败");
            }

            File file2 = new File("d:\\javathread\\io1\\io4");

            boolean mkdirs = file2.mkdirs();
            if (mkdirs){
                System.out.println("创建成功");
            }else{
                System.out.println("失败");
            }
        }
```

> 注意一下，`mkdir` 和 `mkdirs`的区别，后者是复数，就意味着可以一次性创建多个文件夹，所以呢就是如果你要创建某个目录，如果他的父目录不存在，后者就顺便帮你一起创建了，前者如果没有的话就拜拜了
>
> 2. 使用删的时候有一点跟cmd比较像，你要删一个文件夹的话那么他就得是空的， 。

## 2. IO流

### 流的分类

- 按操作 **数据单位** 不同分为： **字节流(8bit)，字符流(16bit)**，前者一般用于传输视频，图片等，后者则是文本
- 按数据流的流向不同分为：输入流、输出流
- 按流的角色不同分为：节点流，处理流

![image-20200729113221926](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200729113221926.png)

![image-20200729112728484](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200729112728484.png)

> 问题：处理流和节点流分别是什么？
>
> 节点流相当一个最基础的连接管道，然后处理流相当于一个buff，在基础管道之上再加一些处理的东西，比如加快啊速度啊啥的，就是图里面的橙色和黄色

![](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200729113344665.png)

比较需要关注的是蓝框的





![image-20200729115155971](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200729115155971.png)

注意下这个当前工程和Module，不然有可能找不到位置，前者对应的是那个`JavaSenior`，后者对应的是`day09`

####  关于异常

不要用throws，要用try catch finally，因为如果中间出现了问题，流被创建了，前者会导致流无法关闭，可能会导致泄露，所以的话就可以把流关闭的方法放到finally里面去

**这是最基本的，一般用的都是这么用的**

```java
/**
 * 一、流的分类：
 * 1.操作数据单位：字节流、字符流
 * 2.数据的流向：输入流、输出流
 * 3.流的角色：节点流、处理流
 *
 * 二、流的体系结构
 * 抽象基类            节点流（文件流）     缓冲流（处理流的一种）
 * InputStream        FileInputStream   BufferedInputStream
 * OutputStream       FileOutputStream  BufferedOutputStream
 * Reader             FileReader        BufferedReader
 * Writer             FileWriter        BufferedWriter
 */
public class FileReaderWriterTest {  
    @Test
    public void testFileReader()  {
        FileReader fr = null;
        try {
            //1.实例化File类的对象，指明要操作的文件
            File file = new File("hello.txt");
            //2.提供具体的流
            fr = new FileReader(file);

            //3.数据的读入
            //read():返回读入的一个字符。如果文件达到末尾，返回-1
            int data;
            while ((data= fr.read() )!= -1){
                System.out.print((char)data);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //4.流的关闭操作,必须的哈
            try {
                if (fr != null){
                    fr.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```



> 说明点：
>
> 1. `read()`的理解：返回读入的一个字符。如果达到文件的末尾，返回-1
> 2. 异常的处理：为了保证流资源一定可以执行关闭操作。需要使用 `try-catch-finally`处理
> 3. 读入的文件一定要存在，否则就会报`FileNotFoundException`

--------------------------------------------------------------------------2020.7.31 anki到这里，明天继续哈-----------------------------------------------------------------------------------------

#### read(char[] cbuf) 的难点与重点

```java
 //对read()操作升级：使用read的重载方法
    @Test
    public void test2() {
        FileReader fr = null;
        try {
            //1.File类的实例化
            File file = new File("hello.txt");
            //2.FileReader流的实例化
            fr = new FileReader(file);
            //3.读入的操作
            //read(char[] cbuf):返回每次读入cbuf数组中的字符的个数，如果达到文件末尾，返回-1 cbuf相当于是一个容器，放到构造器里面执行以下就装上去了
            char[] cbuf = new char[5];
            int len;
            while ((len=fr.read(cbuf))!= -1){
                //方式一：
                //错误写法：
//                for (int i = 0; i < cbuf.length; i++) {
//                    System.out.println(cbuf[i]);
//                }
                //正确写法
//                for (int i = 0; i < len; i++){
//                    System.out.println(cbuf[i]);
//                }

                //方式二：
                //错误的写法，对应着方式一的错误写法
//                String str = new String(cbuf);
//                System.out.println(str);
                //正确写法
                String str = new String(cbuf,0,len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //4.资源的关闭
            if(fr!= null){
                try {
                    fr.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }

        }

    }
```

> 说明一下，read()  的返回值是int，所以如果你只读一个的话，就得转成char类型先

![image-20200729163319622](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200729163319622.png)

> 如果你遍历的时候是 `i < cbuf.length 这种默认的话，那么就会出现如上情况，因为原理是覆盖掉，所以导致最后两个没有覆盖掉，一起输出了

####   FileWriter

```java
/**
     * 从内存中写出数据到硬盘的文件中
     *
     * 说明：
     * 1. 输出操作，对应的File可以不存在，不会报异常
     * 2.
     *      File对应的硬盘中的文件如果不存在，在输出的过程中，会自动创建此文件。
     *      File对应的硬盘中的文件如果存在：
     *             如果流使用的构造器是：FileWriter(file,false)/FileWriter(file):对原有文件的覆盖
     *             如果流使用的构造器是：FileWriter(file,true)就不会覆盖，而是append，拼接上去，应该是调用一次才覆盖哈，所以下面的两句话是不会进行覆盖的
     */
    @Test
    public void testFileWriter() throws IOException {
//        1.提供File类对象，指明写出到的文件
        File file = new File("hello1.txt");

        //2.提供FileWriter的对象，用于数据的写出
        FileWriter fw = new FileWriter(file,true);

        //3.写出的操作
        fw.write("I have a dream!\n");
        fw.write("you need to have a dream!");
        //4.流的关闭
        fw.close();
    }
```





#### 实现FileReader 和FileWriter 相当于复制

```java
 @Test
    public void testFileReaderFileWriter(){
        FileReader fr = null;
        FileWriter fw = null;
        try {
            //1.创建File类对象，指明读入和写出的文件
            //要求存在
            File scrFile = new File("hello.txt");
            //可以不存在
            File destFile = new File("hello2.txt");

            //2.创建流的对象，输入和输出
            fr = new FileReader(scrFile);
            fw = new FileWriter(destFile);
            //3.数据的读入和写出
            char[] cbuf = new char[5];
            //记录每次读入到cbuf数组中的字符个数
            int len;
            while ((len = fr.read(cbuf))!= -1){
                //每次写出len个字符
                fw.write(cbuf,0,len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {//4.关闭流资源
            try {
                if (fw!=null) {
                    fw.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                if(fr!= null) {
                    fr.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
```

> 感觉倒是差不多

### 字节流

> 首先要搞清楚一个点，字节流是以二进制进行编码的，而字符流是utf-8，因此呢，字节流在某种程度上也可以对文本上进行读取与写，但对于中文来讲，有可能会有乱码，也有可能不会。

```java
@Test
    public void testFileInputStream(){

        FileInputStream fis = null;
        try {
            File file = new File("hello.txt");

            fis = new FileInputStream(file);

            byte[] buffer = new byte[5];
            int len;
            while ((len = fis.read(buffer))!= -1){
                String str = new String(buffer,0,len);
                System.out.print(str);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fis!=null){

                try {
                    fis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
```

> 套路还是那4步，但是需要说的是为什么会出现中文乱码？
>
> 因为byte数组作为一个容器去读，你看上面的长度是5，也就是能储存5个字节，但是对于汉字来讲，通常是3个字节，就有可能存在一个汉字被劈成两半的情况。那为什么字符流那边不会呢？因为他不是根据一个字节一个字节来的，我猜的，是一个字符字符来的，'a','我‘，这样子，允许的字节长度是1~6个字节，所以的话中文基本上是不会乱码的。

#### 总结，字节流与字符流使用的格式操作：

1. 对于文本文件(`txt,java,c,cpp`),使用字符流处理
2. 对于非文本文件(`jpg,mp3,mp4,avi,doc,ppt,...`)使用字节流处理
3. 补充：根据下面复制视频和图片等的操作学到的东西：前面1,2得出的结论是在控制台中输出得来的，但并不影响复制。也就是可以使用字节流进行文本复制，尽管在控制台上面输出乱码，但问题不大，就主要是这点。但是，非文本文件还是不能使用字符流的哈，毕竟人家就是二进制。

#### 复制视频和图片等

```java
 @Test
    public void testFileInputOutputStream(){

        FileInputStream fis = null;
        FileOutputStream fos = null;
        try {
            File scrFile = new File("2019-07-24 192503.jpg");
            File destFile = new File("1.jpg");

            fis = new FileInputStream(scrFile);
            fos = new FileOutputStream(destFile);

            byte[] buffer = new byte[5];
            int len;
            while ((len = fis.read(buffer))!=-1){
                fos.write(buffer,0,len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if(fos!= null) {
                    fos.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                if(fis!=null) {
                    fis.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }


    }
    //指定路径下文件的复制
    public void copyFile(String scrPath,String destPath) {
        FileInputStream fis = null;
        FileOutputStream fos = null;
        try {
            //1.创建File类对象，指明读入和写出的文件
            File scrFile = new File(scrPath);
            File destFile = new File(destPath);

            //2.创建流的对象，输入和输出
            fis = new FileInputStream(scrFile);
            fos = new FileOutputStream(destFile);
            //3.数据的读入和写出
            byte[] buffer = new byte[3];
            //记录每次读入到cbuf数组中的字符个数
            int len;
            while ((len = fis.read(buffer)) != -1) {
                //每次写出len个字符
                String str = new String(buffer,0,len);
                System.out.println(str);
                fos.write(buffer, 0, len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {//4.关闭流资源
            try {
                if (fis != null) {
                    fis.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                if (fos != null) {
                    fos.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
    @Test
    public void testCopyFile(){
        long start = System.currentTimeMillis();
        String srcPath = "hello.txt";
        String destPath = "h2.txt";
        copyFile(srcPath,destPath);
        long end = System.currentTimeMillis();

        System.out.println("花费时间为" + (end-start));//4091
    }
```

> 基本上和之前的差不多，就是把他变成了个程序罢了。
>
> 但学到了一些别的东西，看上面的那个总结。

### 处理流之一：缓冲流

```java
/**
 * 处理流之一：缓冲流的使用
 *
 * 1.缓冲流：
 * BufferedInputStream
 * BufferedOutputStream
 * BufferedReader
 * BufferedWriter
 *
 * 2.作用：提高流的读取、写入的速度
 */
public class BufferTest {


    @Test
    public void test1(){
        BufferedInputStream bis = null;
        BufferedOutputStream bos = null;
        try {
            //1.造文件
            File srcFile = new File("1.jpg");
            File destFile = new File("2.jpg");
            //2.造流
            //2.1 造节点流
            FileInputStream fis = new FileInputStream(srcFile);
            FileOutputStream fos = new FileOutputStream(destFile);
            //2.2 造缓冲流,其实基本上就是多了这一步罢了
            bis = new BufferedInputStream(fis);
            bos = new BufferedOutputStream(fos);


            //3.复制的细节：读取、写入
            byte[] buffer = new byte[10];
            int len;
            while ((len=bis.read(buffer))!=-1){
                bos.write(buffer,0,len);
                
                bos.flush();//刷新缓冲区，本来是缓冲区有个规定的size，达到这个size就直接缓冲过去，但你调用这个方法则是尽管你没有达到size也可以缓冲。这个size呢，基本上是byte[x]里面x充当一个小水盆，把水装入一个nL的桶中，装够了nL以后就送到目的地去
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //4.资源关闭
            //要求：先关闭外层的流，再关闭内层的流
            if (bos!=null) {
                try {
                    bos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (bis!= null) {
                try {
                    bis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            //说明：关闭外层流的同时，内层流也会自动的关闭，我们可以省略
//        fos.close();
//        fis.close();
        }


    }
}

```

#### 插播一个小知识，什么是`^`?

![image-20200730102240278](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200730102240278.png)

`m^n^n = m`,这样可以实现加密操作

#### 课后小练习

![image-20200730102452646](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200730102452646.png)

![image-20200730103446271](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200730103446271.png)

![image-20200730103424991](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200730103424991.png)

### 处理流之二：转换流

> 转换流提供了在字节流和字符流之间的转换

![image-20200730122314864](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200730122314864.png)

```java
/**
 * 处理流之二：转换流的使用
 * 1. 转换流：属于字符流(看后面)
 *  InputStreamReader：将一个字节的输入流转换为字符的输入流
 *  OutputStreamWriter：将一个字符的输出流转换为字节的输出流
 * 2. 作用：提供字节流与字符流之间的转换
 *
 * 3.解码：字节、字节数组 --> 字符数组、字符串
 *    编码：字符数组、字符串 --> 字节、字节数组
 *
 * 4.字符集
 //用InputStreamReader 中解码设置字符集是哪种，根据啥？ 根据你这个文件存来的时候就使用什么字符集，如果解码的时候是另外一种的话就有可能会导致乱码
 */
public class InputStreamReaderTest {

    @Test
    public void test1(){

        InputStreamReader isr = null;
        try {
            FileInputStream fis = new FileInputStream("hello.txt");
//        InputStreamReader isr =new InputStreamReader(fis);//使用系统默认的字符集 utf-8
            //参数2指明了字符集，具体使用那个，取决于文件保存时使用的字符集
            isr = new InputStreamReader(fis,"UTF-8");

            char[] cbuf = new char[20];
            int len;
            while ((len = isr.read(cbuf))!= -1){
                String str = new String(cbuf,0,len);
                System.out.println(str);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (isr != null) {
                try {
                    isr.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

> 现在个人理解的作用是可以在控制台输出了，如果你要使用字节流进行复制的话，但没明白为什么要这样多此一举，好像可以指定字符集,感觉是这样子的

```java
//综合使用，用utf-8进行读，用gbk格式进行写哈 
@Test
    public void test2(){
        InputStreamReader isr = null;
        OutputStreamWriter osw = null;
        try {
            File file1 = new File("hello.txt");
            File file2 = new File("hhh.txt");

            FileInputStream fis = new FileInputStream(file1);
            FileOutputStream fos = new FileOutputStream(file2);

            isr = new InputStreamReader(fis,"utf-8");
            osw = new OutputStreamWriter(fos,"gbk");

            char[] cbuf = new char[20];
            int len;
            while ((len = isr.read(cbuf))!= -1){
                osw.write(cbuf,0,len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(isr != null) {
                try {
                    isr.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(osw != null) {
                try {
                    osw.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
```

#### 多种字符编码集的说明

![image-20200730163425342](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200730163425342.png)

> 补充下： `ASCII` 用1个字节就ok了， 刚好2的七次方是128，刚好
>
> `ISO8859-1`：拉丁码表，欧洲码表，用一个字节的8位表示
>
> ![image-20200730165202664](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200730165202664.png)
>
> ![image-20200730173635300](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200730173635300.png)

![image-20200730165902956](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200730165902956.png)

> 我觉得这里还是说的比较模糊哈，主要是出现在Unicode那里，他讲到 GBK 不是两个（中文的情况下）吗，那怎么区分是哪两个呢，万一刚好劈成两半了呢，他说的是gbk会在最开头写0或1,0表示1个，1表示两个即中文。但是unicode如果也这么用的话那么可以写的就变少了很多，从2的十六次方变到2的十五次方的，对于这方面unicode是不能忍受的，所以不知道怎么的就？？？？？？？？？、没听懂在讲啥了，好像是这也是导致unicode用不了的原因，后面就只是一个表作为参照作用，实际还是转给 utf进行的？，感觉是把
>
> 

### 标准的输入流和输出流

> 就是代替了Scanner 自己写一个方法出来处理，利用IO ，刚好就有

```java
/**
 * 1.标准的输入、输出流
 * 2.打印流
 * 3.数据流
 */
public class OtherStreamTest {

    /**
     * 1.标准的输入、输出流
     * 1.1
     * System.in:标准的输入流，默认从键盘输入
     * System.out:标准的输出流，默认从控制台输出
     * 1.2
     * System类的setIn(InputStream in)/setOut(PrintStream ps，OutputStream子类)方式重新指定输入和输出的流
     * <p>
     * 方式一：使用Scanner实现，调用next()返回一个字符串
     * 方式二：使用System.in实现。System.in --> 转换流--> BufferedReader的 readLine(为了使用读一行的操作哈)
     //为什么要用转换流？ 因为最开始是字节流，但是你要读一行啊，BufferedInputStream满足不了你的要求，只有BufferedReader可以，所以就需要转换流了
     */
//    //用单元测试不支持控制台输入
//    @Test
//    public void test1(){
    public static void main(String[] args) {
        BufferedReader br = null;
        try {
            InputStreamReader isr = new InputStreamReader(System.in);
            br = new BufferedReader(isr);
            while (true) {
                System.out.println("请输入字符串");
                String data = br.readLine();
                if (data.equalsIgnoreCase("e") || data.equalsIgnoreCase("exit")) {
                    System.out.println("程序结束");
                    break;
                }
                String s = data.toUpperCase();
                System.out.println(s);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (br != null) {
                try {
                    br.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
//}
```

### 打印流（了解）

![image-20200730184431141](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200730184431141.png)

> 感觉对打印流有点新思路了，因为一开始觉得这个直接用FileWriter写进去不就好了，但是你想想这个文本的内容从哪来？按这样来说这个就是自己提供的，但是打印流呢，可以把原本输入到控制台的东西打印到文件中，有点像日志功能 了
>
> 打印流没有Input的哈不是成对的

![image-20200730214015938](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200730214015938.png)

## 总结

![image-20200730215042235](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200730215042235.png)

### 处理流之六，对象流

![image-20200731152451907](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731152451907.png)

![image-20200731152755601](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731152755601.png)

```java
/**
 * 对象流的使用
 * 1.ObjectInputStream 和 ObjectOutputStream
 * 2.作用
 * 3.要想一个java对象可以序列化，需要实现序列化接口
 *
 */
public class ObjectInputOutputStream {

    //序列化：将内存中的java对象保存到磁盘中或通过网络传输出去
    //使用ObjectOutputStream实现
    @Test
    public void testObjectOutputStream(){
        ObjectOutputStream oos = null;
        try {
            //这种写txt也行，但都不是点开来看的
            oos = new ObjectOutputStream(new FileOutputStream("Object.dat"));

            oos.writeObject(new String("我爱北京天安门"));
            //刷新操作
            oos.flush();

            oos.writeObject(new Person("王明",23));
            oos.flush();

            oos.writeObject(new Person("小明",22,new Account11(1000)));
            oos.flush();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if(oos != null) {
                    oos.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }

    }

    /**
     * 反序列化：将磁盘文件中的对象还原为内存中的一个java对象
     * 使用ObjectInputStream实现
     */
    @Test
    public void testObjectInputStream(){
        ObjectInputStream ois = null;
        try {
            ois = new ObjectInputStream(new FileInputStream("Object.dat"));

            Object o = ois.readObject();

            String str = (String) o;
            System.out.println(str);
            //要按照顺序来呀
            Person p = (Person) ois.readObject();
            System.out.println(p);

            Person p1 = (Person) ois.readObject();
            System.out.println(p1);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } finally {
            if(ois != null) {
                try {
                    ois.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
/**
 * Person需要满足如下的要求，方可序列化
 * 1.需要实现接口：Serializable
 * 2.当前类提供一个全局变量：serialVersionUID
 * 3.除了当前Person类需要实现Serializable接口之外，还必须保证其内部所有属性也必须是可序列化的(默认情况下，基本数据类型是可序列化的)
 *
 *
 * 补充：ObjectOutputStream和ObjectInputStream不能序列化static和transient修饰的成员变量
 */
public class Person implements Serializable {
    public static final long serialVersionUID = 421321313L;

    private String name;
    private int age;
    private Account11 account;
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public Person(String name, int age, Account11 account) {
        this.name = name;
        this.age = age;
        this.account = account;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", account=" + account +
                '}';
    }
}
class Account11 implements Serializable{
    private double balance;
    public static final long serialVersionUID = 42122321313L;

    public Account11(double balance) {
        this.balance = balance;
    }

    public double getBalance() {
        return balance;
    }

    public void setBalance(double balance) {
        this.balance = balance;
    }

    @Override
    public String toString() {
        return "Account11{" +
                "balance=" + balance +
                '}';
    }
}
```

>
>
>我以为这里有flush，没想到没有（明白了为啥没有了，一会儿讲），我记得有一个地方写完之后就会flush一下(找到了对象流那里)，对象流要flush的原因是他可以写入多个对象，flush的话可以使两个对象区分开，不弄混，就是排队洗澡一样，每个人的东西都要自己带然后再带回去，当一个人洗澡完，没有刷新缓冲区的话，有可能会漏掉东西没带走，可能会由下一个洗澡的人带走，这样的话丢了东西不就不完整了吗？对吧。

![image-20200731162657879](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731162657879.png)

> 注意，你不加的时候感觉序列化也没报错，但是你反序列化会来就可能有问题了。
>
> 因为如果你的类修改了一些属性，添加啥的，你没自己加就是默认给你分配，你改完属性之后你的Person的分配的Id又变化了，然后你的序列化之前的识别码还是那个，然后你就识别不回来了。就像电影里突然爆发大战，然后你拿着原来的身份证去往别的地方，但是你原来的地方已经把所有人的身份证给改了，以后靠这个识别，但是你到的时候还是拿着原来的，就发现你是一个查无此人，自己不能证明自己。

### RandomAccessFile（随机存储文件流）

![image-20200731172602974](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731172602974.png)

> 比较特别的一个流，可以输入也可以输出，还有写内容的时候从头到尾覆盖？

![image-20200731173456592](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731173456592.png)

![image-20200731173856309](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731173856309.png)

![image-20200731210352439](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731210352439.png)

> 关于插入的时候刚好把中文劈成两半的问题怎么解决？ 我没有想到，然后网上的例子都是插入的时候文本内容全英文的，所以毫无烦恼。
>
> 我觉得要么把编码格式改下，大家都统一，但是效率太低了，要么就可以识别中文的那种？ 我好像做不来

```java
/*
 * RandomAccessFile的使用
 * 1.RandomAccessFile直接继承于java.lang.Object类，实现了DataInput、DataOutput接口
 * 2.RandomAccessFile既可以作为一个输入流，也可以作为一个输出流
 * 3.如果RandomAccessFile作为输出流时，写出到的文件如果不存在，则在执行过程中自动创建
 *  如果写出到的文件存在，则会对原有文件内容进行覆盖（默认情况下，从头覆盖）
 * 4.可以通过相关的操作，实现RandomAccessFile"插入"输入的效果
 */
public class RandomAccessFileTest {
    @Test
    public void test1(){
        RandomAccessFile raf1 = null;
        RandomAccessFile raf2 = null;
        try {
            raf1 = new RandomAccessFile(new File("1.jpg"),"r");
            raf2 = new RandomAccessFile(new File("2.jpg"),"rw");

            byte[] buffer = new byte[1024];

            int len;
            while ((len = raf1.read(buffer)) != -1){
                raf2.write(buffer,0,len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(raf1 != null) {
                try {
                    raf1.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(raf2 != null) {
                try {
                    raf2.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }
    @Test
    public void test2() throws IOException {
        RandomAccessFile raf1 = new RandomAccessFile("h1.txt","rw");
        //将指针调到角标为3的位置，默认为0，所以默认情况下从0开始覆盖
        //思考:如果想实现append操作的话可以找到最末尾的位置，通过file的一个方法可以这样子做，但是如果有中文字符也？一会儿试试
        raf1.seek(3);
        raf1.write("xyz".getBytes());

         raf1.close();
    }

    /**
     * 使用RandomAccessFile实现数据的插入效果
     * 不过如果写中文的话可能会乱码
     */
    @Test
    public void test3(){
        RandomAccessFile raf1 = null;
        try {
            raf1 = new RandomAccessFile("h1.txt","rw");
            //这里如果是中文的话可能会被劈成两半。。。
             raf1.seek(3);
            System.out.println(raf1.length()+"!!");
            //保存指针3后面的所有数据到StringBuilder中
            StringBuilder sb = new StringBuilder((int) new File("h1.txt").length());
            System.out.println(new File("h1.txt").length()+"!!!");
            byte[] buffer = new byte[20];
            int len;
            while ((len = raf1.read(buffer)) != -1){
            sb.append(new String(buffer,0,len));
            }
            //在上面的时候指针跑到最后了，需要再调回来
            raf1.seek(3);
            //写入xyz
            raf1.write("xyz".getBytes());

            //将StringBuilder的数据写入到文件里,要先变到String，因为sb的话没有getBytes方法，感觉基本是跟char[]接触的
            raf1.write(sb.toString().getBytes());
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(raf1 != null) {
                try {
                    raf1.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

### NIO概述

![image-20200731214439020](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731214439020.png)

![image-20200731214540688](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731214540688.png)

![image-20200731214810813](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731214810813.png)

> Path 代替 File

*********************************************************************************************************************************************************************************补充：2020.8.3 anki到这里 *********************************************************************************************************************************************

![image-20200731214951766](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731214951766.png)

![image-20200731215007321](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731215007321.png)

![image-20200731215019613](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731215019613.png)

![image-20200731215050582](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731215050582.png)

![image-20200731215102775](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731215102775.png)

![image-20200731215111084](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731215111084.png)

![image-20200731215120104](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731215120104.png)

![image-20200731215138887](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731215138887.png)

![image-20200731215538289](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731215538289.png)

> 这个jar包里面有个FileUtils 都写好了什么复制文件啥的



![image-20200731235511920](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731235511920.png)

![image-20200731235900197](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200731235900197.png)

> IP：主机
>
> 端口号：哪个应用程序在通信	

![image-20200801002705628](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801002705628.png)

![image-20200801002912274](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801002912274.png)

#### IP

![image-20200801140301754](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801140301754.png)

![image-20200801153336899](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801153336899.png)

> 个人理解这些类就像File 类一样，可以通过FIle类来获取对应的路径，`getByName()`就已经是实例化了，应该就是通过一个ip或者域名来获取一个类，进行实例化，然后你可以用这个类去获取对应的主机名，和主机地址（我觉得这就是一个^ 这个关系，可能以后用的时候这个类别人是可以给到我们的），`getLocalHost`就是获取本机的ip，那这个就挺好理解的了吧

```java
/**
 * 一、网络编程中有两个主要的问题
 *
 * 二、网络编程中的两个要素
 * 1.对应问题一：IP和端口号
 * 2.对应问题二：提供网络通信协议：TCP/IP参考模型（应用层、传输层、网络层、物理+数据链层）
 *
 *
 * 三：通信要素一：IP和端口号
 * 1.IP：唯一的标识Internet上的计算机（通信实体）
 * 2.在Java中使用InetAddress类代表IP
 * 3.IP分类：IPV4和IPV6；万维网和局域网
 * 4.域名：www.baidu.com(形象，不用输入ip地址)
 * 5.本地回路地址： 127.0.0.1 对应：localhost
 * 6.如何实例化IneAddress:两个方法：getByName(String host)、 getLocalHost()
 *                      两个常用方法：getHostName(),getHostAddress
 * 7.端口号：正在计算机上运行的进程
 *  要求：不同的进程有不同的端口号
 *  范围：0~65535
 *
 * 8.端口号和IP地址的组合得出一个网络套接字：Socket    
 */
public class InetAddressTest {

    public static void main(String[] args) {
        try {
            //File file = new File("hello.txt");
            InetAddress name = InetAddress.getByName("192.168.0.116");
            ///192.168.0.116
            System.out.println(name);

            //www.baidu.com/14.215.177.38
            InetAddress name2 = InetAddress.getByName("www.baidu.com");
            System.out.println(name2);

            //DESKTOP-1G4GVRT/192.168.0.116,获取本地ip
            InetAddress name3 = InetAddress.getLocalHost();
            System.out.println(name3);

            System.out.println(name2.getHostAddress());

            System.out.println(name2.getHostName());
        } catch (UnknownHostException e) {
            e.printStackTrace();
        }

    }
}

```

![image-20200801155531427](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801155531427.png)

#### 网络通信协议

![image-20200801160417321](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801160417321.png)

![image-20200801160428291](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801160428291.png)

![image-20200801161602062](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801161602062.png)

![image-20200801162358824](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801162358824.png)

> 个人理解哈，TCP相当架座桥，架桥需要成本的，所以要判断这个桥到底有没有用，有用的就能进行大量传输，但是缺点就是效率低，因为架桥需要时间，当没有人走的时候，就拆桥（隔绝两地来往）
>
> UDP 的话就是本来隔绝的两地，允许通信了，但是只能扔包裹过去，包裹能装的东西不多，上面写个收信人相关信息就好了，所以不需要建立连接，就不是很可靠，可能会有丢掉包裹的危险，好处就是不需要释放资源啦，没什么好释放的，开销也小，速度就变快了

![image-20200801161835800](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801161835800.png)

> 使用协议前，要进行连接，就是你要想遵守规则，你首先得使用把，然后三次握手就是确定是否连接上的。
>
> 第一次握手单方面在，两次握手双方在，三次握手放在第一次握手的一方不在



![image-20200801162710424](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801162710424.png)

![image-20200801162931321](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801162931321.png)

关闭连接

> 一般情况下是客户端断开连接，不是服务端

```java
/**
 * 实现TCP的网络编程
 * 例子1：客户端发送信息给服务端，服务端将数据显示在控制台上
 */
public class TCPTets1 {

    @Test
    public void client()  {
        Socket socket = null;
        OutputStream os = null;
        try {
            //对方的IP地址
            //1.创建socket对象，指明服务器端的ip和端口号
            InetAddress inet  = InetAddress.getByName("127.0.0.1");
            socket = new Socket(inet,8899);
            //2.获取输出流，用于输出数据
            os = socket.getOutputStream();
            os.write("你好，我是客户端".getBytes());
            //3.写出数据的操作
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //资源的关闭
            if(socket != null) {
                try {
                    socket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(os != null) {
                try {
                    os.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }


    }

    @Test
    public void server(){
        ServerSocket ss = null;
        Socket socket = null;
        InputStream is = null;
        ByteArrayOutputStream baos = null;
        try {
            //1.创建服务器端的ServerSocket，指明自己的端口号，ip地址已经知道
            ss = new ServerSocket(8899);
            //能够接受到别人给的socket
            //2.调用accpet()表示接收来自于客户端的socket,就像别人问可不可以干嘛时，首先是说可以，然后再接收别人请求的内容
            socket = ss.accept();
            //3.读取输入流中的数据
            is = socket.getInputStream();
            //不建议这么写，可能会有乱码
//        int len;
//        byte[] buffer = new byte[20];
//        while ((len = is.read(buffer)) != -1){
//            String str = new String(buffer,0,len);
//            System.out.println(str);
//        }
            //4.读取流中的数据
            int len;
            baos = new ByteArrayOutputStream();
            byte[] buffer = new byte[5];
            while ((len = is.read(buffer)) != -1){
                //写到baos的array中，所以用到的是output
                baos.write(buffer,0,len);
            }

            System.out.println(baos.toString());
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //5.关闭资源
            if(baos != null) {
                try {
                    baos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(is != null) {
                try {
                    is.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(socket != null) {
                try {
                    socket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(ss != null) {
                try {
                    ss.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }
}

```

#### 例题

![image-20200801203521415](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801203521415.png)

![image-20200801210912765](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801210912765.png)

```java
//客户端发送文件给服务端，服务端将文件保存到本地
public class TCPtest2 {
    @Test
    public void client(){
        Socket socket = null;
        OutputStream os = null;
        BufferedInputStream bis = null;

        try {
            InetAddress inet = InetAddress.getByName("127.0.0.1");
            socket = new Socket(inet,8888);

            os = socket.getOutputStream();
            bis = new BufferedInputStream(new FileInputStream("h1.txt"));
            int len;
            byte[] buffer = new byte[20];
            while ((len = bis.read(buffer)) != -1){
                os.write(buffer,0,len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(os != null) {
                try {
                    os.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(bis != null) {
                try {
                    bis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }

            if(socket != null) {
                try {
                    socket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }

        }
    }
    @Test
    public void server(){
        ServerSocket ss = null;
        Socket socket = null;
        InputStream is = null;
        BufferedOutputStream bos = null;
        try {
            ss = new ServerSocket(8888);
            socket = ss.accept();

            is = socket.getInputStream();
            int len;
            byte[] buffer = new byte[20];

            bos = new BufferedOutputStream(new FileOutputStream("hhhh1.txt"));
            while ((len = is.read(buffer)) != -1){
                bos.write(buffer,0,len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(bos != null) {
                try {
                    bos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(is != null) {
                try {
                    is.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(socket != null) {
                try {
                    socket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(ss != null) {
                try {
                    ss.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }
}
```

```java
//客户端发送文件给服务端，服务端将文件保存到本地,并发送“你好，已经收到”的反馈给客户端，并关闭连接
public class TCP3 {
    @Test
    public void client(){
        Socket socket = null;
        OutputStream os = null;
        BufferedInputStream bis = null;
//        BufferedOutputStream bos = null;
        ByteArrayOutputStream baos = null;
        try {
            InetAddress inet = InetAddress.getByName("127.0.0.1");
            socket = new Socket(inet,8888);

            os = socket.getOutputStream();
            bis = new BufferedInputStream(new FileInputStream("h1.txt"));
//            bos = new BufferedOutputStream(os);
            int len;
            byte[] buffer = new byte[20];
            while ((len = bis.read(buffer)) != -1){
                os.write(buffer,0,len);
            }
            //关闭数据的输出
            socket.shutdownOutput();
            InputStream is = socket.getInputStream();
             baos = new ByteArrayOutputStream();
            byte[] buffer2 = new byte[20];
            int len2;
            while ((len2 = is.read(buffer2)) != -1){
                baos.write(buffer2,0,len2);
            }
            System.out.println(baos.toString());
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(os != null) {
                try {
                    os.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(bis != null) {
                try {
                    bis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if (baos != null){
                try {
                    baos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(socket != null) {
                try {
                    socket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
    @Test
    public void server(){
        ServerSocket ss = null;
        Socket socket = null;
        InputStream is = null;
        BufferedOutputStream bos = null;
        try {
            ss = new ServerSocket(8888);
            socket = ss.accept();

            is = socket.getInputStream();
            int len;
            byte[] buffer = new byte[20];

            bos = new BufferedOutputStream(new FileOutputStream("hhhh2.txt"));
            while ((len = is.read(buffer)) != -1){
                bos.write(buffer,0,len);
            }
            //服务器端给予客户端反馈
            OutputStream os = socket.getOutputStream();
            os.write("你好，文件已经收到".getBytes());
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(bos != null) {
                try {
                    bos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(is != null) {
                try {
                    is.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(socket != null) {
                try {
                    socket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(ss != null) {
                try {
                    ss.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}

```

> 这里有个点就是用了`socket.shudownOutput`，为什么这么说，因为遇到了些问题，如果没有的话客户端和服务端都卡着了，是因为首先，这是一个多线程操作，感觉像是一个想寄快递的客户和收快递的快递员，客户呢，他不是一次性给的，他是包装好一个给一个，然后快递员也一个个接着处理，但是呢快递员也不知道客户啥时候处理完，因为他看不到，干完手中的活后就一直等着。所以这时候需要客户端给个信号说我这里搞好啦，你去下一个客户那把。
>
> 那为什么就这里出现了，前面没有用到的感觉？因为前面的处理完之后直接就关闭资源了，就像客户直接关门关灯了，然后快递员也知道得走了。

#### 感觉明白了flush

> 我以为这里有flush，没想到没有（明白了为啥没有了，一会儿讲），我记得有一个地方写完之后就会flush一下(找到了对象流那里)，对象流要flush的原因是他可以写入多个对象，flush的话可以使两个对象区分开，不弄混，就是排队洗澡一样，每个人的东西都要自己带然后再带回去，当一个人洗澡完，没有刷新缓冲区的话，有可能会漏掉东西没带走，可能会由下一个洗澡的人带走，这样的话丢了东西不就不完整了吗？对吧。
>
> 这里没有flush的原因是这里一次性只写一个东西，如果你想再写的话就需要搞个shutdown，但是另一端也得有人接受才行啊，是吧，所以这里的话就挺复杂的

#### ！！！！更新的一种，解决TCP传输一次的问题

之前一直被困扰到，但是不知道怎么办，因为你client端传东西过去之前是shutdownOutput的，那你就没法开启了，今天学到的是用打印流的方式。

而且我今晚竟然一直在弄这道题，而且写完一种方法后才发现欸，行不通，但是学到了多线程嘻嘻嘻，而且学到了打印流。因为这可以聊天，但是拿不到数据。

client

```java
package Exp32_ZhengBR;

import java.io.*;
import java.net.InetAddress;
import java.net.Socket;
import java.util.Scanner;

public class Exp32_Client_ZhengBR {
    private static Socket socket;
    private static InetAddress inet;

    public static void main(String[] args) {
        String output;
        String input;
        BufferedReader br = null;
        Scanner scanner = null;
        PrintWriter pw = null;
        try {
            inet = InetAddress.getByName("127.0.0.1");
            socket = new Socket(inet,8899);

            while (true) {
                 pw = new PrintWriter(socket.getOutputStream(), true);
                 scanner = new Scanner(System.in);
                output = scanner.nextLine();
                pw.println(output);

                br = new BufferedReader(new InputStreamReader(socket.getInputStream()));
                input = br.readLine();
                System.out.println("服务端:" + input);
                if(input.endsWith("exit")){
                    break;
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(br != null) {
                try {
                    br.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(scanner != null) {
                scanner.close();
            }
            if(pw != null) {
                pw.close();
            }
            if(socket != null) {
                try {
                    socket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }
}
```

server

```java
package Exp32_ZhengBR;

import java.io.*;
import java.net.InetAddress;
import java.net.ServerSocket;
import java.net.Socket;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Map;
import java.util.Scanner;

public class Exp32_Server_ZhengBR {

    private static ServerSocket serverSocket;
    private static Socket socket;
    public static void main(String[] args) {
        String output;
        String input;
        BufferedReader br = null;
        PrintWriter pw = null;
        try {
            serverSocket = new ServerSocket(8899);
            socket = serverSocket.accept();
            while (true) {
                br = new BufferedReader(new InputStreamReader(socket.getInputStream()));
                input = br.readLine();
                System.out.println("用户端:" + input);
                pw = new PrintWriter(socket.getOutputStream(), true);
                Map<String, String> map = Exp32_Utils_ZhengBR.getInfo(input);
                String message = map.get("message");
                if(!map.containsKey("name")){
                    pw.println(message);
                }else {
                    pw.println("To " + map.get("name") + " " + message);
                }
                if ("bye".equals(message)) {
                    break;
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (br != null) {
                try {
                    br.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }

            if (pw != null) {
                pw.close();
            }
            if (socket != null) {
                try {
                    socket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }
}

```

```java
package Exp32_ZhengBR;

import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

public class Exp32_Utils_ZhengBR {

    public static Map<String, String> getInfo(String data){
        Map<String, String> map = new HashMap<>();
        String message = "请重试";
        if(data == null || "".equals(data)){
            message = "没有数据噢";
        }else{
            String[] strings = data.split("姓名");
            String info = strings[1].substring(1);
            String[] infos = info.split(" ", 2);
            System.out.println(Arrays.toString(infos));
            map.put("name", infos[0]);
            String question = infos[1].trim();
            System.out.println(question);
            if("what time is it".equals(question)){
                LocalDateTime time = LocalDateTime.now();
                DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd hh:mm:ss");
                String now = formatter.format(time);
                message = "现在时间为 " + now;
            }else if("exit".equals(question.toLowerCase())){
                message = "bye";
            }else{
                message = "请重试";
            }

        }
        map.put("message", message);
        return map;
    }
}
```

#### 多线程与TCP的结合

recieve

```java
public class Exp32_Recieve_ZhengBR implements Runnable {
    private String msgFrom;
    ByteArrayOutputStream baos = null;
    private Socket socket = null;
    BufferedReader br;

    public Exp32_Recieve_ZhengBR(String msgFrom, Socket socket) {
        this.msgFrom = msgFrom;
        this.socket = socket;
    }

    @Override
    public void run() {
        String data = null;
        try {
            br = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            while (true) {
                data = br.readLine();
                System.out.println(msgFrom + ":" +data);
                if (data.endsWith("bye"))
                {
                    break;
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (br != null) {
                    br.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }

            if(socket != null){
                try {
                    socket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

send

```java
package Exp32_ZhengBR.unused;

import java.io.BufferedInputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.io.PrintWriter;
import java.net.InetAddress;
import java.net.Socket;
import java.net.UnknownHostException;
import java.util.Scanner;

public class Exp32_Send_ZhengBR implements Runnable{


    private String msgFrom;
    private Socket socket = null;
    OutputStream os = null;
    Scanner scanner = null;
    PrintWriter pw;

    public Exp32_Send_ZhengBR(String msgFrom, Socket socket) {
        this.msgFrom = msgFrom;
        this.socket = socket;
    }

    @Override
    public void run() {
        String data = null;
        scanner = new Scanner(System.in);
        try {
            pw = new PrintWriter(socket.getOutputStream(),true);

            while (true){
                    data = scanner.nextLine();
                pw.println(data);
                if(data.endsWith("bye"))
                {
                    break;
                }
            }

        } catch (IOException e) {
            e.printStackTrace();
        }finally {
            if(pw != null) {
                pw.close();
            }
        }
    }
}
```

server

```java
public class Exp32_Server_ZhengBR {
    public static void main(String[] args) {
        ServerSocket serverSocket = null;
        Socket socket = null;
        try {
            serverSocket = new ServerSocket(8899);
            socket = serverSocket.accept();
        } catch (IOException e) {
            e.printStackTrace();
        }


        new Thread(new Exp32_Recieve_ZhengBR("用户端", socket)).start();
        new Thread(new Exp32_Send_ZhengBR("服务端", socket)).start();
    }
}

```

client

```java
public class Exp32_Client_ZhengBR {
    public static void main(String[] args) {
        InetAddress inet = null;
        try {
             inet = InetAddress.getByName("127.0.0.1");
        } catch (UnknownHostException e) {
            e.printStackTrace();
        }
        Socket socket = null;
        try {
             socket = new Socket(inet, 8899);
        } catch (IOException e) {
            e.printStackTrace();
        }
        Thread reception = new Thread(new Exp32_Recieve_ZhengBR("服务端", socket));
        Thread send = new Thread(new Exp32_Send_ZhengBR("客户端", socket));
        reception.start();
        send.start();
    }
}

```



#### UDP

```java
/**
 * UDP协议的网络编程
 */
public class UDPTest {
    //发送端
    @Test
    public void sender(){
        DatagramSocket socket = null;
        try {
            socket = new DatagramSocket();

            String str  = "我是UDP方式发送的导弹";
            byte[] data = str.getBytes();
            InetAddress inet = InetAddress.getByName("127.0.0.1");
            DatagramPacket packet = new DatagramPacket(data,0,data.length,inet,8888);

            socket.send(packet);
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(socket != null) {
                socket.close();
            }
        }
    }
//  接收端
    @Test
    public void receiver(){
        DatagramSocket socket = null;
        try {
            socket = new DatagramSocket(8888);

            byte[] buffer  = new byte[100];
            DatagramPacket packet = new DatagramPacket(buffer,0,buffer.length);

            socket.receive(packet);
            //获取packet中的数据buffer
            //注意一下要写长度
            System.out.println(new String(packet.getData(),0,packet.getLength()));
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(socket != null) {
                socket.close();
            }
        }
    }
}
```

> 1. 这个就有些不一样了数据都以包裹形式储存，然后注意一点，上面讲过，UDP不管你连接没有，我发就是发了，就跟发短信一样，所以这个直接启动sender是不会报错的(一般来说是先启动receiver后启动sender)，但是上面TCP那里是会报错的，因为需要握手。
>
> 2. 我如上写了注意下要写长度是为啥？ 因为如果数组没补满的话是会把剩余的一起输出的。
>
>    ![image-20200801235128544](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801235128544.png)
>
>    ![image-20200801234717081](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801234717081.png)

#### byteArrayOutputArray

![image-20200801235230732](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200801235230732.png)

> 原理是啥？读到东西写到 `baos`中，相当于拼接效果，而不是读一些byte之后就马上转，避免中文被劈成两半。

#### URL

![image-20200802000252492](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200802000252492.png)

> 种子实际上是个url，不保险，易失效