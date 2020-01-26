### 问题：<br>
给定一个字符串，请你找出其中不含有重复字符的『最长子串』的长度。
### 思路：<br>
从第一个字符开始，依次『判断』每个字符：<br>
如果该字符没有和之前出现过的字符重复，则将当前长度加一来并继续往后看；<br>
如果有重复，则记录当前长度作为子串长度，然后将下一个字符作为第一个字符，再依次向后进行上述判断。<br>
通过上述方法可以记录下所有的子串长度，从而得到最大长度。不断的循环判断过程，可以用递归来实现。
### 解决：
```
char a[250]={'\0'};
int len=0,num=0,length[200]={0},flag=0,start=0;
void recur_1(char * s,int i);
void recur_2(char *s,int i,int start,int len)
{
    if(i==strlen(s))
    {   length[num++]=len;
            return;}
    flag=0;
    for(int j=start;j<start+len;j++)
       if(s[i]==a[j])
        {   length[num++]=len;
            recur_1(s,i);
            flag=1;}
    if(flag==0)
        {a[i]=s[i];
        recur_2(s,++i,start,++len);}
}
void recur_1(char * s,int i)
{
    start=i;
    a[i]=s[i],len=1;
    recur_2(s,i+1,i,1);
}
int lengthOfLongestSubstring(char * s){
    recur_1(s,0);
    int ans=0;
    for(int i=0;i<num;i++)
        if(length[i]>ans)
            ans=length[i];
    return ans;
}
```
