[013. strStr](http://www.lintcode.com/problem/strstr)

- [prev: 012. Min Stack](012-min-stack.md)
- [next: 014. First Position of Target](014-first-position-of-target.md)

---
The esay way of solving this question is quite simple: just using two nested for-loop to bruth-force searching the result. One corner case need to consider about is **when to stop the searching**: we only need to search the source string from `0` to `source.length - target.length + 1`, because we need to ensure that the matching part of source string in each iteration has at least length of target string length.

@corner test case: ["source", "rced"]

The solution in [Jiuzhang](http://www.jiuzhang.com/solutions/implement-strstr/) is more concise than mine. I have a redundant if-statement to filter the case of both source and target string are empty.

There also has a O(n) time complexity solution called [KMP algorithm](https://en.wikipedia.org/wiki/Knuth–Morris–Pratt_algorithm). I noted it here for furture study.

```java
// keyword: brute-force, KMP algorithm (my solution not implement this yet..)
// time complexity: O(n^2)
// space complexity: no extra space
class Solution {
    /**
     * Returns a index to the first occurrence of target in source,
     * or -1  if target is not part of source.
     * @param source string to be scanned.
     * @param target string containing the sequence of characters to match.
     */
    public int strStr(String source, String target) {
        //write your code here
        if(source == null || target == null || source.length() < target.length())
            return -1;
        
        // this if-statement is redundant 
        // if(source.length() == 0 && target.length() == 0)
        //     return 0;
        
        // notice that we only need to search source str from 0 to source.length - target.length + 1
        for(int i = 0; i < source.length() - target.length() + 1; i++) {
            int j = 0;
            for(int k = i; j < target.length(); j++, k++) {
                if(source.charAt(k) != target.charAt(j))
                    break;
            }
            if(j == target.length())
                return i;
        }
            
        return -1;
    }
}
```

---

- [prev: 012. Min Stack](012-min-stack.md)
- [next: 014. First Position of Target](014-first-position-of-target.md)
