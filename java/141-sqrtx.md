[141. Sqrt(x)](http://www.lintcode.com/problem/sqrtx)

- [prev: 140. Fast Power](140-fast-power.md)
- [next: 142. O(1) Check Power of 2](142-o1-check-power-of-2.md)

---

This is a typical application of [binary search algorithm](https://en.wikipedia.org/wiki/Binary_search_algorithm).

```java
class Solution {
    /**
     * @param x: An integer
     * @return: The sqrt of x
     */
    public int sqrt(int x) {
        // write your code here
        if(x < 2) {
            return x;
        }
        
        int left = 0, right = x;
        int sqrt_x = 0;
        while(left <= right) {
            //overflow!
            //don't use `m = (r + l) / 2;`
            int m = left  + (right - left) / 2;
            //overflow!!!
            //don't use `r = m * m;` !
            int r = x / m;
            if(r < m) {
                right = m - 1;
            } 
            else if ( r == m) {
                return m;
            } 
            else if(r > m) {
                sqrt_x = m;
                left = m + 1;
            }
        }
        
        return sqrt_x;
    }
}
```

reference: [Binary Search Algorithm](https://en.wikipedia.org/wiki/Binary_search_algorithm)

---

- [prev: 140. Fast Power](140-fast-power.md)
- [next: 142. O(1) Check Power of 2](142-o1-check-power-of-2.md)
