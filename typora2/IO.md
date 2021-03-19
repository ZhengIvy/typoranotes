### IO 流

IO 流也可以叫做File handling  但是不是很准确。

1.为什么需要IO流(Input and output streams)?

IO流实际上是与file相关进行连接的，举个简单的例子就是银行账户，你开了个银行账户，但是这部分的数据是需要保存的，但是在编译器上运行一个程序之后，里面的数据也在运行完之后被清空，但这不是我们想要的。所以我们需要一个地方来储存数据，这时候就需要file文件来储存数据，但正常情况下大量的数据file也储存不了，这时候数据库就派上了用场，IO流是从java将数据与file进行输入与输出的方式，那JDBC就是数据库输出输入的方式。





2.就像厨房中需要洗碗用的水一样，需要出水口和排水口，file也一样，在java之间需要一个输入口和输出口，而且两个口不能为一样的(从正常情况下可知)，那Stream就是这个流。那对于java和file之间的水又是什么？

是数据，有两种，一种是数字，一种是文本，根据你的需要。

对于数字我们简单把他的名字定义为输入(虽然对于java和file此时的输入也是输出，但是以java视角为准)

InputStream 和OutputStream

那字符用啥？ 其实Input&Output实际上就是读和写，从file中读取数据，把写好的数据给file这样。

所以名字就为Reader and Writer。

都是抽象类。为什么？ 你可以想象为平常我们读和写可以有很多种工具，用鼠标点也是，用monitor也是，因此实际上是这个动作的内容不同，这个类的其他方法都是相同的，只有这个不同，由他的性质所决定，所以是抽象类。

但是从数字输出输入上也有很多种方式，因为是有很多类型的，而且毕竟这也是个抽象类，不能实例化肯定是要子类的嘛，所以一共有9种。

这些的命名方式基本上是 operation+InputStream

所以

1.FileInputStream是基础，指的是以byte的形式读取file，其他子类的作用都要与这个联系上，相当于打开了出水管口，准备好了出水。

2.ByteArrayInputStream 实际就是以ByteArray的形式进行的。

3.FilterInputStream 实际上是过滤的意思，像水就是要过滤的，在这里呢，就可以分为两个子类。

DataInputStream ，在1的基础上以primitive 的形式，各种都ok 就基本类型都可以

bufferedInputStream,实际上呢是，过滤掉一些东西，加快速度，不是像直接以file的形式就读过来了，先通过buffer再过来，可能是某种加速器把，我猜，过滤掉某种东西。

4.Object 就是以object的形式进行就ok

5.Piped 的话就是你的写输出到别人的读输入去了。

6.Sequence 就是可以multiple files

7.Stringbuffer 



当我们用完这个过程之后怎么办。是需要关掉出水管的口的，这时候就需要closed ，这个是在1.5之后提出的，作为一个功能，所以是接口，之前的closed直接就在InputStream当中，现在1.7后更高级还有一个

Autoclosed 虽然不知道怎么搞，反正是一个接口，是closed 的父类。

然后还有两个接口，是一个是DataInput 是上面DataInputStream的接口，虽然不知道是干嘛的。

还有一个ObjectInputStream 虽然也不知道是干嘛的。但是这个是上面的子类？虽然也不知道原因哈、





2.OuteputStream(8个)

-2+1

没有了Sequence 和Stringbuffer

多了一个PrintStream

有什么作用呢，跟byte 的不一样吧，好像跟很多东西都不一样，因为很多的都是转为二进制的，反正这个好像不转为二进制，直接就是输出

还多了一个Flushable 缓冲的意思就是你写完也不会马上交吧，先放到一个地方后用Flushable就可以交了，也有closed哈

是一个接口，跟closed 差不多的。

除了Auto 和Object 在java.lang里面 其他都是在java.io里面的。

因为Auto在JDBC里面也有用到

然后其他基本一样



InputStream里面的method(9+3)

一个java 1.0就有了，后面是Java 9才有的，还没讲哈

与reallife联系在一起，等会再看看

1. (int)计算页数(计算多少个byte)
2. 然后你关上了书(其实是在最后执行的)
3. read的方式不同了，(唯一一个抽象方法) 1byte at  a time 返回那个byte
4. read 一个数组，返回长度？(我不确定)
5. read some parts 从哪里开始看起，看一个数组的多少(返回啥啊、？)(没讲)
6. 问下可不可以做笔记
7. 进行做笔记(有限制的)
8. 回看到做笔记的地方
9. 跳掉一些部分，用Long
10. writer 的话就只有5个method
11. 首先不能skip 不能做笔记，不能询问，![image-20200406230940037](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200406230940037.png)

flush 是啥呢，就是writer 的时候首先是放在pipe中的，然后再用flush出去







关于具体的读数据和写数据到文档中

1. 开通与file 之间的连接，FileOutputStream
2. write
3. flusale
4. close
5. exception handling



读的话就没有flush 了，就差不多是这样吧

![image-20200408141045525](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200408141045525.png)

![image-20200408141051749](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200408141051749.png)





![image-20200409155036279](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200409155036279.png)

```java
public class Main {
        public static void main(String[] args) throws IOException {
        File file = new File("C:\\Users\\zbr\\Desktop\\abc.txt");
            FileInputStream fileInputStream = new FileInputStream(file);
            int data = fileInputStream.read();
            System.out.println(data);//char(data) 可以转换成正常的数值
        }
    }
ascii 因为 1byte at a time
    
    public class Main {
        public static void main(String[] args) throws IOException {
        File file = new File("C:\\Users\\zbr\\Desktop\\abc.txt");
            FileInputStream fileInputStream = new FileInputStream(file);
          int data = 0;
           while((data=fileInputStream.read())!=-1) {
               System.out.print((char)data);
           }
            fileInputStream.close();
        }
    }
```

如果没有的话返回-1哈，binary的

```java
public class Main {
        public static void main(String[] args) throws IOException {
        File file = new File("C:\\Users\\zbr\\Desktop\\abc.txt");
        File file2 = new File("C:\\Users\\zbr\\Desktop\\captmidn.txt");
        FileInputStream fileInputStream = new FileInputStream(file2);
            FileOutputStream fileOutputStream = new FileOutputStream(file);
            int data;
            while((data=fileInputStream.read())!=-1) {
                fileOutputStream.write(data);
                fileOutputStream.flush();
            }
            System.out.println("copy success");
            fileOutputStream.close();
            fileInputStream.close();
        }
    }
```

copy





先说下今天一整天下午都在学这个但好像也没学点啥东西出来

#### 1. writing data into a file

![image-20200410004601819](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410004601819.png)

有六个步骤，先import a class

创造fos 的 object 再是放data ，把data冲到file 里面  close 就完事 handle exception 记住了

![image-20200410004755579](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410004755579.png)

这个也差不多 只不过少一步冲罢了



![image-20200410005158415](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410005158415.png)

用scanner

但说实话我好像对 filewriter 没有什么印象，他好像没有讲过的样子，的确是没有讲过的样子



![image-20200410005416060](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410005416060.png)

这里也只是讲了 fos constructor 的形式，主要是分为两种，一种是用路径直接，另外一种是把路径放到String 里面，再传这个String 进去就可以了，boolean 啥意思呢，就是要不要append  append 还是代替你选一个

InputputStream 也是一样的，只不过我还不知道这个descriptor 啥意思罢了

![image-20200410005728716](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410005728716.png)

![image-20200410005738543](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410005738543.png)

记住是one byte at a time 而且是以二进制的形式，所以通常要转换一下

![image-20200410005818446](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410005818446.png)

![image-20200410005826993](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410005826993.png)

![image-20200410005836682](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410005836682.png)

![image-20200410005844383](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410005844383.png)

file 如何 copy 其实也很简单

![image-20200410005859764](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410005859764.png)

![image-20200410005918777](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410005918777.png)

但是这个目前我是不知道的哈

![image-20200410005936344](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410005936344.png)

![image-20200410005945941](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410005945941.png)

![image-20200410010004814](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410010004814.png)

![image-20200410010011728](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410010011728.png)

如何用bufferreader 问题了啊，比scanner 难用 但是速度快呀

![image-20200410010130213](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200410010130213.png)

这种直接了当 更好哈



## 2. NIO IO

![image-20200421161501489](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421161501489.png)

![image-20200421182608978](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421182608978.png)

![image-20200421182617531](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421182617531.png)

是d哦 不是100 原因是如果是100 的话就是'100'，否则就是ascii码，因为 需要输入的是int 简而言之char 也ok

char数组也ok string也ok

![image-20200421182856276](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421182856276.png)

![image-20200421192218830](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192218830.png)

噢原来是这样的哈，怪不得人家100 可以直接输 我这边只可以'100' 这样子输

## 3. file

![image-20200421192624367](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192624367.png)

这个呢就是file的时候拿到一个连接，但是你还不确定存在不存在，所以你可以createnewfile 是专门create fiel的

![image-20200421192630453](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192630453.png)

然后这个file是可以指file和directory的，所以呢你要创建directory的话就可以是 mkdir上面有写区别哈

![image-20200421192635080](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192635080.png)

然后这个是什么意思，就是指在该目录下的file

![image-20200421192639883](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192639883.png)

这个也是一样的哈

![image-20200421192644424](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192644424.png)

![image-20200421192648834](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192648834.png)

![image-20200421192653529](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192653529.png)

![image-20200421192659978](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192659978.png)

![image-20200421192704546](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192704546.png)

然后这是file的方法哈，是否存在 新建file 或directory 到底是file还是directory 你这个list里面是有几个文件的，你的length是多少以char计算把，

![image-20200421192709928](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192709928.png)

如果你想算其中一个file或者是directory 的个数的话记住要这样子在下面

![image-20200421192719080](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192719080.png)

![image-20200421192723768](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192723768.png)

这就是考验你对forloop的理解了，这个s1应该代表的是每个的值，所以这个意思是拿到file文件夹中的file文件，判断是不是，然后就++ 记住不能用`s1.isFile`这是个String数组a

![image-20200421192728004](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192728004.png)

write的几种写法，本质上都是character

![image-20200421192732658](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192732658.png)

![image-20200421192738828](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192738828.png)

![image-20200421192743009](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200421192743009.png)

然后呢他好像提到了`\n`  在不同的系统中是不一样的，所以他说就为啥使用 buffer？？？？

继续看吧，这就是我今天下午得到的东西

## 4、buffer

话说那个字节流的返回值是int把？？？应该是int啊

不过相同点是如果没有了话就return -1

传的图片太慢了，我先写吧，怎么说呢就是，buffer的话可以实现一行一行来进行，buffer由writer 或者是reader进行连接，不可以直接连接到file里面去，就相当于那些是个通道，buffer作为缓冲，有序地排列这样子，然后关的时候都是用buffer关掉就好了，其他不用关，因为会自动关掉的。简单来说就是这样哈，今晚睡看



## 5. 与servlet 相关

今天真的做到累死，做到后面也不知道自己在做什么今天中午就改了数据几小时，因为发现了一种更好的封装方法，但是呢，因为各种匹配的原因不得行，首先是隐藏域覆盖的问题，覆盖掉了

然后是数据库textare乱码的问题，等会要修一下，再者是不知道无语怎么传数据传不上去的？？？迷茫哈

还有需要改进的地方是 不知道为啥不直接跳转哈，这是一个bug把 来了 来了，是我蠢了，update 多个字段的时候不用and 好吧 应该用，连接 无语  了真的无语了 真的无语了，心态就是这样崩的，好了是我菜了，然后分页是可以改进一下的，搞那种尾页的就ok啦

