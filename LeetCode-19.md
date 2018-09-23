### LeetCode-19	删除链表的倒数第N个节点

##### 题目

给定一个链表，删除链表的倒数第 *n* 个节点，并且返回链表的头结点。

**示例：**

```
给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
```

**说明：**

给定的 *n* 保证是有效的。

**进阶：**

你能尝试使用一趟扫描实现吗？

##### 思路

一趟扫描实现，需要设置2个指针，将后面的指针通过n来往后扫描，然后当后面指针为空时，删除ptr-next即可。

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */

class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* ptr = head;
        ListNode* temp = ptr;
        while(n > 0) {
            temp = temp->next;
            n--;
        }
        if (temp == nullptr) return head->next;
        while(temp->next) {
            ptr = ptr->next;
            temp = temp->next;
        }
        ptr->next = ptr->next->next;
        return head;
    }
};
```

