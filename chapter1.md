# Linked-List

* 遍历linked list， Add two numbers

模版：

确定输入输出，定好parameter 和 return type

```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
//a. check l1 ==null and l2==null 情况

//make a new dummy head as return, and!!!!make a new pointer to it
ListNode rt=new ListNode(0);
ListNode curr=rt; //不能忘，这个pointer是用来走list的

int add=0; //相加勿忘进位
while(l1!=null||l2!=null){  //是用||还是&&要看情况
//将值相加，如果add=val/10 currVal=val%10
}

if(add!=0) //如果进位不为0，程序还不能返回
curr.next=new ListNode(add);
｝
```

总结：1.create dummy as return list head,

```
     2.create a list runner/or append input head to dummy

     3.如果input是两个list，while的终止条件可以是l1!=null\|\|l2!=null， 内部实现分情况判断，然后注意在if内写l1=l1.next

      4.最后记得判断add
```

* Delete linked list with only access to remove node

**Input: **\(2 -&gt;4 -&gt;3\) , 4

**Output:**2 -&gt;3

一般情况，对于singly linked list，remove时会保留一个pre，然后通过pre.next=remove.next来remove

但是这道题只给了remove node没有pre，方法是：

```java
remove.val=remove.next.val;
remove.next=remove.next.next;
```

* Reverse Linked List

* iterative 每次remove一个node，然后append到dummy的位置,1 2 3 4 5- &gt;21345-&gt;32145-&gt;

```java
public ListNode reverseList(ListNode head){
//check if head is null

//ListNode rt=new ListNode(0);
    rt.next=head;
    while(head!=null&&head.next!=null){
    //remove node
    ListNode removed=head.next;
    head.next=head.next.next;
    //insert to dummy
    removed.next=rt.next;
    rt.next=removed;
    //moving head
    //head=head.next
    }
return  rt.next;
}
```

1. 总结： 1.remove node of head.next

   1. insert after dummy

   2. head.next 永远指向下一个要remove的node，所以不用head＝head.next

2. Recursive reverse

1&gt;2&gt;3&gt;4&gt;5 进入最后一个点5，

然后把list变为1&gt;2&gt;3-&gt;4&lt;-5 返回5

然后把list变为1&gt;2&gt;3&lt;-4&lt;-5 返回5

```java
public ListNode reverseList(ListNode head){
if(head==null||head.next==null)
return head;
//going deeper into the list
ListNode newHead=reverseList(head.next);
head.next.next=head;
head.next=null;
return newHead;
}

```

总结：1. 任何时候判断结束时，如果有head.next==null，前面必须加head==null来判断结束，不然会抛出nullpointerException。

          2.注意head.next.next=head 而不是newhead.next＝head，前面的reverserList\(head.next\)只是为了让你进入循环





