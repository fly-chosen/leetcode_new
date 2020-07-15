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

* 第三种：打印不重复的值
> nums = {4, 1, 4, 6} =====>不重复的值是{1,6}
```java
public int[] singleNumbers(int[] nums) {
    // 题目要求出现两个一次的数字
    int[] result = new int[2];
    // 要求时间负责度O(n),空间复杂度O(1)
    HashSet<Integer> set = new HashSet<>();
    // 然后使用Hashset进行判断
    for (int num : nums) {
        if (set.contains(num)) {
            set.remove(num);
        } else {
            set.add(num);
        }
    }
    return set.stream().mapToInt(Integer::intValue).toArray();
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

### （4）按照key值进行排序

```java
public class test10 {
    public static void main(String[] args) {
        int[] arr = new int[] {2, 8, 9, 10, 8, 7, 6};
        // 遍历整个数组，对记录每个数值出现的次数(利用HashMap，其中key为数值，value为出现次数)；
        Map<Integer, Long> map =
            Arrays.stream(arr).boxed().collect(Collectors.groupingBy(Function.identity(), Collectors.counting()));
        for (Map.Entry<Integer, Long> entry : map.entrySet()) {
            if (entry.getValue() > 0) {
                System.out
                    .println("按照每个数值key出现的次数value值进行排序：" + "key是：" + entry.getKey() + " value是：" + entry.getValue());
            }
        }

    }
}
```
```
按照每个数值key出现的次数value值进行排序：key是：2 value是：1
按照每个数值key出现的次数value值进行排序：key是：6 value是：1
按照每个数值key出现的次数value值进行排序：key是：7 value是：1
按照每个数值key出现的次数value值进行排序：key是：8 value是：2
按照每个数值key出现的次数value值进行排序：key是：9 value是：1
按照每个数值key出现的次数value值进行排序：key是：10 value是：1

```
### (5) 取数组中的key值出现的最大次数
* 使用Map<Integer, Integer> countMap，Map的键为元素的值，Map的值为该元素出现的次数。遍历原数组后得到Map，再遍历Map找到最大的出现次数，就得到了数组的度maxCount。
```java
public class test11 {
    public static void main(String[] args) {
        int[] nums = new int[] {1, 2, 3, 1, 1, 1, 1};
        HashMap<Integer, Integer> countMap = new HashMap<>();
        for (int num : nums) {
            if (countMap.containsKey(num)) {
                countMap.put(num, countMap.get(num) + 1);
            } else {
                countMap.put(num, 1);
            }
        }
        int maxCount = 0;
        for (int key : countMap.keySet()) {
            if (countMap.get(key) > maxCount) {
                maxCount = countMap.get(key);
            }
        }
        System.out.println(maxCount);

    }
}
```
```
结果： 数组{1, 2, 3, 1, 1, 1, 1}中，1出现的次数是maxCount=5 次。
```
