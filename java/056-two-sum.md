[056. Two Sum](http://www.lintcode.com/problem/two-sum)

- [prev: 055. Compare Strings](055-compare-strings.md)
- [next: 057. 3Sum](057-3sum.md)

---

## Hash Table Version

```java
 public int[] twoSum(int[] numbers, int target) {
        // write your code here
        if(numbers == null || numbers.length < 2) {
            return null;
        }
        
        Hashtable<Integer, Integer> diffTab = 
            new Hashtable<Integer, Integer>(numbers.length);
            
        for(int i = 0; i < numbers.length; i++) {
            if(diffTab.get(numbers[i]) != null) {
                int[] result = new int [] {diffTab.get(numbers[i]), i + 1};
                return result;
            }
            diffTab.put(target - numbers[i], i + 1);
        }
        
        int[] result = new int[0];
        return result;
    }
```

## sort + two pointers

```java
public class Solution {
    /*
     * @param numbers : An array of Integer
     * @param target : target = numbers[index1] + numbers[index2]
     * @return : [index1 + 1, index2 + 1] (index1 < index2)
     */
    public int[] twoSum(int[] nums, int target) {
        if (nums == null || nums.length < 2) {
            return new int[0];
        }

        Pair[] pairArr = new Pair[nums.length];

        for (int i = 0; i < nums.length; i++) {
            pairArr[i] = new Pair(nums[i], i);
        }

        Arrays.sort(pairArr, new Comparator<Pair> () {
            public int compare(Pair p1, Pair p2) {
                return p1.val - p2.val;
            }
        });

        int small = 0;
        int big = pairArr.length - 1;

        while (small < big) {
            int val = pairArr[small].val + pairArr[big].val;
            if (val == target) {
                int idx1 = pairArr[small].idx + 1;
                int idx2 = pairArr[big].idx + 1;
                return new int[] {
                    idx1 > idx2 ? idx2 : idx1,
                    idx1 > idx2 ? idx1 : idx2
                };
            } else if (val < target) {
                small++;
            } else if (val > target) {
                big--;
            } else {
                assert false;
            }
        }

        return new int[0];
    }

    class Pair {
        int val;
        int idx;
        public Pair(int val, int idx) {
            this.val = val;
            this.idx = idx;
        }
    }
}
```
---

- [prev: 055. Compare Strings](055-compare-strings.md)
- [next: 057. 3Sum](057-3sum.md)
