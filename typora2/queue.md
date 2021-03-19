```java
public class QQQ {
    int[] queue=new int[5];
    int size;
    int front;
    int rear;
    public void enQueue(int data){
        queue[rear]=data;
        rear=(rear+1)%5;
        size++;
    }

    public int deQueue(){
        int data=queue[front];
        front=(front+1)%5;
        size--;
        return data;
    }

    public void show(){
        System.out.println("Elements:  ");
        for(int i=0;i<size;i++){
            System.out.println(queue[(i+front)%5]);
        }
    }
}
```

queue的原理

```java
public class Main {
    public static void main(String[] args) {
        QQQ q=new QQQ();
        q.enQueue(3);
        q.enQueue(2);
        q.enQueue(1);
        q.enQueue(5);
        q.enQueue(9);
        q.deQueue();
        q.deQueue();
        q.enQueue(0);
        q.enQueue(7);

        q.show();
    }

}
```

不过 记住peek和poll 都是return int 的，所以要sout

```java
public class Main {
    public static void main(String[] args) {
        Queue<String> q=new LinkedList<>();
        q.add("Su");
        q.add("Iby");
        System.out.println(q.peek());
        q.add("e");
        System.out.println(q);
    }

}
```

这才是真正的队列，最上面的是自己做的