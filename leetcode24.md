# 两两交换链表中的节点
### 多指针要手画图理清操作顺序
### 递归思想继续学习

```
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        if(head == nullptr || head->next == nullptr) return head;
        ListNode* temp1 = head, *temp2 = head->next->next;
        head = head->next;
        head->next = temp1;
        temp1->next = swapPairs(temp2);  //递归的精妙
        return head;
    }
};
```