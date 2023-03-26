#### <a href="https://leetcode.cn/problems/k-items-with-the-maximum-sum/">K 件物品的最大和</a>

----------------

```java
class Solution {
    public int kItemsWithMaximumSum(int numOnes, int numZeros, int numNegOnes, int k) {
        int res = 0;
        while (k > 0 && numOnes > 0) {
            res += 1;
            k -= 1;
            numOnes --;
        }
        while (k > 0 && numZeros > 0) {
            k -= 1;
            numZeros --;
        }
        while (k > 0 && numNegOnes > 0) {
            res -= 1;
            k -= 1;
            numNegOnes --;
        }
        return res;
    }
}
```

