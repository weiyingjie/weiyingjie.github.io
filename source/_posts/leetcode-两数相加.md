---
title: leetcode-两数相加
date: 2020-07-08 00:26:58
tags: [leetcode,C语言]
---

## 题目内容

### 两数相加
给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：
```
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
```

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/add-two-numbers

## 解题代码
这个题可是把我给搞惨了，试了N种方法，都有测试用例不符合。。。不过最后还是成功啦，开心～

### 结果
![结果](https://cdn.jsdelivr.net/gh/Creeper-boom/cdn/img/markdown/add_two_num_res.png)

24ms只击败了21.54%的hxd！！还是太年轻鸭

康康代码吧：

### 代码

``` c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */


struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2){
    struct ListNode *p = NULL, *temp_l = NULL;
    int temp_n = 0, num = 0;

	// 对头结点开辟空间
    temp_l = calloc(sizeof(*p), 1);
    p = temp_l;

	// 判断两个输入链表的结点进行判断
    while(l1 != NULL || l2 != NULL) {
        if(l1 == NULL)
            num = 0 + l2->val;
        else if(l2 == NULL)
            num = l1->val + 0;
        else
            num = l1->val + l2->val;

        num += temp_n; // temp_n来记录上一位的和有没有进位

        if(num > 9) {
            temp_n = 1;
            temp_l->val += num - 10;
        } else {
            temp_n = 0;
            temp_l->val += num;
        }
		
		// 将指针指向下一个结点
        if(l1 == NULL)
            l2 = l2->next;
        else if(l2 == NULL)
            l1 = l1->next;
        else {
            l1 = l1->next;
            l2 = l2->next;
        }
        if(l1 == NULL && l2 == NULL && temp_n == 0)
            break;

        temp_l->next = calloc(sizeof(*p), 1);
        temp_l = temp_l->next;

    }
	
	// 处理连续进位的情况,如 [1]和[9,9] 的用例
    if (temp_n == 1) {
        temp_l->val = 1;
        temp_l->next = NULL;
    }
	
    return p;
    
}
```

## 代码解析

### Round 1

题目说将两个链表进行想加, 之后由说`原因：342 + 465 = 807`,我直接寻思, 将两个链表分别转换成整数, 进行求和, 得到的结果再按位存储到结果链表中

整挺好~

可是可是呀, 系统给出测试用例长这个样
```
[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1]
[5,6,4]
```

直接给我报了个长度不够的错误, 那可不是不够么! 这么大个数转换成整型能放得下才怪..

### Round 2

这回换了个思路, 按位直接求和之后放在结果链表中, 并记录下需要进位的值, 再处理一下结束的条件,就完成啦. 最后要注意连续进位的情况,这里又栽了一次...

## 牢骚牢骚~~~
又到了晚上一点, 明天工作肯定完不成, 嗨..

==继续坚持,fighting~ #F44336==