[041. Maximum Subarray](http://www.lintcode.com/problem/maximum-subarray)

- [prev: 040. Implement Queue by Two Stacks](040-implement-queue-by-two-stacks.md)
- [next: 042. Maximum Subarray II](042-maximum-subarray-ii.md)

---

## DP/Greedy? version

```java
    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length < 1) {
            return Integer.MIN_VALUE;
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
```

## n square prefix Sum version

```java
public int maxSubArray(int[] nums) {
        if (nums == null || nums.length < 1) {
            return Integer.MIN_VALUE;
        }

        int[] preSumArr = new int [nums.length + 1];
        
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            preSumArr[i + 1] = sum;
        }

        int max = Integer.MIN_VALUE;

        for (int i = preSumArr.length - 1; i > 0; i--) {
            for (int j = i - 1; j > -1; j--) {
                max = Math.max(max, preSumArr[i] - preSumArr[j]);
            }
        }

        return max;
    }
```

---

- [prev: 040. Implement Queue by Two Stacks](040-implement-queue-by-two-stacks.md)
- [next: 042. Maximum Subarray II](042-maximum-subarray-ii.md)
