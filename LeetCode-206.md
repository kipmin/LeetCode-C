### LeetCode-206	反转链表

##### 题目

反转一个单链表。

**示例:**

```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

**进阶:**
你可以迭代或递归地反转链表。你能否用两种方法解决这道题？

##### 思路

###### 迭代

遍历，先找到ptr->next->next存起来，再将ptr->next指向ptr，遍历结束后把head节点的next设为nullptr即可。

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
static int x = []() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    return 0;
}();

class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if (!head || !head->next) return head;
        ListNode* ptr = head;
        ListNode* pve = head->next;
        ListNode* tmp;
        while(pve->next) {
            tmp = pve->next;
            pve->next = ptr;
            ptr = pve;
            pve = tmp;
        }
        pve->next = ptr;
        head->next = nullptr;
        return pve;
    }
};
```

###### 递归

用递归得到输入最后指针后，把最后的值挪到前面值的next指针上。

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
static int x = []() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    return 0;
}();

class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if (!head || !head->next) return head;
        ListNode* res = reverseList(head->next);
        head->next->next = head;
        head->next = nullptr;
        return res;
    }
};
```

