![image-20200510202512536](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510202512536.png)![image-20200510094617278](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510094617278.png)

控制反转

![image-20200510095054596](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510095054596.png)

![image-20200510105547925](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510105547925.png)

![image-20200510105647533](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510105647533.png)

所以当有两个东西的时候就要创两次？，ememe感觉的话有点麻烦？



单实例的，就是你再创一个相同的person01，那么也是相等的

![image-20200510110117015](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510110117015.png)

![image-20200510111648797](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510111648797.png)

用constructor 进行赋值

![image-20200510112555912](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510112555912.png)

重载的时候是这样子的

![image-20200510114236364](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510114236364.png)

进行复杂的赋值要在里面进行

如果person中有car的话是可以进行引用的

是一个严格的引用，如果你直接拿到car那也是一样的





内部bean 只能在内部使用，不能被获取到 id无用哈

![image-20200510130159951](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510130159951.png)

工具类map在哪都可以使用哈





list也有

级联属性， 属性的属性

![image-20200510130622320](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510130622320.png)

![image-20200510131150299](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510131150299.png)

信息的继承

![image-20200510131714120](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510131714120.png)

![image-20200510131754433](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510131754433.png)

还是不知道有什么作用啊

![image-20200510132046019](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510132046019.png)

![image-20200510132516970](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510132516970.png)

![image-20200510132610038](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510132610038.png)

多实例的话就是可以有无限个哈，就是之前判断那样的，每拿一个都是一样的，这次是相反的，没拿个就创建一个新的哈，所以呢有什么用吗？？？？？？？？？？？？？？不清楚啊

![image-20200510133539880](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510133539880.png)

所以我一直用到的是实例工厂吗？？？？？？

![image-20200510133834757](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510133834757.png)

![image-20200510133927006](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510133927006.png)

区别是啥那？？

![image-20200510144701456](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510144701456.png)

![image-20200510145057034](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510145057034.png)

思路不一样哈，实例的话要先创建一个工厂，再到工厂里面去拿东西，所以这个bean主要是自己，实体类，再去用工厂搞出来哈

![image-20200510151535044](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510151535044.png)

![image-20200510151742065](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510151742065.png)

![image-20200510151920531](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510151920531.png)

![image-20200510153130462](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510153130462.png)

![image-20200510153334782](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510153334782.png)

![image-20200510153451903](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510153451903.png)

![image-20200510154324783](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-2020051015432

为什么说那是一个工厂呢，因为他会给你返回一个object啊

而且就算是单实例也不会创建对象暗黑

![image-20200510155121395](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510155121395.png)

![image-20200510155829741](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510155829741.png)

有什么用呢？ 不知道啊，注意一下，这个close 在 ApplicationContext 是没有的，所以他这里的话就这样子吧，需要init 和method 容器关闭的时候就有那个close 所以到底有什么用呢

![image-20200510155933802](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510155933802.png)

![image-20200510160905670](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510160905670.png)

是不是因为多个销毁不好销毁啊，如果是1个的话就直接销毁了吧

![image-20200510161751167](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510161751167.png)

之歌就是前置处理和后置处理，就是在被调用的时候或者说是初始化前会执行的操作，后也有，像是trigger把

![image-20200510162320235](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510162320235.png)

![image-20200510162800736](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510162800736.png)

![image-20200510163003358](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510163003358.png)

感觉有些像过滤器 可以增强某种东西

![image-20200510163605606](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510163605606.png)

![image-20200510163718328](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510163718328.png)

![image-20200510193331861](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510193331861.png)

这个干啥的呢，就是自动装配，你在xml里面配置了东西，像person里面有car的话 你想把car的值赋值到person里面怎么搞 你可以手动ref 

![image-20200510194013847](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510194013847.png)

![image-20200510194152631](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510194152631.png)

![image-20200510194231054](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510194231054.png)

![image-20200510194449130](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510194449130.png)

![image-20200510195309230](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510195309230.png)

像el表达式![image-20200510200251389](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510200251389.png)

![image-20200510202211664](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510202211664.png)

注解的作用，![image-20200510202326957](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510202326957.png)

![image-20200510202515170](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510202515170.png)

![image-20200510203050447](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510203050447.png)

当你要加到容器中时 默认id首字母小写ok

![image-20200510204254898](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510204254898.png)

![image-20200510204508659](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510204508659.png)

所以单实例和多实例的区别又是什么嗯

![image-20200510205009796](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510205009796.png)

你扫描的时候可以只扫一些东西 或者不扫一些东西哈

![image-20200510205645761](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510205645761.png)

![image-20200510205831155](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510205831155.png)

![image-20200510225817907](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200510225817907.png)

![image-20200511012547100](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200511012547100.png)

![image-20200511013736338](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200511013736338.png)

![image-20200511014430454](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200511014430454.png)

![image-20200511075716265](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200511075716265.png)

![image-20200511075751928](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200511075751928.png)

![image-20200511075913546](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200511075913546.png)

![image-20200511080231901](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200511080231901.png)

这些组件都是启动的时候自动运行的，相当于bean了

![image-20200511083941577](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200511083941577.png)

spring的单元测试，为什么要这样呢是因为哈，就是上面又讲到，这样会一直循环下去，但是你不那样拿的话也好像没啥？

![image-20200511084611079](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200511084611079.png)

但是呢怎么说呢，这个装配是在，eem反正我不用那两个注解的话就直接为null 了。用了之后还有值的



好像test 的话比较特殊把，也不是叫特殊，如果你需要自动注入的话上面的类得有东西给i哈

![image-20200511093706402](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200511093706402.png)

![image-20200511093915151](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200511093915151.png)

![image-20200511094139899](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200511094139899.png)

![image-20200511094756521](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200511094756521.png)

学完了，但是可能不够扎实哈



因为时间不够，所以得跳了。所以目前学到的就是管理ioc，如何进行，添加注解，然后呢那个持久化dao层到底是个什么东西？？？？，真的是不知道呀