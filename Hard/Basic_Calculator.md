### 问题：
实现一个简单计算器来计算一个简单的字符串表达式。这个字符串表达式可以包含左括号‘（’，右括号‘）’，加号‘+’和减号‘-’，非负整数以及空格‘ ’。
### 思路：
1、先去括号：从内层括号到外层括号，依次判断括号前是否为负号，是则将括号内的符号变号。
2、从左到右依次计算：用oper记录加减号，每遇+、-号即更新。遇到数字则根据当前符号进行运算。
### 解决：
```
int calculate(char * s){
//先去括号:从内层括号依次到外层括号。
int len=strlen(s),j=1;;
for(int i=0;i<len;i++)
{
    if(s[i]==')')
    {
        j=1;
        while(s[i-j]!='(')
            j++;
        if(i-j-1>=0&&s[i-j-1]=='-')
            for(int k=i-j+1;k<i;k++)
            {   if(s[k]=='+')
                    s[k]='-';
                else if(s[k]=='-')
                    s[k]='+';}
        s[i-j]=s[i]=' ';
    }
}
//计算
int ans=0,di=1,digit;
char oper='+';
for(int i=0;i<len;i++)
{
    if(s[i]==' ')
        continue;
    else if(s[i]=='+'||s[i]=='-')
    {   oper=s[i];
        continue;}
    else 
    {
        di=1;
        while(i+di<len&&'0'<=s[i+di]&&s[i+di]<='9')
            di++;
        digit=di;
        
        if(oper=='+')
            for(int j=i;j<i+digit;j++)
                ans+=((int)s[j]-48)*pow(10,--di);
        else
            for(int j=i;j<i+digit;j++)
                ans-=((int)s[j]-48)*pow(10,--di);
        i=i+digit-1;
    }
}
return ans;
}
```
