# 矩阵的标量乘法的程序

> 原文： [https://www.geeksforgeeks.org/program-for-scalar-multiplication-of-a-matrix/](https://www.geeksforgeeks.org/program-for-scalar-multiplication-of-a-matrix/)

给定一个矩阵和一个标量元素`k`，我们的任务是找出该矩阵的标量积。

**示例**：

```
Input : mat[][] = {{2, 3}
                   {5, 4}}
        k = 5
Output : 10 15 
         25 20 
We multiply 5 with every element.

Input : 1 2 3 
        4 5 6
        7 8 9
        k = 4
Output :  4 8  12
          16 20 24
          28 32 36 

```



数为`k`（标量）的**标量乘法**，将其乘以矩阵中的每个条目。 矩阵`A`为矩阵`kA`。

## C++ 

```cpp

// C++ program to find the scalar product  
// of a matrix 
#include <bits/stdc++.h> 
using namespace std; 

// Size of given matrix 
#define N 3 

void scalarProductMat(int mat[][N], int k) 
{ 
    // scalar element is multiplied by the matrix 
    for (int i = 0; i < N; i++)  
        for (int j = 0; j < N; j++)  
            mat[i][j] = mat[i][j] * k;         
} 

// Driver code 
int main() 
{ 
    int mat[N][N] = { { 1, 2, 3 }, 
                      { 4, 5, 6 }, 
                      { 7, 8, 9 } }; 
    int k = 4; 

    scalarProductMat(mat, k); 

    // to display the resultant matrix 
    printf("Scalar Product Matrix is : \n"); 
    for (int i = 0; i < N; i++) { 
        for (int j = 0; j < N; j++)  
            printf("%d ", mat[i][j]); 
        printf("\n"); 
    } 

    return 0; 
} 

```

## Java

```java

// Java program to find 
// the scalar product  
// of a matrix 
import java.io.*; 

class GFG { 

static final int N = 3; 
static void scalarProductMat(int mat[][],  
                                  int k) 
{ 

    // scalar element is multiplied 
    // by the matrix 
    for (int i = 0; i < N; i++)  
        for (int j = 0; j < N; j++)  
            mat[i][j] = mat[i][j] * k;  
} 

// Driver code 
public static void main (String[] args) 
{ 
    int mat[][] = { { 1, 2, 3 }, 
                    { 4, 5, 6 }, 
                    { 7, 8, 9 } }; 
    int k = 4; 

    scalarProductMat(mat, k); 

    // to display the resultant matrix 
    System.out.println("Scalar Product Matrix is : "); 

    for (int i = 0; i < N; i++) 
    { 
        for (int j = 0; j < N; j++)  
            System.out.print(mat[i][j] + " "); 
        System.out.println(); 
    } 
} 
} 

// This code is contributed by Ajit. 

```

## Python 3

```py

# Python 3 program to find the scalar  
# product of a matrix 

# Size of given matrix 
N = 3

def scalarProductMat( mat, k): 

    # scalar element is multiplied  
    # by the matrix 
    for i in range( N): 
        for j in range( N):  
            mat[i][j] = mat[i][j] * k      

# Driver code 
if __name__ == "__main__": 

    mat = [[ 1, 2, 3 ], 
           [ 4, 5, 6 ], 
           [ 7, 8, 9 ]] 
    k = 4

    scalarProductMat(mat, k) 

    # to display the resultant matrix 
    print("Scalar Product Matrix is : ") 
    for i in range(N): 
        for j in range(N): 
            print(mat[i][j], end = " ") 
        print() 

# This code is contributed by ita_c 

```

## C# 

```cs

// C# program to find 
// the scalar product  
// of a matrix 
using System; 

class GFG{ 

static int N = 3; 
static void scalarProductMat(int[,] mat,  
                                  int k) 
{ 

    // scalar element is multiplied  
    // by the matrix 
    for (int i = 0; i < N; i++)  
        for (int j = 0; j < N; j++)  
            mat[i,j] = mat[i, j] * k;      
} 

// Driver code 
static public void Main () 
{ 
    int[,] mat = {{1, 2, 3}, 
                  {4, 5, 6}, 
                  {7, 8, 9}}; 
    int k = 4; 

    scalarProductMat(mat, k); 

    // to display the resultant matrix 
    Console.WriteLine("Scalar Product Matrix is : "); 

    for (int i = 0; i < N; i++) { 
        for (int j = 0; j < N; j++)  
            Console.Write(mat[i, j] + " "); 
        Console.WriteLine(); 
    } 
} 
} 

// This code is contributed by Ajit. 

```

## PHP

```php

<?php 
// PHP program to find 
// the scalar product  
// of a matrix 

function scalarProductMat($mat,  
                          $k) 
{ 
    $N = 3; 

    // scalar element is multiplied 
    // by the matrix 
    for ( $i = 0; $i < $N; $i++)  
        for ($j = 0; $j < $N; $j++)  
            $mat[$i][$j] = $mat[$i][$j] * $k;  

    return $mat; 
} 

// Driver code 
$N = 3; 
$mat = array(array(1, 2, 3 ), 
             array( 4, 5, 6 ), 
             array(7, 8, 9 )); 
$k = 4; 

$mat1 = scalarProductMat($mat, $k); 

// to display the resultant matrix 
echo("Scalar Product Matrix is : " . "\n"); 

for ($i = 0; $i < $N; $i++) 
{ 
    for ($j = 0; $j < $N; $j++)  
        echo($mat1[$i][$j] . " "); 
    echo "\n"; 
} 

// This code is contributed 
// by Mukul Singh 

```

**输出**：

```
Scalar Product Matrix is : 
4 8 12 
16 20 24 
28 32 36

```



* * *

* * *



