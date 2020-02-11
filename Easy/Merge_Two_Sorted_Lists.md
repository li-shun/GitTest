### 问题：
将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 
### 解决：
```
struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2){
    if(l1==NULL)    return l2;
    if(l2==NULL)    return l1;
    struct ListNode *detect=l1,*head=l1,*forward=l2->next;
    l1=(struct ListNode*)malloc(sizeof(struct ListNode));
    l1->next=detect;
    if(l2->val<=detect->val) head=l2;
    while(1)
    {
        while(detect!=NULL&&detect->val<l2->val)
        {    l1=detect;
            detect=detect->next;}
        if(detect==NULL)  
        {    l1->next=l2;
            return head;}
        else
        {   l2->next=detect;
            l1->next=l2;
            l1=l2;         //将l2插入到detect前。
            if(forward==NULL)
                break;
            l2=forward;   //l2后移
            forward=l2->next;}
    }
    return head;
}
```
