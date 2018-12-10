# Maximum Length of Pair Chain
You are given `n` pairs of numbers. In every pair, the first number is always smaller than the second number.

Now, we define a pair `(c, d)` can follow another pair `(a, b)` if and only if `b < c`. Chain of pairs can be formed in this fashion.

Given a set of pairs, find the length longest chain which can be formed. You needn't use up all the given pairs. You can select pairs in any order.

**Example:**
```
Input: [[1,2], [2,3], [3,4]]
Output: 2
```

## Approach
We know that a chain of two pairs would happen when pairs[i][1] < pairs[j][0]. If we sort all the pairs then we will be able to find chains faster. We can then calculate the length of the longest chain and then use the chain definition we got above to know if we can increase the chain. Then we can find the largest number in the array of lengths and return that value.

### Using stored solutions to sub-problems
We can create an array that will contain the length of the longest chain at each pair. By doing this we can dynamically store the best result each iteration.


### Recursive definition
We will be iterating through the array of pairs and comparing one pair to the rest, then doing the same with the next pair. When we find two pairs such that pairs[i][1] < pairs[j][0], then we can assume this is a chain or a continuation of a chain, and we can check this by looking at the array of results.

The call that we will be using is:
``` java
array[j] = Math.max(array[j], array[i] + 1);
```

## Code
``` java
    public int findLongestChain(int[][] pairs) {
        Arrays.sort(pairs, (a, b) -> a[0] - b[0]);
        int size = pairs.length;
        int[] array = new int[size];
        Arrays.fill(array, 1);
        for (int j = 1; j < size; ++j) {
            for (int i = 0; i < j; ++i) {
                if (pairs[i][1] < pairs[j][0])
                    array[j] = Math.max(array[j], array[i] + 1);
            }
        }

        int result = 0;
        for (int longestChain : array){
            if (longestChain > result) 
                result = longestChain;
        }
        return result;
    }
```