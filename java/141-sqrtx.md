[141. Sqrt(x)](http://www.lintcode.com/problem/sqrtx)

- [prev: 140. Fast Power](140-fast-power.md)
- [next: 142. O(1) Check Power of 2](142-o1-check-power-of-2.md)

---

This is a typical application of [binary search algorithm](https://en.wikipedia.org/wiki/Binary_search_algorithm). The basic idea is at each iteration, we check whether the medium element is the sqrt by comparing `r = x / m` and `m`, if `r < m`, that means we should smaller the check point by searching `left, m - 1`; else if `r = m`, then we already find the sqrt; else if `r > m`, then `r` might be the sqrt but we have to further check whether in `m + 1, right` we can find a larger m that  `r > m`.

Note that we can not use `r = m * m` to check the sqrt if we declaired `m` as an `int`, because `r` might be overflow if `m * m > Integer.MAX_VALUE`.

The other thing should note is when calculating the mid point `m`, we should use `m = l + (r - l) / 2` rather than `m = (l + r) / 2` because latter would get overflow if `l + r > Integer.MAX_VALUE`.

The solution in [Jiuzhang](http://www.jiuzhang.com/solutions/sqrtx/) using `long` to calculate the sqrt thus they could using `m * m` to check. 

- TODO: why Jiuzhang using `long` rather than using dividing? Is that because production has higher efficence than division in computer?

```java
// keyword: binary search
// time complexity: O(log x)
// space complexity: O(1)
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
