# [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

## Problem

![image-20200810003205682](pic/image-20200810003205682.png)

## Solution
* 思路：主要使用**双指针技巧**。具体先看代码
* 代码
```
class Solution {
public:
    string minWindow(string s, string t) {
        unordered_map<char, int> need, window;
        for (char c: t) need[c]++;
        
        int left = 0, right = 0;
        int valid = 0;
        int start=0, len=s.size()+1;
        while(right < s.size()){
            char c = s[right];
            right++;
            if (need.count(c)){
                window[c]++;
                if (window[c] == need[c])
                    valid++;
            }
            while (valid == need.size()){
                if (right - left < len){
                    start = left;
                    len = right - left;
                }
                char d = s[left];
                left++;
                if (need.count(d)){
                    if (window[d] == need[d])
                        valid--;
                    window[d]--;
                }
            }
        }
        return len == (s.size()+1) ? "":s.substr(start, len);
    }
};
```

