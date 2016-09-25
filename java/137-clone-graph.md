[137. Clone Graph](http://www.lintcode.com/problem/clone-graph)

- [prev: 136. Palindrome Partitioning](136-palindrome-partitioning.md)
- [next: 138. Subarray Sum](138-subarray-sum.md)

---

Simple BFS.

```java
/**
     * @param node: A undirected graph node
     * @return: A undirected graph node
     */
    public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
        if (node == null) {
            return null;
        }

        // origNode -> cloneNode
        Map<UndirectedGraphNode, UndirectedGraphNode> map = new HashMap<>();

        Queue<UndirectedGraphNode> queue = new LinkedList<>();

        queue.offer(node);

        // clone nodes
        while (!queue.isEmpty()) {
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                UndirectedGraphNode cur = queue.poll();
                if (map.containsKey(cur)) {
                    continue;
                }
                // mark visited and store clone
                map.put(cur, new UndirectedGraphNode(cur.label));
                // put all neighbors into queue
                for (UndirectedGraphNode neighbor : cur.neighbors) {
                    queue.offer(neighbor);
                }
            }
        }

        // clone edges
        for (Map.Entry<UndirectedGraphNode, UndirectedGraphNode> entry : map.entrySet()) {
            UndirectedGraphNode orig = entry.getKey();
            UndirectedGraphNode clone = entry.getValue();
            for (UndirectedGraphNode origN : orig.neighbors) {
                clone.neighbors.add(map.get(origN));
            }
        }

        return map.get(node);
    }
```

---

- [prev: 136. Palindrome Partitioning](136-palindrome-partitioning.md)
- [next: 138. Subarray Sum](138-subarray-sum.md)
