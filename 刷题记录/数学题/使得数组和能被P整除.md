#### <a href="https://leetcode.cn/problems/make-sum-divisible-by-p/">使得数组和能被P整除</a>

----------------

> 定理一：**给定正整数 x, y, z, p，如果 y mod p = x，那么 (y - z) mod p = 0 等价于 z mod p = x** 
>
> 证明：y mod p = x 等价于 y = k1 * p + x，(y - z) mod p = 0 等价于 y - z = k2 * p，z mod p = x 等价于 z = k3 * p + x，其中 k1、k2、k3 都是整数，那么给定 y = k1 * p + x，有 y - z = k2 * p $\equiv$ z = (k1 - k2) * p + x $\equiv$ z = k3 * p + x $\equiv$ z mod p = x

> 定理二：**给定正整数 x, y, z, p，那么 (y - z) mod p = x 等价于 z mod p = (y - x) mod p** 

```java
class Solution {
    public int minSubarray(int[] nums, int p) {
        int x = 0;
        for (int num : nums) {
            x = (x + num) % p;
        }

        if (x == 0) return 0;

        Map<Integer, Integer> map = new HashMap<>();
        int pre = 0;
        int res = nums.length;
        for (int i = 0; i < nums.length; i ++) {
            map.put(pre, i); // 只记最大的下标
            pre = (pre + nums[i]) % p;
            if (map.containsKey((pre - x + p) % p)) {
                res = Math.min(res, i - map.get((pre - x + p) % p) + 1);
            }
        }
        return res == nums.length ? -1 : res;
    }
}
```

