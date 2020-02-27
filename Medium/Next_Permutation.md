### 问题：
实现一个能将给定数字序列重新排列成字典序中下一个更大的排列的函数。
如果不存在这样的数列，则使它成为最小的排列。必须原地修改，只允许使用额外常数空间。
### 思路：
1、从后往前寻找第一个能够替换的数字：即该数字之后要存在比其更大的数字；进行替换：将该数字和“其之后比其大且最小的数字”替换。
2、被替换位得到更大数字后，还需要将被替换位之后的数字序列进行降序排列。
### 解决：
```
void nextPermutation(int* nums, int numsSize){
    int max=nums[numsSize-1],flag=numsSize,f=numsSize-1,temp;
    for(int i=numsSize-1;i>=0;i--)
    {
        if(nums[i]>max)
        {   max=nums[i];
            f=i;}
        if(nums[i]<max)
        {   flag=i;
            break;}
    }
    if(flag==numsSize)
    {
        for(int i=0;i<numsSize/2;i++)
        {   temp=nums[i];
            nums[i]=nums[numsSize-1-i];
            nums[numsSize-1-i]=temp;}
        return;
    }
    for(int i=numsSize-1;i>flag;i--)
        if(nums[i]>nums[flag]&&nums[i]<max)
        {   max=nums[i];
            f=i;}
    nums[f]=nums[flag];
    nums[flag]=max;
    //第flag位上已经换上其后nums[]中大于nums[flag]且最小的数了。
    for(int i=0;i<numsSize-flag-2;i++)
        for(int j=flag+1+1;j<numsSize-i;j++)
            if(nums[j-1]>nums[j])
            {   temp=nums[j-1];
                nums[j-1]=nums[j];
                nums[j]=temp;}
}
```
