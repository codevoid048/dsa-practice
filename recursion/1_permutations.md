# Permutations

[Problem Link](https://leetcode.com/problems/permutations/description/)

## Problem Description

Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

**Examples**
```
Input: nums = [1,2,3]  
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

Input: nums = [0,1]  
Output: [[0,1],[1,0]]
```

**Constraints:**
```
- 1 <= nums.length <= 6
- -10 <= nums[i] <= 10
- All the integers of nums are unique.
````

## Approach
```
Use backtracking to generate all permutations. Start from the first index, swap the current element with each subsequent element, recurse for the next index, and backtrack by swapping back.
```

**Time Complexity:** O(n!)  
**Space Complexity:** O(n)

## Code

### C++

```cpp
#include <bits/stdc++.h>
using namespace std;

void recurse(vector<int> &nums, int ind, vector<vector<int>> &res) {
   if(ind == (int)nums.size()) {
    res.push_back(nums);
    return;
   }

   for(int i = ind; i < (int)nums.size(); i++) {
    swap(nums[ind], nums[i]);
    recurse(nums, ind+1, res);
    swap(nums[ind], nums[i]);
   }
}

void solve(){
   int n; cin >> n;
   vector<int> nums(n);
   for(int &i : nums) cin >> i;

   vector<vector<int>> res;
   recurse(nums, 0, res);

   for(auto &v : res){
    for(int i : v) cout << i << " ";
    cout << endl;
   }
}

signed main(){
    int tt = 1; //cin >> tt;
    while(tt--){
      solve();
    }
}
```

### Python

```python
def permute(nums):
    def backtrack(start):
        if start == len(nums):
            result.append(nums[:])
            return
        for i in range(start, len(nums)):
            nums[start], nums[i] = nums[i], nums[start]
            backtrack(start + 1)
            nums[start], nums[i] = nums[i], nums[start]
    
    result = []
    backtrack(0)
    return result

nums = [1,2,3]
print(permute(nums))
```

### Java

```java
import java.util.*;

public class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(nums, 0, result);
        return result;
    }

    private void backtrack(int[] nums, int start, List<List<Integer>> result) {
        if (start == nums.length) {
            List<Integer> perm = new ArrayList<>();
            for (int num : nums) {
                perm.add(num);
            }
            result.add(perm);
            return;
        }
        for (int i = start; i < nums.length; i++) {
            swap(nums, start, i);
            backtrack(nums, start + 1, result);
            swap(nums, start, i);
        }
    }

    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }

    public static void main(String[] args) {
        Solution sol = new Solution();
        int[] nums = {1,2,3};
        List<List<Integer>> res = sol.permute(nums);
        for (List<Integer> list : res) {
            System.out.println(list);
        }
    }
}
```

## Input/Output Example
```
Input: [1,2,3]  
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```