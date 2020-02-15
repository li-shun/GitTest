### 问题：
「外观数列」是一个整数序列，从数字 1 开始，序列中的每一项都是对前一项的描述。前五项如下：
1.     1
2.     11
3.     21
4.     1211
5.     111221

1 被读作  "one 1"  ("一个一") , 即 11。
11 被读作 "two 1s" ("两个一"）, 即 21。
21 被读作 "one 2",  "one 1" （"一个二" ,  "一个一") , 即 1211。

给定一个正整数 n（1 ≤ n ≤ 30），输出外观数列的第 n 项。
### 思路：
用ahd表示前一项序列，用now（表示现在的序列）对ahd进行描述：从第一个字符到最后一个字符逐个描述。描述完后若now并不是第n项，将now更新为ahd，now清空，中服役上步骤。
### 解决：
```
char * countAndSay(int n){
    int m=1,count=1,k=0;//
    //char ahd[5000]={'1'},now[5000]={'\0'};
    char *ahd=(char *)calloc(5000,sizeof(char));
    char *now=(char *)calloc(5000,sizeof(char));
    ahd[0]='1';
    char list[4]={'0','1','2','3'};//表示有count个ahd[i]用list[count]。
    if(n==1)
        return ahd;
while(m!=n){
    if(m!=1){
        strcpy(ahd,now);
        for(int i=strlen(now);i<5000;i++)
            ahd[i]='\0';
        for(int i=0;i<5000;i++)
            now[i]='\0';}
    k=0;
    for(int i=0;i<strlen(ahd);i++){
        count=1;
        for(int j=i+1;j<strlen(ahd);j++){//向后找该字符ahd[i]有几个,记为count；
            if(ahd[j]==ahd[i])
                count++;
            else
                break;}
        now[k++]=list[count];
        now[k++]=ahd[i];
        i+=count-1;
    }
    m++;
}
return now;
}
```
