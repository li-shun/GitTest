### 问题：
给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。
### 思路：
冒泡排序
### 解决：
```
void sortColors(int* nums, int numsSize){
    int temp=0;
    for(int i=0;i<numsSize;i++)
    {
        if(nums[i]==0)
            for(int j=0;j<i;j++)
                if(nums[j]!=0)
                {   nums[i]=nums[j];
                    nums[j]=0;
                    break;} 
        else if(nums[i]==2)
            for(int j=numsSize-1;j>i;j--)
                if(nums[j]!=2)
                {   nums[i]=nums[j];
                    nums[j]=2;
                    break;}
    }
    for(int i=0;i<numsSize;i++)
        if(nums[i]==0)
            for(int j=0;j<i;j++)
                if(nums[j]!=0)
                {   nums[i]=nums[j];
                    nums[j]=0;}
    for(int i=0;i<numsSize;i++)
        if(nums[i]==2)
            for(int j=numsSize-1;j>i;j--)
                if(nums[j]!=2)
                {   nums[i]=nums[j];
                    nums[j]=2;
                    break;}
}
```
