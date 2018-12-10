# Minimum Falling Path Sum
Given a square array of integers A, we want the minimum sum of a falling path through A.

A falling path starts at any element in the first row, and chooses one element from each row.  The next row's choice must be in a column that is different from the previous row's column by at most one.

**Example 1**
```
Input: [[1,2,3],[4,5,6],[7,8,9]]
Output: 12
Explanation: 
The possible falling paths are:
```
`[1,4,7], [1,4,8], [1,5,7], [1,5,8], [1,5,9]`

`[2,4,7], [2,4,8], [2,5,7], [2,5,8], [2,5,9], [2,6,8], [2,6,9]`

`[3,5,7], [3,5,8], [3,5,9], [3,6,8], [3,6,9]`

The falling path with the smallest sum is `[1,4,7]`, so the answer is `12`.

## Approach
The way we tried to solve this problem was to start focusing on the second row. After that, we wanted to compare the values of the elements in the first row to find the smallest one. (We have to remember that the column's range is one to each side)
After finding the smallest element from the first row, we added that value with the value of the current element (from the second row). 

We did this for every element in the current row and we got the sum from each falling path at that certain point. The next step was repeating this process with the next row (third). When we finished calculating these values, we found that the falling path sums were all in the last row of the array.
To get the result we just had to find the minimum of those paths.

### Using stored solutions to sub-problems
We can notice that this process can be repeated many times and every time we go to the next row we already have the sum of the falling path calculated, so we are reusing that information and calculations to ge the next ones.
More info below...

### Recursive definition
This is the recursive defintion that we came up with:
We use this code to compare each element (A[row][column]) to the elements from the previous row. 
Then we add the minimum element from the previous row to the current one.
``` java
if(column == 0)  // first column
	A[row][column] += Math.min(A[row-1][column] , A[row-1][column+1]);
else if(column == A[0].length-1)  // last column
    A[row][column] += Math.min(A[row-1][column] , A[row-1][column-1]);
else 
    A[row][column] += Math.min(A[row-1][column+1] , Math.min(A[row-1][column] , A[row-1][column-1]));
```
and also:
``` java
minValue = Math.min(minValue , A[row-1][i]);
```

## Code
``` java
public int minFallingPathSum(int[][] A) {
    int row = A.length;
    int column = A[0].length;
    for(int i = 1 ; i < row ; i++) {
        for(int j = 0 ; j < column ; j++) {
            if(j == 0)
                A[i][j] += Math.min(A[i-1][j] , A[i-1][j+1]);
            else if(j == column - 1)
            	A[i][j] += Math.min(A[i-1][j] , A[i-1][j-1]);
            else
            	A[i][j] += Math.min(A[i-1][j+1] , Math.min(A[i-1][j] , A[i-1][j-1]));
        }
    }
    
    int minValue = Integer.MAX_VALUE;
    for(int i = 0 ; i < column ; i++)
        minValue = Math.min(minValue , A[row-1][i]);
    return minValue;
}
```