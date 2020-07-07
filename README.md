## 数组
### （1）排序
* list升序和降序排列

```java
List<Integer> list = Arrays.asList(1, 4, 2, 5, 8);
list.sort(Comparator.naturalOrder()); //对整数列表进行排序（升序）
System.out.println(list);

List<Integer> list1 = Arrays.asList(1,45,3,67,8,9);
list1.sort(Comparator.reverseOrder()); //对整数列表进行排序（降序）
System.out.println(list1);
```

* int类型的数组进行升序和降序

```java
Integer[] nums1 = new Integer[] {3, 5, 1, 90, 9};
Arrays.sort(nums1, Collections.reverseOrder());   //对数组进行降序排列
for (int i : nums1) {
    System.out.println("降序好的数组:" + i);
}

//降序的另外一种方式：
Integer[] nums1 = new Integer[] {3, 5, 1, 90, 9};
Arrays.sort(nums1); // 1.排序
List<Integer> listn = Arrays.asList(nums1); //2.转为list
Arrays.sort(nums1, Collections.reverseOrder()); //3.转置reverse
for (int i : nums1) {
    System.out.println("排序好的数组:" + i);
}





Integer[] nums1 = new Integer[] {3, 5, 1, 90, 9};
Arrays.sort(nums1);                             //对数组进行升序排列
for (int i : nums1) {
    System.out.println("升序好的数组:" + i);
}

```

### (2) 重复
* hashset方法

```java
// 第一种解法： hashset
    // static class Solution {
    // public boolean containsDuplicate(int[] nums) {
    // HashSet<Integer> set = new HashSet<>();
    // for (int i = 0; i < nums.length; i++) {
    // if (set.contains(nums[i])) {
    // return true;
    // }
    // set.add(nums[i]);
    // }
    // return false;
    // }
    // }
```
* 第二种:相邻比较

```java
// 第二种解法，先排序，然后进行相邻比较，有重复的返回true即可
    static class Solution {
        public boolean containsDuplicate(int[] nums) {
            Arrays.sort(nums);
            for (int i = 1; i <= nums.length; i++) {
                if (nums[i] == nums[i - 1]) {
                    return true;
                }
            }
            return false;
        }
    }
```

### (3) 最大值/最小值
```java
public class max {
    public static void main(String[] args) {
        int[] arr = new int[] {2, 8, 9, 10, 8, 7, 6};
        // 第一种解法
        Arrays.sort(arr);
        System.out.println(arr[arr.length - 1]);

        // 第二种解法
        System.out.println(Arrays.stream(arr).max().getAsInt());
        //第三种解法
        int max = 0;
        for (int i = 0; i < arr.length; i++) {
             max = Math.max(arr[i], max);
        }

    }
}
```

