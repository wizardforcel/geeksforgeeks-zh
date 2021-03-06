# 在矩阵中打印具有相同矩形和的单元格

> 原文： [https://www.geeksforgeeks.org/print-cells-rectangular-sum-matrix/](https://www.geeksforgeeks.org/print-cells-rectangular-sum-matrix/)

给定一个`m x n`矩阵的矩阵，我们需要打印所有子矩阵，这些子矩阵的总和在此单元结束，并且子矩阵从该单元开始等于其余元素。 为了更好地理解，请参见下图，

**示例**：

```
Input : mat[][] = {1, 2, 3, 5,
                   4, 1, 0, 2,
                   0, 1, 2, 0,
                   7, 1, 1, 0};
Output : (1, 1), (2, 2)      

In above matrix, cell (1, 1) and cell (2, 2)
are our required cells because,
For cell (1, 1), sum of red and green areas is same
1+2+4+1+0+2+1+2+0+1+1+0 = 3+5+0+7        
Same is true for cell (2, 2)
1+2+3+4+1+0+0+1+2+0+1+0 = 5+2+7+1    

We need to print all blue boundary cells for 
which sum of <font color="Red">red</font> area is equal to <font color="Green">green</font> area.

```



首先，我们[构造类似于链接文章的辅助子矩阵](https://www.geeksforgeeks.org/submatrix-sum-queries/)。

我们构造两个矩阵`sum[][]`和`sumr[][]`，使得`sum[i][j]`表示从`mat[0][0]`到`mat[i][j]`。 用于存储总和直到最后一个索引的求和器，即`sumr[i][j]`表示子矩阵`mat[i][j]`与`mat[m – 1][n – 1]`的总和。

现在我们可以使用上述矩阵来解决此问题，可以通过将求和矩阵与求和矩阵相加相应的单元格来计算上图中的红色区域，因为在计算此和时要考虑两次`mat[i][j]`减去一次即可得到红色区域的总和。 获取剩余元素的总和（绿色部分）非常容易，我们将从给定矩阵的总和中减去红色部分的总和。

因此，要检查特定单元格是否满足给定条件，我们将如上所述计算红色部分的总和，并将其与矩阵的总和进行比较，如果该总和为矩阵总和的一半，则当前单元格满足条件，因此是结果的候选。

## C/C++ 

```

// C++ program to print cells with same rectangular 
// sum diagonally 
#include <bits/stdc++.h> 
using namespace std; 
#define R 4 
#define C 4 

// Method prints cell index at which rectangular sum is 
// same at prime diagonal and other diagonal 
void printCellWithSameRectangularArea(int mat[R][C], 
                                     int m, int n) 
{ 
    /* sum[i][j] denotes sum of sub-matrix, mat[0][0] 
       to mat[i][j] 
       sumr[i][j] denotes sum of sub-matrix, mat[i][j] 
       to mat[m - 1][n - 1]  */
    int sum[m][n], sumr[m][n]; 

    //  Initialize both sum matrices by mat 
    int totalSum = 0; 
    for (int i = 0; i < m; i++) 
    { 
        for (int j = 0; j < n; j++) 
        { 
            sumr[i][j] = sum[i][j] = mat[i][j]; 
            totalSum += mat[i][j]; 
        } 
    } 

    //  updating first and last row separately 
    for (int i = 1; i < m; i++) 
    { 
        sum[i][0] += sum[i-1][0]; 
        sumr[m-i-1][n-1] += sumr[m-i][n-1]; 
    } 

    //  updating first and last column separately 
    for (int j = 1; j < n; j++) 
    { 
        sum[0][j] += sum[0][j-1]; 
        sumr[m-1][n-j-1] += sumr[m-1][n-j]; 
    } 

    //  updating sum and sumr indices by nearby indices 
    for (int i = 1; i < m; i++) 
    { 
        for (int j = 1; j < n; j++) 
        { 
            sum[i][j] += sum[i-1][j] + sum[i][j-1] - 
                                      sum[i-1][j-1]; 
            sumr[m-i-1][n-j-1] += sumr[m-i][n-j-1] + 
                                  sumr[m-i-1][n-j] - 
                                  sumr[m-i][n-j]; 
        } 
    } 

    //  Uncomment below code to print sum and reverse sum 
    // matrix 
    /* 
        for (int i = 0; i < m; i++) 
        { 
            for (int j = 0; j < n; j++) 
            { 
                cout << sum[i][j] << " "; 
            } 
            cout << endl; 
        } 
        cout << endl; 
        for (int i = 0; i < m; i++) 
        { 
            for (int j = 0; j < n; j++) 
            { 
                cout << sumr[i][j] << " "; 
            } 
            cout << endl; 
        } 
        cout << endl;    */

    /* print all those indices at which sum of prime diagonal 
       rectangles is half of the total sum of matrix  */
    for (int i = 0; i < m; i++) 
    { 
        for (int j = 0; j < n; j++) 
        { 
            int mainDiagRectangleSum = sum[i][j] + sumr[i][j] - 
                                                   mat[i][j]; 
            if (totalSum == 2 * mainDiagRectangleSum) 
                cout << "(" << i << ", " << j << ")" << endl; 
        } 
    } 
} 

//  Driver code to test above methods 
int main() 
{ 
    int mat[R][C] = 
    { 
        1, 2, 3, 5, 
        4, 1, 0, 2, 
        0, 1, 2, 0, 
        7, 1, 1, 0 
    }; 

    printCellWithSameRectangularArea(mat, R, C); 

    return 0; 
} 

```

## Java

```java

// Java program to print cells with  
// same rectangular sum diagonally 

class GFG { 

static final int R = 4; 
static final int C = 4; 

// Method prints cell index at which  
// rectangular sum is same at  
// prime diagonal and other diagonal 
static void printCellWithSameRectangularArea(int mat[][],  
                                             int m, int n)  
{ 
    /* sum[i][j] denotes sum of sub-matrix, mat[0][0] 
    to mat[i][j] 
    sumr[i][j] denotes sum of sub-matrix, mat[i][j] 
    to mat[m - 1][n - 1] */
    int sum[][] = new int[m][n]; 
    int sumr[][] = new int[m][n]; 

    // Initialize both sum matrices by mat 
    int totalSum = 0; 
    for (int i = 0; i < m; i++) { 
    for (int j = 0; j < n; j++) { 
        sumr[i][j] = sum[i][j] = mat[i][j]; 
        totalSum += mat[i][j]; 
    } 
    } 

    // updating first and last row separately 
    for (int i = 1; i < m; i++) { 
    sum[i][0] += sum[i - 1][0]; 
    sumr[m - i - 1][n - 1] += sumr[m - i][n - 1]; 
    } 

    // updating first and last column separately 
    for (int j = 1; j < n; j++) { 
    sum[0][j] += sum[0][j - 1]; 
    sumr[m - 1][n - j - 1] += sumr[m - 1][n - j]; 
    } 

    // updating sum and sumr indices by nearby indices 
    for (int i = 1; i < m; i++) { 
    for (int j = 1; j < n; j++) { 
        sum[i][j] += sum[i - 1][j] + sum[i][j - 1] -  
                                     sum[i - 1][j - 1]; 
        sumr[m - i - 1][n - j - 1] += sumr[m - i][n - j - 1] + 
                                      sumr[m - i - 1][n - j] - 
                                      sumr[m - i][n - j]; 
    } 
    } 

    // Uncomment below code to print sum and reverse sum 
    // matrix 
    /* 
        for (int i = 0; i < m; i++) 
        { 
            for (int j = 0; j < n; j++) 
            { 
                System.out.print( sum[i][j] + " "); 
            } 
            System.out.println(); 
        } 
        System.out.println(); 
        for (int i = 0; i < m; i++) 
        { 
            for (int j = 0; j < n; j++) 
            { 
                System.out.print(sumr[i][j] + " "); 
            } 
            System.out.println(); 
        } 
        System.out.println(); */

    /* print all those indices at which sum of prime diagonal 
    rectangles is half of the total sum of matrix */
    for (int i = 0; i < m; i++) { 
    for (int j = 0; j < n; j++) { 
        int mainDiagRectangleSum = sum[i][j] +  
                       sumr[i][j] - mat[i][j]; 
        if (totalSum == 2 * mainDiagRectangleSum) 
        System.out.println("(" + i + ", " + j + ")"); 
    } 
    } 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int mat[][] = {{1, 2, 3, 5}, 
                   {4, 1, 0, 2},  
                   {0, 1, 2, 0},  
                   {7, 1, 1, 0}}; 

    printCellWithSameRectangularArea(mat, R, C); 
} 
} 

// This code is contributed by Anant Agarwal. 

```

## Python

```py

# Python program to print cells with same rectangular 
# sum diagonally 
# R 4 
# C 4 

# Method prints cell index at which rectangular sum is 
# same at prime diagonal and other diagonal 
def printCellWithSameRectangularArea(mat, m, n): 
    # sum[i][j] denotes sum of sub-matrix, mat[0][0] 
    #  to mat[i][j] 
    # sumr[i][j] denotes sum of sub-matrix, mat[i][j] 
    # to mat[m - 1][n - 1]   
    sum = [[0 for i in range(m)]for j in range(n)] 
    sumr = [[0 for i in range(m)]for j in range(n)] 

    #  Initialize both sum matrices by mat 
    totalSum = 0
    for i in range(m): 
        for j in range(n): 
            sumr[i][j] = sum[i][j] = mat[i][j]; 
            totalSum += mat[i][j] 

    #  updating first and last row separately 
    for i in range(1,m): 
        sum[i][0] += sum[i-1][0] 
        sumr[m-i-1][n-1] += sumr[m-i][n-1] 

    #  updating first and last column separately 
    for j in range(1,n): 
        sum[0][j] += sum[0][j-1]; 
        sumr[m-1][n-j-1] += sumr[m-1][n-j] 

    #  updating sum and sumr indices by nearby indices 
    for i in range(1,m): 
        for j in range(1,n): 
            sum[i][j] += sum[i-1][j] + sum[i][j-1] - sum[i-1][j-1] 
            sumr[m-i-1][n-j-1] += sumr[m-i][n-j-1] + sumr[m-i-1][n-j] - sumr[m-i][n-j] 

    #  Uncomment below code to print sum and reverse sum 
    # matrix 

    # print all those indices at which sum of prime diagonal 
    #   rectangles is half of the total sum of matrix   
    for i in range(m): 
        for j in range(n): 
            mainDiagRectangleSum = sum[i][j] + sumr[i][j] - mat[i][j] 
            if (totalSum == 2 * mainDiagRectangleSum): 
                print "(", 
                print i, 
                print ",", 
                print j, 
                print ")", 

#  Driver code to test above methods 
mat =[[1, 2, 3, 5,], 
     [4, 1, 0, 2,], 
     [0, 1, 2, 0], 
     [7, 1, 1, 0]] 
printCellWithSameRectangularArea(mat, 4, 4) 

# Contributed by Afzal 

```

## C# 

```cs

// C# program to print cells with  
// same rectangular sum diagonally 
using System; 

class GFG { 

static int R = 4; 
static int C = 4; 

// Method prints cell index at which  
// rectangular sum is same at  
// prime diagonal and other diagonal 
static void printCellWithSameRectangularArea(int [,]mat,  
                                             int m, int n)  
{ 
    /* sum[i][j] denotes sum of sub- 
       matrix, mat[0][0] to mat[i][j] 
       sumr[i][j] denotes sum of sub-matrix, 
       mat[i][j] to mat[m - 1][n - 1] */
    int [,]sum = new int[m, n]; 
    int [,]sumr = new int[m, n]; 

    // Initialize both sum matrices by mat 
    int totalSum = 0; 
    for (int i = 0; i < m; i++) { 
    for (int j = 0; j < n; j++) { 
        sumr[i, j] = sum[i, j] = mat[i, j]; 
        totalSum += mat[i, j]; 
    } 
    } 

    // updating first and last row separately 
    for (int i = 1; i < m; i++) 
    { 
    sum[i, 0] += sum[i - 1, 0]; 
    sumr[m - i - 1, n - 1] += sumr[m - i, n - 1]; 
    } 

    // updating first and last column separately 
    for (int j = 1; j < n; j++)  
    { 
    sum[0,j] += sum[0,j - 1]; 
    sumr[m - 1,n - j - 1] += sumr[m - 1,n - j]; 
    } 

    // updating sum and sumr indices by nearby indices 
    for (int i = 1; i < m; i++) { 
    for (int j = 1; j < n; j++) { 
        sum[i,j] += sum[i - 1,j] + sum[i,j - 1] -  
                                   sum[i - 1,j - 1]; 
        sumr[m - i - 1,n - j - 1] += sumr[m - i,n - j - 1] + 
                                     sumr[m - i - 1,n - j] - 
                                     sumr[m - i,n - j]; 
    } 
    } 

    // Uncomment below code to print sum and reverse sum 
    // matrix 
    /* 
        for (int i = 0; i < m; i++) 
        { 
            for (int j = 0; j < n; j++) 
            { 
                System.out.print( sum[i][j] + " "); 
            } 
            System.out.println(); 
        } 
        System.out.println(); 
        for (int i = 0; i < m; i++) 
        { 
            for (int j = 0; j < n; j++) 
            { 
                System.out.print(sumr[i][j] + " "); 
            } 
            System.out.println(); 
        } 
        System.out.println(); */

    /* print all those indices at which sum 
       of prime diagonal rectangles is half  
       of the total sum of matrix */
    for (int i = 0; i < m; i++) { 
    for (int j = 0; j < n; j++) { 
        int mainDiagRectangleSum = sum[i,j] +  
                    sumr[i,j] - mat[i,j]; 

        if (totalSum == 2 * mainDiagRectangleSum) 
        Console.WriteLine("(" + i + ", " + j + ")"); 
    } 
    } 
} 

// Driver code 
public static void Main() 
{ 
    int [,]mat = {{1, 2, 3, 5}, 
                  {4, 1, 0, 2},  
                  {0, 1, 2, 0},  
                  {7, 1, 1, 0}}; 

    printCellWithSameRectangularArea(mat, R, C); 
} 
} 

// This code is contributed by vt_m. 

```

Output:

```
(1, 1)
(2, 2)

```



