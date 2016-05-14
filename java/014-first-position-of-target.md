[014. First Position of Target](http://www.lintcode.com/problem/first-position-of-target)

- [prev: 013. strStr](013-strstr.md)
- [next: 015. Permutations](015-permutations.md)

---

Simple application of binary search.  This could be solved by basic template from Jiuzhang. Moreover, [finding last index](http://www.lintcode.com/en/problem/last-position-of-target/) is very similar to this one and just modify the order of judgement after while-loop and also made a little modification of the while-loop searching condition.

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
    public int binarySearch(int[] A, int target) {
        // Write your code here
        if (A == null || A.length < 1) {
            return -1;
        }
        
        int start = 0;
        int end = A.length - 1;
        
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            int val = A[mid];
            
            if (val < target) {
                start = mid + 1;
            }
            else {
                end = mid;
            }
        }
        
        if (A[start] == target) {
            return start;
        }
        else if (A[end] == target) {
            return end;
        }
        
        return -1;
    }
}
```

---

- [prev: 013. strStr](013-strstr.md)
- [next: 015. Permutations](015-permutations.md)
