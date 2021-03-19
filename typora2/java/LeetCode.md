# 1.链表

## 1. 相交链表

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201120204214905.png" alt="image-20201120204214905" style="zoom:50%;" />

要求是 时间复杂度O(n),空间复杂度是O(1)，而且求出相交的值

1. 暴力解法的话就是O(n^2)了，感觉不是很行得通，所以pass掉

2. n的话那就只能用一个链表去遍历，这是java诶，所以的话可以用到Set呀

   ```java
   public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
       //创建集合set
       Set<ListNode> set = new HashSet<>();
       //先把链表A的结点全部存放到集合set中
       while (headA != null) {
           set.add(headA);
           headA = headA.next;
       }
   
       //然后访问链表B的结点，判断集合中是否包含链表B的结点，如果包含就直接返回
       while (headB != null) {
           if (set.contains(headB))
               return headB;
           headB = headB.next;
       }
       //如果集合set不包含链表B的任何一个结点，说明他们没有交点，直接返回null
       return null;
   }
   
   作者：sdwwld
   链接：https://leetcode-cn.com/problems/intersection-of-two-linked-lists/solution/ji-he-shuang-zhi-zhen-deng-3chong-jie-jue-fang-s-2/
   来源：力扣（LeetCode）
   著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
   ```

   

3. 感觉和循环链表很像，就是链表成了一个圆了，这时候的话就是因为长度相同，`a+b+c=b+a+c`,所以的话如果有相交的值的话碰到一起肯定就是那个相交的值，否则的话就是`a+b=b+a`，直接为null，最底端

   ```java
   /**
    * Definition for singly-linked list.
    * public class ListNode {
    *     int val;
    *     ListNode next;
    *     ListNode(int x) {
    *         val = x;
    *         next = null;
    *     }
    * }
    */
   public class Solution {
      public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
       ListNode l1 = headA, l2 = headB;
       while (l1 != l2) {
           l1 = (l1 == null) ? headB : l1.next;
           l2 = (l2 == null) ? headA : l2.next;
       }
       return l1;
   }
   }
   ```




## 2. 反转链表

https://leetcode-cn.com/problems/reverse-linked-list/

![image-20201123205805791](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201123205805791.png)

怎么说呢，mycodeschool两种方法都交过，但我目前就记得迭代法，但递归法还是有记忆的，永远的神！

希望你可以再做一遍

### 1. 迭代法

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {

        ListNode prev;
        ListNode currentNode;
        ListNode temp;
        if(head == null){
            return null;
        }
        prev = head;
        currentNode = head.next;
        while(currentNode != null){;
            temp = currentNode.next;
            currentNode.next = prev;
            prev = currentNode;
            currentNode = temp;
        }
        head.next = null;
        head = prev;
        return head;
    }
}
```

### 2.递归法

```java
class Solution {
	public ListNode reverseList(ListNode head) {
		//递归终止条件是当前为空，或者下一个节点为空
		if(head==null || head.next==null) {
			return head;
		}
		//这里的cur就是最后一个节点
		ListNode cur = reverseList(head.next);
		//这里请配合动画演示理解
		//如果链表是 1->2->3->4->5，那么此时的cur就是5
		//而head是4，head的下一个是5，下下一个是空
		//所以head.next.next 就是5->4
		head.next.next = head;
		//防止链表循环，需要将head.next设置为空
		head.next = null;
		//每层递归函数都返回cur，也就是最后一个节点
		return cur;
	}
}

作者：wang_ni_ma
链接：https://leetcode-cn.com/problems/reverse-linked-list/solution/dong-hua-yan-shi-206-fan-zhuan-lian-biao-by-user74/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

这个递归返回的是每层的最后一个结点，利用每轮的参数进行赋值，很tricky，很有趣哈

## 3. 按升序合并链表

https://leetcode-cn.com/problems/merge-two-sorted-lists/

![image-20201124225714520](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201124225714520.png)

### 我的代码(迭代)

我的代码的问题就是太冗余拉，而且很多没有必要的变量吧，还有的就是技巧不够，因为要解决空指针，就是第一个指针的问题，我的代码处理的不够好。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode temp1 = l1;
        ListNode temp2 = l2;
        ListNode newList = null;
        ListNode temp3 = null;
        if(temp1 == null){
            return temp2;
        }
        if(temp2 == null){
            return temp1;
        }
        while(temp1 != null && temp2 != null){
            if(temp1.val <= temp2.val){
                if(newList == null){
                    newList = temp1;
                    temp1 = temp1.next;
                    temp3 = newList;
                   
                }else{
                temp3.next = temp1;
                temp1 = temp1.next;
                temp3 = temp3.next;
                }
            }else if(temp1.val > temp2.val){
                if(newList == null){
                    newList = temp2;
                    temp2 = temp2.next;
                    temp3 = newList;
                }else {
                temp3.next = temp2;
                temp2 = temp2.next;
                temp3 = temp3.next;
                }
            }
        
        }
        // if(temp1 == null && temp2 != null){
        //     temp3.next = temp2; 
        // }else if(temp2 == null && temp1!= null){
        //     temp3.next  = temp1; 
        // }
        //我觉得我不怎么习惯用这种，我得多想这种，因为我觉得这种比较简洁
        temp3.next = (temp1 == null ? temp2 : temp1);
        return newList;
    }
}
```

### 标准代码

看这个-1就是用来代替上面的头节点怎么初始化的情况。太棒了哈

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode prehead = new ListNode(-1);

        ListNode prev = prehead;
        while (l1 != null && l2 != null) {
            if (l1.val <= l2.val) {
                prev.next = l1;
                l1 = l1.next;
            } else {
                prev.next = l2;
                l2 = l2.next;
            }
            prev = prev.next;
        }

        // 合并后 l1 和 l2 最多只有一个还未被合并完，我们直接将链表末尾指向未合并完的链表即可
        prev.next = l1 == null ? l2 : l1;

        return prehead.next;
    }
}

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/merge-two-sorted-lists/solution/he-bing-liang-ge-you-xu-lian-biao-by-leetcode-solu/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

### 

递归方法

看起来真的very简单？的代码，还是得想一下的哈,很想试一试

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        } else if (l2 == null) {
            return l1;
        } else if (l1.val < l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        } else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }

    }
}

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/merge-two-sorted-lists/solution/he-bing-liang-ge-you-xu-lian-biao-by-leetcode-solu/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

---------------------------11.25 anki---------------------------------

## 4. 递归

```c
/**********
【题目】假设以二维数组g[1..m][1..n]表示一个图像
区域，g[i][j]表示该区域中点(i,j)所具颜色，其值
为从0到k的整数。试编写递归算法，将点(i0,j0)所在
区域的颜色置换为颜色c。约定与(i0,j0)同色的上、
下、左、右的邻接点为同色区域的点。

表示图像区域的类型定义如下：
typedef char GTYPE[m+1][n+1];
**********/
void ChangeColor(GTYPE g, int m, int n, 
                 char c, int i0, int j0)
/* 在g[1..m][1..n]中，将元素g[i0][j0] */
/* 所在的同色区域的颜色置换为颜色c    */
{
      if(i0 > m || j0 > n || i0 < 1 || j0 < 1)
        return;

    char temp = g[i0][j0];
    g[i0][j0] = c;

    if(j0 - 1 >= 1)    
        if(g[i0][j0 - 1] == temp)
            ChangeColor(g, m, n, c, i0, j0 - 1);
    
    if(i0 - 1 >= 1)
        if(g[i0 - 1][j0] == temp)            
            ChangeColor(g, m, n, c, i0 - 1, j0);
            
    if(i0 + 1 <= m)
        if(g[i0 + 1][j0] == temp)
            ChangeColor(g, m, n, c, i0 + 1, j0);
    
    if(j0 + 1<= n)
        if(g[i0][j0 + 1] == temp)
            ChangeColor(g, m, n, c, i0, j0 + 1);  
     
     
}
```

我觉得是个比较简单的递归，但for some reason 我没做出来哈，感觉递归这方面我觉得我是真的不咋地哎

## 5.删除排序链表中的重复元素

https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201127113457086.png" alt="image-20201127113457086" style="zoom: 67%;" />

我只能说我傻逼，刚开始居然用了双指针

有两种方法，一种是递归，另外一种就是直接找

```java
//递归
public ListNode deleteDuplicates(ListNode head) {
    if (head == null || head.next == null) return head;
    head.next = deleteDuplicates(head.next);
    return head.val == head.next.val ? head.next : head;
}
```

```java
//直接法
 ListNode current = head;
    while (current != null && current.next != null) {
        if (current.next.val == current.val) {
             ListNode node = current.next; 
                current.next = node.next;
                node = null;//清除野指针
        } else {
            current = current.next;
        }
    }
    return head;
    }
```

## 6. Remove nth node from end of list

我做这道题基本是做出来了，但是呢，没有考虑到细节问题，这是我的错误，就很烦哈，实际上就是用到了快慢指针。

没有考虑到头节点的情况哈，蠢了蠢了，所以这时候用dummy's head是最好的方法

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201129100026285.png" alt="image-20201129100026285" style="zoom:67%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201129100049051.png" alt="image-20201129100049051" style="zoom:67%;" />

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
// 我的思路是使用双指针
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
       ListNode slow = head;
        ListNode fast = head;
        while(n-- > 0){
            fast = fast.next;
        }
        //这个是特殊情况噢，想得有点久了。就是刚好是第一个的时候。n = size时,噢，不对吼，那你如果为空的话必不能这样写
        if(fast == null) return head.next;
        fast = fast.next;
        while(fast != null){
            slow = slow.next;
            fast = fast.next;
        }
        slow.next = slow.next.next;
        return head;   
    }
}
```

我觉得更好的代码

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0, head);
        ListNode first = head;
        ListNode second = dummy;
        for (int i = 0; i < n; ++i) {
            first = first.next;
        }
        while (first != null) {
            first = first.next;
            second = second.next;
        }
        second.next = second.next.next;
        ListNode ans = dummy.next;
        return ans;
    }
}

作者：LeetCode-Solution
链接：https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/solution/shan-chu-lian-biao-de-dao-shu-di-nge-jie-dian-b-61/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

### dummy node

其实之前就遇到过了，而且觉得很好用。

个人理解，哑节点（dummy node）是初始值为NULL的节点，创建在使用到链表的函数中，可以起到避免处理头节点为空的边界问题的作用，减少代码执行异常的可能性。

也就是说，哑节点的使用可以对代码**起到简化作用**（**省略**当函数的入口参数**为空时的判断**）。

**总结：
哑节点（dummy Node）是一个被人为创建的节点，虽然其内容为NULL，但是它在堆中有占有一定的空间。
哑节点的使用可以避免边界问题的处理，达到简化代码与减少代码出错可能性的目的**

就是一般

```java
 ListNode dummy = new ListNode(0, head); //这种哈
```



## 7. Swap nodes in pairs

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201130153736968.png" alt="image-20201130153736968" style="zoom:67%;" />

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode swapPairs(ListNode head) {
        //dummy 结点，避免为空
        ListNode dummy = new ListNode(-1);
        ListNode slow = dummy;
        dummy.next = head;
        ListNode fast = dummy.next;
        while(fast!=null && fast.next!=null){
            slow.next = fast.next;
            fast.next = fast.next.next;
            slow.next.next = fast;
            slow = fast;
            fast = fast.next;  
        }
        return dummy.next;
    }
}
```

这个是我的解法，反正怎么说呢，我觉得我应该边写边画图的，这样不用搞来搞去了。

### 递归法

递归法是我不擅长也是不熟悉的，但是我也得学会使用

```java
  //recursion version，看下能不能做出来把,感觉摸到了点门路了。
        if (head == null || head.next == null) {
            return head;
        }
        ListNode newHead = head.next;
        head.next = swapPairs(newHead.next);
        newHead.next = head;
        return newHead;
```

感觉摸到了点门路，因为我差不多是看了 一篇文章的，因为基本上每个都是一样的，所以你只要关注一个递归过程就可以了。

https://lyl0724.github.io/2020/01/25/1/

相信很多初学者和我一样，这是一个思维误区，一定要走出来。既然递归是一个反复调用自身的过程，这就说明它每一级的功能都是一样的，**因此我们只需要关注一级递归的解决过程即可。**

我们需要关心的主要是以下三点：

1. 整个递归的终止条件。
2. 一级递归需要做什么？
3. 应该返回给上一级的返回值是什么？

**因此，也就有了我们解递归题的三部曲：**

1. **找整个递归的终止条件：递归应该在什么时候结束？**
2. **找返回值：应该给上一级返回什么信息？**
3. **本级递归应该做什么：在这一级递归中，应该完成什么任务？**

一定要理解这3步，这就是以后递归秒杀算法题的依据和思路。

没错哈，有点动力了。

然后看到discussion的时候，想问下什么是tail recursion? 我觉得我有必要去研究一下了

## 8. Add Numbers II

https://leetcode.com/problems/add-two-numbers-ii/

![image-20201202185408797](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201202185408797.png)

就是把一个链表加起来把，然后思考了下几种方法，递归的我没有想出来，我就硬想，实际上是需要辅助函数 的啊！

### 递归

```java
class Solution {
    int carry = 0;
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if (l1 == null)
            return l2;
        if (l2 == null)
            return l1;
        ListNode res;
        int len1 = getLen(l1), len2 = getLen(l2);
        if (len1 < len2) {
            res = add(l1, l2, len2 - len1);
        } else {
            res = add(l2, l1, len1 - len2);
        }
        if (carry > 0) {
            ListNode res1 = res;
            res = new ListNode(carry);
            res.next = res1;
        }
        return res;
    }
    public int getLen(ListNode l1) {
        int len = 0;
        while (l1 != null) {
            len++;
            l1 = l1.next;
        }
        return len;
    }
    //l2.length - l1.length == diff;
    public ListNode add(ListNode l1, ListNode l2, int diff) {
        if (l1.next == null && l2.next == null) {
            int sum = l1.val + l2.val;
            carry = sum / 10;
            return new ListNode(sum % 10);
        }
        ListNode res, next;
        int sum;
        if (diff == 0) {
            next = add(l1.next, l2.next, 0);
            sum = l1.val + l2.val + carry;
        } else {
            next = add(l1, l2.next, diff - 1);
            sum = carry + l2.val;
        }
        carry = sum / 10;
        res = new ListNode(sum % 10);
        res.next = next;
        return res;
    }
}
```

### 迭代

这个是比较好想出来的方法

用栈的方式

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Stack<Integer> s1 = new Stack<>();
        Stack<Integer> s2 = new Stack<>();
        ListNode temp1 = l1;
        ListNode temp2 = l2;
        while(l1 != null){
            s1.push(l1.val);
            l1 = l1.next;
        }
        while(l2 != null){
            s2.push(l2.val);
            l2 = l2.next;
        }
        int carry = 0;
        int sum = 0;
        int digit = 0;
        ListNode dummy = new ListNode(1);
        ListNode temp = dummy;
        while(!s1.isEmpty() || !s2.isEmpty() ){
            sum = carry;
            sum += s1.isEmpty() ? 0 : s1.pop();
            sum += s2.isEmpty() ? 0 : s2.pop();
            carry = sum / 10;
            digit = sum % 10;
            ListNode node = new ListNode(digit);
            node.next = temp.next;
            temp.next = node; 
        }
        if(carry == 1){
            return dummy;
        }
        return dummy.next;
    }
}
```

## 9. 回文链表

https://leetcode.com/problems/palindrome-linked-list/

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201203161853337.png" alt="image-20201203161853337" style="zoom:67%;" />

嘻嘻，基本上是我自己想的，但是呢还是有些欠考虑的地方把，比如说没有先提前考虑到空和一个的情况

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
//奇怪了，怎么会呢？
class Solution {
    public boolean isPalindrome(ListNode head) {
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode slow = dummy;
        ListNode fast = dummy;
        //无语了，越改越错，先回去把，应该是哪里出了问题。
        if(head == null || head.next == null){
            return true;
        }
        while(fast != null && fast.next != null){
            fast = fast.next.next;
            slow = slow.next;
        }
        //虽然说是简单，但也还是遇到问题了。
        //偶数结点
        if(fast != null){
            //变成一个奇数结点
            ListNode mid = new ListNode(-1);
            mid.next = slow.next;
            slow.next = mid;
            slow = slow.next;
        }
        //反转
        ListNode nex = slow.next;
        ListNode temp = slow;
        while(nex != null){
            temp = nex.next;
            nex.next = slow;
            slow = nex;
            nex = temp;
        }
        
        ListNode l1 = head;
        ListNode l2 = slow;
        int flag = 0;
        while(l1 != l2){
            if(l1.val != l2.val){
                flag = 0;
                break;
            }   
            l1 = l1.next;
            l2 = l2.next;
            flag = 1;
        }  
        return flag == 0 ? false : true;      
    }
}
```

缺点就是改变了原有的链表。

### 递归法

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    private ListNode front;
    private boolean recursivelyCheck(ListNode currentNode){

        if(currentNode != null){

            if(!recursivelyCheck(currentNode.next)){
                return false;
            }
            if(currentNode.val != front.val){
                return false;
            }
            front = front.next;
        }
        return true;
    }
    public boolean isPalindrome(ListNode head) {
       front = head;
        return recursivelyCheck(head);
    }
}
```

我觉得按照学到的方法蛮容易看懂的，后面自己试试！！

## 10. 分隔链表

蛮简单的，虽然我不是一次性过的，还是有一些小错误

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201205153927076.png" alt="image-20201205153927076" style="zoom: 50%;" />

https://leetcode.com/problems/split-linked-list-in-parts/

我一开始是分成了两种情况，但后面发现其实没有必要哈，因为数组初始化值就为null。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode[] splitListToParts(ListNode root, int k) {
        ListNode[] arr = new ListNode[k];
        int length = 0;
        ListNode temp = root;
        while(temp != null){
            temp = temp.next;
            length++;
        }
        temp = root;
        ListNode cur = root;
      
        int mod = length % k;
        int size = length / k;
       
        for(int i = 0; cur!= null && i < k; i++){
            arr[i] = cur;
            int curSize = size + (mod-- > 0 ? 1 : 0);
            for(int j = 0; j< curSize - 1; j++){
                cur = cur.next;
            }          
            ListNode next = cur.next;
            cur.next = null;
            cur = next;
        }
        return arr;
    }
}
```

## 11.  奇偶链表

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201206135517994.png" alt="image-20201206135517994" style="zoom:50%;" />

https://leetcode.com/problems/odd-even-linked-list/

这道题真的不难，但是我就是想错一些东西了！就我的思路基本上是差不多的，就是一些小细节没搞到。

1. while的内容判断不对，因为还是没搞清楚内核，实际上是一个必走得快的，走得快的去判断是否为null就好了。
2. while语句走，走的慢的要先走，不然走的快的会把后面的链表给打乱。没错，这就是我没仔细想的原因。
3. 解决最后even的null问题，所以直接让even走快就直接可以解决，而让odd走快，你还解决这个null问题。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    // public ListNode oddEvenList(ListNode head) {
    //     if(head == null){
    //         return null;
    //     }
    //     ListNode dummy = new ListNode(-1);
    //     dummy.next = head;
    //     ListNode odd = head;
    //     ListNode even = dummy;
        // ListNode temp = head.next;

        // while(odd != null && odd.next != null){
           
        //     // if(odd.next != null){
        //         even.next = even.next.next;
        //         even = even.next;
        //          odd.next = odd.next.next;
        //     odd = odd.next;
        //     // }
            
        // }
        // odd.next = dummy.next;
        // even.next = null;

        // return head;
    // }
    public ListNode oddEvenList(ListNode head) {
    if (head == null) {
        return head;
    }
    ListNode odd = head, even = head.next, evenHead = even;
    while (even != null && even.next != null) {
        odd.next = odd.next.next;
        odd = odd.next;
        even.next = even.next.next;
        even = even.next;
    }
    odd.next = evenHead;
    return head;
}
}
```

# 2. 栈和队列

## 1.用栈实现对列(easy)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201209174010342.png" alt="image-20201209174010342" style="zoom:67%;" />

```java
class MyQueue {
    public Stack<Integer> stack1 = new Stack<>();
    public Stack<Integer> stack2 = new Stack<>();

    /** Initialize your data structure here. */
    public MyQueue() {

    }
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        stack1.push(x);
        
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        transfer();
        return stack2.pop();
    }
    
    /** Get the front element. */
    public int peek() {
        transfer();
        return stack2.peek();
    }
    //用完了再拿过去。
    public void transfer(){
        if(stack2.isEmpty()){
            while(!stack1.isEmpty()){
                stack2.push(stack1.pop());
            }      
         }
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return stack1.isEmpty() && stack2.isEmpty();
    }
}
```

不难，主要是在pop那里的问题，得思考思考。

## 2. 天气预测

这里接触到了一个新的概念，是单调栈，意思就是栈里面的元素都是具有单调性的，而且单调栈的题目都蛮有特点的

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210119223123637.png" alt="image-20210119223123637" style="zoom: 67%;" />

找到变暖的时间，就是找到比你大的在几天后，我的代码就是很暴力解，也没有用到队列什么的，所以的话就非常地慢。

反正我的思路就是我拿到一个，去一轮找一下，拿到下一个再去一轮找下，但我们并不是真的这么找的把，而是拿到这一个，，先放着，再去看下一个，再如果大的，那就直接是这个，但是如果小的话再继续放着，直到找到大的哈

```java
class Solution {
    public int[] dailyTemperatures(int[] T) {
         int n = T.length;
    int[] dist = new int[n];
    Stack<Integer> indexs = new Stack<>();
    for (int curIndex = 0; curIndex < n; curIndex++) {
        while (!indexs.isEmpty() && T[curIndex] > T[indexs.peek()]) {
            int preIndex = indexs.pop();
            dist[preIndex] = curIndex - preIndex;
        }
        indexs.add(curIndex);
    }
    return dist;
    }
}
```

## 3. 循环数组找下一个greater值

我蠢，我想了超级久

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210128224508167.png" alt="image-20210128224508167" style="zoom:67%;" />

无语哈，反正我是理解错题目了，一直在理解错，我觉得看英文反而能看懂，意思就是你自己为对头，你往下去找下一个greater的值，比如 `4729`,4找`729`,7找`294`，因此的话可以视作长度是 2n-1的。我服了我自己

```java
  int n = nums.length;
    int[] res = new int[n];
        Stack<Integer> stack = new Stack<>();
        Arrays.fill(res,-1);
        for(int i = 0; i < 2 * n - 1; i++){
            
            while(!stack.isEmpty() && nums[stack.peek()] < nums[i % n]){
                int temp = stack.pop();
                res[temp] = nums[i % n];
                if(temp == n - 1 && stack.isEmpty()) break;//这个条件减少了一点把，不过不要应该也是ok的
            }
            stack.push(i % n);   
        }
        return res;
```

正着来，也可以反着来,

```java
public class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int[] res = new int[nums.length];
        Stack<Integer> stack = new Stack<>();
        for (int i = 2 * nums.length - 1; i >= 0; --i) {
            while (!stack.empty() && nums[stack.peek()] <= nums[i % nums.length]) {
                stack.pop();
            }
            res[i % nums.length] = stack.empty() ? -1 : nums[stack.peek()];
            stack.push(i % nums.length);
        }
        return res;
    }
}

作者：LeetCode
链接：https://leetcode-cn.com/problems/next-greater-element-ii/solution/xia-yi-ge-geng-da-yuan-su-ii-by-leetcode/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

# 3. 树

## 1. 路径总和 III

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210203115009433.png" alt="image-20210203115009433" style="zoom: 50%;" />

就怎么说呢，这道题很interesting,好像是有好几种方法来着的， 但是我呢，感觉也不是完全自己写出来的把，因为蛮神奇的，其实我想到了差不多的点子，希望下次可以自己想出来啊

```java
class Solution {
    public int pathSum(TreeNode root, int sum) {
        if(root == null) return 0;
        int result = path(root,sum) + pathSum(root.left, sum) + pathSum(root.right, sum);
        return result;
    }
    
    public int path(TreeNode root, int sum){
        if(root == null) return 0;
        int result = 0;
        if(sum == root.val) result++;
        result += path(root.left, sum - root.val) + path(root.right, sum - root.val);
        return result;
    }
}
```

### 2. prefix sum

![image-20210204141725508](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210204141725508.png)

这个是前缀和，怎么说呢，差不多的原理在排序那里遇到过，希尔排序那里，

![image-20210204141847715](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210204141847715.png)

![image-20210204142105357](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210204142105357.png)

这个的确我有想到了，你想算subarray的话，基本上就是这个原理

![image-20210204113820730](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20210204113820730.png)

```java
class Solution {
    public int pathSum(TreeNode root, int sum) {
       HashMap<Integer,Integer> map =  new HashMap<>();
       map.put(0,1);
       return path(root, 0, sum, map);
    }
    
    public int path(TreeNode root, int runningSum, int target, HashMap<Integer,Integer> map){
       if(root == null){
           return 0;
       }
       runningSum += root.val;
       int count = map.getOrDefault(runningSum - target, 0);
       map.put(runningSum, map.getOrDefault(runningSum, 0) + 1);
       
       count += path(root.left, runningSum, target, map) 
        + path(root.right,runningSum,target,map);
        map.put(runningSum,map.get(runningSum) - 1);
        return count;
    }
}
```

我终于懂这个代码什么意思了呃，他主要是说了O(n)，所以就一轮，而且上面prefix sum讲了，如果你不从根节点算的话，你可以通过减的形式去判断是否获取一种路径，`running- target`这里就是哈，count 就是获取本轮可以凑成的数，再对下面进行加加就好了，实际上也是一个dfs，而且要回溯，那么就要在map里面的`runningSum - 1`就可以了，有趣啊啊啊啊