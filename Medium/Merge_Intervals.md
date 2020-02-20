### 问题：
给出一个区间的集合，合并所有重叠的区间。
### 思路：
将数轴<br>
0，0.5，1，1.5，2，2.5，3，3.5，4，……，500，……<br>
与0-1数列<br>
0，0，0，0，0，0，0，0，0，……，0，……建立对应关系，将数轴上给定区间对应的数列值由0设为1后：数列中数字1在数轴中对应的区间即为合并后的区间。
P.S.:数轴以0.5为间隔是为了应对区间的连续性，若以1为间隔，则【1，4】,【5，6】将合并为【1，6】，而4.5的存在使两者不可合并。
### 解决：
```
int** merge(int** intervals, int intervalsSize, int* intervalsColSize, int* returnSize, int** returnColumnSizes){
    float arr[10000][2]={0};
    for(int i=0;i<10000;i++)
        arr[i][0]=i/2;
    for(int i=0;i<intervalsSize;i++)
        for(int j=2*intervals[i][0];j<=2*intervals[i][1];j++)
            arr[j][1]=1;
    int **ans=(int **)malloc(sizeof(int*)*500);
    for(int i=0;i<500;i++)
        ans[i]=(int *)malloc(sizeof(int)*2);
    int m=0,j=0;//m标区间的个数
    for(int i=0;i<9000;i++)
    {
        if(arr[i][1]==1)
        {   
            ans[m][0]=arr[i][0];
            j=1;
            while(i+j<10000&&arr[i+j][1]==1)
                j++;
            ans[m][1]=arr[i+j-1][0];
            i=i+j;
            m++;
        }
    }
    *returnSize=m;
    *returnColumnSizes=(int *)malloc(sizeof(int)*m);
    for(int i=0;i<m;i++)
        (*returnColumnSizes)[i]=2;
    return ans;
}
```
