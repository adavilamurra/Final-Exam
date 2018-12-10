# Minimum ASCII Delete Sum for Two Strings
Given two strings s1, s2, find the lowest ASCII sum of deleted characters to make two strings equal.

**Example 1:**
```
Input: s1 = "sea", s2 = "eat"
Output: 231
```

**Example 2:**
```
Input: s1 = "delete", s2 = "leet"
Output: 403
```

## Approach
For our approach, we decided to store the sum up to every position of a character in the string. This way we will have information that can be used for later. We will use a matrix for this.

### Using stored solutions to sub-problems
Since we will already have the sum up to each character, we can start from the end and work our way to the beginning of the string.

### Recursive definition
We will fill out the last row and column of the matrix with the sum of the characters that we already stored and we will go from the end to the beginning.
Then we will keep filling out the matrix from bottom right to top left.

The call that we will be using is:
``` java
if (s1.charAt(i) == s2.charAt(j))
    dp[i][j] = dp[i+1][j+1];
else {
    dp[i][j] = Math.min(dp[i+1][j] + s1.codePointAt(i),
    dp[i][j+1] + s2.codePointAt(j));
}
```

## Code
``` java
    public int minimumDeleteSum(String s1, String s2) {
        int[][] array = new int[s1.length() + 1][s2.length() + 1];

        for (int i = s1.length() - 1; i >= 0; i--) {
            array[i][s2.length()] = array[i+1][s2.length()] + s1.codePointAt(i);
        }
        for (int j = s2.length() - 1; j >= 0; j--) {
            array[s1.length()][j] = array[s1.length()][j+1] + s2.codePointAt(j);
        }
        for (int i = s1.length() - 1; i >= 0; i--) {
            for (int j = s2.length() - 1; j >= 0; j--) {
                if (s1.charAt(i) == s2.charAt(j)) {
                    array[i][j] = array[i+1][j+1];
                } else {
                    array[i][j] = Math.min(array[i+1][j] + s1.codePointAt(i),
                                        array[i][j+1] + s2.codePointAt(j));
                }
            }
        }
        return array[0][0];
    }
```