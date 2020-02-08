### 问题：
在显示着数字的坏计算器上，我们可以执行以下两种操作：
    双倍（Double）：将显示屏上的数字乘 2；
    递减（Decrement）：将显示屏上的数字减 1 。
最初，计算器显示数字 X。返回显示数字 Y 所需的最小操作数。
###思路：
逆向思维；由Y到X；
###解决：
```
int brokenCalc(int X, int Y){
    int step=0; 
    if(Y>=0&&Y<X||X==Y)//大正-》小正/0
        return X-Y;
    if(X>=0&&Y<0)//正/0-》负：先变为负-》负；
    {    step+=X+1;X=-1;}
    if(X<0&&Y<X)//负-》负；
    {
        while((double)Y/4<X)
        {
            if(Y%2!=0)
            {   Y+=1;step++;}
            Y/=2;step++;
        }
        Y/=2;step++;//现在Y<X且Y/2>=X;
        return step+(X-Y);
    }
    //其余情况只有：小正/0-》大正；
    if(X==0)
    {   step++;X=1;}
    while((double)Y/2>X)
    {   
        if(Y%2!=0)
        {   Y+=1;step++;}
        Y/=2;step++;
    }//现在Y>X且Y/2<=X;
    Y/=2;step++;
    return step+(X-Y);
}
```
