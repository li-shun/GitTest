### 问题：
给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。给出数字到字母的映射与电话按键相同。注意 1 不对应任何字母。
### 思路：
digits中的每一位数都与字母组合中的一位字母相对应；所以我依次给所有字母组合中第的di（0<di<组合长度-1）个位置同时确定字母，每确定一个字母位置时，都找出与该位置对应的数所关联的3/4个字母，并且根据一定规律确定不同组合该位置为哪个字母。规律的寻找：排列组合树状图中每一列（位）中（该3/4个字母)排列规律。
### 解决（终端上正确，力扣上出现执行错误）：
```
char ** letterCombinations(char * digits, int* returnSize){
    int left=0,n=strlen(digits),right=n-1,nn;//n为每个答案位数,nn为答案个数，left为对应3个字母的数字个数，right为对应4个字母的数字组合
    char ** df;char ** ans;//digits中的每位数都对应3/4个字母，而答案中的每种字母组合中的每一位都与digits中的一位数对应。df用来建立字母组合的每一位和该位置上可能出现的3/4个字母的对应关系。
    df=(char **)malloc(sizeof(char *)*n);
    for(int i=0;i<n;i++)
        df[i]=(char *)malloc(sizeof(char)*6);
    char trs[8][6]={"2abc","3def","4ghi","5jkl","6mno","8tuv","7pqrs","9wxyz"};
    for(int i=0;i<n;i++)
        for(int j=0;j<8;j++)
            if(digits[i]==trs[j][0])
            {
                if(j<=5)
                    strcpy(df[left++],trs[j]);
                else
                    strcpy(df[right--],trs[j]);
            }
    int k=0;
    nn=pow(3,left)*pow(4,(n-left));
    ans=(char **)malloc(sizeof(char *)*nn);
    for(int i=0;i<nn;i++)
        ans[i]=(char *)malloc(sizeof(char)*n);
    for(int di=0;di<left;di++)//每个答案的0到left-1位
    {
        int intv=nn/pow(3,di+1);
        for(int i=0;i<nn;i++)//赋df[di][1]给ans[][di]
        {
            ans[i][di]=df[di][1];k++;
            if(k==intv)
            {   i=i+2*k;k=0;}
        }k=0;
        for(int i=intv;i<nn;i++)
        {
            ans[i][di]=df[di][2];k++;
            if(k==intv)
            {   i=i+2*k;k=0;}
        }k=0;
        for(int i=intv*2;i<nn;i++)
        {
            ans[i][di]=df[di][3];k++;
            if(k==intv)
            {   i=i+2*k;k=0;}
        }k=0;
    }
   for(int di=left;di<n;di++)//每个答案的left到n-1位
    {
        int intv=nn/(pow(3,left)*pow(4,di+1-left));
         for(int i=0;i<nn;i++)//赋df[di][1]给ans[][di]
        {
            ans[i][di]=df[di][1];k++;
            if(k==intv)
            {   i=i+3*k;k=0;}
        }k=0;
        for(int i=intv;i<nn;i++)
        {
            ans[i][di]=df[di][2];k++;
            if(k==intv)
            {   i=i+3*k;k=0;}
        }k=0;
        for(int i=intv*2;i<nn;i++)
        {
            ans[i][di]=df[di][3];k++;
            if(k==intv)
            {   i=i+3*k;k=0;}
        }k=0;
        for(int i=intv*3;i<nn;i++)
        {
            ans[i][di]=df[di][4];k++;
            if(k==intv)
            {   i=i+3*k;k=0;}
        }
    }
    *returnSize=nn;
    return ans;
}
```
