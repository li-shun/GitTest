### 问题：
给定一个没有重复数字的序列，返回其所有可能的全排列。
### 思路：
根据高中所学知识，我们可以画出一个树形结构图来解决这个问题。在程序上，可以进行深度优先搜索回溯遍历整个树形成解。
具体如下，使用递归实现：从所有数中选择一个不与已选数重复的数——作为第m个答案第k位数——继续上述过程确定第m个答案第k+1位数；

当第n位数选择完毕——回溯到上个结点——判断第k位数是否有下一种选择：若无，回溯到上个结点；若有，——建立第m+1位答案——重新对第k位数进行下一种选择（如上）
### 解决：
```
int m=0;
void recur(int **ans,int k,int numsSize,int*nums)
{
    int f=0;
    for(int i=0;i<numsSize;i++)
    {
        f=0;
        for(int j=0;j<k;j++)
            if(nums[i]==ans[m][j])
            {   f=1;
                break;}
        if(f==0)
        {   
            ans[m][k]=nums[i];
            if(k==numsSize-1)
                return;
            else
            {   recur(ans,k+1,numsSize,nums);
                int flag=0;
                for(int l=i+1;l<numsSize;l++)
                {   flag=0;
                    for(int h=0;h<k;h++)
                        if(nums[l]==ans[m][h])
                        {   flag=1;break;}
                    if(flag==0)
                        break;}
                
                if(i+1<numsSize&&flag==0)
                {   m++;
                    for(int y=0;y<k;y++)
                        ans[m][y]=ans[m-1][y];}
                else
                    return;
            }
        }
    }
}
int** permute(int* nums, int numsSize, int* returnSize, int** returnColumnSizes){
    int nfac=1;
    for(int i=numsSize;i>=1;i--)
        nfac*=i;
    *returnSize=nfac;
    *returnColumnSizes=(int *)malloc(sizeof(int)*nfac);
    for(int i=0;i<nfac;i++)
        (*returnColumnSizes)[i]=numsSize;
    int **ans=(int **)malloc(sizeof(int *)*nfac);
    for(int i=0;i<nfac;i++)
        ans[i]=(int *)calloc(numsSize,sizeof(int));
    m=0;
    recur(ans,0,numsSize,nums);
    return ans;
}
```
