---
layout: post
title: "Leetcode Pascal's Triangle II"
date: 2023-04-23
---


# Approach
Essentially, the solution is based on the equation found here: [https://en.wikipedia.org/wiki/Pascal%27s_triangle#Calculating_a_row_or_diagonal_by_itself] (https://en.wikipedia.org/wiki/Pascal%27s_triangle#Calculating_a_row_or_diagonal_by_itself)

If you don't want to bother going to the link, the equation is sort of as follows: 

$$\binom{n}{k} = \binom{n}{k-1} * \dfrac{n + 1 - k}{k}$$

The variable n is the row being calculated, essentially the row index value, while k is the element position of the row starting with 0 from the initial 1 value for a given row all the way to k = n which results in 1.

Ex:
Given the problem of searching for row index 4, element 2, we know past the initial 1 as the 0 element, that the element after that is going to be the same value of the row index.
$$n = 4, k = 2, \binom{4}{1} = 4$$
$$\binom{4}{2} = 4 * \dfrac{4 + 1 - 2}{2} = 6$$
if you wanted to find k = 3.
$$\binom{4}{3} = 6 * \dfrac{4 + 1 - 3}{3} = 4$$
It's 4 due to the number of elements available in row index 4.
And of course k = 4 would be 1:
$$\binom{4}{4} = 4 * \dfrac{4 + 1 - 4}{4} = 1$$

Ex:
Let's try for row index of 30 to find element 2.
$$n = 30, k = 2, \binom{30}{1} = 30$$
$$\binom{30}{2} = 30 * \dfrac{30 + 1 - 2}{2} = 435$$
if you wanted to find k = 3.
$$\binom{30}{3} = 435 * \dfrac{30 + 1 - 3}{3} = 4060$$

Now, one potential issue with using this equation comes with memory. If you're using something like Python you don't have to worry about it as much, but, there is the chance for there to be an integer overflow. That is why you need to cast the calculation as a `long` to prevent it and cast it back to an `int` once it's done. 

If we wanted to surpass the `0 <= rowIndex <= 33` restriction, we would have to change memory allocation for the lists and the casts. However, the restriction is a limit to the given problem, so we don't need to do that here.

# Complexity
- Time complexity: $$O(n)$$
<!-- Add your time complexity here, e.g. $$O(n)$$ -->

- Space complexity: $$O(n)$$ 
<!-- Add your space complexity here, e.g. $$O(n)$$ -->

# Code
```C++ []
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        vector<int> row {1};
        for(int i = 1; i <= rowIndex; i++) {
            row.push_back((int)((long)row[i-1]*(rowIndex+1-i)/i));
        }
        return row;
    }
};
```
```csharp []
public class Solution {
    public IList<int> GetRow(int rowIndex) {
        IList<int> row = new List<int>() {1};
        for(int i = 1; i <= rowIndex; i++) {
            row.Add((int)((long)row[i-1]*(rowIndex+1-i)/i));
        }
        return row;
    }
}
```
```Python []
class Solution:
    def getRow(self, rowIndex: int) -> List[int]:
        row = [1]
        for i in range(1, rowIndex + 1):
            row.append(int(row[i-1]*(rowIndex+1-i)/i))
        return row
```
