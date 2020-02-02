### 问题：
给定一个整数nums，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。
### 思路：
最简单的做法是将所有的子数组都找遍：即确定从不同的数开始，分别向后取连续和过程中的最大值。得到numsSize个最大值，其中最大值即为所求。
### 解决：
```
int maxSubArray(int* nums, int numsSize){
    int fwd=0;
    int *max=(int *)malloc(sizeof(int)*numsSize);
    for(int i=0;i<numsSize;i++)
    {    
        fwd=max[i]=nums[i];
        for(int j=i+1;j<numsSize;j++)
        {
            fwd+=nums[j];
            if(fwd>max[i])
                max[i]=fwd;
        }
    }
    int ans=max[0];
    for(int i=1;i<numsSize;i++)
        if(max[i]>ans)
            ans=max[i];
    free(max);
    return ans;
}
```

