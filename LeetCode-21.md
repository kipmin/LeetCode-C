### LeetCode-21	合并两个有序链表

##### 题目

将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

**示例：**

```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```













##### 思路

先判断是否有空链表，有空直接输出另一个，再判断第一个值哪个最小，将其作为主链表，然后将另一个链表挨个比较，插入到主链表里去。

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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if (!l1) {
            return l2;
        } else if (!l2) {
            return l1;
        }
        ListNode* head,* temp;
        if (l1->val > l2->val) {
            temp = l1;
            l1 = l2;
            l2 = temp;
        }
        head = l1;
        while(l2) {
            if (l1->next == NULL) {
                l1->next = l2;
                break;
            } else if (l1->next->val < l2->val) {
                l1 = l1->next;
            } else {
                temp = l2->next;
                l2->next = l1->next;
                l1->next = l2;
                l2 = temp;
            }
        }
        return head;
    }
};
```

