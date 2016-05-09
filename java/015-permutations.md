[015. Permutations](http://www.lintcode.com/problem/permutations)

- [prev: 014. First Position of Target](014-first-position-of-target.md)
- [next: 016. Permutations II](016-permutations-ii.md)

---
** update **

I learn a good trick from [the solution of permutation ii](http://www.jiuzhang.com/solutions/permutations-ii/), that is using visited array as a mark method of which element has already been visited during the DFS.

Although it use an extra O(n) array, I think this solution is more self-articulate than the a little tricky solution of [permutations](http://www.jiuzhang.com/solutions/permutations). Thus I updated it above the original solution here:

```java
class Solution {
    /**
     * @param nums: A list of integers.
     * @return: A list of permutations.
     */
    public ArrayList<ArrayList<Integer>> permute(ArrayList<Integer> nums) {
        // write your code here
        if ( nums == null || nums.size() < 1) {
            return new ArrayList<ArrayList<Integer>> ();
        }

        Collections.sort(nums);
        ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>> ();

        ArrayList<Integer> list = new ArrayList<Integer> ();
        
        int[] visited = new int [nums.size()];
        
        backtrace(res, list, nums, visited);
        
        return res;
    }
    
    public void backtrace (ArrayList<ArrayList<Integer>> res, ArrayList<Integer> list,
    ArrayList<Integer> nums,int[] visited) {
            if(list.size() == nums.size()) {
                res.add(new ArrayList<Integer> (list));
                return;
            }

            for(int i = 0; i < nums.size(); i++) {
                if(visited[i] == 1) {
                    continue;
                }
                visited[i] = 1;
                list.add(nums.get(i));
                backtrace(res, list, nums, visited);
                list.remove(list.size() - 1);
                visited[i] = 0;
            }
        }
}
```

The idea is similiar to [subset](http://www.lintcode.com/en/problem/subsets/). I found the difficult part is to firgure out the search part of recusive method... Is there any good idea about in what way to think of the search & filter & prone condition in the recusive method?

```java
// keywords: backtrace, recursive
class Solution {
    /**
     * @param nums: A list of integers.
     * @return: A list of permutations.
     */
    public ArrayList<ArrayList<Integer>> permute(ArrayList<Integer> nums) {
        // write your code here
        if ( nums == null || nums.size() < 1) {
            return new ArrayList<ArrayList<Integer>> ();
        }

        Collections.sort(nums);
        ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>> ();

        ArrayList<Integer> list = new ArrayList<Integer> ();

        backtrace(res, list, nums);
        
        return res;
    }
    
    public void backtrace (ArrayList<ArrayList<Integer>> res, ArrayList<Integer> list,
    ArrayList<Integer> nums) {
            if(list.size() == nums.size()) {
                res.add(new ArrayList<Integer> (list));
                return;
            }

            for(int i = 0; i < nums.size(); i++) {
                if(list.contains(nums.get(i))) {
                    continue;
                }
                list.add(nums.get(i));
                backtrace(res, list, nums);
                list.remove(list.size() - 1);
            }
        }
}

```
---

- [prev: 014. First Position of Target](014-first-position-of-target.md)
- [next: 016. Permutations II](016-permutations-ii.md)
