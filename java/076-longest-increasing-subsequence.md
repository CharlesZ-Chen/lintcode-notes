[076. Longest Increasing Subsequence](http://www.lintcode.com/problem/longest-increasing-subsequence)

- [prev: 075. Find Peak Element](075-find-peak-element.md)
- [next: 077. Longest Common Subsequence](077-longest-common-subsequence.md)

---

```java
public class Solution {
    /**
     * @param nums: The integer array
     * @return: The length of LIS (longest increasing subsequence)
     */
    public int longestIncreasingSubsequence(int[] nums) {
        if (nums == null || nums.length < 1) {
            return 0;
        }

        int max = 0;

        // state: f[i] is the LIS length reached i position
        int[] f = new int[nums.length];

        // initialize: each position is length 1
        for (int i = 0; i < f.length; i++) {
            f[i] = 1;
        }

        for (int i = 0; i < nums.length; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[j] > nums[i]) {
                    continue;
                }
                int lis = f[j] + 1;
                f[i] = lis > f[i] ? lis : f[i];
            }
            max = Math.max(max, f[i]);
        }

        return max;
    }
}
```
---

- [prev: 075. Find Peak Element](075-find-peak-element.md)
- [next: 077. Longest Common Subsequence](077-longest-common-subsequence.md)
