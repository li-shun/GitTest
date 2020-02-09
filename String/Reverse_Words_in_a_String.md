### 问题：
给定一个字符串，逐个翻转字符串中的每个单词。
### 思路：
从所给字符串的最后一个字符开始寻找单词；再将单词从后往前依次“复制”给ans；
### 解决：
```
char * reverseWords(char * s){
    int len=strlen(s),p=0,i=len-1,j=0;//p记录ans中单词的位置
    static char ans[55000];
    for(int i=0;i<55000;i++)
        ans[i]='\0';
    if(len==0)
        return ans;//字符型数组ans用于存储翻转后的单词串
    while(1)
    {
        //找一个单词,从非空格字符开始，遇到空格结束。
        while(i>=0&&s[i]==' ')
            i--;
        if(i<0)
        {   if(p>0)
                ans[p-1]='\0';
            return ans;//之前有0++个空格，现在是“s[-1]”;
        }
        j=1;
        while(i-j>=0&&s[i-j]!=' ')
            j++;
        if(i-j<0)
        {
            for(int k=0;k<=i;k++)
                ans[p++]=s[k];
            return ans;
        }
        //由上，s[i-j+1]-s[i]为一个单词；
        for(int k=i-j+1;k<=i;k++)
            ans[p++]=s[k];
        ans[p++]=' ';//将单词+' '传给ans
        i=i-j-1;
    }
    ans[p-1]='\0';
    return ans;
}
```
