有环：一个faster，一个slower，如果交会，说明有环

环位置：新一个runner从头走，slow或fast继续走，交汇处为环起始点（slow＝a+b，fast=a+b+c+b, 2slow=fast =&gt;a=c）

```java
public ListNode hasCycle(ListNode head) {
  if(head==null)
  return null;

  ListNode fast=head;
  ListNode slow=head;
  while(fast!=null&&fast.next!=null){
  fast=fast.next.next;
  slow=slow.next;
       if(slow==fast){
          ListNode start=head;
          while(start!=slow){
               start=start.next;
               slow=slow.next;
          }
          return start;
       }
  }
  return null;
  }

```

总结： 1. list中while循环的条件，要看里面用到的条件！！

               如果内部用了fast＝fast.next.next，那么while一定要写while\(fast!=null&&fast.next!=null\) 不然会抛出异常

