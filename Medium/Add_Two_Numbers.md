### 问题：
给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：

输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
### 思路：
新建一个链表来存储两数之和，每计算出一位的和，加上上一位向前进的0或1后，即为temp所指向的结点赋值。
### 解决：
```
struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2){
    struct ListNode*head=(struct ListNode*)malloc(sizeof(struct ListNode)),*temp=head;
    head->val=0;
    int n=0;  //和
    //l1和l2一结点上的两数字相加赋给temp,若（l1->next与l2->next都是NULL或l->val都是0）且n<10(即进0),使当前结点指向NULL并跳出该循环。
    while(1)
    {   
        if(l1==NULL&&l2==NULL)//若l1和l2都是NULL
        {   temp->val=1;
            temp->next=NULL;
            return head;}
        else if(l1==NULL||l2==NULL)//若其中一个是NULL
        {   if(l1==NULL)
            {temp->val=n=l2->val+n/10;//将temp与l1/l2剩下的结点连接起来
            temp->next=l2->next;}
            else
            {temp->val=n=l1->val+n/10;//将temp与l1/l2剩下的结点连接起来
            temp->next=l1->next;}
            while(n>=10)//如果需要进位
            {   temp->val=n%10;
                if(temp->next==NULL)//如果没有下一个结点，新建结点并进一位1。
                {   temp->next=(struct ListNode*)malloc(sizeof(struct ListNode));
                    temp=temp->next;
                    temp->val=1;
                    temp->next=NULL;
                    return head;}
                temp=temp->next;//temp移到下一位
                temp->val=n=temp->val+1;//加上1；更新和n；
            }
            //temp上的数n不需要进位
            return head;
        }
        n=l1->val+l2->val+n/10;//n/10为要进的数
        temp->val=n%10;
        if(n<10&&((l1->next==NULL&&l2->next==NULL)||l2->next->val==l2->next->val==0))
        {    temp->next=NULL;
            return head;}
        else
        {   l1=l1->next;
            l2=l2->next;
            temp->next=(struct ListNode*)malloc(sizeof(struct ListNode));
            temp=temp->next;
            temp->next=NULL;}
    }
}
```


