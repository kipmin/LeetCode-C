### LeetCode-141	环形链表

##### 题目

给定一个链表，判断链表中是否有环。

**进阶：**
你能否不使用额外空间解决此题？

##### 思路

快慢指针，看慢的指针会不会追上快的指针。

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
    cin.tie(0);
    return 0;
}();

class Solution {
public:
    bool hasCycle(ListNode *head) {
        if (head == nullptr)
            return false;
        ListNode* ptr = head;
        ListNode* tp = head;
        while(tp && tp->next) {
            ptr = ptr->next;
            tp = tp->next->next;
            if(ptr == tp) {
                return true;
            }
        }
        return false;
    }
};
```

