### LeetCode-234	回文链表

##### 题目

请判断一个链表是否为回文链表。

**示例 1:**

```
输入: 1->2
输出: false
```

**示例 2:**

```
输入: 1->2->2->1
输出: true
```

**进阶：**
你能否用 O(n) 时间复杂度和 O(1) 空间复杂度解决此题？

##### 思路

用快慢指针找到链表中点后一位的指针，反转后面的链表，进行比较。

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
    bool isPalindrome(ListNode* head) {
        if (head == nullptr || head->next == nullptr) {
            return true;
        }
        ListNode* ptr = head;
        ListNode* height = ptr->next;
        ListNode* prev = ptr;
        while(prev->next && prev->next->next != nullptr) {
            height = height->next;
            prev = prev->next->next;
        }
        height = reverseList(height);
        while (height->next) {
            if(ptr->val == height->val) {
                ptr = ptr->next;
                height = height->next;
            } else {
                return false;
            }
        }
        if(ptr->val == height->val) {
            return true;
        } else {
            return false;
        }
    }
    
    ListNode* reverseList(ListNode* head) {
        if (!head || !head->next) return head;
        ListNode* res = reverseList(head->next);
        head->next->next = head;
        head->next = nullptr;
        return res;
    }
};
```

