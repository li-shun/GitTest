### 问题：
有 N 个房间，开始时你位于 0 号房间。每个房间有不同的号码：0，1，2，...，N-1，并且房间里可能有一些钥匙能使你进入下一个房间。在形式上，对于每个房间 i 都有一个钥匙列表 rooms[i]，每个钥匙 rooms[i][j] 由 [0,1，...，N-1] 中的一个整数表示，其中 N = rooms.length。 钥匙 rooms[i][j] = v 可以打开编号为 v 的房间。(最初，除 0 号房间外的其余所有房间都被锁住。)
如果能进入每个房间返回 true，否则返回 false。
### 思路：
进入一个房间，如果这个房间里的钥匙对应的房间仍未被打开并进入过，则进入该房间。
（进入另一个房间后仍然进行上述判断）上述不断重复的动作可以用递归来实现。递归的终点则是所有我能进入的房间里的钥匙都被使用过了。
### 解决：
```
void play(int now,int *sta,int **rooms,int *roomsColSize)//now是我现在进入的房间号
{
    for(int i=0;i<roomsColSize[now];i++)
        if(sta[rooms[now][i]]==0)
        {    
            sta[rooms[now][i]]=1;
            play(rooms[now][i],sta,rooms,roomsColSize);
        }    
}
bool canVisitAllRooms(int** rooms, int roomsSize, int* roomsColSize){
    int sta[1000]={0};sta[0]=1;//sta[]用来记录每个房间的状态，1为进入过，0为不能进入
    play(0,sta,rooms,roomsColSize);
    for(int i=0;i<roomsSize;i++)
        if(sta[i]==0)
            return 0;
    return 1;
}
```
