---
title: 算法之反转问题
date: 2021-05-21
categories:
- algorithm
---
## 反转问题
- 链表反转 -剑指Offer.24
```java
//迭代
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode pre = null, cur = head;
        while(cur != null){
            ListNode nxt = cur.next; //保存下一个
            cur.next = pre; //当前连接上一个
            pre = cur; //将上一个后移
            cur = nxt; //将当前后移
        }
        return pre;
    }
}

//递归
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

```
递归的比较难理解，这里配合三个图(只要把这三步搞懂，这题就通了)
- 实际上在图1的红区已经是在执行4的next的next，所以head在下面是4，4.next=5，cur=5。这波啊，这波是秦王绕柱走
<img :src="$withBase('/img/fanzhuan-1.png')" alt="foo">
- 下面是给给指针调头的，让指针从4->5变成4<-5
<img :src="$withBase('/img/fanzhuan-2.png')" alt="foo">
<img :src="$withBase('/img/fanzhuan-3.png')" alt="foo">
  
---
整数反转
- 题目是这样的：
  - 给你一个 32 位的有符号整数 x ，返回将 x 中的数字部分反转后的结果。
  如果反转后整数超过 32 位的有符号整数的范围 [−231,  231 − 1] ，就返回 0。
  假设环境不允许存储 64 位整数（有符号或无符号）。
  - 分析：这个题考察的难点其实在数学，32位数，Integer范围在±2^32，而MAX_VALUE和MIN_VALUE就是代表的这个上下限
```java
class Solution {
    public int reverse(int x) {
        int ans = 0;
        while(x != 0){
            int pop = x%10;
            if(ans > Integer.MAX_VALUE/10 || (ans==Integer.MAX_VALUE/10 && pop>7))
                return 0;
            if(ans<Integer.MIN_VALUE/10 || (ans==Integer.MIN_VALUE/10 && pop<-8))
                return 0;
            ans = ans*10 + pop;
            x /= 10;
        }
        return ans;
    }
}
```