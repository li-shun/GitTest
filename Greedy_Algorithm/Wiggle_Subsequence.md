### 问题：
如果连续数字之间的差严格地在正数和负数之间交替，则数字序列称为摆动序列。第一个差（如果存在的话）可能是正数或负数。少于两个元素的序列也是摆动序列。
例如， [1,7,4,9,2,5] 是一个摆动序列，因为差值 (6,-3,5,-7,3) 是正负交替出现的。相反, [1,4,7,2,5] 和 [1,7,4,5,5] 不是摆动序列，第一个序列是因为它的前两个差值都是正数，第二个序列是因为它的最后一个差值为零。
给定一个整数序列，返回作为摆动序列的最长子序列的长度。 通过从原始序列中删除一些（也可以不删除）元素来获得子序列，剩下的元素保持其原始顺序。
### 思路：
猜想：把第一个元素当作摆动序列的起点，从第二个元素开始，第一个不与第一个元素相等的元素作摆动序列的第二个数。然后遍历之后的整个数组，沿着前面的大小关系判断该数是否>/<上一个确定的摆动元素。

错误/更改：如现在我需要找一个大于上一个摆动元素的数，目前遍历到nums[i]，但nums[i],nums[i+1],nums[i+2],…,nums[i+k]呈递增规律增加，也显然都大于上一个摆动元素，则此时，选择nums[i+k]作为下一个摆动元素是最好的。
### 解决：
```
int wiggleMaxLength(int* nums, int numsSize){
//x寻找一段摆动序列的关键，是找到序列的起点..能假设最长的序列是从第一/二个元素开始的吗？
    if(numsSize==0)
        return 0;
    int flag=0,ah=0,ans=1,j=0;//表示摆动序列前一个元素的序号数
    for(int i=1;i<numsSize;i++)
    {   if(nums[i]>nums[0])
        {   flag=0;break;}
        if(nums[i]<nums[0])
        {   flag=1;break;}
    }//flag=1表当前元素大于上个元素,flag=0表小于，现在flag为初始状态
    for(int i=1;i<numsSize;i++)
    {
        if(flag==1)//表示刚遇到了“大数”，要找“小数”
        {
            if(nums[i]<nums[ah])
            {   j=1;
                while(i+j<numsSize&&nums[i+j]<nums[i+j-1])
                    j++;
                i=i+j-1;
                ans++;
                flag=0;
                ah=i;
                continue;}
        }
        if(flag==0)
        {
            if(nums[i]>nums[ah])
            {   j=1;
                while(i+j<numsSize&&nums[i+j]>nums[i+j-1])
                    j++;
                i=i+j-1;
                ans++;
                flag=1;
                ah=i;
                continue;}
        }
    }
    return ans;
}
```
