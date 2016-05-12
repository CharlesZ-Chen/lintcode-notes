[014. First Position of Target](http://www.lintcode.com/problem/first-position-of-target)

- [prev: 013. strStr](013-strstr.md)
- [next: 015. Permutations](015-permutations.md)

---

Simple application of binary search.

```java
// keyword: binary search
// time complexity O(log n)
// sapce complexity O(10
class Solution {
    /**
     * @param nums: The integer array.
     * @param target: Target to find.
     * @return: The first position of target. Position starts from 0.
     */
    public int binarySearch(int[] nums, int target) {
        //write your code here
        if (nums == null || nums.length < 1) {
            return -1;
        }

        int start = 0;
        int end = nums.length - 1;
        int idx = -1;

        while (start + 1 < end) {
            int m = start + (end - start) / 2;

            if (nums[m] == target) {
                idx = m;
                end = m - 1;
            }
            else if (nums[m] < target) {
                start = m + 1;
            }
            else if (nums[m] > target) {
                end = m - 1;
            }
        }

        if (nums[start] == target) {
            return start;
        }
        else if (nums[end] == target) {
            return end;
        }

        return idx;
    }
}
```

---

- [prev: 013. strStr](013-strstr.md)
- [next: 015. Permutations](015-permutations.md)
