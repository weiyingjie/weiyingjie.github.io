---
title: leetcode-无重复字符的最长子串
date: 2020-07-09 00:44:04
tags: [leetcode, C语言]
---

## 题目描述
###无重复字符的最长子串
给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

示例 1:
```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```
示例 2:
```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```
示例 3:
```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/longest-substring-without-repeating-characters

## 代码(不正确)

今天没有解决这个问题, 先将代码保存一下, 明天再看吧

```c
int lengthOfLongestSubstring(char * s){
    int max_len = 0; // 最大长度
    int cur_len = 0; // 当前长度
    char *max_p = NULL; // 最长子串的指针
    char *head_p = NULL; // 子串开始的指针
    char *cur_p = NULL; // 当前的指针
    
    max_p = head_p = s;
    cur_p = head_p + 1;

    while(*s) {
        if(*head_p != *cur_p && *cur_p != '\0') {
           cur_p++;
        } else {
            // 有与首字符重复的字符
            max_p = head_p;
            cur_len = cur_p - head_p;
            printf("%d\n", cur_len);
            if(max_len < cur_len) {
                if(cur_len >= 3) {
                    head_p = max_p + 1;
                    cur_p = head_p + 1;
                    while(head_p != max_p + cur_len - 1) {
                        if(*head_p == *cur_p) {
                            cur_len = cur_p - max_p;
                            printf("26:%d max: %c\n",cur_len, *max_p);
                            head_p = max_p + 1;
                            cur_p = head_p + 1;
                        } else {
                            cur_p++;
                        }
                        if(cur_p == max_p + cur_len)
                            head_p++;
                        if(cur_p == head_p)
                            break;
                    }                    
                }
                printf("38: %d %c %c\n", cur_len, *head_p, *cur_p);
                if(cur_len > max_len)
                    max_len = cur_len;  
                printf("maxlen:%d\n", max_len);            
            } else {
                head_p = max_p + 1;
                cur_p = head_p + 1;
                cur_len = 0;
            }
        }
        if(head_p[1] == '\0')
            break;
    }


    return max_len;
}
```
---

2020年07月09日 00时50分20秒

---
