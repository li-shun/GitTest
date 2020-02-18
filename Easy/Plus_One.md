### 问题：
给定一个由整数组成的非空数组所表示的非负整数，在该数的基础上加一。最高位数字存放在数组的首位， 数组中每个元素只存储单个数字。你可以假设除了整数 0 之外，这个整数不会以零开头。
### 思路：
将最后一位数字加一后：若<10,则完成，退出；若=10且非最高位，则变0进一位，继续重复判断前一位；若=10且为最高位，则退出并加在最高位前加一位数1。
### 解决：
```
int* plusOne(int* digits, int digitsSize, int* returnSize){
    *returnSize=digitsSize;
    int f=0,k=0;
    for(int i=digitsSize-1;i>=0;i--)
    {   k=1;
        if(i==digitsSize-1)
            digits[i]++;
        if(digits[i]<10)
            break;
        else if(digits[i]==10&&i-1>=0)
        {   digits[i-1]++;
            digits[i]=0;}
        else 
        {   f=1;
            digits[i]=0;}
    }
    if(f==0&&k==1)
            return digits;
    else
    {   *returnSize=digitsSize+1;
        int *ans=(int *)calloc(digitsSize+1,sizeof(int));
        ans[0]=1;
        for(int i=1;i<digitsSize+1;i++)
            ans[i]=digits[i-1];
        return ans;
    }
}
```
