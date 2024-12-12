# GFG_12
---
Difficulty: Hard  
Source: 160 Days of Problem Solving  
Tags:
  - Arrays  
---

# 🚀 _Day 12. Max Circular Subarray Sum_ 🧠
The problem can be found at the following link: [Problem Link](https://www.geeksforgeeks.org/batch/gfg-160-problems/track/arrays-gfg-160/problem/max-circular-subarray-sum-1587115620)

## 💡 **Problem Description:**

Given an array of integers `arr[]` in a circular fashion, return the maximum sum of a subarray that can be obtained assuming the array is circular.

**Note:** The solution should account for both regular and circular subarrays.

## 🔍 **Example Walkthrough:**

**Input:**  
`arr[] = [8, -8, 9, -9, 10, -11, 12]`  
**Output:**  
`22`

**Explanation:**  
Starting from the last element of the array, i.e., `12`, and moving in a circular fashion, the maximum subarray is `[12, 8, -8, 9, -9, 10]`, which gives the maximum sum of `22`.

**Input:**  
`arr[] = [10, -3, -4, 7, 6, 5, -4, -1]`  
**Output:**  
`23`

**Explanation:**  
Maximum sum of the circular subarray is `23`. The subarray is `[7, 6, 5, -4, -1, 10]`.

### Constraints:
- $`1 <= arr.size() <= 10^5`$
- $`-10^4 <= arr[i] <= 10^4`$

## 🎯 **My Approach:**

1. **Kadane's Algorithm for Maximum Subarray Sum:**
   - First, use Kadane’s algorithm to find the maximum subarray sum in the non-circular array (normal subarray sum).
   
2. **Kadane’s Algorithm for Minimum Subarray Sum:**
   - Use Kadane’s algorithm to find the minimum subarray sum in the array. This helps in calculating the circular maximum subarray sum.
   
3. **Total Sum Calculation:**
   - Calculate the total sum of the array and subtract the minimum subarray sum from it. This will give us the maximum circular subarray sum.
   
4. **Final Answer:**
   - The answer is the maximum of:
     - The result from Kadane’s algorithm (non-circular subarray sum).
     - The result from the circular subarray sum calculation (total sum - minimum subarray sum).
   
5. **Handle All Negative Case:**
   - If the entire array consists of negative numbers, return the result from Kadane’s algorithm for the maximum subarray sum.
     
### <div align="center">_*or*_</div>

1. **Kadane’s Algorithm**:
   - The problem is split into two parts: finding the maximum sum of a normal subarray and finding the maximum sum of a circular subarray.
   
2. **Steps:**
   - First, use Kadane's algorithm to find the maximum sum of a regular subarray.
   - Then, calculate the total sum of the array and use Kadane’s algorithm again on the negated values of the array to find the minimum subarray sum.
   - The circular subarray sum is obtained by subtracting the minimum subarray sum from the total sum.
   - Return the maximum of the regular subarray sum and the circular subarray sum.
    
## 🕒 **Time and Auxiliary Space Complexity** 

- **Expected Time Complexity:** O(n), where `n` is the size of the array. Kadane's algorithm runs in linear time, and we perform only two linear scans of the array.
  
- **Expected Auxiliary Space Complexity:** O(1), as we only use a constant amount of additional space.

## 📝 **Solution Code**
## Code (Python)

```python
def circularSubarraySum(arr):
    total_sum = 0
    max_sum = float('-inf')
    min_sum = float('inf')
    curr_max = 0
    curr_min = 0
    all_negative = True

    for num in arr:
        total_sum += num

        curr_max = max(num, curr_max + num)
        max_sum = max(max_sum, curr_max)

        curr_min = min(num, curr_min + num)
        min_sum = min(min_sum, curr_min)

        if num > 0:
            all_negative = False

    if all_negative:
        return max_sum

    return max(max_sum, total_sum - min_sum)
```
