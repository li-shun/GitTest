### 问题：
假设有打乱顺序的一群人站成一个队列。 每个人由一个整数对(h, k)表示，其中h是这个人的身高，k是排在这个人前面且身高大于或等于h的人数。 编写一个算法来重建这个队列。
总人数少于1100。
### 思路：
先把人们按身高从小到大排列，从大个开始排列位置，并且每个人对应的K+1就是他在前面已经先排了的人中要插入的位置号，插入前先把K后面的人位置号都+1。
### 解决：
```
int** reconstructQueue(int** people, int peopleSize, int* peopleColSize, int* returnSize, int** returnColumnSizes){
    int **ans=(int **)malloc(sizeof(int *)*peopleSize);
    *returnSize=peopleSize;
    *returnColumnSizes=peopleColSize;
    if(peopleSize==0)
        return ans;
    //先把人们按身高从小到大排序，同一身高不同k按k小在前排序。
    int* temp=NULL;
    for(int i=0;i<peopleSize-1;i++)
        for(int j=1;j<peopleSize-i;j++)
        {
            if(people[j][0]<people[j-1][0])
            {
               temp=people[j];
               people[j]=people[j-1];
               people[j-1]=temp;
            }
            if(people[j][0]==people[j-1][0])
                if(people[j][1]>people[j-1][1])
                {
                    temp=people[j];
                    people[j]=people[j-1];
                    people[j-1]=temp;
                } 
        }
    //开始排序
    int rank[1100]={0};//rank用来放置名次。
    rank[peopleSize-1]=1;
    //要将每个人的rank改为k+1，先将rank在k+1及以后的都+1；
    for(int i=peopleSize-2;i>=0;i--)
    {
        for(int j=peopleSize-1;j>i;j--)
            if(rank[j]>=people[i][1]+1)
                rank[j]+=1;
        rank[i]=people[i][1]+1;
    }//。
    //按名次将人输入到ans中；
    for(int j=1;j<=peopleSize;j++)//j作名次
        for(int i=0;i<peopleSize;i++)
            if(rank[i]==j)
            {   *(ans+j-1)=*(people+i);
                break;}
    return ans;
    
}
```

