### 问题：
实现 int sqrt(int x) 函数。
计算并返回 x 的平方根，其中 x 是非负整数。
由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。
### 思路：
将公差为10的等差数列10，20，30，40，……作为估计数est，将x和其平方比较，若est^2<=x<(est+10)^2,则从est-est+10之间可以选出答案。这样可以快速确定答案位置。
### 解决：
```
int mySqrt(int x){
    if(x==0)    return 0;
    int ans=0,est=10;
    long long k=100;
    if(x<=k)
        for(int i=1;i<=10;i++)
            if(i*i&&(i+1)*(i+1)>x)
                return i;
    while(x>k){
        est+=10;
        k=(long long)est*est;
    }//est=90或k>=x;
    if(k==x)
        return est;
    est-=10;
    for(int i=est;i<=est+10;i++)
        if((long long)i*i<=x&&(long long)(i+1)*(i+1)>x)
            return i;
    return 0;
}
```
