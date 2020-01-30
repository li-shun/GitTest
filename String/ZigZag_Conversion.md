### 问题：
将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。
### 思路：
用含numRows式子表示每一行的s下标，用for循环一行一行输入ans中
### 解决：
```
char * convert(char * s, int numRows){
    int len=strlen(s),j=0,t=2*numRows-2;
    static char ans[1000]={'\0'};
    for(int i=0;i<1000;i++)
        ans[i]='\0';
    if(len==0||numRows==0)
        return ans;
    if(len==1||numRows==1||len<=numRows)
    {    strcpy(ans,s);
        return ans;}
    for(int i=0;i<len;i=i+t)
        ans[j++]=s[i];
    for(int r=2;r<=numRows-1;r++)
    {
        ans[j++]=s[r-1];
        for(int i=r-1+t-2*(r-1);i<len;)
        {
            ans[j++]=s[i];
            i=i+2*(r-1);
            if(i<len)
                ans[j++]=s[i];
            else
                break;
            i=i+t-2*(r-1);
        }
    }
    for(int i=numRows-1;i<len;i=i+t)
        ans[j++]=s[i];
    return ans;
}
```
