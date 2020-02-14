### 问题：
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
An input string is valid if:

    Open brackets must be closed by the same type of brackets.
    Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.
### 解决：
```
bool isValid(char * s){
    int flag=0,f=0;
    for(int i=0;i<strlen(s);i++)
        if(s[i]==')'||s[i]==']'||s[i]=='}'){
            f=i;
            break;
        }
    if(strlen(s)==0)
        return 1;
    if(f==0)
        return 0;
    for(int i=f;i<strlen(s);i++){
        
        if(s[i]==')'){
            int j=1;
            while(i-j>=0&&s[i-j]=='*')
                j++;
            if(i-j==-1)
                return 0;
            else if(s[i-j]=='('){
                s[i-j]=s[i]='*';
                }
            else
                return 0;}
        if(s[i]=='}'){
            int j=1;
            while(i-j>=0&&s[i-j]=='*')
                j++;
            if(i-j==-1)
                return 0;
            else if(s[i-j]=='{'){
                s[i-j]=s[i]='*';
                }
            else
                return 0;}
        if(s[i]==']'){
            int j=1;
            while(i-j>=0&&s[i-j]=='*')
                j++;
            if(i-j==-1)
                return 0;
            else if(s[i-j]=='['){
                s[i-j]=s[i]='*';
                }
            else
                return 0;}
    }
    for(int i=0;i<strlen(s);i++)
        if(s[i]!='*')
            return 0;
    return 1;
}
```
