#### <a href="https://leetcode.cn/problems/lru-cache/">LRU缓存</a>

--------------

哈希表＋双链表

哈希表实现getput

双链表左边表示新访问的key，右边表示旧访问的key

```java
class LRUCache {

    static class Node {
        Node left, right;
        int key, val;

        public Node(int key, int val, Node left, Node right) {
            this.key = key;
            this.val = val;
            this.left = left;
            this.right = right;
        }
    }

    Node head, tail;

    Map<Integer, Node> map;
    int n;

    public LRUCache(int capacity) {
        this.head = new Node(-1, -1, null, null);
        this.tail = new Node(-1, -1, null, null);
        map = new HashMap<>();
        this.n = capacity;
        head.right = tail;
        tail.left = head;
    }

    public int get(int key) {
        if (!map.containsKey(key)) return -1;
        Node node = map.get(key);
        remove(node);
        insert(node);
        return node.val;
    }

    public void put(int key, int value) {
        if (map.containsKey(key)) {
            Node node = map.get(key);
            node.val = value;
            remove(node);
            insert(node);
        } else {
            if (map.size() == n) {
                Node node = tail.left;
                remove(node);
                map.remove(node.key);
            }
            Node node = new Node(key, value, null, null);
            map.put(key, node);
            insert(node);
        }
    }

    private void remove(Node node) {
        node.left.right = node.right;
        node.right.left = node.left;
    }

    private void insert(Node node) {
        node.right = head.right;
        node.left = head;
        head.right.left = node;
        head.right = node;
    }
}
```

