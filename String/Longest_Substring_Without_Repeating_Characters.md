### 问题：<br>
给定一个字符串，请你找出其中不含有重复字符的『最长子串』的长度。
### 思路：<br>
（大循环）从第一个字符开始，依次『判断』每个字符：<br>
（小循环）1、如果该字符没有和当前子串已出现过的字符重复，则将子串当前长度加一并继续往后看；<br>
          2、如果有重复，则记录当前长度作为子串长度，然后将下一个字符作为第一个字符，再依次向后进行上述判断。<br>
通过上述方法可以记录下所有的子串长度，从而得到最大长度。不断的循环判断过程，可以用递归来实现。
### 解决：
```
char a[250]={'\0'};  //a用来存放“已出现的字符”。
int len=0,num=0,length[200]={0},flag=0,start=0;  //len记录子串当前长度，num为子串个数，length记录所有的子串长度，start用来记录当前子串的开头。
void recur_1(char * s,int i);
void recur_2(char *s,int i,int start,int len) //小循环
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
void recur_1(char * s,int i)  //大循环
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
### 结果分析：
   执行错误：使用了全局变量，同一个测试用例，执行代码与提交代码的结果不同，执行代码结果正确。
