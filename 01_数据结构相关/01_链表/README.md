# 🦎链表
> 与数组相似，链表也是一种线性数据结构。与数组相似，链表也是一种线性数据结构。
* 链表有两种类型：单链表和双链表。

------------


## 🦎学习目的：

```
了解单链表和双链表的结构；
在单链表或双链表中实现遍历、插入和删除；
分析在单链表或双链表中的各种操作的复杂度；
在链表中使用双指针技巧（快指针慢指针技巧）；
解决一些经典问题，例如反转链表；
分析你设计的算法的复杂度；
积累设计和调试的经验。
```

------------

## 单链表
单链表中的每个结点不仅包含值，还包含链接到下一个结点的**引用字段**。通过这种方式，单链表将所有结点按顺序组织起来.
:👻:


|  数据域val |  next指针 |数据域val|next指针|
| ------------ | ------------ |------------ |------------ |
|  23 | ->  |6|->  |


### 结点结构
```java
// Definition for singly-linked list.
public class SinglyListNode {
    int val;
    SinglyListNode next;
    SinglyListNode(int x) { val = x; }
}
```
### 操作
* 👻
与数组不同，我们无法在常量时间内访问单链表中的随机元素。 如果我们想要获得第 i 个元素，我们必须从头结点逐个遍历。 我们**按索引来访问元素**平均要花费 O(N) 时间，其中 N 是链表的长度。
* 👻
例如，在上面的示例中，头结点是 23。访问第 3 个结点的唯一方法是使用头结点中的“next”字段到达第 2 个结点（结点 6）; 然后使用结点 6 的“next”字段，我们能够访问第 3 个结点。

* 👻
你可能想知道为什么链表很有用，尽管它在通过索引访问数据时（与数组相比）具有如此糟糕的性能。 在接下来的两篇文章中，我们将介绍插入和删除操作，你将了解到链表的好处。

### 设计链表
> 单链表中的节点应该具有两个属性：val 和 next。val 是当前节点的值，next 是指向下一个节点的指针/引用。如果要使用双向链表，则还需要一个属性 prev 以指示链表中的上一个节点

|  属性 | 意义  |
| ------------ | ------------ |
|  val | 当前节点的值  |
| next  |  指向下一个节点的指针/引用 |
|  prev | 指向链表中的上一个节点【针对于双链表而言】  |

### 相比数组，链表的非连续，非顺序确实让它在性能上处于劣势，那什么情况下该使用链表呢？考虑以下情况
* 大内存空间分配

由于数组空间的连续性，如果要为数组分配 500M 的空间，这 500M 的空间必须是连续的，未使用的，所以在内存空间的分配上数组的要求会比较严格，如果内存碎片太多，分配连续的大空间很可能导致失败。而链表由于是非连续的，所以这种情况下选择链表更合适。

* 元素频繁删除和插入
  * 如果涉及到元素的频繁删除和插入，用链表就会高效很多，对于数组来说，如果要在元素间插入一个元素，需要把其余元素一个个往后移（如图示），以为新元素腾空间（同理，如果是删除则需要把被删除元素之后的元素一个个往前移），效率上无疑是比较低的。
  * 而链表的插入删除相对来说就比较简单了，修改指针位置即可，其他元素无需做任何移动操作
  
> 综上所述：如果数据以查为主，很少涉及到增和删，选择数组，如果数据涉及到频繁的插入和删除，或元素所需分配空间过大，倾向于选择链表。
