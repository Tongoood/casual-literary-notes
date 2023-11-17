
# 问题描述

给你一个字符串 s 、一个字符串 t 。返回 s 中涵盖 t 所有字符的最小子串。如果 s 中不存在涵盖 t 所有字符的子串，则返回空字符串 "" 。

 

注意：

    对于 t 中重复字符，我们寻找的子字符串中该字符数量必须不少于 t 中该字符数量。
    如果 s 中存在这样的子串，我们保证它是唯一的答案。

 

# 示例 


示例 1：

输入：s = "ADOBECODEBANC", t = "ABC"
输出："BANC"
解释：最小覆盖子串 "BANC" 包含来自字符串 t 的 'A'、'B' 和 'C'。

示例 2：

输入：s = "a", t = "a"
输出："a"
解释：整个字符串 s 是最小覆盖子串。

示例 3:

输入: s = "a", t = "aa"
输出: ""
解释: t 中两个字符 'a' 均应包含在 s 的子串中，
因此没有符合条件的子字符串，返回空字符串。


```

ss Solution {
public:
    string minWindow(string s, string t) {
        unordered_map<char, int> tmap, smap;
        int left = 0, correct = 0;
        string res = s + "initialize a max string";
        // 对于t制作字符出现数的字典
        for (auto item : t) 
            ++tmap[item];

        for (int right = 0; right < s.size(); ++right) {
            // smap维护的是当前窗口内的字符出现数的字典
            ++smap[s[right]];
            // 当前right对应s的字符是在t中出现的，并且数量上还没有达到冗余，是一次有效添加
            if (tmap[s[right]] >= smap[s[right]])
                ++correct;
            // 字符串最短是空串 && 如果left对应的字符是冗余，那么进行右移删除
            while (left < right && smap[s[left]] > tmap[s[left]])
                --smap[s[left++]];
            if (correct == t.size()){
                // 窗口内已经满足t串的所有字符
                if (right - left + 1 < res.size())
                    res = s.substr(left, right - left + 1);
            }

        }
        return res == s + "initialize a max string" ? "" : res;
    }
    
    ```