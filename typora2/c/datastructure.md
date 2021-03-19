##  Tree

![IMG_4954](D:\tim\1097641461\FileRecv\MobileFile\IMG_4954.PNG)![IMG_4953](D:\tim\1097641461\FileRecv\MobileFile\IMG_4953.PNG)

树在这里的例子实际上就是倒过来的，根在最上面，然后branches 在最下面。



![IMG_4955](D:\tim\1097641461\FileRecv\MobileFile\IMG_4955.PNG)





![IMG_4956](D:\tim\1097641461\FileRecv\MobileFile\IMG_4956.PNG)



![IMG_4957](D:\tim\1097641461\FileRecv\MobileFile\IMG_4957.PNG)





![IMG_4958](D:\tim\1097641461\FileRecv\MobileFile\IMG_4958.PNG)





 ![IMG_4959](D:\tim\1097641461\FileRecv\MobileFile\IMG_4959.PNG)

有很多种关系，我觉得我可以一一来讲一下

1. root 就是最上面那个
2. children 就是有parent的东西
3. parent 有下面的分支
4. sibling 兄弟姐妹，有同个爸妈
5. leaf 没有children 的，自己是最后一个
6. ancestor 就是grandparents
7. descendent 后代，就是grandparents 的孩子
8. cousin 就是有相同的grandparents 不同的parents



![IMG_4960](D:\tim\1097641461\FileRecv\MobileFile\IMG_4960.PNG)

edges 是link 的意思，就是几条指的哪个link



![IMG_4961](D:\tim\1097641461\FileRecv\MobileFile\IMG_4961.PNG)

depth的话就是上往下数，不不不，就是一个单纯衡量深度的东西，root就是0，再往下是1，再往下是2这样子



![IMG_4962](D:\tim\1097641461\FileRecv\MobileFile\IMG_4962.PNG)

height就是下往上数，也差不多，最下的为0，然后依次



![IMG_4963](D:\tim\1097641461\FileRecv\MobileFile\IMG_4963.PNG)







![IMG_4964](D:\tim\1097641461\FileRecv\MobileFile\IMG_4964.PNG)





![IMG_4965](D:\tim\1097641461\FileRecv\MobileFile\IMG_4965.PNG)

height of tree 你直接数就好



![IMG_4966](D:\tim\1097641461\FileRecv\MobileFile\IMG_4966.PNG)

binary tree 应该算是最常见的了，他只允许一个parent有两个kids 



![IMG_4967](D:\tim\1097641461\FileRecv\MobileFile\IMG_4967.PNG)

左边的那个储存的是左边孩子的address，右边那个储存的是右边孩子的address

![IMG_4968](D:\tim\1097641461\FileRecv\MobileFile\IMG_4968.PNG)





![IMG_4969](D:\tim\1097641461\FileRecv\MobileFile\IMG_4969.PNG)





![IMG_4970](D:\tim\1097641461\FileRecv\MobileFile\IMG_4970.PNG)

最后一个是校验拼写的，觉得很有趣哈





## 2. binary tree



这节基本讲的是一些性质和类型吧

1. strict proper binary tree

> 只能有0个或2个 的子node

1. complete binary tree

> 就是从左往右，进行添加node就可以，无论你的子node有多少个

1. perfect binary tree

> 就是完美的，你的所有node都有两个子node

1. balanced binary tree

> 有规定，左边最底，和右边最底的差距不能超过k，通常情况下是1

![IMG_5018](D:\tim\1097641461\FileRecv\MobileFile\IMG_5018.PNG)





![IMG_5019](D:\tim\1097641461\FileRecv\MobileFile\IMG_5019.PNG)





![IMG_5020](D:\tim\1097641461\FileRecv\MobileFile\IMG_5020.PNG)







![IMG_5021](D:\tim\1097641461\FileRecv\MobileFile\IMG_5021.PNG)







![IMG_5022](D:\tim\1097641461\FileRecv\MobileFile\IMG_5022.PNG)







![IMG_5023](D:\tim\1097641461\FileRecv\MobileFile\IMG_5023.PNG)







![IMG_5024](D:\tim\1097641461\FileRecv\MobileFile\IMG_5024.PNG)

这个就是计算的公式咯，



![IMG_5025](D:\tim\1097641461\FileRecv\MobileFile\IMG_5025.PNG)





![IMG_5026](D:\tim\1097641461\FileRecv\MobileFile\IMG_5026.PNG)







![IMG_5027](D:\tim\1097641461\FileRecv\MobileFile\IMG_5027.PNG)







![IMG_5028](D:\tim\1097641461\FileRecv\MobileFile\IMG_5028.PNG)

当我们要充分利用树的话，就要尽量dense，所以呢就需要把每个都填满，右边那个是很不好的



![IMG_5029](D:\tim\1097641461\FileRecv\MobileFile\IMG_5029.PNG)





![IMG_5030](D:\tim\1097641461\FileRecv\MobileFile\IMG_5030.PNG)





![IMG_5031](D:\tim\1097641461\FileRecv\MobileFile\IMG_5031.PNG)





![IMG_5032](D:\tim\1097641461\FileRecv\MobileFile\IMG_5032.PNG)





![IMG_5033](D:\tim\1097641461\FileRecv\MobileFile\IMG_5033.PNG)

好像又有两种tree的模式把，一个是数组，一个是链表



![IMG_5034](D:\tim\1097641461\FileRecv\MobileFile\IMG_5034.PNG)







![IMG_5035](D:\tim\1097641461\FileRecv\MobileFile\IMG_5035.PNG)

emm这个还是可以求的。。啦

![IMG_5036](D:\tim\1097641461\FileRecv\MobileFile\IMG_5036.PNG)





![IMG_5037](D:\tim\1097641461\FileRecv\MobileFile\IMG_5037.PNG)

就讲了一些性质上的东西就没了哈

## 3. binary search tree

![IMG_5082](D:\tim\1097641461\FileRecv\MobileFile\IMG_5082.PNG)

binary search tree 的摆放是有一定规则的，左边的比自己小，右边比自己大

![IMG_5076](D:\tim\1097641461\FileRecv\MobileFile\IMG_5076.PNG)

因为单纯的数组和链表的效率都不怎么样，所以选择了这个，因为三个的O 都是logn



![IMG_5077](D:\tim\1097641461\FileRecv\MobileFile\IMG_5077.PNG)





![IMG_5078](D:\tim\1097641461\FileRecv\MobileFile\IMG_5078.PNG)



![IMG_5079](D:\tim\1097641461\FileRecv\MobileFile\IMG_5079.PNG)



![IMG_5082](D:\tim\1097641461\FileRecv\MobileFile\IMG_5082.PNG)



![IMG_5083](D:\tim\1097641461\FileRecv\MobileFile\IMG_5083.PNG)



![IMG_5084](D:\tim\1097641461\FileRecv\MobileFile\IMG_5084.PNG)

wrong 哈，而且但我们插入的时候是不会让你跑到左边去的





![IMG_5085](D:\tim\1097641461\FileRecv\MobileFile\IMG_5085.PNG)





![IMG_5086](D:\tim\1097641461\FileRecv\MobileFile\IMG_5086.PNG)

这样是不行的，所以要balanced

![IMG_5087](D:\tim\1097641461\FileRecv\MobileFile\IMG_5087.PNG)

#### 代码

> 主要是用到了递归，因为要不断的比较，代码等我一起学完那些再去补哈

![IMG_5093](D:\tim\1097641461\FileRecv\MobileFile\IMG_5093.PNG)







![IMG_5094](D:\tim\1097641461\FileRecv\MobileFile\IMG_5094.PNG)





![IMG_5095](D:\tim\1097641461\FileRecv\MobileFile\IMG_5095.PNG)





![IMG_5096](D:\tim\1097641461\FileRecv\MobileFile\IMG_5096.PNG)





![IMG_5097](D:\tim\1097641461\FileRecv\MobileFile\IMG_5097.PNG)





![IMG_5098](D:\tim\1097641461\FileRecv\MobileFile\IMG_5098.PNG)



![IMG_5099](D:\tim\1097641461\FileRecv\MobileFile\IMG_5099.PNG)

其实没讲什么

但是还是觉得最后不是很高效，因为发现每插入一次进去的话就要对root重新赋一次值，感觉还可以提高下效率？ 

### 2. findMin findMax

>  怎么说呢，可以有两种方式去找，一种是迭代，另外一种是递归，本身也没那么难找啊  ，一直往左 一直往右就好了

> ![IMG_5252](D:\tim\1097641461\FileRecv\MobileFile\IMG_5252.PNG)





![IMG_5253](D:\tim\1097641461\FileRecv\MobileFile\IMG_5253.PNG)

### 3.find height

> 根据之前 的 找高度，leaf node 的高度就为0

![IMG_5254](D:\tim\1097641461\FileRecv\MobileFile\IMG_5254.PNG)







![IMG_5255](D:\tim\1097641461\FileRecv\MobileFile\IMG_5255.PNG)







![IMG_5256](D:\tim\1097641461\FileRecv\MobileFile\IMG_5256.PNG)



这里的最终结果就是最后的为 -1.因为之前本来也就规定了如果没有root的话 高度就为-1的然后自身的高度是在+1 那里实现 的

也不难不过大概也就这样子了吧



![IMG_5257](D:\tim\1097641461\FileRecv\MobileFile\IMG_5257.PNG)



-----------------------------------------------anki到这里把---------------------------------------------------------------------

## 4.Binary tree travesal

![image-20200718230236478](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200718230236478.png)

可以从两个角度进行遍历

![image-20200718230425736](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200718230425736.png)

depth first 的话就有三种顺序哈

![image-20200718230719490](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200718230719490.png)

这个的话要求你遍历到一个 child node 的时候就要把 child node 下面的东西都给遍历了，所以他大概是这个样子哈

![image-20200718230843835](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200718230843835.png)

![image-20200718231003988](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200718231003988.png)

> 这里的话就很tricky哈，虽然说我不知道这个会应用在哪里，但是的话就十分地有趣。主要有趣就是体现在从F开始这里，left搞完了，开始搞右，但对右来说，他们也是一个结点，所以也要从left -> data ->right来搞，所以的话就是直接到G ->H->I->J->K。
>
> 这个给出来的是sorted order

![image-20200718231015573](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20200718231015573.png)

> 这里的话原理也差不多，和上面的，最重要的是你是别人的left or right，但你是自己的root，所以的话是要这样子看的哈。

## 5. Level-order Traversal(实际上就是 breadth 查找)

![image-20201019210642876](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019210642876.png)

要用queue诶，因为单链表是不现实的，他不能返回去。

![image-20201019211915186](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019211915186.png)

> 这个就是临时创建了一个queue来，所以这种会比较占内存

```c++
#include<iostream>
#include<queue>
using namespace std;

struct Node{
    char data;
    Node *left;
    Node *right;
};

void LevelOrder(Node *root){
    if(root == NULL){
        return;
    }
    queue<Node*> Q;
    Q.push(root);
    while (!Q.empty())
    {
        /* code */
        Node* current = Q.front();
        cout<<current->data<<" ";
        if(current->left !=NULL){
            Q.push(current->left);
        }
        if(current->right != NULL){
            Q.push(current->right);
        }
        Q.pop();//removing the element at front
    }
}
Node* Insert(Node *root,char data){
    if(root  == NULL){
        root = new Node();
        root->data = data;
        root->left = root->right = NULL;
    }else if(data <= root->data){
        root->left = Insert(root->left,data);
    }else{
        root->right = Insert(root->right,data);
    }
    return root;
}
int main(){
    	/*Code To Test the logic
	  Creating an example tree
	             M
			   / \
			  B   Q
			 / \   \
			A   C   Z
    */
	Node* root = NULL;
	root = Insert(root,'M'); root = Insert(root,'B');
	root = Insert(root,'Q'); root = Insert(root,'Z'); 
	root = Insert(root,'A'); root = Insert(root,'C');
	//Print Nodes in Level Order. 
	LevelOrder(root);
}
```

### Time Complexity & Space Complexity

![image-20201019214931467](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019214931467.png)

> 为什么是constant呢？因为基本上就是去掉一个加一个，那最大也就是1了哈

![image-20201019215203715](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201019215203715.png)

worst case 也很好理解吧，就是在最后一排的时候就是了，差不多少n/2把

## 6.  depth first 的代码

![image-20201022093248415](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022093248415.png)

![image-20201022093254251](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022093254251.png)

![image-20201022094319044](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094319044.png)

![image-20201022094326736](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094326736.png)

![image-20201022094333992](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094333992.png)

![image-20201022094342460](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094342460.png)

![image-20201022094348402](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094348402.png)

![image-20201022094354124](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094354124.png)

```c++
/* Binary Tree Traversal - Preorder, Inorder, Postorder */
#include<iostream>
using namespace std;

struct Node{
    char data;
    Node* left;
    Node* right;
};

//Function to visit nodes in Preorder
void Preorder(Node* root){
    if(root == NULL){
        return;
    }
    cout<< root->data << " ";
    Preorder(root->left);
    Preorder(root->right);
}

//Function to visit nodes in Inorder
void Inorder(Node* root){
    if(root == NULL){
        return;
    }
    Inorder(root->left);
    cout<< root->data << " ";
    Inorder(root->right);
}

//Function to visit nodes in Postorder
void Postorder(Node *root){
    if(root == NULL){
        return;
    }
    Postorder(root->left);
    Postorder(root->right);
    cout << root->data <<  " ";
}
Node* Insert(Node *root,char data){
    if(root  == NULL){
        root = new Node();
        root->data = data;
        root->left = root->right = NULL;
    }else if(data <= root->data){
        root->left = Insert(root->left,data);
    }else{
        root->right = Insert(root->right,data);
    }
    return root;
}
int main(){
    Node* root = NULL;
    root = Insert(root,'M'); root = Insert(root,'B');
	root = Insert(root,'Q'); root = Insert(root,'Z'); 
	root = Insert(root,'A'); root = Insert(root,'C');

    Preorder(root);
    cout << endl;
    Inorder(root);
    cout << endl;
    Postorder(root);
    cout<< endl;


}

```

这个真的很简单，代码看起来要简单很多

其实的确很简单，后面再去实现吧。

## 7. check if it is BST

![image-20201022094536491](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094536491.png)

这个最起码的是要左小右大把，每个结点都要这样子

![image-20201022094541767](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094541767.png)

![image-20201022094546786](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094546786.png)

-------------------------2020.10.25 anki到这里--------------------------

![image-20201022094551852](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094551852.png)

![image-20201022094556889](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094556889.png)

ok，这里一开始比较难理解的就是`IsSubtreeLesser` `IsSubTreeGreater`

```
    7
  3   8
 1 4 7 9
```

他呢就是从7开始，传的7的node，value一直是7，然后这个value就一直不变了哈，所以的话就是判断7左边的subtree是不是每个结点 都小于7，就这样子。`IsSubtreeGreater`也是一样，比较右边的结点是不是都大于root，然后就继续查，这样想想，很慢啊，因为涉及到了每个结点都要比较的问题。就像是同个区域的快递，不讨论一次能送多少的问题，就是一个人一个人地送，然后再返回去拿，正确的做法是全部拿好久派送啊对吧。

![image-20201022094602497](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094602497.png)

![image-20201022094609496](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094609496.png)

这个就是比较的代码，十分地复杂，其实我是不会用这种方法的

![image-20201022094615789](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094615789.png)

![image-20201022094622062](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094622062.png)

![image-20201022094628560](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094628560.png)

![image-20201022094635157](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094635157.png)

![image-20201022094640609](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094640609.png)

![image-20201022094646196](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094646196.png)

改了改了，在这里改了，这里改后的代码就不需要重复了，不过也挺符合我们的思路的，我们比较的时候也是按这种思路去比较判断，并没有重复。这个就是不断的改范围，只要你数字是这个范围的，那就ok哈。然后我一直疑惑的是这个无穷是怎么表示的，看到后面我就知道了。

![image-20201022094653091](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094653091.png)

![image-20201022094658936](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094658936.png)

![image-20201022094704407](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094704407.png)

```c++
#include<iostream>
#include<queue>
using namespace std;
struct Node{
    char data;
    Node *left;
    Node *right;
};

Node* Insert(Node *root,char data){
    if(root == NULL){
        root = new Node();
        root->data = data;
        root->left = root->right = NULL;
    }else if(data <= root->data){
        root->left = Insert(root->left,data);
    }else{
        root->right = Insert(root->right,data);
    }
    return root;
}

void LevelOrder(Node *root){
    if(root == NULL){
        return;
    }
    queue<Node*> Q;
    Q.push(root);
    while (!Q.empty())
    {
        /* code */
        Node* current = Q.front();
        cout<<current->data<<" ";
        if(current->left !=NULL){
            Q.push(current->left);
        }
        if(current->right != NULL){
            Q.push(current->right);
        }
        Q.pop();//removing the element at front

    }
    

}
bool IsBstUtil(Node* root,int minValue,int maxValue){
    if(root == NULL){
        return true;
    }
    if(root->data > minValue && root->data < maxValue 
    && IsBstUtil(root->left,minValue,root->data)
    && IsBstUtil(root->right,root->data,maxValue)){
        return true;
    }
    return false;
}
//判断是否为BST
bool IsBinarySearchTree(Node* root){
    return IsBstUtil(root,INT_MIN,INT_MAX);
}

int main(){
    Node* root = NULL;
    //这里的root的返回多理解了一层，返回的是根结点，这个不像普通链表一样，你能在insert中直接保存一个根节点的，不过也主要是在递归中起反复赋值的作用
    root = Insert(root,'M'); root = Insert(root,'B');
	root = Insert(root,'Q'); root = Insert(root,'Z'); 
	root = Insert(root,'C'); root = Insert(root,'A');
    bool flag = IsBinarySearchTree(root);
    cout << flag << endl;
    LevelOrder(root);
}
```



### 另外的方法，按照排出来的顺序看

因为之前我们排序dfs的时候的inorder，排出来刚好是从小到大的，那这里也可以先排出来，然后看是不是从小到大，另外一种方法，有趣。

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094723754.png" alt="image-20201022094723754" style="zoom:25%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094733066.png" alt="image-20201022094733066" style="zoom:25%;" />![image-20201022094741216](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094741216.png)

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022150334371.png" alt="image-20201022150334371" style="zoom:25%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022150346553.png" alt="image-20201022150346553" style="zoom:25%;" />

感觉差不多懂了，还蛮有趣的感觉，就是/\ ，这样子比较，找到最左边底下，然后就比较右边的了，反正比左边大就对了哈

## 8. delete a node from a BST

> 因为我之前学过binary heap，但是这和binary heap不一样哈，binary heap的insert就直接到最后的，但是这个的insert是要从最开始算起的。所以delete的方式也没有binary heap那样子来delete哈

![image-20201022094907427](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094907427.png)

![image-20201022094912893](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094912893.png)

![image-20201022094917790](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094917790.png)

> 这是当只有一个child的时候，非常好delete，直接链接上去就可以了哈

![image-20201022094932736](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094932736.png)

![image-20201022094939980](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094939980.png)

> 当一个node有两个children的时候就比较复杂，你不像heap sort那样是交换数据的，这个是直接删掉的，但是当有2个children的时候就不一样，我们要把第三种情况化为第二种和第一种，所以这里的话就可以为了避免有两个child，所以的话就应该找左边最大或者右边最小的。

![image-20201022094945793](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094945793.png)

![image-20201022094951936](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094951936.png)

![image-20201022094957480](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022094957480.png)

![image-20201022095002882](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022095002882.png)

![image-20201022095007919](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022095007919.png)

![image-20201022095013035](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022095013035.png)

![image-20201022163552033](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022163552033.png)

![image-20201022163557165](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022163557165.png)

![image-20201022163601787](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022163601787.png)

![image-20201022163606017](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022163606017.png)

![image-20201022163610305](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022163610305.png)

![image-20201022164314806](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022164314806.png)

![image-20201022164329453](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022164329453.png)

![image-20201022164603960](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022164603960.png)

![image-20201022164634989](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201022164634989.png)

```c++
#include<iostream>
using namespace std;

struct Node{
    int data;
    Node *left;
    Node *right;
};

//Function to find minimum in a tree
Node* FindMin(Node* root){
    while (root->left != NULL)
    {
        /* code */
        root = root->left;
    }
    return root;

}

//Function to search a delete a value from tree
struct Node* Delete(Node* root,int data){
    if(root == NULL){
        return root;
    }
    else if(data < root->data){
        root->left = Delete(root->left,data);
    }else if(data > root->data){
        root->right = Delete(root->right,data);
    //Wohoo... I found you, get ready to be deleted
    }else{
        //Case 1: No child
        if(root->left == NULL && root->right == NULL){
            delete root;
            root = NULL;
        }
        //Case 2: 1 child
        else if(root->left == NULL){
            Node* temp = root;
            root = root->right;
            delete temp;
        }
        else if(root->right == NULL){
            Node* temp = root;
            root = root->left;
            delete temp;
        }
        //Case 3: 2 children
        else{
            Node* temp = FindMin(root->right);
            root->data = temp->data;
            root->right = Delete(root->right,temp->data);
        }
        
    }
    return root;
}

//Function to visit nodes in Inorder
void Inorder(Node* root){
    if(root == NULL){
        return;
    }
    Inorder(root->left);
    cout<< root->data << " ";
    Inorder(root->right);
}

//Function to Insert Node in a Binary Search Tree
Node* Insert(Node* root,char data){
    if(root == NULL){
        root = new Node();
        root->data = data;
        root->left = root->right = NULL;
        
    }else if(data <= root->data){
        root->left = Insert(root->left,data);
    }else{
        root->right = Insert(root->right,data);
    }
    return root;
}
int main(){
    /*Code To Test the logic
	  Creating an example tree
	            5
			   / \
			  3   10
			 / \   \
			1   4   11
    */

   Node* root = NULL;
    root = Insert(root,5); root = Insert(root,10);
	root = Insert(root,3); root = Insert(root,4); 
	root = Insert(root,1); root = Insert(root,11);

	// Deleting node with value 5, change this value to test other cases
	root = Delete(root,5);

	//Print Nodes in Inorder
	cout<<"Inorder: ";
	Inorder(root);
	cout<<"\n";
}
```

## 9. inorder successor in a BST

之前没搞懂successor啥意思哈，实际上就是找下一个的点，应该找的点。因为是inorder，就是找你的下一个位是谁。然后有分成好多种情况的

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201028203122588.png" alt="image-20201028203122588" style="zoom:67%;" />

![image-20201028203129251](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201028203129251.png)

![image-20201028203136587](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201028203136587.png)

他的可能问题应该是比如4的下一位是谁啊，他就给你个数字而已，所以你要通过这个数字先去找这个结点才可以哈，所以先判空嘛，找不到结点那就为空



![image-20201028203141804](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201028203141804.png)

这个如果你有右子树的话那就很容易哈，比较难搞的是你要返回上面去找的。如果你要traversal之后再去找的话是O(n)，挺浪费的。

![image-20201028203147355](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201028203147355.png)

没有右子树情况，实际上也很有趣，因为BST的性质，就是你找你的下个是多少，毕竟inorder嘛，这说实话 我看了好久了。不得不说nb哈。其实就是在一个subtree中找另外的最左的点，或者直接是那个subtree的根节点，感觉不好表达出来呢，就是你找到一个比current值大的点了，再去他的左边，如果还有比current大的，就证明不是下一个，那就重新找successor，直到找到为止。

![image-20201028203152693](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201028203152693.png)

![image-20201028203158395](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201028203158395.png)

![image-20201028203204091](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201028203204091.png)

```c++
#include<iostream>
using namespace std;
struct Node{
    int data;
    Node* left;
    Node* right;
};
Node* Insert(Node* root,int data){
    if(root == NULL){
        root = new Node();
        root->data = data;
        root->left = root->right = NULL;
    
    }
    else if(data <= root->data){
        root->left = Insert(root->left,data);
    }else{
        root->right = Insert(root->right,data);
    }
    return root;
}
Node* FindMin(Node* root){
    
    if(root == NULL){
        return NULL;
    }
    while (root->left != NULL)
    {
        /* code */
        root=root->left;
    }
    return root;
}

Node* Find(Node* root,int data){
    if(root->data == data){
        return root;
    }
    if(root->data > data){
        return Find(root->left,data);
    }else if (root->data <= data)
    {
              return Find(root->right,data);
    }
    else
    {
        return NULL;
    } 
}

Node* GetSuccessor(Node* root,int data){
    Node* current = Find(root,data);
    //不会报空指针异常的哈，只是很无语罢了
    // cout<<temp->data<<endl;
    if(current == NULL){
        return NULL;
    }
     Node* temp = current->left;
    //Case 1: Node has right SubTree
    if(current->right != NULL){
        // Node* temp = current->right;
        // while (temp->left != NULL){
        //     temp = temp->left;
        // }
        // return temp;
        return FindMin(current->right);       
    }
    //Case 2: Node has no right SubTree
    else{
        Node* successor  = NULL;
        Node* ancestor = root;
        while (ancestor != current)
        {
            /* code */
            if(current->data < ancestor->data){
                successor = ancestor;
                ancestor = ancestor->left;
            }else{
                ancestor = ancestor->right;
            }
        } 
        return successor;
    }
}
void Inorder(Node* root){
    if(root == NULL){
        return;
    }
    Inorder(root->left);
    cout<< root->data << " ";
    Inorder(root->right);
}
int main(){
    Node* root = NULL;
    root = Insert(root,5);
   
     root = Insert(root,10);
     
	root = Insert(root,3);
    
     root = Insert(root,4); 
	root = Insert(root,1); root = Insert(root,11);
	//Print Nodes in Inorder
	cout<<"Inorder: ";
	Inorder(root);
	cout<<"\n";
    Node* temp = GetSuccessor(root,2);
    if(temp != NULL){
    cout<< temp->data << endl;
    }else
    {
        cout<<"没有哦"<<endl;
    }
}
```

## 10. heap

额，反正优先队列就是可以用二叉树实现的，所以无问题哈

怎么说呢，heap用到的ADT是tree，但有属于自己一套的增删规则，所以就是heap了。首先是complete binary tree,意思是必须是按顺序进行增删查改的。你可以化成下面的数组，中间是不能有空格的。

![image-20201029153304280](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153304280.png)

![image-20201029153315443](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153315443.png)

然后一般是用于优先队列中，用来排序的哈。

![image-20201029153324966](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153324966.png)

这个是在讲如何add，那就很简单其实，之前也已经说过了在优先队列那里。

-------------------------------anki到这里 2020.11.9--------------------------------

![image-20201029153334836](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153334836.png)

heap sort实际上就是从这个来的，根据delete，只是他不delete，但是我觉得顺序就反了。不知道他后面怎么解决额，就是本来delete就是和最后一个node进行交换，然后删掉，但是他不删掉，他只是放在最后，然后每次都是删掉第一个，那就刚好是排序了，因为会和最后一个交换，最后一个的位置是这样子变化的7->6->5->4->3->2->1，最后就好了。

![image-20201119215855671](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201119215855671.png)

heapify？我记得heapify有点特别的啊，然后这个heapsort还是和我想的一样。是倒序的。但是heapify的话就也是简单的，heapsort也是简单的，大概是nlogn把我猜，比bubblesort好，quicksort的话可能差不多

![image-20201029153346008](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153346008.png)

![image-20201029153357841](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153357841.png)

其实很简单哈，就是那一步步过程哈

![image-20201029153407539](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153407539.png)

time complexity，为什么这么说，因为是n个，然后呢每个都要swim，往上游，然后最多也就是height的程度了哈

### heapify

这里介绍了一种更好的create方式，time complexity更少，终于明白heapify是啥子了。

![image-20201029153440967](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153440967.png)

![image-20201029153451079](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153451079.png)

![image-20201029153500336](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153500336.png)

但是这个是有树了之后再整理排序诶。不过也应该是O(n)的样子。然后是对每个子树进行排序，然后升上去。有点bubblesort的感觉，但没重复那么多。我后面再找找具体的代码把

## 11. graph

![image-20201029153528224](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153528224.png)

![image-20201029153538495](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153538495.png)

其实图就和离散学的差不多，V是vertices，就是每个点，E是edges就是边，ordered就是有向的把，unordered就是，无向的把。

![image-20201029153547655](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153547655.png)

![image-20201029153556653](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153556653.png)

![image-20201029153608311](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153608311.png)

![image-20201029153617253](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153617253.png)

![image-20201029153627990](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153627990.png)

无向图就是这种朋友网，互关的这种。

![image-20201029153638881](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153638881.png)

这种就是有向的时候，不断的连接和连接

![image-20201029153649853](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153649853.png)

加权的图，算距离

![image-20201029153702281](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153702281.png)

![image-20201029153713767](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153713767.png)

### properties

![image-20201029153729749](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153729749.png)

一般括个绝对值代表个数的意思哈

![image-20201029153739683](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153739683.png)

self loop存在的意义比如你上某个网站，你点到别的页面，你还是可以通过点图标的形式回来的。

![image-20201029153750377](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153750377.png)

![image-20201029153801272](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153801272.png)

简单图就是你没有self loop 也没有多条loop

![image-20201029153812291](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153812291.png)

![image-20201029153823829](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153823829.png)

这个有向的很好理解把，就每个edge除了自己以外都可以连。无向的呢，就这样吧

![image-20201029153835971](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153835971.png)



![image-20201029153845856](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153845856.png)

![image-20201029153856291](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153856291.png)

trail是no edge repeated

![image-20201029153905815](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153905815.png)

强连通图就是每两个点之间就可以到达，弱连通图就是变成无向图的时候可以做到强连通的功能

![image-20201029153917793](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153917793.png)

closed walk实际上就是转一圈，但是呢可以重复点

![image-20201029153927717](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153927717.png)

cycle就是不重复点

![image-20201029153939724](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201029153939724.png)

没有cycle的图。

--------------------------------------anki 11.20======-----------------------------------

### 2. Representation part1

这里讲的是一种表达的方式，vertice首先毫无疑问是用个list搞起来，另外一个edge list的话一种思路是用struct的形式存的。

![image-20201101112536018](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101112536018.png)

![image-20201101112550837](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101112550837.png)

![image-20201101112603782](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101112603782.png)

![image-20201101112611153](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101112611153.png)![image-20201101112617497](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101112617497.png)

![image-20201101112623570](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101112623570.png)

![image-20201101112630652](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101112630652.png)

有权图就可以这么搞，然后你看下如果你要去找两个点是否是以edges形式连在一起的时候，首先你要去vertexlist看你对应的index，然后你在edge list里面要一一地找，这个效率非常差的哈

![image-20201101112637407](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101112637407.png)![image-20201101112644510](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101112644510.png)

![image-20201101112650711](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101112650711.png)

![image-20201101112657690](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101112657690.png)

### 3. representation part2

![image-20201101113756219](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101113756219.png)

这种是直接用个二维数组搞了，查是否连上的话就特别方便。只不过你要先一个个填就会比较浪费时间。就很像那种，你先难后易，这种就适合大型的

![image-20201101113804765](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101113804765.png)

![image-20201101113811271](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101113811271.png)

![image-20201101113818095](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201101113818095.png)

very fast了哈

## 12. disjoint sets

这是检查一个graph里面是否有cycle的？

其实这些步骤总的可以说是find and union，基本上的原理就是在一个set里面找是否有重复的点，有的话就证明有cycle哈

![image-20201105094222258](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094222258.png)

![image-20201105094232353](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094232353.png)

![image-20201105094239585](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094239585.png)



![image-20201105094244502](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094244502.png)

![image-20201105094316244](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094316244.png)

![image-20201105094321210](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094321210.png)

怎么又突然讲到树了？因为这是实际应用中会遇到的哈，你怎么去把这个想法去实施起来，那我们就用树哈，他是怎么一个实行的道理呢？我们一般认为在前面的那个为父类，当union的时候你是怎么操作的？首先{1,2},1 为parent node，{3,4}，3为parent node，{5,6}，5为parent node,{7,8}，7为parent node，{2,4}那怎么搞呢？让2为parent node的吗？后面你会发现，我们尽量不会增加depth，所以不可能的哈。因为2的parent node 是1，所以的话34这条直接连到1那里去，然后其他的就差不多这样了哈

![image-20201105094326259](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094326259.png)

![image-20201105094331210](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094331210.png)

![image-20201105094336113](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094336113.png)

然后现在是最后实践了，在数组这里，负号代表自己是parent node，1代表现在这个树有几个node。

![image-20201105094340549](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094340549.png)

所以这里连了一个edge之后，就有之前讲的指定node，所以的话连上了之后就变成了-2了，2这里的话指定的是他的parent node，所以为正。

![image-20201105094345364](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094345364.png)

![image-20201105094350243](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094350243.png)

![image-20201105094356705](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094356705.png)

![image-20201105094401883](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094401883.png)

![image-20201105094407420](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094407420.png)

![image-20201105094412408](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094412408.png)![image-20201105094417465](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094417465.png)

![image-20201105094422138](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201105094422138.png)

最后就是collapse，为什么这么做呢？因为他说的是浪费时间哈，的确也是。所以你可以把depth全都搞成1，那就完美了。

## 13. minimum cost spanning tree

你觉得这个可以实践在哪里啊，算距离的时候，最短的距离。

![image-20201112152736385](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112152736385.png)

![image-20201112152744282](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112152744282.png)

![image-20201112152750541](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112152750541.png)



![image-20201112152757614](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112152757614.png)

这个啥意思咯，其实就是不形成回路能形成的最短距离，所以这里总edges数要去掉cycle的个数

![image-20201112152808057](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112152808057.png)

这里有两种方法去计算哦，一个是像树一样把身边最小的去找，另外一种方法是先把小的全部找出来再说。

![image-20201112152814717](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112152814717.png)

![image-20201112152822913](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112152822913.png)

不要形成环就ok了

![image-20201112152829615](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112152829615.png)

![image-20201112152836366](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112152836366.png)



![image-20201112152843696](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112152843696.png)

![image-20201112152851647](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112152851647.png)

![image-20201112152859842](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112152859842.png)

![image-20201112153139493](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112153139493.png)

![image-20201112153214969](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112153214969.png)

很简单很简单啦。

## 14. union find 实际上也就是disjoint sets 的补充

和前面提到的不同的点在于呢，他在缩短距离讲的比较多，而且涉及到 了代码的部分

![image-20201112154541862](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112154541862.png)

![image-20201112154550942](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112154550942.png)

![image-20201112154557042](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112154557042.png)

![image-20201112154603622](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112154603622.png)

说一下这里有点不一样，这里是初始都默认自己是parent结点，其实这样也挺好的，不一样的就是多创建了一个数组罢了。

![image-20201112154609939](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112154609939.png)

![image-20201112154616629](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112154616629.png)

![image-20201112154630646](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112154630646.png)

![image-20201112155529015](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112155529015.png)

![image-20201112155536891](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112155536891.png)

![image-20201112155707847](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112155707847.png)

## 15. Hash Table

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201112155714479.png" alt="image-20201112155714479" style="zoom:50%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118095924285.png" alt="image-20201118095924285" style="zoom:50%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118100123222.png" alt="image-20201118100123222" style="zoom:50%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118100421650.png" alt="image-20201118100421650" style="zoom:50%;" />

这个意思是我们比较两个东西的时候，我们可以先比较他们的哈希值再来搞

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118100612532.png" alt="image-20201118100612532" style="zoom:50%;" />

这个例子就很好吧，当我们比较两个文件是否相同的时候，我们不想去比较他里面的内容，而是想去比较他的id把，差不多？哈希值

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118101029984.png" alt="image-20201118101029984" style="zoom:50%;" />

每次产生的hash值要一样！

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118103137149.png" alt="image-20201118103137149" style="zoom:50%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118103826424.png" alt="image-20201118103826424" style="zoom:50%;" />

how a hash table works

### 如果发生collision怎么做

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118104051887.png" alt="image-20201118104051887" style="zoom:50%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118104521273.png" alt="image-20201118104521273" style="zoom:50%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118114425187.png" alt="image-20201118114425187" style="zoom:50%;" />

#### separate chaining



## 15.2另外一个版本的Hash Table and Hash Functions

他是这么介绍的，你在一个数组里找数据需要知道他的index，但是有种方法可以让index与data有关，然后去找data，就是hash function

![image-20201118105135230](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118105135230.png)

他这里这么做的，把每个字母的ascii码加起来再取模数组的长度也就是11，得到最后的数字， Sum(Ascii) mod 11

![image-20201118105551135](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118105551135.png)

而且我们经常用hashmap这样做

![image-20201118105944512](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118105944512.png)

### opening address之linear probing

![image-20201118110204632](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118110204632.png)

反正我看这里的意思就是你发生collision的话，就会去旁边找，一个个找的感觉，因为这些address就都是open的

然后你要找的时候就也要linear search，就很麻烦

### load factor 装载因子

![image-20201118111024839](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118111024839.png)

### close chaining

![image-20201118112325136](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118112325136.png)

原来是这种啊用链表的形式，这样的话很多都是是对的，就是你要linear search而已，这样的话如果load factor小的话，用开放定址法比较合适，也就是size很充足的时候

### 总结

![image-20201118113118284](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118113118284.png)

开放定址法还是有很多种的，就不光是linear search，还有别的，你可以三个三个找，也可以二次方二次方找，也可以double找

### objectives of Hash Function

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118113931047.png" alt="image-20201118113931047" style="zoom:50%;" />

<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201118114020152.png" alt="image-20201118114020152" style="zoom:50%;" />

## 16.直接插入排序使用监视哨

这个是一个优化的算法，我个人觉得蛮有趣的，加快了速率非常好，话不多少，先看下吧

基本上是从这里学来的，https://blog.csdn.net/k0115/article/details/78994101

~~之前的插入排序的话感觉没那么像我们玩扑克那样洗牌，升级版之后才更像了，因为之前的出入排序就是按顺序一个个来的。~~

![image-20201116153944476](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201116153944476.png)

这样咯，但是你发现有很多移动啊，之类的，就不是很好。重复的感觉



### 升级版



<img src="C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201116154132018.png" alt="image-20201116154132018" style="zoom:67%;" />

改变下思路，先不要急着改变顺序哈，就像我们洗牌的时候也是经常这样干，有往两边拉的过程。然后这样子右边都是比自己大的了，就还不错

看看代码吧

```c
void insert_sort(int arr[],int length)
{
    int i,j;
    for( i=1 ; i< length; i++){
        int key = arr[i];//将待插入的元素保存起来
        for( j=i-1 ; j>=0; j--){
            if( arr[j]>key)//从后往前将所有大于key的元素往后移一格
                arr[j+1] = arr[j];
            else
                break;
            }   
            arr[j+1] = key;
            //函数运行到此处有两种情况：
            //1，j指向从后往前第一个小于或等于key的元素，只需将key
            //插入到此元素后即j+1处即可
            //2，已排序序列中没有比key大的元素，已被全部往后移动一格，
            //此时i指向-1，将key插入到arr[0]处刚好也是j+1处  
        }
}
```

但是可以改进一下，把if加到for循环里面去

```c
void insert_sort(int arr[],int length)
{
    int i,j;
    for(i=1; i<length; i++){
        int key = arr[i];
        for(j=i-1; j>=0 && arr[j]>key; j--){
            arr[j+1] = arr[j];
        }   
        arr[j+1] = key;
    }   
}
```

但是这时候还差点什么。

### 监视哨

这时候这个东西的作用就来了

对以上的代码有两个改进之处

第一个作用是用来存储每次待插入的元素，作用和上面那个函数中设置的变量key一样，监视哨要是只有这么一个作用的话，我们为什么要舍弃创建一个临时变量这么简单的办法不用而去用它呢。意思就是在这个数组中留一个位置专门放监视哨而不是创建一个变量。

第二个作用

解释第二个作用之前，我们先看一下我们之前写的一段代码：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190314141558327.png)
for循环条件部分，每次都要判断j>=0是否成立，不能省略。
而如果将带插入数据存放到arr[0]中，我们只需判断arr[j]>arr[0],因为即便已排序序列中所有数据都比带插入数据大，当循环进行到j=0时，依然会停下来，然后将带插入数据插入到arr[1[中。
因此设置监视哨可以省略判断j>=0这一步，可不要小看了这一步，一次循环少判断一次，n次循环就少判断n次，当要排序的元素数量极其庞大时，提高的效率就十分可观了。

### 最终版代码

```c
void insert_sort( int arr[], int length)
{
    int i,j;
    for(i=2; i<=length; i++){
        arr[0] = arr[i];//将待插入元素存放到监视哨中
        for(j=i-1; arr[j]>arr[0]; j--)
            arr[j+1] = arr[j];//将大于待插入元素的全部向后移一个
        arr[j+1] = arr[0];//插入待插入元素
    }   
}
```

## 17. Hash 函数等等的实操

```c
/**********
【题目】已知某哈希表的装载因子小于1，哈希函数H(key)
为关键字(标识符)的第一个字母在字母表中的序号，处理
冲突的方法为线性探测开放定址法。试编写一个按第一个
字母的顺序输出哈希表中所有关键字的算法。
哈希表的类型HashTable定义如下：
#define SUCCESS    1
#define UNSUCCESS  0
#define DUPLICATE -1
typedef char StrKeyType[4];
typedef struct {
   StrKeyType key; // 关键字项
   int    tag;     // 标记 0:空；1:有效; -1:已删除
   void  *any;     // 其他信息
} RcdType;
typedef struct {
  RcdType *rcd;    // 存储空间基址
  int      size;   // 哈希表容量
  int      count;  // 表中当前记录个数
} HashTable;
**********/
void PrintKeys(HashTable ht, void(*print)(StrKeyType))
/* 依题意用print输出关键字 */
{
    for(int i = 'A'; i <= 'Z'; ++i)
    {
        int j, k;
        int flag = 0;
        j = k = (i - 'A') % ht.size;
        while(((j + 1) % ht.size != k)&& flag == 0)
        {
            if(ht.rcd[j].tag == 1 && ht.rcd[j].key[0] == i)
            {
                print(ht.rcd[j].key);
                flag = 1;
            }
            ++j;
            j %= ht.size;
        }
    }
}
```

![image-20201120103309868](C:\Users\zbr\AppData\Roaming\Typora\typora-user-images\image-20201120103309868.png)

他是这样子的，线性探测嘛，他的方法就是绕一圈去探测，所以会有while里面的条件，找到了就可以说拜拜，进入下一轮，俺觉得没啥难的哈。

```c
/**********
【题目】假设哈希表长为m，哈希函数为H(x)，用链地址法
处理冲突。试编写输入一组关键字并建造哈希表的算法。
哈希表的类型ChainHashTab定义如下：
#define NUM         7
#define NULLKEY    -1
#define SUCCESS     1
#define UNSUCCESS   0
#define DUPLICATE  -1
typedef char HKeyType;
typedef struct HNode {
   HKeyType  data;
   struct HNode*  next;
}*HLink;
typedef struct {
   HLink  *rcd;   // 指针存储基址，动态分配数组
   int    count;  // 当前表中含有的记录个数
   int    size;  // 哈希表的当前容量
}ChainHashTab;    // 链地址哈希表
int Hash(ChainHashTab H, HKeyType k) { // 哈希函数
  return k % H.size;
}
Status Collision(ChainHashTab H, HLink &p) {
  // 求得下一个探查地址p 
  if (p && p->next) { 
    p = p->next;
    return SUCCESS;
  } else return UNSUCCESS;
}
**********/
int BuildHashTab(ChainHashTab &H, int n, HKeyType es[]) 
/* 直接调用下列函数                             */
/* 哈希函数：                                   */
/*    int Hash(ChainHashTab H, HKeyType k);     */
/* 冲突处理函数：                               */
/*    int Collision(ChainHashTab H, HLink &p);  */
{
   for(int i = 0; i < n; ++i)
    {
        int pos = Hash(H, es[i]);
        HLink temp;
        HLink p;
        int flag = 1;
         p =temp = H.rcd[pos];
       //我觉得这个collision用不上啊，因为这个链地址法是像是个栈一样的，就完全不用去找后面的，只是你要检查是否有重复罢了
      // while(p->data != NULLKEY && p->data != es[i] && p->next)
        //    Collision(H, p);
        while(temp){
            if(temp->data == es[i]){
                flag = 0;
            }
            temp = temp->next;
        }   
       //没有重复就可以变成头结点了
        if(flag)
        {       
            HNode *newNode;
            newNode = (HNode*)malloc(sizeof(HNode));
            newNode->data = es[i];
            newNode->next = p;
            H.rcd[pos] = newNode;
        }
    }
    return SUCCESS;
}
```

