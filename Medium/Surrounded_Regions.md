### 问题：
给一个包含“X”和“O”的二维矩阵，找到所有被“X”包围的区域,并将这些区域里的“O”用“X”填充。
### 思路：
任何与边界上的'O'相连的'O',都一定不符合条件，任何与不符合条件的'O'相连的'O',也都一定不符合条件。将不符合条件的'O'记为' * ';每找到一个' * ',都将遍历其四周，将与其相邻的'O'记为' * '。最终，剩余的'O'则为符合条件的'o'。
### 解决：
```
void find(char** board,int row,int col,int a,int b)
{
    if(a-1>=0&&board[a-1][b]=='O')
    {   board[a-1][b]='*';
        find(board,row,col,a-1,b);}
    if(a+1<row&&board[a+1][b]=='O')
    {   board[a+1][b]='*';
        find(board,row,col,a+1,b);}
    if(b-1>=0&&board[a][b-1]=='O')
    {   board[a][b-1]='*';
        find(board,row,col,a,b-1);}
    if(b+1<col&&board[a][b+1]=='O')
    {   board[a][b+1]='*';
        find(board,row,col,a,b+1);}
}
void solve(char** board, int boardSize, int* boardColSize){
    if(boardSize<=2||boardColSize[0]<=2)
        return;
    int row=boardSize,col=boardColSize[0];
    //任何与边界上的'O'相连的'O',都一定不符合条件，任何与不符合条件的'O'相连的'O',也都一定不符合条件。将不符合条件的'O'记为'*';
    for(int j=0;j<col;j++)
    {
        if(board[0][j]=='O')
        {   board[0][j]='*';
            find(board,row,col,0,j);}
        if(board[row-1][j]=='O')
        {   board[row-1][j]='*';
            find(board,row,col,row-1,j);}
    }
    for(int i=1;i<row-1;i++)
    {
        if(board[i][0]=='O')
        {   board[i][0]='*';
            find(board,row,col,i,0);}
        if(board[i][col-1]=='O')
        {   board[i][col-1]='*';
            find(board,row,col,i,col-1);}
    }
    for(int i=0;i<row;i++)
        for(int j=0;j<col;j++)
        {
            if(board[i][j]=='*')
                board[i][j]='O';
            else if(board[i][j]=='O')
                board[i][j]='X';
        }
}
``` 
