### 问题：
给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。
### 解决：
```
int searchInsert(int* nums, int numsSize, int target){
    for(int i=0;i<numsSize;i++)
        if(nums[i]>=target)
            return i;
    return numsSize;
}
```
