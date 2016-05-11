[028. Search a 2D Matrix](http://www.lintcode.com/problem/search-a-2d-matrix)

- [prev: 018. Subsets II](018-subsets-ii.md)
- [next: 029. Interleaving String](029-interleaving-string.md)

---

# Naive Solution O (log m*n) time complexity

Just transform m*n 2D matrix to  a m*n length 1D array and binary search this array.

```java
    /**
     * @param matrix, a list of lists of integers
     * @param target, an integer
     * @return a boolean, indicate whether matrix contains target
     */
    public boolean searchMatrix(int[][] matrix, int target) {
        // write your code here
        if (matrix == null || matrix.length < 1 || matrix[0].length < 1) {
            return false;
        }
        int rowNum = matrix.length;
        int colNum = matrix[0].length;
        int left = 0;
        int right = colNum * rowNum;
        
        while(left < right) {
            int m = left + (right - left) / 2;
            int val = matrix[ m / colNum ][ m % colNum ];

            if ( val == target ) {
                return true;
            }
            else if ( val < target ) {
                left = m + 1;
            }
            else if (val > target ) {
                right = m - 1;
            }
        }
        // Be aware of checking the element at left (if left is not exceed the boundary of matrix
        return (left < colNum * rowNum) && matrix[ left / colNum ][ left % colNum ] == target;
    }
```
# O(log m + log n) solution

Doing binary search twice, first searching on row dimension and then searching on column dimension if there were a row that row[0] <= target.

In mine solution, the while-loop didn't check the last `left` element (if left does not exceed boundary after loop). Thus it must be **very careful** about this missing check element --- It should apply all conditions of whether this missing element is a target value or not. In our case, that is, if matrix[left][0] <= target (not only less than), then matrix[left] is the target row to search.

The solution in [Jiuzhang](http://www.jiuzhang.com/solutions/search-a-2d-matrix/) although seems quite clumsy, it is very clear with the pre-condition and post-condition of the while-loop, because it only checking open range (left, right) during the loop, and then check left and right seperately after the loop. The other good feature of this template is that the `left` and `right` ( which is `start` and `end` in Jiuzhang's solution) is ensure that never out-of-boundary.


```java
public class Solution {
    /**
     * @param matrix, a list of lists of integers
     * @param target, an integer
     * @return a boolean, indicate whether matrix contains target
     */
    public boolean searchMatrix(int[][] matrix, int target) {
        // !! the right way of checking corner case in matrix is 
        // seperately checking each dimension
        // e.g. this is not safe when matrix[0] is null:
        // if (matrix == null || matrix.length < 1 || matrix[0].length < 1) {
        //     return false;
        // }

        if (matrix == null || matrix.length < 1) {
            return false;
        }
        
        if (matrix[0] == null || matrix[0].length < 1) {
            return false;
        }
        
        // bad naming! right-most is distinguish-most!
        // int rowNum = matrix.length;
        // int colNum = matrix[0].length;
        // better using:
        int row = matrix.length;
        int column = matrix[0].length;
        int left = 0;
        int right = row;
        int targetRow = -1;

        while (left < right) {
            int mid = left + (right - left) / 2;
            int val = matrix[mid][0];
            if (val == target) {
                return true;
            }
            else if (val < target) {
                targetRow = mid;
                left = mid + 1;
            }
            else if (val > target) {
                right = mid - 1;
            }
        }
        
        if (left < row) {
            targetRow = matrix[left][0] <= target ? left : targetRow;
        }
        
        if (targetRow == -1) {
            return false;
        }
        
        

        left = 0;
        right = column;

        while (left < right) {
            int mid = left + (right - left) / 2;
            int val = matrix[targetRow][mid];
            
            if ( val == target) {
                return true;
            }
            else if (val < target) {
                left = mid + 1;
            }
            else if (val > target) {
                right = mid - 1;
            }
        }
        
        return left < column && matrix[targetRow][left] == target;
        
    }
}
```
---

- [prev: 018. Subsets II](018-subsets-ii.md)
- [next: 029. Interleaving String](029-interleaving-string.md)
