[017. Subsets](http://www.lintcode.com/problem/subsets)

- [prev: 016. Permutations II](016-permutations-ii.md)
- [next: 018. Subsets II](018-subsets-ii.md)

---

#### Recursion method

At first glance, it seems we can use recursion to solve this subsets problem, because computing subsets of a set seems could be solved by narrowing down the scale of the original problem to a same or similiar sub-problem, and recursively narrow down the sub-problem untill reach a base case: empty set. Then we can back-trace the recursion path to have the solution of the orginal problem.

Then we transfer this problem to that how to narrow down the problem (or how to divide the problem to several same sub-problems).

One dividing way would be easily to come out if we can see subsets of a set as a binary view ( binary view is learned from  [prove subsets numbers is 2^n -2 baidu](http://baike.baidu.com/view/1205.htm):

for a set has n elements, it subsets could be seens as all arrangements of a length n binary number:

111...1 to 000...0

In which `1` means has this element, `0` means doesn't has this element for a particular subset.

Thus, we can see that for a set has 1 element, its subsets are：

| 1 | 0 |

And for a set has 2 elements, its subsets are:

| 1 1 | 1 0 |

| 0 1 | 0 0 |

Which could be seen as the existence of sencond element combinate with all the subsets of 1 element subset.

Further, for a set has n elements, its subsets could be seens as the existence of nth element combinate with all the subsets of n - 1 elements subset.

Base on this idea, we can have below solution:

```java
class Solution {
    /**
     * @param S: A set of numbers.
     * @return: A list of lists. All valid subsets.
     */
    public ArrayList<ArrayList<Integer>> subsets(int[] nums) {
        // write your code here
        if( nums == null ) {
            return null;
        }
        
        ArrayList<ArrayList<Integer>> subset = new ArrayList<ArrayList<Integer>>();
        
        if(nums.length == 0) {
            subset.add(new ArrayList<Integer> ());
            return subset;
        }
        
        Arrays.sort(nums);
        // the copyOfRange() method actually might be very costy, because it create a new copy of the partial array
        // this un-neccessary copy could be avoid by creating a helper method using a wrapper and pass reference only
        // like: http://stackoverflow.com/questions/1100371/grab-a-segment-of-an-array-in-java-without-creating-a-new-array-on-heap
        // Or may refer tha way of Jiuzhang, passing an extra int pos as an indicator of valid range of a method call
        ArrayList<ArrayList<Integer>> sub_subset = subsets(Arrays.copyOfRange(nums, 0, nums.length - 1));
  
        subset.addAll(sub_subset);
        
        int addUp = nums[nums.length - 1];
        
        for(ArrayList<Integer> list : sub_subset) {
            ArrayList<Integer> addUpList = new ArrayList<Integer> ();
            addUpList.addAll(list);
            addUpList.add(addUp);
            subset.add(addUpList);
        }

        return subset;
    }
}
```

Note that this solution are actually space-expensive because it made too many copys of ArrayList and also create too many sub-array copys, and even not counts the stack usage of recursive function calls.

The solution in [Jiuzhang](http://www.jiuzhang.com/solutions/subsets/) is much better but this recursion way is hard to come out (at least it is not intuitive for me...). I cannot find a porper way to explain this algorithm (maybe I am stiil not understand it). I will try to explain it later on.

---

- [prev: 016. Permutations II](016-permutations-ii.md)
- [next: 018. Subsets II](018-subsets-ii.md)
