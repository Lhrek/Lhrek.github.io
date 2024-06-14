---
layout:     post
title:      "lc141 环形链表 "
subtitle:   "判断链表是否有环"
date:       2024-06-14 14:21:04
author:     "GanZJ"
header-img: "img/post-bg-cs106b.jpg"
catalog: true
tags:
  - 每日一题
  - 双指针
---

> 使用双指针，一个指针每次移动一个节点，一个指针每次移动两个节点，如果存在环，那么这两个指针一定会相遇。

```cpp
    bool hasCycle(ListNode *head) {
        if(head == NULL) return false;
        auto f1 = head;
        auto f2 = head->next;
        while(f1 != NULL && f2 != NULL && f2->next != NULL){
          if(f1 == f2)
            return true;
          f1 = f1->next;
          f2 = f2->next->next;
        }
        return false;
    }
```

