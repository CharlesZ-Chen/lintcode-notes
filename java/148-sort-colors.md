[148. Sort Colors](http://www.lintcode.com/problem/sort-colors)

- [prev: 144. Interleaving Positive and Negative Numbers](144-interleaving-positive-and-negative-numbers.md)
- [next: 149. Best Time to Buy and Sell Stock](149-best-time-to-buy-and-sell-stock.md)

---

## Better Three Pointers way of coding
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

        int left = 0;
        int right = nums.length - 1;
        int scan = 0;
        final int RED = 0;
        final int WHITE = 1;
        final int BLUE = 2;

        while (scan <= right) {
            int color = nums[scan];
            if (color == RED) {
                swap(nums, left, scan);
                left++;
                scan++;
            } else if (color == WHITE) {
                scan++;
            } else if (color == BLUE) {
                swap(nums, right, scan);
                right--;
            } else {
                assert false : "unexpected color!";
            }
        }
    }

    public void swap (int[] arr, int i, int j) {
        if (arr == null || i < 0 || j < 0 || i >= arr.length || j > arr.length) {
            return;
        }

        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
```
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
