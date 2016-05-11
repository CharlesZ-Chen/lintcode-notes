[060. Search Insert Position](http://www.lintcode.com/problem/search-insert-position)

- [prev: 059. 3Sum Closest](059-3sum-closest.md)
- [next: 061. Search for a Range](061-search-for-a-range.md)

---

Just a direct application of binary search. Carefully reading the question, if does not find target, return the index that the target should be. Carefully think about the stop condition of while-loop, it can ensure that `left` would be the position of target should be after the while-loop. 

The solution in [Jiuzhang](http://www.jiuzhang.com/solutions/search-insert-position/) has too many if-statements after the main while-loop.

```java
// keyword: binary search
// time complexity: O(log n)
// space complexity: O(1)
public class Solution {
    /** 
     * param A : an integer sorted array
     * param target :  an integer to be inserted
     * return : an integer
     */
    public int searchInsert(int[] A, int target) {
        // write your code here
        if(A == null) {
            return 0; // note: null is incompatible with primitive type int
        }
        
        int left = 0;
        int right = A.length;
        
        while(left < right) {
            int m = left + (right - left) / 2 ;
            if( A[m] == target) {
                return m;
            }
            else if( A[m] < target) {
                left = m + 1;
            }
            else if( A[m] > target) {
                right = m - 1;
            }
        }
        
        return left;
        
    }
}

```

---

- [prev: 059. 3Sum Closest](059-3sum-closest.md)
- [next: 061. Search for a Range](061-search-for-a-range.md)
