### 问题：
在一条环路上有 N 个加油站，其中第 i 个加油站有汽油 gas[i] 升。你有一辆油箱容量无限的的汽车，从第 i 个加油站开往第 i+1 个加油站需要消耗汽油 cost[i] 升。你从其中的一个加油站出发，开始时油箱为空。
如果你可以绕环路行驶一周，则返回出发时加油站的编号，否则返回 -1。
说明：如果题目有解，该答案即为唯一答案。
### 思路：
我拥有的汽油为（加油站汽油-到下一个站消耗的汽油），判断：若该值为负，则不能继续行驶，排除答案；反之，行驶到下一站，我拥有的汽油量更新，再进行该判断。若上述上述过程能循环一周，即为答案。
### 解决：
```
int canCompleteCircuit(int* gas, int gasSize, int* cost, int costSize){
    for(int start=0;start<gasSize;start++)
        if(gas[start]>=cost[start])
        {
            int own=0,flag=0;
            for(int i=start;i<gasSize;i++)
            {
                own+=gas[i]-cost[i];
                if(own<0)
                {    flag=1;break;}
                if(i==gasSize-1)    i=-1;
                if(i==start-1)  break;
            }
            if(flag==0)
                return start;
        }
    return -1;
}
```

