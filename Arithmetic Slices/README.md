# Arithmetic Slices
A sequence of number is called arithmetic if it consists of at least three elements and if the difference between any two consecutive elements is the same.

For example, these are arithmetic sequence:
```
1, 3, 5, 7, 9
7, 7, 7, 7
3, -1, -5, -9
```

The following sequence is not arithmetic.
```
1, 1, 2, 5, 7
```

A zero-indexed array A consisting of N numbers is given. A slice of that array is any pair of integers (P, Q) such that 0 <= P < Q < N.

A slice (P, Q) of array A is called arithmetic if the sequence:
A[P], A[p + 1], ..., A[Q - 1], A[Q] is arithmetic. In particular, this means that P + 1 < Q.

The function should return the number of arithmetic slices in the array A.

**Example:**
```
Input: [1, 2, 3, 4]
Output: 3, for 3 arithmetic slices in A: [1, 2, 3], [2, 3, 4] and [1, 2, 3, 4] itself. 
```

## Approach
We need to find an approach that uses Dynamic Programming, one way would be to store the differences of every two consecutive values in an array. Then we can store the number of arithmetic slices at each position. This way we can store solutions to sub-problems that can help us for the following positions.

### Using stored solutions to sub-problems
We will be using an array and we will be storing the number of arithmetic slices at each index, as well as the differences between every two consecutive elements (i and i+1)
By storing these values, we can reuse them to keep calculating future values.

### Recursive definition
The call that we will use depends on whether the difference of the previous two elements is equals to the difference of the next two. If it is not, then we just copy the previous value of the array to the current one and repeat. If those two differences are the same, then we have an arithmethic slice and we have to check if the following values are also part of the slice.

The call that we will be using is:
``` java
if(difference[i - 1] == difference[i]){
    if(1 < i && difference[i - 2] == difference[i - 1])    
        array[i] = 2 * array[i - 1] - array[i - 2] + 1;
    else
        array[i] = array[i - 1] + 1;
} else
    array[i] = array[i - 1];
```

## Code
``` java
    public final int numberOfArithmeticSlices(int[] A) {
        if (2 >= A.length)
            return 0;
        final int[] difference = new int[A.length - 1];
        for (int i = 0; i < difference.length; i++)
            difference[i] = A[i + 1] - A[i];
        final int[] array = new int[difference.length];
        for (int i = 1; i < array.length; i++)
            if(difference[i - 1] == difference[i])
                if(1 < i && difference[i - 2] == difference[i - 1])    
                    array[i] = 2 * array[i - 1] - array[i - 2] + 1;
                else
                    array[i] = array[i - 1] + 1;
            else
                array[i] = array[i - 1];

        return array[difference.length - 1];
    }
```