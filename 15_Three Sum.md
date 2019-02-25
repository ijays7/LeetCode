## Three Sum

Given an array `nums` of *n* integers, are there elements *a*, *b*, *c* in `nums` such that *a* + *b* + *c* = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:**

The solution set must not contain duplicate triplets.

**Example:**

```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

## Solution

这道题是[Two Sum](https://github.com/ijays7/LeetCode/blob/master/1_Two%20Sum.md)的升级版，给定一个数组，找到三个数a，b，c，使得 a + b + c = 0，并且答案不重复。

### Approach1

第一种思路是 sort and find。首先对数组进行排序，之后以第0位起作为基准点，从基准点的下一位到最后一位开始往中间夹。

什么意思呢？比如说在上面的 exmaple 中，以 -1 为基准点，0 和 -4 分别作为 low 和 high 指针，计算这三个数的和，如果刚好等于0，那么恭喜你，命中目标；如果和大于0，那么则吧 high 往左移；否则把 low 指针往右移。这么做的时间复杂度是 O($n^2$)。

这里要注意一点需要注意（两次 Wrong Answer 得出的教训），在第一次命中了目标之后，需要继续往下扫描，否则会少结果，并且要判断是否有重复的数据。上代码。

```java
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        
        if (nums == null || nums.length == 0) {
            return result;
        }
     
        Arrays.sort(nums);

        for (int i = 0; i < nums.length - 2; i++) {
            int low = i + 1;
            int high = nums.length - 1;

            while (low < high) {
                int sum = nums[i] + nums[low] + nums[high];

                if (sum == 0) {
                    List<Integer> integers = new ArrayList<>();
                    integers.add(nums[i]);
                    integers.add(nums[low]);
                    integers.add(nums[high]);
                    if (!result.contains(integers)) {
                        result.add(integers);
                    }
                    low += 1;
                    
                } else if (sum > 0) {
                    high -= 1;
                } else {
                    low += 1;
                }

            }

        }
        return result;
    }
```

上面的代码中命中目标后继续往下进行了扫描，但是为了判重使用了 contains 方法进行判断，可想而知，这个代码虽然可行，但是成绩不会太好。

参考了 discussion 中的类似代码后对上面的代码进行了优化，运行时间只用了35ms，由于99%的 Java 提交。

```java
 public static List<List<Integer>> threeSum(int[] nums) {
     // ...与前面一致
        for (int i = 0; i < nums.length - 2; i++) {

            if (nums[i] > 0) {
                // 如果基准点都大于0了，那么肯定不会存在等于0的情况了
                break;
            }

            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int low = i + 1;
            int high = nums.length - 1;

            while (low < high) {
                int sum = nums[i] + nums[low] + nums[high];

                if (sum == 0) {
                    List<Integer> integers = new ArrayList<>();
                    integers.add(nums[i]);
                    integers.add(nums[low]);
                    integers.add(nums[high]);
                    result.add(integers);

                    while (low < high && nums[low] == nums[low + 1]) low++;
                    low++;
                    while (low < high && nums[high] == nums[high - 1]) high--;
                    high--;

                } else if (sum > 0) {
                    high -= 1;
                } else {
                    low += 1;
                }
            }
        }
        return result;
    }
```



