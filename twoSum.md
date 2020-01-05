## 两数相加
* 给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

       你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

        示例:

        给定 nums = [2, 7, 11, 15], target = 9

        因为 nums[0] + nums[1] = 2 + 7 = 9
        所以返回 [0, 1]

### 第一种解法

最简单直接想法的方法就是：使用双层循环。对数组中的值进行遍历，找到坐标i，j对应的目标值求和的target即可。 最后直接返回两个值的元素下标值即可
但是这种方法的复杂度太高。 O(n^2)

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i=0;i < nums.length;i++){
            for(int j=i+1; j<nums.length;j++){
                if(nums[i] == target - nums[j]){
                    return new int[]{i,j};
                }
            }
        }throw new IllegalArgumentException("No two sum solution");
    }
}
```

### 第二种解法

在第一种解法的基础上，尽量减少遍历的次数，定义两个指针。从数组的前后两端进行遍历。

