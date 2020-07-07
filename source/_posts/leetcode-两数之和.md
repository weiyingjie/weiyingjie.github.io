---
title: leetcode-两数之和
date: 2020-07-06 22:27:14
tags: [leetcode, C语言]
---

---

## 题目内容

### 两数之和

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

 

示例:

给定 `nums = [2, 7, 11, 15], target = 9`

因为 `nums[0] + nums[1] = 2 + 7 = 9`
所以返回 `[0, 1]`

## 我滴解题代码

我用了C语言解决了一哈，虽然方法很俗，暴力破解了一手。

![结果](https://cdn.jsdelivr.net/gh/Creeper-boom/cdn/img/markdown/two_sum_res.png)
先上代码～

``` c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* twoSum(int* nums, int numsSize, int target, int* returnSize){
    int *p_arr = NULL;
    int i = 0, j = 0;

    p_arr = calloc(sizeof(int), 2);

    for(i = 0; i < numsSize - 1; i++) {
        for(j = i + 1; j < numsSize; j++) {
            if(nums[i] + nums[j] == target) {
                p_arr[0] = i;
                p_arr[1] = j;
                *returnSize = 2;
                return p_arr;
            }
        }
    }
    free(p_arr);
    return NULL;
}
```

## 关于代码的解释

题目要求将求得的结果以数组形式返回，并且编辑区开头给出

``` c
/**
 * Note: The returned array must be malloced, assume caller calls free().
 */
```

大概意思是所需要返回的数组必须是**动态开辟**出来的，假装调用者会调用`free()`函数释放它，所以在代码中调用malloc一族的函数`calloc()`进行动态开辟，开辟出两个int大小的空间给指针变量`p_arr`。通过`i, j`两个变量分别代表两个下标，`i`变量从第0个元素遍历到第numsSize - 1个元素，每一次i得到新值，j都从i的后一位开始遍历到numsSize个元素，过程中对每一个`i + j`的值与`target`进行比较，如果符合条件，则将两个下标的值存进数组`p_arr`中进行返回，同时将returnSize的值赋为2；如果遍历结束都没有找到符合条件的两个下标，则将`p_arr`指针进行释放，并且返回空值。

## Today 的收获
```
== 45 ==ERROR: AddressSanitizer: heap-buffer-overflow on address 0x60200000003
```
今天执行代码的时候跳出了这个错误，查了一下百度，康到了知乎上有一篇写了一句

![知乎](https://cdn.jsdelivr.net/gh/Creeper-boom/cdn/img/markdown/two_sum_zh.png)

大概的意思就是在返回结果的时候，不单要返回结果的数组，还要返回这个数组的长度。长知识辽～～
个人的解题思路太窄了，只能想到一种暴力滴方法，唉～还要多加努力鸭！

## 闲言碎语
今天可是有点东西，这周要交活辽，然而进展不是很顺利，加油，奥利给！！！嘻嘻～～
