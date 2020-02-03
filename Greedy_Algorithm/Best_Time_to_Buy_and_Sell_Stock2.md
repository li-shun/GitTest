### 问题：
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。
设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。
注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。
### 分析：
**该问题的关键**是：要证明在价格变化【极小1，极大1，极小2，极大2，…，极小n，极大n】（设pro【n】=极大n-极小n）过程中的最优解一定是pro【1】+pro【2】+…+pro【n】，而不会是极大j-极小i+极大m-极小n+…+极大x-极小x+…。易证。
### 解决：
```
int maxProfit(int * prices, int pricesSize){
    int ans=0;
    for(int i=0;i<pricesSize;i++)
        if(i+1<pricesSize&&prices[i]<prices[i+1])
        {
            int j=i+1;
            while(j<pricesSize&&prices[j]>prices[j-1])  j++;
            ans+=prices[j-1]-prices[i];
            i=j-1;
        }
    return ans;
}
```
