## 1.1递归介绍

> 递归是一种编程技巧，一种解决问题的思维方式；严格来说，递归并不是一种算法。简单地说，就是如果在函数中存在着调用函数本身的情况，这种现象就叫递归。

* 递归的思想就是，将大问题分解为小问题来求解，然后再将小问题分解为更小的问题。这样一层一层地分解，直到问题规模被分解得足够小，不用继续分解，可以直接计算结果为止。
* 如果把这个一层一层的分解过程画成图，它其实就是一棵树。我们给这棵树起一个名字，叫作递归树。以斐波那契数列为例：

```java
public class Solution {
    public int fib(int N) {
        if (N <= 1) {
            return N;
        }
        return fib(N-1) + fib(N-2);
    }
}
```

* 计算公式如下：

| col1 | col2 | col3 |
| - | - | - |
| f(n) = f(n-1) + f(n-2) |   |   |
|   | f(n-1) = f(n-2) + f(n-3) |   |
|   | f(n-2) = f(n-3) + f(n-4) |   |

## 1.2 原理介绍

> 递归在**“归”**的过程中，符合后进先出的规则，所以需要用一个堆栈的数据结构。递归过程中函数调用会自动产生栈帧，当函数帧栈的深度越来越大的时候，栈也越来越大，如果递归没有终止条件，就会爆栈。所有基于递归思想实现的算法，第一步要思考的就是递归的终止条件。

* 分治算法和动态规划很大程度上是递归思想基础上的，解决更具体问题的两类算法思想。
* 进一步剖析「递归」，先有**「递」**再有**「归」**，「递」的意思是将问题拆解成子问题来解决， 子问题再拆解成子子问题，...，**直到被拆解的子问题无需再拆分成更细的子问题（即可以求解）**，「归」是说最小的子问题解决了，那么它的上一层子问题也就解决了，上一层的子问题解决了，上上层子问题自然也就解决了。
* `参考`：[https://www.jianshu.com/p/b2d2edb4ba5b]

## 1.3 基本步骤

* 定义一个函数，明确函数功能
* 寻找问题与子问题之间的关系（递推公式）
* 将递推公式在定义的函数中实现
* 推导时间复杂度，判定是否可以接受，无法接受更换算法

## 1.4 代表题目

### 1.4.1  [70\. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)

Difficulty: **简单**

假设你正在爬楼梯。需要 _n_ 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

**注意：**给定 _n_ 是一个正整数。

**示例 1：**

```
输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。
1\.  1 阶 + 1 阶
2\.  2 阶
```

**示例 2：**

```
输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。
1\.  1 阶 + 1 阶 + 1 阶
2\.  1 阶 + 2 阶
3\.  2 阶 + 1 阶
```

#### 解题思路：

* （1）定义一个函数，明确函数功能

> 定义函数签名，明确入参为n个台阶，返回数值为爬台阶的方法个数。
> int climbStairs(int n)

* （2）寻找问题与子问题之间的关系（递推公式）

> 这两者之前的关系初看确实看不出什么头绪，但是**自上而下地思考**，也就是说如果要上到 n 级台阶只能从n-1 或 n-2 级跳， 所以问题就转化为上到第 n-1 和 n-2 级台阶的方法, 这就是我们要找的问题与子问题的关系,而显然当 n = 1, n =2， 即跳一二级台阶是问题的最终解。
> f(n) = f(n-1) + f(n-2);

* （3）将递推公式在定义的函数中实现

```
public int climbStairs(int n) {
            //先对边界值进行处理
            if (n == 1) {
                return 1;
            }
            if (n == 2) {
                return 2;
            }
            return climbStairs(n - 1) + climbStairs(n - 2);

        }
```

* (4). 推导时间复杂度，判定是否可以接受，无法接受更换算法

> 按照递归实现该方法，在力扣提交之后：**31/ 45** 个通过测试用例。显然递归的效率很低时间复杂度过高，但是在楼梯数量较低的情况下还是解决了大部分问题。这时候就要思考更换算法。可以考虑提供带缓存机制的递归实现方法

#### Solution1

Language: ****
```
class Solution {
        public int climb(int n, int[] memo) {
            //先对边界值进行处理
            if (n == 1) {
                return 1;
            }
            if (n == 2) {
                return 2;
            }
            if (memo[n] > 0) {
                return memo[n];
            }
            memo[n] = climb(n - 1, memo)+climb(n - 2, memo);
            return memo[n];
        }

        public int climbStairs(int n) {
            int[] memo = new int[n+1];
            return climb(n, memo);
        }
    }
```

#### Solution2

```java
class Solution {
    public int climbStairs(int n) {
        int a = 1, b = 1;
        for (int i = 2; i <= n; i++) {
            int sum = a + b;
            a = b;
            b = sum;
        }
        return b;
    }
}
```
