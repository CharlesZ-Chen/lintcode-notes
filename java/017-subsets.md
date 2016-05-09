[017. Subsets](http://www.lintcode.com/problem/subsets)

- [prev: 016. Permutations II](016-permutations-ii.md)
- [next: 018. Subsets II](018-subsets-ii.md)

---

#### Recursion method
The solution in [Jiuzhang](http://www.jiuzhang.com/solutions/subsets/) is much better but this recursion way is hard to come out (at least it is not intuitive for me...). The method is using DFS + backtrace to implement.

[here is a good explaination of this method](http://www.code123.cc/docs/leetcode-notes/backtracking/subsets.html)

```java
// keyword: DFS, backtrace, NP problem
// time complexity: this is a NP problem. O(2^n)
// space complexity: O(2^n)
class Solution {
    /**
     * @param S: A set of numbers.
     * @return: A list of lists. All valid subsets.
     */
    public ArrayList<ArrayList<Integer>> subsets(int[] nums) {
        // write your code here
        if( nums == null) {
            return null;
        }
        
        Arrays.sort(nums);
        
        ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>> ();
        
        ArrayList<Integer> list = new ArrayList<Integer> ();
        
        backtrace(res, list, nums, 0);
        
        return res;
    }
    
    public void backtrace(ArrayList<ArrayList<Integer>> res, ArrayList<Integer> list,
        int[] nums, int pos) {
            //remember to allocate memory for adding list!!
            res.add(new ArrayList<Integer>(list));
            
            for(int i = pos; i < nums.length; i++) {
                list.add(nums[i]);
                backtrace(res, list, nums, i + 1);
                list.remove(list.size() - 1);
            }
        }
}
```

---

- [prev: 016. Permutations II](016-permutations-ii.md)
- [next: 018. Subsets II](018-subsets-ii.md)
