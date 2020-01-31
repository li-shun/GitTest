### 问题：
给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。
### 思路：
遍历整个数组，若该字符和needle第一个字符相同，则判断其后的strlen（needle）-1个字符是否和needle相同，若相同，即符合。但出现了**超出时间限制**的错误。(执行用例是“aaaaaaaaaaa…,aaaaaaaaaaa…b”用这种解法会大大延长循环时间和次数）改正：在判断每一个字符（hay[i]）和needle第一个字符的相同的同时判断hay[i+len-1]和needle最后一个字符是否相同。
### 注意：特殊情况的考虑：needle虽与hay同但却长于hay，或者说只考虑到hey【j】不越界而未考虑到还没有判断完整个needle。
### 解决：
```
int strStr(char * haystack, char * needle){
    int len=strlen(needle),k=0,flag=0;
    if(len==0)  return 0;
    if(strlen(haystack)<len)    return -1;
    for(int i=0;i<strlen(haystack);i++)
    {
        k=0;
        if(haystack[i]==needle[k++]&&(i+len-1)<strlen(haystack)&&needle[len-1]==haystack[i+len-1])
        {   flag=0;
             for(int j=i+1;j<strlen(haystack)&&j<i+len;j++)
                if(haystack[j]!=needle[k++]) 
                    flag=1;
            if(flag==0&&k==len)
                return i;
        }
    }
    return -1;
}
```
