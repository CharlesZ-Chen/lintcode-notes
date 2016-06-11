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

---

- [prev: 055. Compare Strings](055-compare-strings.md)
- [next: 057. 3Sum](057-3sum.md)
