### 问题：
给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。
### 思路：
定义三个指针分别表示ahead,now,after,借助ahead来交换after和now。
### 解决：
```
struct ListNode* swapPairs(struct ListNode* head){
    if(head==NULL||head->next==NULL)
        return head;
    struct ListNode *ahead=(struct ListNode *)malloc(sizeof(struct ListNode)),*now=head,*after=now->next;
    ahead->val=0,ahead->next=now;
    head=after;
    //将after和now借助ahead互换;
    while(1){
        ahead->next=after;
        now->next=after->next;
        after->next=now;
        if(now->next==NULL||now->next->next==NULL)
            return head;
        //否则后移ahead,now,after,继续交换；
        ahead=now;
        now=now->next;
        after=now->next;
    }
}
```
