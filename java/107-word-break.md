[107. Word Break](http://www.lintcode.com/problem/word-break)

- [prev: 106. Convert Sorted List to Balanced BST](106-convert-sorted-list-to-balanced-bst.md)
- [next: 108. Palindrome Partitioning II](108-palindrome-partitioning-ii.md)

---

```java
public class Solution {
    /**
     * @param s: A string s
     * @param dict: A dictionary of words dict
     */
    public boolean wordBreak(String s, Set<String> dict) {
        if (s == null || dict == null) {
            return false;
        }

        if (s.length() < 1) {
            return dict.size() < 1;
        }

        int n = s.length();
        // tricky thing is here: trim the unless search as much as possible
        int maxLength = getLongestWordInDict(dict);

        // state: f[i] is chars from 0 ~ i -1 could have a wordBreak
        boolean[] f = new boolean [n + 1];

        // initialize: chars from 0 ~ -1 default as true
        f[0] = true;

        for (int i = 1; i < n + 1; i++) {
            for (int j = i - 1; j > -1 &&
                i - j <= maxLength; /*trim the unless search as much as possible*/
                j--) {
                if (!f[j]) {
                    continue;
                }

                // subString(beginIndex, endIndex) return begin to end - 1. length is end - begin
                String subS = s.substring(j, i);
                if (dict.contains(subS)) {
                    f[i] = true;
                    break;
                }
            }
        }

        return f[n];
    }

    public int getLongestWordInDict(Set<String> dict) {
        int max = 0;
        for(String word : dict) {
            max = word.length() > max ? word.length() : max;
        }
        return max;
    }
}
```

---

- [prev: 106. Convert Sorted List to Balanced BST](106-convert-sorted-list-to-balanced-bst.md)
- [next: 108. Palindrome Partitioning II](108-palindrome-partitioning-ii.md)
