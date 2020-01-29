###问题：<dr>
给定两个整数，被除数 dividend 和除数 divisor。将两数相除，要求不使用乘法、除法和 mod 运算符。返回被除数除以除数所得到的商。<dr>
###分析：<dr>
使用while循环：dividend与divisor相减，每减一次，商便加一。但：<dr>
1. 如-2147483648与-1，转换为正数时，会出现int溢出问题，要用long long（双长型）,所以，还要注意强制类型转换的问题。<dr>
2.  如 2147483647与1，会超出时间限制，因此，我采取的做法是：<dr>
记录while循环次数，当循环次数增加到500时，将已经减去的数作为新的除数，当循环次数增加到600时，又将已经减去的数作为新的除数……用这种能方式大大缩短执行用时。并且能够根据所计算的数据范围适当调节“升级除数”的大小和次数。<dr>
###解决：<dr>
```
int divide(int dividend, int divisor){
    long long int qu=0,qu1=0,qu2=0,temp0=dividend,temp1=dividend,temp2=divisor,temp3=0,temp4=0;
    int f1=0,f2=0,times=0;
    if(temp1<0)
    {   temp1=-temp1; temp0=-temp0,f1=1;}
    if(temp2<0)
    {   temp2=-temp2; f2=1;}
    while(temp1>=temp2)
    {
        temp1-=temp2;
        qu++;
        qu1=qu;
        times++;
        if(times==500)
        {
            temp3=temp0-temp1;
            while(temp1>=temp3)
            {   temp1-=temp3;
                qu1+=qu;
                qu2=qu1;
                times++;
                if(times==600)
                {   
                    temp4=temp0-temp1;
                    while(temp1>=temp4)
                    {
                        temp1-=temp4;
                        qu2+=qu1;
                    }
                    qu1=qu2;
                }
            }
            qu=qu1;
        }
    }
    if(f1+f2==1)
        qu=-qu;
    if(qu<-2147483648||qu>2147483647)
        return 2147483647;
    return (int)qu;
}
```

