### 问题：
比较version1和version2两个版本号。若version1 > version2,返回1；version1 < version2,返回-1；否则返回0。你可以假设版本号字符串是非空的，并且只包含数字和'.'字符。'.'不是小数点，而是代表着数字序列的分隔。例如，2.5不是“两个半”，也不是“还差一半到版本3”，而是第二版中的第五个小版本。你可以假设版本号每一级的默认修订号是0。例如，版本号3.4的第一级（大版本）和第二级（小版本）修订号分别为3和4。其第三级和第四级修订号均为0。
### 思路：
用两个数组(字符型)分别记录该两个版本号每一级的修订号，然后再从最高一级开始逐级比较两个版本号，则当出现不同时，修订号较大的那个版本号更大。
### 解决：
```
int compareVersion(char * version1, char * version2){
    char v1[20][4]={'\0'},v2[20][4]={'\0'};
    int m=0,k=0;
    for(int i=0;i<strlen(version1);i++)
    {
        if(version1[i]=='.')
        {   m++;
            k=0;
            continue;}
        if(version1[i]=='0'&&((i>0&&(version1[i-1]=='.'||version1[i-1]=='0'))||i==0))
            continue;
        else
            v1[m][k++]=version1[i];
    }
    m=k=0;
    for(int i=0;i<strlen(version2);i++)
    {
        if(version2[i]=='.')
        {   m++;
            k=0;
            continue;}
        if(version2[i]=='0'&&((i>0&&(version2[i-1]=='.'||version2[i-1]=='0'))||i==0))
            continue;
        else
            v2[m][k++]=version2[i];
    }
    for(int i=0;i<20;i++)
    {
        if(strlen(v1[i])>strlen(v2[i]))
            return 1;
        else if(strlen(v1[i])<strlen(v2[i]))
            return -1;
        else
            for(int j=0;j<strlen(v1[i]);j++)
            {
                if(v1[i][j]>v2[i][j])
                    return 1;
                else if(v1[i][j]<v2[i][j])
                    return -1;
            }
    }
    return 0;

}


```
