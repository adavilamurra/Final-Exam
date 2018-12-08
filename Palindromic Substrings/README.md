# Palindromic Substrings
Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

**Example 1**
```
Input: "abc"
Output: 3
```

**Example 2**
```
Input: "aaa"
Output: 6
```

## Approach
We tried to solve this problem by creating a matrix that would store which strings are palindromes and the indexes of the matrix would be mapped to the indexes of the chracters in the string. If a string was a palindrome, we would use a 1, otherwise we would use a 0. We used this convention because we will add all the 1s in the end. For example, if we use matrix[1,3] would check if the string between the indexes 2-4 is a palindrome.

### Using stored solutions to sub-problems
Since we are storing all the information in the matrix, we can re use as much as we want. We can count the number of 1s in the matrix (only in one half). We are only using one half because that's how we are mapping the indexes of the matrix to the indexes of the characters in the string. 

### Recursive definition
First we set all the matrix elements to -1, just to make sure that we would get a 0 or a 1 for all of them.
The call that we will be using is:
```
if(matrix[i+1][j-1] == 1){
    if(str[i] == str[j])
        matrix[i][j] = 1;
    else
        matrix[i][j] = 0; 
    else
        matrix[i][j] = 0;
} 
```

