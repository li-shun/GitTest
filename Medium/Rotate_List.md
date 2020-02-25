### 问题：
给定一个链表，旋转链表，将链表每个节点向右移动k个位置，其中k是非负数。
### 思路：
len为链表长度，则移动k个位置等同于移动k=k%len(k < len)个位置。旋转后序号为len-k的节点将作为头节点（0除外），再使两边首尾相连，于头节点前一节点断开即可。
### 解决：
```
struct ListNode* rotateRight(struct ListNode* head, int k){
    if(head==NULL)
        return head;
    int len=1;
    struct ListNode *temp=head,*ahead=head;
    while(temp->next!=NULL)
    {   temp=temp->next;
        len++;}
    k=k%len;//0<=k<=len-1;对应Head0-len-1-len-2------1;
    //k(0)对应旋转后以节点len-k(0)为Head的链表
    if(k==0||len==1)
        return head;
    temp->next=head;//形成环形链表
    temp=head->next;
    for(int i=1;;i++)
    {
        if(i==len-k)
        {   ahead->next=NULL;
            return temp;}
        ahead=temp;
        temp=temp->next;
    }
}
```
