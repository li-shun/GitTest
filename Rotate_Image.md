### 问题：
给定一个 n × n 的二维矩阵表示一个图像。将图像顺时针旋转 90 度。
说明：
你必须在原地旋转图像，这意味着你需要直接修改输入的二维矩阵。请不要使用另一个矩阵来旋转图像。
### 思路：
从矩形的中心开始由内而外，将边长为1，3，…,n(奇数)或2,4,…,n(偶数)的正方形进行旋转，旋转方法如下：将上边暂移到一个数组中储存，再依次将左边移到上边，下边移到左边，右边移到下边，最后将数组中储存的原上边移到右边。
### 解决：
```
void rotate(int** matrix, int matrixSize, int* matrixColSize){
    
    int *arr=(int *)calloc(50,sizeof(int));
    int n=*matrixColSize,b=0,f=0;//b为边长，f为每“层”矩形左上角的坐标[f][f]。
    if(n%2!=0)
    {   f=n/2,b=1;}
    if(n%2==0)
    {   f=n/2-1,b=2;}
    while(b!=n+2)
    {
        if(b==1)
        {   b+=2;
            f--;
            continue;}                                     
        for(int i=0;i<b-1;i++)
            arr[i]=matrix[f][f+i];
        for(int i=0;i<b-1;i++)                  
            matrix[f][f+i]=matrix[f+b-1-i][f];
        for(int i=0;i<b-1;i++)
            matrix[f+b-1-i][f]=matrix[f+b-1][f+b-1-i];
        for(int i=0;i<b-1;i++)
            matrix[f+b-1][f+b-1-i]=matrix[f+i][f+b-1];
        for(int i=0;i<b-1;i++)
            matrix[f+i][f+b-1]=arr[i];
        b+=2;
        f--;
    }
    return;
}
```
