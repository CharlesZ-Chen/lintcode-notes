[016. Permutations II](http://www.lintcode.com/problem/permutations-ii)

- [prev: 015. Permutations](015-permutations.md)
- [next: 017. Subsets](017-subsets.md)

---
Very smart method. Learned from [Jiuzhang](http://www.jiuzhang.com/solutions/permutations-ii/)

Using visited array to mark visited element and also filter out the duplicate elements.

Seems the kind of `subset` series with duplicate elements could use one general rule to solve:

That is to ** forbid ** construct solution with ** jump over ** the duplicate elements. i.e. with duplicate elements we must get the first one, then get the second one, then so on... we cannot get the second one before getting the first one in our solution.

```java
class Solution {
    /**
     * @param nums: A list of integers.
     * @return: A list of unique permutations.
     */
    public ArrayList<ArrayList<Integer>> permuteUnique(ArrayList<Integer> nums) {
        // write your code here
        ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>> ();
        
        if(nums == null || nums.size() < 1) {
            return res;
        }
        
        Collections.sort(nums);
        
        ArrayList<Integer> list = new ArrayList<Integer> ();
        int[] visited = new int[nums.size()];
        backtrace(res, list, nums, visited);
        return res;
    }
    
    public void backtrace(ArrayList<ArrayList<Integer>> res, ArrayList<Integer> list,
        ArrayList<Integer> nums, int[] visited) {
            if(list.size() == nums.size()) {
                res.add(new ArrayList<Integer> (list));
                return;
            }
            
            for(int i = 0; i < nums.size(); i++) {
                if(visited[i] == 1 || (i != 0 && nums.get(i) == nums.get(i - 1) && 
                    visited[i - 1] == 0)) { // cannot jump over a same number to construct permute
                        continue;
                    }
                    
                visited[i] = 1;
                list.add(nums.get(i));
                backtrace(res, list, nums, visited);
                list.remove(list.size() -1);
                visited[i] = 0;
                
            }
        }
}
```

---

- [prev: 015. Permutations](015-permutations.md)
- [next: 017. Subsets](017-subsets.md)
