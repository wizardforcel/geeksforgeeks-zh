# 矩阵中沙漏的最大和

> 原文： [https://www.geeksforgeeks.org/maximum-sum-hour-glass-matrix/](https://www.geeksforgeeks.org/maximum-sum-hour-glass-matrix/)

给定 2D 矩阵，任务是找到一个沙漏的最大和。

```
An hour glass is made of 7 cells
in following form.
    A B C
      D
    E F G

```

**示例**：

```
Input : 1 1 1 0 0 
        0 1 0 0 0 
        1 1 1 0 0 
        0 0 0 0 0 
        0 0 0 0 0 
Output : 7
Below is the hour glass with
maximum sum:
1 1 1 
  1
1 1 1

Input : 0 3 0 0 0
        0 1 0 0 0
        1 1 1 0 0
        0 0 2 4 4
        0 0 0 2 4
Output : 11
Below is the hour glass wuth
maximum sum
1 0 0
  4
0 2 4

```



从沙漏的定义可以明显看出，行数和列数必须等于 3。如果我们对矩阵中的沙漏总数进行计数，则可以说该计数等于可能的左上单元格的计数。 沙漏。 沙漏中左上角的单元数等于`(R-2) * (C-2)`。 因此，矩阵中的沙漏总数为`(R-2) * (C-2)`。

```
mat[][] = 2 3 0 0 0 
          0 1 0 0 0
          1 1 1 0 0 
          0 0 2 4 4
          0 0 0 2 0
Possible hour glass are :
2 3 0  3 0 0   0 0 0  
  1      0       0 
1 1 1  1 1 0   1 0 0 

0 1 0  1 0 0  0 0 0 
  1      1      0  
0 0 2  0 2 4  2 4 4 

1 1 1  1 1 0  1 0 0
  0      2      4
0 0 0  0 0 2  0 2 0

```

我们将沙漏的所有左上角单元格一一考虑。 对于每个单元格，我们计算由此形成的沙漏总数。 最后，我们返回最大和。

下面是上述想法的实现：

## C++ 

```cpp

// C++ program to find maximum sum of hour 
// glass in matrix 
#include<bits/stdc++.h> 
using namespace std; 
const int R = 5; 
const int C = 5; 

// Returns maximum sum of hour glass in ar[][] 
int findMaxSum(int mat[R][C]) 
{ 
    if (R<3 || C<3) 
        return -1; 

    // Here loop runs (R-2)*(C-2) times considering 
    // different top left cells of hour glasses. 
    int max_sum = INT_MIN; 
    for (int i=0; i<R-2; i++) 
    { 
        for (int j=0; j<C-2; j++) 
        { 
            // Considering mat[i][j] as top left cell of 
            // hour glass. 
            int sum = (mat[i][j]+mat[i][j+1]+mat[i][j+2])+ 
                      (mat[i+1][j+1])+ 
                  (mat[i+2][j]+mat[i+2][j+1]+mat[i+2][j+2]); 

            // If previous sum is less then current sum then 
            // update new sum in max_sum 
            max_sum = max(max_sum, sum); 
        } 
    } 
    return max_sum; 
} 

// Driver code 
int main() 
{ 
    int mat[][C] = {{1, 2, 3, 0, 0}, 
                    {0, 0, 0, 0, 0}, 
                    {2, 1, 4, 0, 0}, 
                    {0, 0, 0, 0, 0}, 
                    {1, 1, 0, 1, 0}}; 
    int res = findMaxSum(mat); 
    if (res == -1) 
        cout << "Not possible" << endl; 
    else
        cout << "Maximum sum of hour glass = "
             << res << endl; 
    return 0; 
} 

```

## Java

```java

// Java program to find maximum  
// sum of hour glass in matrix 
import java.io.*; 

class GFG { 

static int R = 5; 
static int C = 5; 

// Returns maximum sum of  
// hour glass in ar[][] 
static int findMaxSum(int [][]mat) 
{ 
    if (R < 3 || C < 3) 
        return -1; 

    // Here loop runs (R-2)*(C-2)  
    // times considering different 
    // top left cells of hour glasses. 
    int max_sum = Integer.MIN_VALUE; 
    for (int i = 0; i < R - 2; i++) 
    { 
        for (int j = 0; j < C - 2; j++) 
        { 
            // Considering mat[i][j] as top  
            // left cell of hour glass. 
            int sum = (mat[i][j] + mat[i][j + 1] +  
                       mat[i][j + 2]) + (mat[i + 1][j + 1]) +  
                       (mat[i + 2][j] + mat[i + 2][j + 1] +  
                       mat[i + 2][j + 2]); 

            // If previous sum is less then  
            // current sum then update 
            // new sum in max_sum 
            max_sum = Math.max(max_sum, sum); 
        } 
    } 
    return max_sum; 
} 

    // Driver code 
    static public void main (String[] args) 
    { 
        int [][]mat = {{1, 2, 3, 0, 0}, 
                       {0, 0, 0, 0, 0}, 
                       {2, 1, 4, 0, 0}, 
                       {0, 0, 0, 0, 0}, 
                       {1, 1, 0, 1, 0}}; 
        int res = findMaxSum(mat); 
        if (res == -1) 
            System.out.println("Not possible"); 
        else
            System.out.println("Maximum sum of hour glass = "
                                + res); 
    } 

} 

// This code is contributed by vt_m . 

```

## C# 

```cs

// C# program to find maximum  
// sum of hour glass in matrix 
using System; 

class GFG { 

static int R = 5; 
static int C = 5; 

// Returns maximum sum of  
// hour glass in ar[][] 
static int findMaxSum(int [,]mat) 
{ 
    if (R < 3 || C < 3) 
        return -1; 

    // Here loop runs (R-2)*(C-2)  
    // times considering different 
    // top left cells of hour glasses. 
    int max_sum = int.MinValue; 
    for (int i = 0; i < R - 2; i++) 
    { 
        for (int j = 0; j < C - 2; j++) 
        { 
            // Considering mat[i][j] as top  
            // left cell of hour glass. 
            int sum = (mat[i, j] + mat[i, j + 1] +  
                       mat[i, j + 2]) + (mat[i + 1, j + 1]) +  
                      (mat[i + 2, j] + mat[i + 2, j + 1] +  
                       mat[i + 2, j + 2]); 

            // If previous sum is less then  
            // current sum then update 
            // new sum in max_sum 
            max_sum = Math.Max(max_sum, sum); 
        } 
    } 
    return max_sum; 
} 

    // Driver code 
    static public void Main(String[] args) 
    { 
        int [,]mat = {{1, 2, 3, 0, 0}, 
                       {0, 0, 0, 0, 0}, 
                       {2, 1, 4, 0, 0}, 
                       {0, 0, 0, 0, 0}, 
                       {1, 1, 0, 1, 0}}; 
        int res = findMaxSum(mat); 
        if (res == -1) 
            Console.WriteLine("Not possible"); 
        else
            Console.WriteLine("Maximum sum of hour glass = "
                               + res); 
    } 

} 

// This code is contributed by vt_m . 

```

## PHP

```php

<?php 
// PHP program to find maximum sum  
// of hour glass in matrix 
$R = 5; 
$C = 5; 

// Returns maximum sum  
// of hour glass in ar[][] 
function findMaxSum($mat) 
{ 
    global $R; global $C; 
    if ($R < 3 || $C < 3) 
        return -1; 

    // Here loop runs (R-2)*(C-2) times considering 
    // different top left cells of hour glasses. 
    $max_sum = PHP_INT_MIN; 
    for ($i = 0; $i < ($R - 2); $i++) 
    { 
        for ($j = 0; $j < ($C - 2); $j++) 
        { 
            // Considering mat[i][j] as  
            // top left cell of hour glass. 
            $sum = ($mat[$i][$j] + $mat[$i][$j + 1] +  
                    $mat[$i][$j + 2]) +  
                   ($mat[$i + 1][$j + 1]) + 
                   ($mat[$i + 2][$j] +  
                    $mat[$i + 2][$j + 1] +  
                    $mat[$i + 2][$j + 2]); 

            // If previous sum is less than current sum  
            // then update new sum in max_sum 
            $max_sum = max($max_sum, $sum); 
        } 
    } 
    return $max_sum; 
} 

// Driver code 
$mat = array(array(1, 2, 3, 0, 0), 
             array(0, 0, 0, 0, 0), 
             array(2, 1, 4, 0, 0), 
             array(0, 0, 0, 0, 0), 
             array(1, 1, 0, 1, 0)); 
$res = findMaxSum($mat); 
if ($res == -1) 
    echo "Not possible", "\n"; 
else
    echo "Maximum sum of hour glass = ", 
         $res, "\n"; 

// This code is contributed by ajit. 
?> 

```

**输出**：

```
Maximum sum of hour glass = 13

```

**参考**：

[http://stackoverflow.com/questions/38019861/hourglass-sum-in-2d-array](http://stackoverflow.com/questions/38019861/hourglass-sum-in-2d-array)



