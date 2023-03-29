#### <a href="https://leetcode.cn/problems/kth-largest-element-in-an-array/">数组中的第 K 个最大元素</a>

-----------

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        return help(nums, 0, nums.length - 1, k);
    }

    private int help(int[] nums, int left, int right, int k) {
        if (left == right) return nums[left];
        int x = nums[left + right >> 1], i = left - 1, j = right + 1;
        while (i < j) {
            do i ++; while (nums[i] > x);
            do j --; while (nums[j] < x);
            if (i < j) {
                int t = nums[i];
                nums[i] = nums[j];
                nums[j] = t;
            }
        }

        int numk = j - left + 1;
        if (numk >= k) {
            return help(nums, left, j, k);
        } else {
            return help(nums, j + 1, right, k - numk);
        }
    }
}
```

