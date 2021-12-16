# Arrays
 
+ [Squares of a Sorted Array](#squares-of-a-sorted-array)
 
## Squares of a Sorted Array
 
https://leetcode.com/problems/squares-of-a-sorted-array/
 
<details><summary>Test cases</summary><blockquote>
 
```python
import unittest

from Scratch import Solution


class MyTestArrays1Case(unittest.TestCase):
    def test_sortedSquaresEmpty(self):
        a=[]
        result=self.solution.sortedSquares(a)
        expected=[]
        self.assertEqual(expected, result) # add assertion here
    def test_sortedSuaresPositive(self):
        a = [1,2,3,4,7,9]
        result = self.solution.sortedSquares(a)
        expected = [1,4,9,16,49,81]
        self.assertEqual(expected, result)
    def test_sortedSuaresNegative(self):
        a = [-9,-7,-4,-3,-2,-1]
        result = self.solution.sortedSquares(a)
        expected = [1,4,9,16,49,81]
        self.assertEqual(expected, result)
    def setUp(self):
        self.solution=Solution()


if __name__ == '__main__':
    unittest.main()
```
 
 
</blockquote></details>
 
```python
class Solution(object):
    def sortedSquares(self, n):
        i = -1
        while (i < len(n) - 1) and (n[i + 1] < 0):
            i += 1
        j = i + 1
        result = []
        while (i > -1) and (j < len(n)):
            if ((n[i] ** 2) < (n[j] ** 2)):
                result.append(n[i] ** 2)
                i -= 1
            else:
                result.append(n[j] ** 2)
                j += 1

        for i in range(i, -1, -1):
            result.append(n[i] ** 2)

        for j in range(j, len(n)):
            result.append(n[j] ** 2)

        return (result)
```