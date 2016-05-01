[031. Partition Array](http://www.lintcode.com/problem/partition-array)

- [prev: 030. Insert Interval](030-insert-interval.md)
- [next: 032. Minimum Window Substring](032-minimum-window-substring.md)

---

This is a typical application of two pointers (colliding scan). At first glance, the BCR is O(n) because at least we need to "touch" each element in the array to partition the whole array correctly.

The idea of solution in [Jiuzhang](http://www.jiuzhang.com/solutions/partition-array/) is similiar but it uses nested loops and thus I think mine might have better readability.

I use the left pointer as "scanner" and the right pointer as "swapper". When scanner scanned an element should belong to right part, then swap this element to the position of swapper and update the next avaliable position of swapping. Otherwise scanner continue scan next element from left to right.

Stop criteria: left pointer meet right pointer.

Corner cases:
- nums array is null or empty: return 0 (but be aware of 0 may means normal exist of a func. Thus in real world, if null or empty is not allowed in this func, we might consider return other error code or throw exception)

Solution:
```java
// keyword: two pointers, integer array
// time-complexity: O(n)
// space-complexity: O(1)

public class Solution {
	/** 
     *@param nums: The integer array you should partition
     *@param k: As description
     *return: The index after partition
     */
    public int partitionArray(int[] nums, int k) {
	    //write your code here
	    // BCR(Best Conceivable Runtime): O(n) in place.
	    if(nums == null || nums.length < 1) {
	        return 0;
	    }
	    
	    int left = 0, right = nums.length - 1;

	    while(left < right) {
	        if(nums[left] >= k) {
	            int temp = nums[right];
	            nums[right] = nums[left];
	            nums[left] = temp;
	            right --;
	        } else {
	            left ++;
	        }
	    }
	    
	    //judge the element in the colliding position because we miss it in the above while-loop
	    if(nums[left] >= k) {
	        return right; //this element should belong right part, thus return right
	    } else {
	        return right + 1; //this element should belong left part, thus return the position next to the right pointer
	    }
    }
}
```

Additional note: how to partition if not an array but a link list? This is a question in CC189 [Q2.4 Partition](https://github.com/CharlesZ-Chen/CC189/tree/master/src/Q2_04_Partition)

---

- [prev: 030. Insert Interval](030-insert-interval.md)
- [next: 032. Minimum Window Substring](032-minimum-window-substring.md)
