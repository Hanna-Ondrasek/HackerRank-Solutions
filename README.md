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
        


    result = countSubarraysWithSumAndMaxAtMost(nums, k, M)

    print(result)



# Count Elements Greater Than Previous Average
Given an array of positive integers, return the number of elements that are strictly greater than the average of all previous elements. Skip the first element.

Example

Input

responseTimes = [100, 200, 150,300]
Output

2
Explanation

- Day 0: 100 (no previous days, skip) 
- Day 1: 200 > average(100) = 100 → count = 1 
- Day 2: 150 vs average(100, 200) = 150 → not greater → count = 1 
- Day 3: 300 > average(100, 200, 150) = 150 → count = 2 Return 2.
Input Format

The first line contains an integer n (0 ≤ n ≤ 1000), the number of days.
If n > 0, the next n lines contains an integer representing responseTimes[i].
If n = 0, the second line is omitted or empty.
Example

4
100
200
150
300
here 4 is the length of array, followed by the elements of array on each line.

Constraints

0 <= responseTimes.length <= 1000
1 <= responseTimes[i] <= 10^9 for 0 <= i < responseTimes.length
Output Format

A single integer depicting the count of days.
Sample Input 0

0
Sample Output 0

0
Sample Input 1

1
100
Sample Output 1

0

#include <bits/stdc++.h>

using namespace std;

string ltrim(const string &);
string rtrim(const string &);



/*
 * Complete the 'countResponseTimeRegressions' function below.
 *
 * The function is expected to return an INTEGER.
 * The function accepts INTEGER_ARRAY responseTimes as parameter.
 */




int countResponseTimeRegressions(vector<int> responseTimes) {
    if (responseTimes.empty()) {
        return 0;
    }
    
    else if (responseTimes.size() == 1) {
        return 0;
    }
    
    else {
        double cur_sum = 0;
        //int size_of = 0;
        int greater_than_avg_count = 0;
        for (int i = 0; i < (responseTimes.size()-1); i++) {
            cur_sum = cur_sum + responseTimes[i];
            int size_of = i + 1;
            
            double average = cur_sum / size_of;
            if (responseTimes[i+1] > average) {
                greater_than_avg_count = greater_than_avg_count + 1;
            }
        }
        return greater_than_avg_count;
    }
    //return 0;
}

int main()
{
    string responseTimes_count_temp;
    getline(cin, responseTimes_count_temp);

    int responseTimes_count = stoi(ltrim(rtrim(responseTimes_count_temp)));

    vector<int> responseTimes(responseTimes_count);

    for (int i = 0; i < responseTimes_count; i++) {
        string responseTimes_item_temp;
        getline(cin, responseTimes_item_temp);

        int responseTimes_item = stoi(ltrim(rtrim(responseTimes_item_temp)));

        responseTimes[i] = responseTimes_item;
    }

    int result = countResponseTimeRegressions(responseTimes);

    cout << result << "\n";

    return 0;
}

string ltrim(const string &str) {
    string s(str);

    s.erase(
        s.begin(),
        find_if(s.begin(), s.end(), not1(ptr_fun<int, int>(isspace)))
    );

    return s;
}

string rtrim(const string &str) {
    string s(str);

    s.erase(
        find_if(s.rbegin(), s.rend(), not1(ptr_fun<int, int>(isspace))).base(),
        s.end()
    );

    return s;
}




# Count Number Pairs
Given a sorted array of positive integers and a target value, count the number of pairs (i, j) where i < j and array[i] + array[j] <= target.

Example

Input:

prices = [1, 2, 3, 4, 5]
budget = 7
Output:

8
Explanation:

We need pairs (i, j) with i < j and prices[i] + prices[j] ≤ 7. List all pairs:

(1, 2) = 3 ≤ 7
(1, 3) = 4 ≤ 7
(1, 4) = 5 ≤ 7
(1, 5) = 6 ≤ 7
(2, 3) = 5 ≤ 7
(2, 4) = 6 ≤ 7
(2, 5) = 7 ≤ 7
(3, 4) = 7 ≤ 7
Pairs like (3,5)=8, (4,5)=9 exceed the budget. Total valid pairs = 8.

Input Format

The input is provided in two lines:

The first line contains two space-separated integers n and budget, where:

0 ≤ n ≤ 1000
1 ≤ budget ≤ 10^9
The second line contains n space-separated integers prices[0], prices[1], ..., prices[n-1], where:

1 ≤ prices[i] ≤ 10^9 for all 0 ≤ i < n
prices is sorted in non-decreasing order
Constraints

0 ≤ prices.length ≤ 1000
1 ≤ prices[i] ≤ 10^9 for all 0 ≤ i < prices.length
prices is sorted in non-decreasing order
1 ≤ budget ≤ 10^9
All inputs are integers
Output Format

Output a single integer representing the total count of unique index pairs (i, j) with 0 ≤ i < j < n such that prices[i] + prices[j] ≤ budget. If n < 2, output 0.

Sample Input 0

0
100
Sample Output 0

0
Sample Input 1

1
5
5
Sample Output 1

0

#include <bits/stdc++.h>

using namespace std;

string ltrim(const string &);
string rtrim(const string &);



/*
 * Complete the 'countAffordablePairs' function below.
 *
 * The function is expected to return an INTEGER.
 * The function accepts following parameters:
 *  1. INTEGER_ARRAY prices
 *  2. INTEGER budget
 */

int countAffordablePairs(vector<int> prices, int budget) {
    int pairCount = 0;
    for (int i = 0; i < prices.size(); i++) {
        // the one being compared against
        for (int j = i+1; j < prices.size(); j++) {
        // this should start at whatever the current index is on +1, then loops until the end 
            if ((prices[i] + prices[j]) <= budget) {
                pairCount = pairCount + 1;
            }
        }
        
    }
    
    return pairCount;
}

int main()
{
    string prices_count_temp;
    getline(cin, prices_count_temp);

    int prices_count = stoi(ltrim(rtrim(prices_count_temp)));

    vector<int> prices(prices_count);

    for (int i = 0; i < prices_count; i++) {
        string prices_item_temp;
        getline(cin, prices_item_temp);

        int prices_item = stoi(ltrim(rtrim(prices_item_temp)));

        prices[i] = prices_item;
    }

    string budget_temp;
    getline(cin, budget_temp);

    int budget = stoi(ltrim(rtrim(budget_temp)));

    int result = countAffordablePairs(prices, budget);

    cout << result << "\n";

    return 0;
}

string ltrim(const string &str) {
    string s(str);

    s.erase(
        s.begin(),
        find_if(s.begin(), s.end(), not1(ptr_fun<int, int>(isspace)))
    );

    return s;
}

string rtrim(const string &str) {
    string s(str);

    s.erase(
        find_if(s.rbegin(), s.rend(), not1(ptr_fun<int, int>(isspace))).base(),
        s.end()
    );

    return s;
}


# Merge and Sort Intervals
Given an array of intervals [startTime, endTime], merge all overlapping intervals and return a sorted array of non-overlapping intervals.

Example

Input

intervals = [[1, 3], [2, 6], [8, 10], [15, 18]]
Output

[[1, 6], [8, 10], [15, 18]]
Explanation

- Step 1: Sort intervals by start time (already sorted). 
- Step 2: Initialize merged list with first interval [1,3]. 
- Step 3: Compare [2,6] with last merged [1,3]. They overlap (2 ≤ 3), so merge into [1,6]. Step 4: Compare [8,10] with last merged [1,6]. No overlap (8 > 6), append [8,10]. 
- Step 5: Compare [15,18] with last merged [8,10]. No overlap (15 > 10), append [15,18]. 

Result: [[1,6],[8,10],[15,18]].
Input Format

The first line contains an integer denoting the number of intervals.
The second line contains an integer denoting the length of individual interval array.
Each of the next N lines contains two space-separated integers startTime and endTime
Intervals may be provided in any order; duplicates and fully contained intervals are allowed.
Example

4
2
1 3
2 6
8 10
15 18
here, 4 is the number of intervals, 2 is the length of individual interval array, followed by the intervals.

Constraints

0 <= intervals.length <= 100000
intervals[i].length == 2 for all 0 <= i < intervals.length
0 <= intervals[i][0] < intervals[i][1] <= 10^9 for all 0 <= i < intervals.length
Output Format

Return a 2D array of two space-separated integers start and end, representing the merged intervals sorted by increasing start time.
Sample Input 0

0
0
Sample Input 1

1
2
5 10
Sample Output 1

5 10


#include <bits/stdc++.h>

using namespace std;

string ltrim(const string &);
string rtrim(const string &);
vector<string> split(const string &);



/*
 * Complete the 'mergeHighDefinitionIntervals' function below.
 *
 * The function is expected to return a 2D_INTEGER_ARRAY.
 * The function accepts 2D_INTEGER_ARRAY intervals as parameter.
 */

vector<vector<int>> mergeHighDefinitionIntervals(vector<vector<int>>& intervals) {
    
    sort(intervals.begin(), intervals.end());
        
    if (intervals.size() <= 1) {
        return intervals;
    }
    vector<vector<int>> returnV;
    returnV.push_back(intervals[0]);
    
    

    for (int i = 1; i < intervals.size(); i++) {
        // reference to another vector b/c when this reference's value is
        // changed, the base
        // vector's memory is modified
        // which we need for last[1] = .... because this modifies
        // returnV's last element too
        // also, if we were to use the base vectors, it would be a pain in the ass
        vector<int>& last = returnV.back();
        vector<int>& cur = intervals[i];
            if (last[1] >= cur[0]) {
                last[1] = max(last[1], cur[1]);
            }
            else {
                returnV.push_back(cur);
            }
    }
    return returnV;
}

int main()
{
    string intervals_rows_temp;
    getline(cin, intervals_rows_temp);

    int intervals_rows = stoi(ltrim(rtrim(intervals_rows_temp)));

    string intervals_columns_temp;
    getline(cin, intervals_columns_temp);

    int intervals_columns = stoi(ltrim(rtrim(intervals_columns_temp)));

    vector<vector<int>> intervals(intervals_rows);

    for (int i = 0; i < intervals_rows; i++) {
        intervals[i].resize(intervals_columns);

        string intervals_row_temp_temp;
        getline(cin, intervals_row_temp_temp);

        vector<string> intervals_row_temp = split(rtrim(intervals_row_temp_temp));

        for (int j = 0; j < intervals_columns; j++) {
            int intervals_row_item = stoi(intervals_row_temp[j]);

            intervals[i][j] = intervals_row_item;
        }
    }

    vector<vector<int>> result = mergeHighDefinitionIntervals(intervals);

    for (size_t i = 0; i < result.size(); i++) {
        for (size_t j = 0; j < result[i].size(); j++) {
            cout << result[i][j];

            if (j != result[i].size() - 1) {
                cout << " ";
            }
        }

        if (i != result.size() - 1) {
            cout << "\n";
        }
    }

    cout << "\n";

    return 0;
}

string ltrim(const string &str) {
    string s(str);

    s.erase(
        s.begin(),
        find_if(s.begin(), s.end(), not1(ptr_fun<int, int>(isspace)))
    );

    return s;
}

string rtrim(const string &str) {
    string s(str);

    s.erase(
        find_if(s.rbegin(), s.rend(), not1(ptr_fun<int, int>(isspace))).base(),
        s.end()
    );

    return s;
}

vector<string> split(const string &str) {
    vector<string> tokens;

    string::size_type start = 0;
    string::size_type end = 0;

    while ((end = str.find(" ", start)) != string::npos) {
        tokens.push_back(str.substr(start, end - start));

        start = end + 1;
    }

    tokens.push_back(str.substr(start));

    return tokens;
}
# Pivoted Search
Given a sorted array of unique integers that has been rotated at an unknown pivot, find the index of a target value or return -1 if not found.

Example

Input:

nums = [1609466400, 1609470000, 1609473600, 1609459200, 1609462800]
target = 1609459200
Output:

3
Explanation:

We perform a binary search on the rotated array:

left=0, right=4, mid=(0+4)//2=2, nums[mid]=1609473600.
nums[left]=1609466400 <= nums[mid], so the left half [indices 0..2] is sorted. Target 1609459200 is not in [1609466400..1609473600], so search in right half: left=mid+1=3.
Now left=3, right=4, mid=(3+4)//2=3, nums[mid]=1609459200, which equals the target. Return index 3.
Input Format

The input is given in three lines.

Line 1: an integer n (0 ≤ n ≤ 100000), the number of timestamps.

Line 2: n space-separated long integers nums[i] (0 ≤ nums[i] ≤ 10^18), representing a rotated version of a strictly increasing array of unique Unix timestamps.

Line 3: a single long integer target (0 ≤ target ≤ 10^18), the timestamp to search for. The sequence in nums is guaranteed to be the result of rotating an originally strictly increasing sorted array at an unknown pivot.

Constraints

0 <= nums.length <= 100000
0 <= nums[i] <= 10^18
All elements in nums are unique
nums is obtained by taking a strictly increasing sorted array and rotating it at an unknown pivot
0 <= target <= 10^18
Output Format

Output a single integer: the 0-based index of target in nums if it exists; otherwise output -1.

Sample Input 0

0
5
Sample Output 0

-1
Sample Input 1

1
100
100
Sample Output 1

0
Language
Python 3
11011121314151617181920212223
#!/bin/python3

import math
import os
import random
import re
import sys



#
# Complete the 'searchRotatedTimestamps' function below.
#
# The function is expected to return an INTEGER.
# The function accepts following parameters:
#  1. INTEGER_ARRAY nums
#  2. INTEGER target
#


#include <bits/stdc++.h>

using namespace std;

string ltrim(const string &);
string rtrim(const string &);



/*
 * Complete the 'searchRotatedTimestamps' function below.
 *
 * The function is expected to return an INTEGER.
 * The function accepts following parameters:
 *  1. INTEGER_ARRAY nums
 *  2. INTEGER target
 */

int searchRotatedTimestamps(vector<int> nums, int target) {
    // int mid = (nums.size()) / 2;
    // left and right being ptrs may be overkill but idk
    int left = 0;
    int right = nums.size() - 1; // 2
    // in place
    while (left <= right) { // 1 2 3, looking for 5
        int mid = left + (right-left) / 2; //
        
        if (nums[mid] == target) {
            return mid;
        }
        
        
        if (nums[left] <= nums[mid]) {
            if (nums[left] <= target && target < nums[mid]) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }
        else {
            if (nums[mid] < target && target <= nums[right]) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        
        
    }
    return -1;
}

int main()
{
    string nums_count_temp;
    getline(cin, nums_count_temp);

    int nums_count = stoi(ltrim(rtrim(nums_count_temp)));

    vector<int> nums(nums_count);

    for (int i = 0; i < nums_count; i++) {
        string nums_item_temp;
        getline(cin, nums_item_temp);

        int nums_item = stoi(ltrim(rtrim(nums_item_temp)));

        nums[i] = nums_item;
    }

    string target_temp;
    getline(cin, target_temp);

    int target = stoi(ltrim(rtrim(target_temp)));

    int result = searchRotatedTimestamps(nums, target);

    cout << result << "\n";

    return 0;
}

string ltrim(const string &str) {
    string s(str);

    s.erase(
        s.begin(),
        find_if(s.begin(), s.end(), not1(ptr_fun<int, int>(isspace)))
    );

    return s;
}

string rtrim(const string &str) {
    string s(str);

    s.erase(
        find_if(s.rbegin(), s.rend(), not1(ptr_fun<int, int>(isspace))).base(),
        s.end()
    );

    return s;
}


