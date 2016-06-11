[041. Maximum Subarray](http://www.lintcode.com/problem/maximum-subarray)

- [prev: 040. Implement Queue by Two Stacks](040-implement-queue-by-two-stacks.md)
- [next: 042. Maximum Subarray II](042-maximum-subarray-ii.md)

---

```java
public class Solution {
    /**
     * @param nums: A list of integers
     * @return: A integer indicate the sum of max subarray
     */
    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length < 1) {
            return Integer.MIN_VALUE;
        }
        // first get the prefix sum Array
        int[] preSumArr = new int [nums.length + 1];
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            preSumArr[i + 1] = sum;
        }

        // is this DP?
        //state: f[i], maximum subArray which ends with nums[i]
        //transfer function: f[i] = Math.max(nums[i], nums[i] + f[i - 1])
        //answer: max(f[i])
        int[] f = new int[nums.length];

        f[0] = nums[0];
        int max = f[0];

        for (int i = 1; i < nums.length; i++) {
            f[i] = Math.max(nums[i], nums[i] + f[i - 1]);
            max = Math.max(f[i], max);
        }

        return max;
    }
}
```

---

- [prev: 040. Implement Queue by Two Stacks](040-implement-queue-by-two-stacks.md)
- [next: 042. Maximum Subarray II](042-maximum-subarray-ii.md)
