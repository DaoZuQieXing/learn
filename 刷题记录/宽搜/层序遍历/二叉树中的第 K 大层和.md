#### <a href="https://leetcode.cn/problems/kth-largest-sum-in-a-binary-tree/">二叉树中的第 K 大层和</a>

---------------

```java
class Solution {

    List<Long> list;
    int cnt = -1;

    public long kthLargestLevelSum(TreeNode root, int k) {
        list = new ArrayList<>();
        help(root);
        list.sort((o1, o2) -> o2.compareTo(o1));
        if (cnt < k) return -1;
        return list.get(k - 1);
    }

    private void help(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList();
        queue.offer(root);
        cnt ++;
        while (queue.size() > 0) {
            cnt ++;
            int size = queue.size();
            long sum = 0;
            for (int i = 0; i < size; i ++) {
                TreeNode node = queue.poll();
                sum += node.val;
                if (node.left != null) {
                    queue.offer(node.left);
                }
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
            list.add(sum);
        }
    }
}
```

