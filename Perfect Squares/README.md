# Perfect Squares
Given a positive integer n, find the least number of perfect square numbers (for example, `1, 4, 9, 16, ...`) which sum to `n`.

**Example 1**
```
Input: n = 12
Output: 3 
```

**Example 2**
```
Input: n = 13
Output: 2
```

## Approach
The way we worked on this problem was to first create an array with n+1 elements. We thought that we can use the strategy we learned in class of storing the count of perfect squares to the given n. If we already know the least number of perfect square numbers that sum to that position, it will be easier to come up with the following ones. So we started with the first element and set it up to 0, then after that we would be doing some math work and just loop with previous answers until you find a sum that equals the number you are at.

### Using stored solutions to sub-problems
This was explained above.

### Recursive definition
We will be storing a min value that represents the least number of perfect square numbers. This will be updated with every iteration so that, in the end, we can return it.
The call that we will be using is:
```
min = Math.min(min, array[i - j*j] + 1)
```

## Code
``` java
public int numSquares(int n) {
	int[] array = new int[n + 1];
	Arrays.fill(array, Integer.MAX_VALUE);
	array[0] = 0;
	for(int i = 1; i <= n; ++i) {
		int min = Integer.MAX_VALUE;
		int j = 1;
		while(i - j*j >= 0) {
			min = Math.min(min, array[i - j*j] + 1);
			++j;
		}
		array[i] = min;
	}		
	return array[n];
}
```