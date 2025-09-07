# Remove Adjacent Duplicates

[Problem Link](https://www.geeksforgeeks.org/problems/recursively-remove-all-adjacent-duplicates0744/1)

## Problem Description

Given a string s, remove all its adjacent duplicate characters recursively, until there are no adjacent duplicate characters left.

Note: If the resultant string becomes empty, return an empty string.

**Examples:**
```
Input: s = "geeksforgeek"  
Output: "gksforgk"  
Explanation: g(ee)ksforg(ee)k -> gksforgk

Input: s = "abccbccba"  
Output: ""  
Explanation: ab(cc)b(cc)ba->abbba->a(bbb)a->aa->(aa)->""(empty string)
```

**Constraints:**
```
1 <= s.size() <= 10^5
```

## Approach
```
Use a recursive function to remove adjacent duplicates. In each call, iterate through the string, build a new string by skipping groups of identical adjacent characters (only add if count == 1). If the new string differs in length, recurse on it. This continues until no changes.
```

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

## Code

### C++

```cpp
#include <bits/stdc++.h>
using namespace std;

string recurse(string s) {
    int i = 0, n = s.size();
    string res = "";

    while (i < n) {
        int j = i;
        while (j < n && s[i] == s[j]) j++;
        
        if (j - 1 != i) i = j;
        else res += s[i++];
    }

    if (s.size() == res.size()) {
        return res;
    }

    return recurse(res);
}

void solve() {
    string s; cin >> s;
    string res = recurse(s);
    cout << res << endl;
}

int main() {
    int tt = 1; // cin >> tt;
    while (tt--) {
        solve();
    }
}
```

### Python

```python
def recurse(s):
    n = len(s)
    res = []
    i = 0
    while i < n:
        j = i
        while j < n and s[i] == s[j]:
            j += 1
        if j - i == 1:
            res.append(s[i])
        i = j
    res_str = ''.join(res)
    if len(res_str) == len(s):
        return res_str
    return recurse(res_str)

def solve():
    s = input().strip()
    res = recurse(s)
    print(res)

if __name__ == "__main__":
    solve()
```

### Java

```java
import java.util.*;

public class Solution {
    public static String recurse(String s) {
        int n = s.length();
        StringBuilder res = new StringBuilder();
        int i = 0;
        while (i < n) {
            int j = i;
            while (j < n && s.charAt(i) == s.charAt(j)) j++;
            if (j - i == 1) {
                res.append(s.charAt(i));
            }
            i = j;
        }
        String resStr = res.toString();
        if (resStr.length() == s.length()) {
            return resStr;
        }
        return recurse(resStr);
    }

    public static void solve() {
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine();
        String res = recurse(s);
        System.out.println(res);
    }

    public static void main(String[] args) {
        solve();
    }
}
```

## Input/Output Example
```
Input: geeksforgeek  
Output: gksforgk

Input: abccbccba  
Output:
```