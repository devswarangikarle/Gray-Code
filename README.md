# Gray-Code

An n-bit gray code sequence is a sequence of 2n integers where:
Every integer is in the inclusive range [0, 2n - 1],
The first integer is 0,
An integer appears no more than once in the sequence,
The binary representation of every pair of adjacent integers differs by exactly one bit, and
The binary representation of the first and last integers differs by exactly one bit.
Given an integer n, return any valid n-bit gray code sequence.

Constraints:
1 <= n <= 16

class Solution:
    def grayCode(self, n: int) -> list[int]:
        result = [0]
        visited = set([0])

        def generateGrayCode(num):
            if len(result) == 2 ** n:
                return True
            for i in range(n):
                next_num = num ^ (1 << i)

                if next_num not in visited:
                    result.append(next_num)
                    visited.add(next_num)

                    if generateGrayCode(next_num):
                        return True

                    result.pop()
                    visited.remove(next_num)
            return False

        generateGrayCode(0)
        return result
