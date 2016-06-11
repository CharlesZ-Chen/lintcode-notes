[148. Sort Colors](http://www.lintcode.com/problem/sort-colors)

- [prev: 144. Interleaving Positive and Negative Numbers](144-interleaving-positive-and-negative-numbers.md)
- [next: 149. Best Time to Buy and Sell Stock](149-best-time-to-buy-and-sell-stock.md)

---
## Three Pointers
```java
class Solution {
    /**
     * @param nums: A list of integer which is 0, 1 or 2 
     * @return: nothing
     */
    public void sortColors(int[] nums) {
        if (nums == null || nums.length < 1) {
            return;
        }

        int red = -1;
        int white = 0;
        int blue = nums.length;

        while (white < blue) {
            if (white == red) {
                white++;
                continue;
            }

            int color = nums[white];

            if (color == 0) {
                nums[white] = nums[++red];
                nums[red] = 0;
            } else if (color == 1) {
                white++;
            } else if (color == 2) {
                nums[white] = nums[--blue];
                nums[blue] = 2;
            }
        }
    }
}
```

---

- [prev: 144. Interleaving Positive and Negative Numbers](144-interleaving-positive-and-negative-numbers.md)
- [next: 149. Best Time to Buy and Sell Stock](149-best-time-to-buy-and-sell-stock.md)
