###问题：<br>
判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。
###思路：<br>
依次比较该数对称数位上的数字是否相等。
###解决：
```
int *fun(int x)  //这个函数用于返回一个存放x各个数位上的数的整型数组。
{
        int i=0;
        static int di[10]={0};
        while(i<10)
        {di[i]=x%10;x/=10;i++;}
        return di;
}
bool isPalindrome(int x){
    if(x<0)
        return false;
    else if(0<=x&&x<10)
        return true;          //负数非回文数，0-9为回文数；
    else
    {
        int i=0,j=0;
        for(int k=9;k>=0;k--)
            if(fun(x)[k]!=0)  { j=k;break;}
        while(i<j)
            if(fun(x)[i++]!=fun(x)[j--])
                return false;
        return true;    
    }
}
```
