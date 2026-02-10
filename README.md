# HackerRank-Solutions
Subarrays with Given Sum and Bounded Maximum
Given an integer array nums and integers k and M, count the number of contiguous subarrays whose sum equals k and whose maximum element is at most M.

Example

Input

nums = [2, -1, 2, 1, -2, 3]
k = 3
M = 2
Output

2
Explanation

We need subarrays with sum = 3 and all elements ≤ 2. 
Also, any subarray containing 3 is invalid because 3 > M. Check all starts:

- From index 0: [2, -1, 2] → sum = 3, max = 2 → valid (count = 1).
- From index 2: [2, 1] → sum = 3, max = 2 → valid (count = 2). No other subarray qualifies. Thus the total count is 2.
Input Format

The first line contains an integer n denoting the number of elements in nums.
The next n lines contains an integer denoting elements in nums followed by the value of k & M.
Example

6 → number of elements in nums
2 → elements of nums
-1
2
1
-2
3
3 → value of k
2 → value of M
Constraints

0 <= nums.length <= 1000000
-10^9 <= nums[i] <= 10^9 for all 0 <= i < nums.length
-10^15 <= k <= 10^15
-10^9 <= M <= 10^9
Output Format

Returns a non-negative integer denoting the count of all contiguous subarrays of nums.
Sample Input 0

0
0
0
Sample Output 0

0
Sample Input 1

1
5
5
5
Sample Output 1

1

#!/bin/python3

import math
import os
import random
import re
import sys



#
# Complete the 'countSubarraysWithSumAndMaxAtMost' function below.
#
# The function is expected to return a LONG_INTEGER.
# The function accepts following parameters:
#  1. INTEGER_ARRAY nums
#  2. LONG_INTEGER k
#  3. LONG_INTEGER M
#

def countSubarraysWithSumAndMaxAtMost(nums, k, M):
    # Write your code here
    # ok first of all just want to say this problem is very difficult
    # yeah
    
    start = 0
    totalCount = 0
    
    while start < len(nums):
        if nums[start] > M:
            start += 1
            # we MUST go back to the top of this while loop
            continue
        
        end = start
        #res = 0
        curSum = 0
        prefixSum = {0 : 1}
        
        while end < len(nums) and nums[end] <= M:
            curSum += nums[end]
            diff = curSum - k
            totalCount += prefixSum.get(diff, 0)
            prefixSum[curSum] = 1 + prefixSum.get(curSum, 0)
            end += 1
        
        # something's up, move start to end to make new segment
        # and figure out why (reached end of array or > M?)
        start = end
        
    return totalCount
        
    
    
    
    '''
    res = 0
    curSum = 0
    prefixSum = {0 : 1}
    
    for n in nums:
        # for M: make it so that any n cannot count toward
        # a prefixSum 
        curSum += n
            
        diff = curSum - k
        res += prefixSum.get(diff, 0)
        prefixSum[curSum] = 1 + prefixSum.get(curSum, 0)
        
    return res
    '''
    
    
    
    # count = 0
    # if len(nums) == 0:
    #     return count
    # '''
    # pass 1: cur = 2
    # '''
    # cur = nums[0] 
    # if (cur <= M) and (cur == k):
    #     count = count + 1
    
    # i = 1
    # # this needs to be while: while i < len(nums): add increment at bottom
    # while i < len(nums):
    #     #for i in nums:
    #     '''
    #     pass 1:
    #     if 2 <= 2 (yes) and 2 == 3
    #     this is false - count not incremented
    #     pass 2: 
    #     if 1 <= 2 (yes) and 1 == 3 (no)
    #     not incremented
    #     '''
        
    #     '''
    #     pass 1: cur = 2 + -1 = 1
    #     pass 2: 
    #     cur = 1 + 2 = 3
    #     3: 
    #     3 + 1 = 4
    #     '''
    #     cur = cur + nums[i]
    #     '''
    #     pass 1: -1 > M (3) is untrue
    #     pass 2: 2 > 3 is untrue , cur stays the same
    #     '''
    #     if nums[i] > M:
    #         cur = 0
    #     # logical break
        
    #     ''' 
    #     pass 1: cur = 1, not 3, move on
    #     pass 2: cur (3) = 3, count = 0 + 1 :)
    #     ''' 
    #     if cur == k:
    #         count = count + 1
        
    #     i = i+1
        
    # return count

if __name__ == '__main__':
    nums_count = int(input().strip())

    nums = []

    for _ in range(nums_count):
        nums_item = int(input().strip())
        nums.append(nums_item)

    k = int(input().strip())

    M = int(input().strip())

    result = countSubarraysWithSumAndMaxAtMost(nums, k, M)

    print(result)

