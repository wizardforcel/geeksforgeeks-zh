# 矩阵中的最大路径总和

> 原文： [https://www.geeksforgeeks.org/maximum-path-sum-matrix/](https://www.geeksforgeeks.org/maximum-path-sum-matrix/)

给定一个`N * M`的矩阵。在矩阵中找到最大路径总和。 最大路径是从第一行到最后一行的所有元素的总和，在其中您只能向下或对角线向左或向右移动。 您可以从第一行中的任何元素开始。

**示例**：

```
Input : mat[][] = 10 10  2  0 20  4
                   1  0  0 30  2  5
                   0 10  4  0  2  0
                   1  0  2 20  0  4
Output : 74
The maximum sum path is 20-30-4-20.

Input : mat[][] = 1 2 3
                  9 8 7
                  4 5 6
Output : 17
The maximum sum path is 3-8-6.

```



给定一个`N * M`的矩阵。要首先找到最大路径和，我们必须在矩阵的第一行中找到最大值。 将此值存储在`res`中。 现在，对于矩阵中的每个元素，更新具有最大值的元素，该最大值可以包含在最大路径中。 如果该值比`res`更大，则更新`res`。 最后返回的`res`由最大路径总和值组成。

## C++ 

```cpp

// CPP prorgam for finding max path in matrix 
#include <bits/stdc++.h> 
#define N 4 
#define M 6 
using namespace std; 

// To calculate max path in matrix 
int findMaxPath(int mat[][M]) 
{ 

    for (int i = 1; i < N; i++) { 
        for (int j = 0; j < M; j++) { 

            // When all paths are possible 
            if (j > 0 && j < M - 1) 
                mat[i][j] += max(mat[i - 1][j], 
                             max(mat[i - 1][j - 1],  
                             mat[i - 1][j + 1])); 

            // When diagonal right is not possible 
            else if (j > 0) 
                mat[i][j] += max(mat[i - 1][j], 
                            mat[i - 1][j - 1]); 

            // When diagonal left is not possible 
            else if (j < M - 1) 
                mat[i][j] += max(mat[i - 1][j], 
                            mat[i - 1][j + 1]); 

            // Store max path sum 
        } 
    } 
    int res = 0; 
    for (int j = 0; j < M; j++)  
        res = max(mat[N-1][j], res); 
    return res; 
} 

// Driver program to check findMaxPath 
int main() 
{ 

    int mat1[N][M] = { { 10, 10, 2, 0, 20, 4 }, 
                    { 1, 0, 0, 30, 2, 5 }, 
                    { 0, 10, 4, 0, 2, 0 }, 
                    { 1, 0, 2, 20, 0, 4 } }; 

    cout << findMaxPath(mat1) << endl; 
    return 0; 
} 

```

## Java

```java

// Java prorgam for finding max path in matrix 

import static java.lang.Math.max; 

class GFG  
{ 
    public static int N = 4, M = 6; 

    // Function to calculate max path in matrix 
    static int findMaxPath(int mat[][]) 
    { 
        // To find max val in first row 
        int res = -1; 
        for (int i = 0; i < M; i++) 
            res = max(res, mat[0][i]); 

        for (int i = 1; i < N; i++)  
        { 
            res = -1; 
            for (int j = 0; j < M; j++)  
            { 
                // When all paths are possible 
                if (j > 0 && j < M - 1) 
                    mat[i][j] += max(mat[i - 1][j], 
                                 max(mat[i - 1][j - 1],  
                                    mat[i - 1][j + 1])); 

                // When diagonal right is not possible 
                else if (j > 0) 
                    mat[i][j] += max(mat[i - 1][j], 
                                    mat[i - 1][j - 1]); 

                // When diagonal left is not possible 
                else if (j < M - 1) 
                    mat[i][j] += max(mat[i - 1][j], 
                                mat[i - 1][j + 1]); 

                // Store max path sum 
                res = max(mat[i][j], res); 
            } 
        } 
        return res; 
    } 

    // driver program 
    public static void main (String[] args)  
    { 
        int mat[][] = { { 10, 10, 2, 0, 20, 4 }, 
                        { 1, 0, 0, 30, 2, 5 }, 
                        { 0, 10, 4, 0, 2, 0 }, 
                        { 1, 0, 2, 20, 0, 4 }  
                    }; 

        System.out.println(findMaxPath(mat)); 
    } 
} 

// Contributed by Pramod Kumar 

```

## Python 3

```py

# Python 3 prorgam for finding max path in matrix 
# To calculate max path in matrix 

def findMaxPath(mat): 

    # To find max val in first row 
    res = -1
    for i in range(M): 
        res = max(res, mat[0][i]) 

    for i in range(1, N): 

        res = -1
        for j in range(M): 

            # When all paths are possible 
            if (j > 0 and j < M - 1): 
                mat[i][j] += max(mat[i - 1][j], 
                                 max(mat[i - 1][j - 1],  
                                     mat[i - 1][j + 1])) 

            # When diagonal right is not possible 
            elif (j > 0): 
                mat[i][j] += max(mat[i - 1][j], 
                                 mat[i - 1][j - 1]) 

            # When diagonal left is not possible 
            elif (j < M - 1): 
                mat[i][j] += max(mat[i - 1][j], 
                                 mat[i - 1][j + 1]) 

            # Store max path sum 
            res = max(mat[i][j], res) 
    return res 

# Driver program to check findMaxPath 
N=4
M=6
mat = ([[ 10, 10, 2, 0, 20, 4 ], 
        [ 1, 0, 0, 30, 2, 5 ], 
        [ 0, 10, 4, 0, 2, 0 ], 
        [ 1, 0, 2, 20, 0, 4 ]]) 

print(findMaxPath(mat)) 

# This code is contributed by Azkia Anam. 

```

## C# 

```cs

// C# prorgam for finding 
// max path in matrix 
using System; 

class GFG  
{ 
    static int N = 4, M = 6; 

    // find the max element 
    static int max(int a, int b) 
    { 
        if(a > b) 
        return a; 
        else
        return b; 
    } 

    // Function to calculate 
    // max path in matrix 
    static int findMaxPath(int [,]mat) 
    { 
        // To find max val  
        // in first row 
        int res = -1; 
        for (int i = 0; i < M; i++) 
            res = max(res, mat[0, i]); 

        for (int i = 1; i < N; i++)  
        { 
            res = -1; 
            for (int j = 0; j < M; j++)  
            { 
                // When all paths are possible 
                if (j > 0 && j < M - 1) 
                    mat[i, j] += max(mat[i - 1, j], 
                                 max(mat[i - 1, j - 1],  
                                     mat[i - 1, j + 1])); 

                // When diagonal right 
                // is not possible 
                else if (j > 0) 
                    mat[i, j] += max(mat[i - 1, j], 
                                     mat[i - 1, j - 1]); 

                // When diagonal left  
                // is not possible 
                else if (j < M - 1) 
                    mat[i, j] += max(mat[i - 1, j], 
                                 mat[i - 1, j + 1]); 

                // Store max path sum 
                res = max(mat[i, j], res); 
            } 
        } 
        return res; 
    } 

    // Driver code 
    static public void Main (String[] args)  
    { 
        int[,] mat = {{10, 10, 2, 0, 20, 4}, 
                      {1, 0, 0, 30, 2, 5}, 
                      {0, 10, 4, 0, 2, 0}, 
                      {1, 0, 2, 20, 0, 4}}; 

        Console.WriteLine(findMaxPath(mat)); 
    } 
} 

// This code is contributed  
// by Arnab Kundu 

```

## PHP

```php

<?php 
// PHP prorgam for finding max 
// path in matrix  
$N = 4;  
$M = 6;  

// To calculate max path in matrix  
function findMaxPath($mat)  
{  
    global $N;  
    global $M; 
    for ($i = 1; $i < $N; $i++) 
    {  
        for ( $j = 0; $j < $M; $j++)  
        {  

            // When all paths are possible  
            if ($j > 0 && $j < ($M - 1))  
                $mat[$i][$j] += max($mat[$i - 1][$j],  
                                max($mat[$i - 1][$j - 1],  
                                    $mat[$i - 1][$j + 1]));  

            // When diagonal right is  
            // not possible  
            else if ($j > 0)  
                $mat[$i][$j] += max($mat[$i - 1][$j],  
                                    $mat[$i - 1][$j - 1]);  

            // When diagonal left is  
            // not possible  
            else if ($j < ($M - 1))  
                $mat[$i][$j] += max($mat[$i - 1][$j],  
                                    $mat[$i - 1][$j + 1]);  

            // Store max path sum  
        }  
    }  

    $res = 0;  
    for ($j = 0; $j < $M; $j++)  
        $res = max($mat[$N - 1][$j], $res);  
    return $res;  
}  

// Driver Code 
$mat1 = array( array( 10, 10, 2, 0, 20, 4 ),  
               array( 1, 0, 0, 30, 2, 5 ),  
               array( 0, 10, 4, 0, 2, 0 ),  
               array( 1, 0, 2, 20, 0, 4 ));  

echo findMaxPath($mat1),"\n";  

// This code is contributed by Sach_Code 
?> 

```

**输出**：

```
74

```

**时间复杂度**：`O(N * M)`。


