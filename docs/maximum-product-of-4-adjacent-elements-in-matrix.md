# 矩阵中 4 个相邻元素的最大积

> 原文： [https://www.geeksforgeeks.org/maximum-product-of-4-adjacent-elements-in-matrix/](https://www.geeksforgeeks.org/maximum-product-of-4-adjacent-elements-in-matrix/)

给定一个正方形矩阵，找到矩阵的四个相邻元素的最大积。 矩阵的相邻元素可以是上，下，左，右，对角线或反对角线。 四个或更多数字应彼此相邻。

**注意**：`n`应该大于或等于 4，即`n >= 4`。

**示例**：

```
Input : n = 4
        {{6, 2, 3 4},
         {5, 4, 3, 1},
         {7, 4, 5, 6},
         {8, 3, 1, 0}}

Output : 1680 

Explanation:
Multiplication of 6 5 7 8 produces maximum
result and all element are adjacent to 
each other in one direction

Input : n = 5
        {{1, 2, 3, 4, 5},
         {6, 7, 8, 9, 1},
         {2, 3, 4, 5, 6},
         {7, 8, 9, 1, 0},
         {9, 6, 4, 2, 3}}

Output: 3024

Explanation:
Multiplication of 6 7 8 9 produces maximum 
result and all elements are adjacent to
each other in one direction.

```

**提问者：Tolexo。**



**方法**：

1.将每行中彼此相邻的 4 个元素分组，并计算其最大结果。

2.在每列中彼此相邻的第 4 组元素，并计算其最大结果。

3.对角线中彼此相邻的第 4 组元素，并计算其最大结果。

4.以对角线方向彼此相邻的第 4 组元素，并计算其最大结果。

5.比较所有计算出的最大结果。

下面是上述方法的实现：

## C++ 

```cpp

// C++ program to find out the maximum product 
// in the matrix which four elements are  
// adjacent to each other in one direction 
#include <bits/stdc++.h> 
using namespace std; 

const int n = 5; 

// function to find max product 
int FindMaxProduct(int arr[][n], int n) 
{ 
    int max = 0, result; 

    // iterate the rows. 
    for (int i = 0; i < n; i++)  
    { 

        // iterate the columns. 
        for (int j = 0; j < n; j++)  
        { 

            // check the maximum product  
            // in horizontal row. 
            if ((j - 3) >= 0)  
            { 
                result = arr[i][j] * arr[i][j - 1] * 
                    arr[i][j - 2] * arr[i][j - 3]; 

                if (max < result) 
                    max = result; 
            } 

            // check the maximum product  
            // in vertical row. 
            if ((i - 3) >= 0)  
            { 
                result = arr[i][j] * arr[i - 1][j] * 
                    arr[i - 2][j] * arr[i - 3][j]; 

                if (max < result) 
                    max = result; 
            } 

            // check the maximum product in 
            // diagonal (going through down - right) 
            if ((i - 3) >= 0 && (j - 3) >= 0)  
            { 
                result = arr[i][j] * arr[i - 1][j - 1] * 
                    arr[i - 2][j - 2] * arr[i - 3][j - 3]; 

                if (max < result) 
                    max = result; 
            } 

            // check the maximum product in 
            // diagonal (going through up - right) 
            if ((i - 3) >= 0 && (j - 1) <= 0) 
            { 
                result = arr[i][j] * arr[i - 1][j + 1] * 
                    arr[i - 2][j + 2] * arr[i - 3][j + 3]; 

                if (max < result) 
                    max = result; 
            } 
        } 
    } 

    return max; 
} 

// driver code 
int main() 
{ 

    /* int arr[][4] = {{6, 2, 3, 4},  
                    {5, 4, 3, 1}, 
                    {7, 4, 5, 6}, 
                    {8, 3, 1, 0}};*/
    /* int arr[][5] = {{1, 2, 1, 3, 4}, 
                    {5, 6, 3, 9, 2}, 
                    {7, 8, 8, 1, 2}, 
                    {1, 0, 7, 9, 3}, 
                    {3, 0, 8, 4, 9}};*/

    int arr[][5] = {{1, 2, 3, 4, 5}, 
                    {6, 7, 8, 9, 1}, 
                    {2, 3, 4, 5, 6}, 
                    {7, 8, 9, 1, 0}, 
                    {9, 6, 4, 2, 3}}; 

    cout << FindMaxProduct(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find out the 
// maximum product in the matrix 
// which four elements are adjacent 
// to each other in one direction 
class GFG  
{ 
static final int n = 5; 

// function to find max product 
static int FindMaxProduct(int arr[][], int n)  
{ 
    int max = 0, result; 

    // iterate the rows. 
    for (int i = 0; i < n; i++)  
    { 
    // iterate the columns. 
    for (int j = 0; j < n; j++)  
    { 
        // check the maximum product 
        // in horizontal row. 
        if ((j - 3) >= 0)  
        { 
        result = arr[i][j] * arr[i][j - 1] *  
                arr[i][j - 2] * arr[i][j - 3]; 
        if (max < result) 
            max = result; 
        } 

        // check the maximum product 
        // in vertical row. 
        if ((i - 3) >= 0)  
        { 
        result = arr[i][j] * arr[i - 1][j] *  
                arr[i - 2][j] * arr[i - 3][j]; 

        if (max < result) 
            max = result; 
        } 

        // check the maximum product in 
        // diagonal (going through down - right) 
        if ((i - 3) >= 0 && (j - 3) >= 0)  
        { 
        result = arr[i][j] * arr[i - 1][j - 1] *  
                arr[i - 2][j - 2] * arr[i - 3][j - 3]; 

        if (max < result) 
            max = result; 
        } 

        // check the maximum product in 
        // diagonal (going through up - right) 
        if ((i - 3) >= 0 && (j - 1) <= 0) 
        { 
        result = arr[i][j] * arr[i - 1][j + 1] * 
               arr[i - 2][j + 2] * arr[i - 3][j + 3]; 

        if (max < result) 
            max = result; 
        } 
    } 
    } 

    return max; 
} 

// Driver code 
public static void main(String[] args)  
{ 

    /* int arr[][4] = {{6, 2, 3, 4}, 
                       {5, 4, 3, 1}, 
                       {7, 4, 5, 6}, 
                       {8, 3, 1, 0}};*/
    /* int arr[][5] = {{1, 2, 1, 3, 4}, 
                       {5, 6, 3, 9, 2}, 
                       {7, 8, 8, 1, 2}, 
                       {1, 0, 7, 9, 3}, 
                       {3, 0, 8, 4, 9}};*/

    int arr[][] = {{1, 2, 3, 4, 5}, 
                {6, 7, 8, 9, 1}, 
                {2, 3, 4, 5, 6}, 
                {7, 8, 9, 1, 0}, 
                    {9, 6, 4, 2, 3}}; 

    System.out.print(FindMaxProduct(arr, n)); 
} 
} 

// This code is contributed by Anant Agarwal. 

```

## Python 3

```py

# Python 3 program to find out the maximum  
# product in the matrix which four elements  
# are adjacent to each other in one direction 
n = 5

# function to find max product 
def FindMaxProduct(arr, n): 

    max = 0

    # iterate the rows. 
    for i in range(n):  

        # iterate the columns. 
        for j in range( n):  

            # check the maximum product  
            # in horizontal row. 
            if ((j - 3) >= 0): 
                result = (arr[i][j] * arr[i][j - 1] * 
                          arr[i][j - 2] * arr[i][j - 3]) 

                if (max < result): 
                    max = result 

            # check the maximum product  
            # in vertical row. 
            if ((i - 3) >= 0) : 
                result = (arr[i][j] * arr[i - 1][j] *
                          arr[i - 2][j] * arr[i - 3][j]) 

                if (max < result): 
                    max = result 

            # check the maximum product in 
            # diagonal going through down - right  
            if ((i - 3) >= 0 and (j - 3) >= 0): 
                result = (arr[i][j] * arr[i - 1][j - 1] *
                          arr[i - 2][j - 2] * arr[i - 3][j - 3]) 

                if (max < result): 
                    max = result 

            # check the maximum product in 
            # diagonal going through up - right 
            if ((i - 3) >= 0 and (j - 1) <= 0): 
                result = (arr[i][j] * arr[i - 1][j + 1] *
                          arr[i - 2][j + 2] * arr[i - 3][j + 3]) 

                if (max < result): 
                    max = result 

    return max

# Driver code 
if __name__ == "__main__": 

    # int arr[][4] = {{6, 2, 3, 4},  
    #                  {5, 4, 3, 1}, 
    #                  {7, 4, 5, 6}, 
    #                  {8, 3, 1, 0}}; 
    # int arr[][5] = {{1, 2, 1, 3, 4}, 
    #                  {5, 6, 3, 9, 2}, 
    #                  {7, 8, 8, 1, 2}, 
    #                  {1, 0, 7, 9, 3}, 
    #                  {3, 0, 8, 4, 9}}; 

    arr = [[1, 2, 3, 4, 5], 
           [6, 7, 8, 9, 1], 
           [2, 3, 4, 5, 6], 
           [7, 8, 9, 1, 0], 
            [9, 6, 4, 2, 3]] 

    print(FindMaxProduct(arr, n)) 

# This code is contributed by ita_c 

```

## C# 

```cs

// C# program to find out the 
// maximum product in the matrix 
// which four elements are adjacent 
// to each other in one direction 
using System; 

public class GFG { 

    static int n = 5; 

// Function to find max product 
static int FindMaxProduct(int[,] arr, int n)  
{ 
    int max = 0, result; 

    // iterate the rows 
    for (int i = 0; i < n; i++) { 

    // iterate the columns 
    for (int j = 0; j < n; j++) { 

        // check the maximum product 
        // in horizontal row. 
        if ((j - 3) >= 0) { 

        result = arr[i, j] * arr[i, j - 1] *  
                             arr[i, j - 2] * 
                             arr[i, j - 3]; 

        if (max < result) 
            max = result; 
        } 

        // check the maximum product 
        // in vertical row. 
        if ((i - 3) >= 0) { 
        result = arr[i, j] * arr[i - 1, j] *  
                             arr[i - 2, j] * 
                             arr[i - 3, j]; 

        if (max < result) 
            max = result; 
        } 

        // check the maximum product in 
        // diagonal going through down - right 
        if ((i - 3) >= 0 && (j - 3) >= 0)  
        { 
        result = arr[i, j] * arr[i - 1, j - 1] *  
                             arr[i - 2, j - 2] *  
                             arr[i - 3, j - 3]; 

        if (max < result) 
            max = result; 
        } 

        // check the maximum product in  
        // diagonal going through up - right 
        if ((i - 3 ) >= 0 && (j - 1) <= 0) 
        { 
        result = arr[i, j] * arr[i - 1, j + 1] *  
                             arr[i - 2, j + 2] * 
                             arr[i - 3, j + 3]; 

        if (max < result) 
            max = result; 
        } 
    } 
    } 

    return max; 
} 

    // Driver Code 
    static public void Main () 
    { 
    int[,]arr = {{1, 2, 3, 4, 5}, 
                 {6, 7, 8, 9, 1}, 
                 {2, 3, 4, 5, 6}, 
                 {7, 8, 9, 1, 0}, 
                 {9, 6, 4, 2, 3}}; 

    Console.Write(FindMaxProduct(arr, n)); 
    } 
} 

// This code is contributed by Shrikant13 

```

## PHP

```php

<?php 
// PHP program to find out the maximum product 
// in the matrix which four elements are  
// adjacent to each other in one direction 
$n = 5; 

// function to find max product 
function FindMaxProduct( $arr, $n) 
{ 
    $max = 0; $result; 

    // iterate the rows. 
    for ( $i = 0; $i < $n; $i++)  
    { 

        // iterate the columns. 
        for ( $j = 0; $j < $n; $j++)  
        { 

            // check the maximum product  
            // in horizontal row. 
            if (($j - 3) >= 0)  
            { 
                $result = $arr[$i][$j] *  
                          $arr[$i][$j - 1] * 
                          $arr[$i][$j - 2] *  
                          $arr[$i][$j - 3]; 

                if ($max < $result) 
                    $max = $result; 
            } 

            // check the maximum product  
            // in vertical row. 
            if (($i - 3) >= 0)  
            { 
                $result = $arr[$i][$j] *  
                          $arr[$i - 1][$j] * 
                          $arr[$i - 2][$j] *  
                          $arr[$i - 3][$j]; 

                if ($max < $result) 
                    $max = $result; 
            } 

            // check the maximum product in 
            // diagonal going through down - right 
            if (($i - 3) >= 0 and ($j - 3) >= 0)  
            { 
                $result = $arr[$i][$j] *  
                          $arr[$i - 1][$j - 1] * 
                          $arr[$i - 2][$j - 2] *  
                          $arr[$i - 3][$j - 3]; 

                if ($max < $result) 
                    $max = $result; 
            } 

            // check the maximum product in 
            // diagonal going through up - right 
            if (($i - 3) >= 0 and ($j - 1) <= 0)  
            { 
                $result = $arr[$i][$j] *  
                          $arr[$i - 1][$j + 1] * 
                          $arr[$i - 2][$j + 2] *  
                          $arr[$i - 3][$j + 3]; 

                if ($max < $result) 
                    $max = $result; 
            } 

        } 
    } 

    return $max; 
} 

    // Driver Code                         
    $arr = array(array(1, 2, 3, 4, 5), 
                 array(6, 7, 8, 9, 1), 
                 array(2, 3, 4, 5, 6), 
                 array(7, 8, 9, 1, 0), 
                 array(9, 6, 4, 2, 3)); 

    echo FindMaxProduct($arr, $n); 

// This code is contributed by anuj_67\. 
?> 

```

**输出**：

```
3024
```



* * *

* * *



