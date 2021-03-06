# 二维数组的按行排序

> 原文： [https://www.geeksforgeeks.org/row-wise-sorting-2d-array/](https://www.geeksforgeeks.org/row-wise-sorting-2d-array/)

给定一个 2D 数组，对该数组的每一行进行排序并打印结果。

**示例**：

```
Input :
77 11 22 3
11 89 1 12
32 11 56 7
11 22 44 33
Output :
3 11 22 77
1 11 12 89
7 11 32 56
11 22 33 44

Input :
8 6 4 5
3 5 2 1
9 7 4 2
7 8 9 5
Output :
4 5 6 8
1 2 3 5
2 4 7 9
5 7 8 9

```



**方法 1（使用冒泡排序）**：

开始遍历给定 2D 数组的每一行，并使用有效的排序算法对每一行的元素进行排序。

## Java

```java

// Java code to sort 2D matrix row-wise 
import java.io.*; 

public class Sort2DMatrix { 

    static int sortRowWise(int m[][]) 
    { 
        // loop for rows of matrix 
        for (int i = 0; i < m.length; i++) { 

            // loop for column of matrix 
            for (int j = 0; j < m[i].length; j++) { 

                // loop for comparison and swapping 
                for (int k = 0; k < m[i].length - j - 1; k++) { 
                    if (m[i][k] > m[i][k + 1]) { 

                        // swapping of elements 
                        int t = m[i][k]; 
                        m[i][k] = m[i][k + 1]; 
                        m[i][k + 1] = t; 
                    } 
                } 
            } 
        } 

        // printing the sorted matrix 
        for (int i = 0; i < m.length; i++) { 
            for (int j = 0; j < m[i].length; j++) 
                System.out.print(m[i][j] + " "); 
            System.out.println(); 
        } 

        return 0; 
    } 

    // driver code 
    public static void main(String args[]) 
    { 
        int m[][] = { { 9, 8, 7, 1 }, 
                      { 7, 3, 0, 2 }, 
                      { 9, 5, 3, 2 }, 
                      { 6, 3, 1, 2 } }; 
        sortRowWise(m); 
    } 
} 

```

## Python3

```py

# Python3 code to sort 2D matrix row-wise 
def sortRowWise(m): 

    # loop for rows of matrix 
    for i in range(len(m)): 

        # loop for column of matrix 
        for j in range(len(m[i])): 

            # loop for comparison and swapping 
            for k in range(len(m[i]) - j - 1): 

                if (m[i][k] > m[i][k + 1]): 

                    # swapping of elements 
                    t = m[i][k] 
                    m[i][k] = m[i][k + 1] 
                    m[i][k + 1] = t 

    # printing the sorted matrix 
    for i in range(len(m)): 
        for j in range(len(m[i])): 
            print(m[i][j], end=" ") 
        print() 

# Driver code 
m = [[9, 8, 7, 1 ],[7, 3, 0, 2],[9, 5, 3, 2],[ 6, 3, 1, 2 ]] 
sortRowWise(m) 

# This code is contributed by shubhamsingh10 

```

## C# 

```cs

// C# code to sort 2D matrix row-wise 
using System; 

class GFG  
{ 
static int sortRowWise(int [,]m) 
{ 
    // loop for rows of matrix 
    for (int i = 0;  
             i < m.GetLength(0); i++) 
    { 

        // loop for column of matrix 
        for (int j = 0;  
                 j < m.GetLength(1); j++)  
        { 

            // loop for comparison and swapping 
            for (int k = 0;  
                     k < m.GetLength(1) - j - 1; k++)  
            { 
                if (m[i, k] > m[i, k + 1])  
                { 

                    // swapping of elements 
                    int t = m[i, k]; 
                    m[i, k] = m[i, k + 1]; 
                    m[i, k + 1] = t; 
                } 
            } 
        } 
    } 

    // printing the sorted matrix 
    for (int i = 0; 
             i < m.GetLength(0); i++)  
    { 
        for (int j = 0; 
                 j < m.GetLength(1); j++) 
            Console.Write(m[i, j] + " "); 
        Console.WriteLine(); 
    } 
    return 0; 
} 

// Driver Code 
public static void Main(String []args) 
{ 
    int [,]m = {{ 9, 8, 7, 1 }, 
                { 7, 3, 0, 2 }, 
                { 9, 5, 3, 2 }, 
                { 6, 3, 1, 2 }}; 
    sortRowWise(m); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**输出**：

```
1 7 8 9 
0 2 3 7 
2 3 5 9 
1 2 3 6

```

**方法 2（使用库函数）**：

想法是对矩阵的每一行使用[`Arrays.sort()`](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)。

## Java

```java

// Java code to sort 2D matrix row-wise 
import java.io.*; 
import java.util.Arrays; 

public class Sort2DMatrix { 

    static int sortRowWise(int m[][]) 
    { 
        // One by one sort individual rows. 
        for (int i = 0; i < m.length; i++) 
            Arrays.sort(m[i]); 

        // printing the sorted matrix 
        for (int i = 0; i < m.length; i++) { 
            for (int j = 0; j < m[i].length; j++) 
                System.out.print(m[i][j] + " "); 
            System.out.println(); 
        } 

        return 0; 
    } 

    // driver code 
    public static void main(String args[]) 
    { 
        int m[][] = { { 9, 8, 7, 1 }, 
                      { 7, 3, 0, 2 }, 
                      { 9, 5, 3, 2 }, 
                      { 6, 3, 1, 2 } }; 

        sortRowWise(m); 
    } 
} 

```

## Python3

```py

# Python3 code to sort 2D matrix row-wise 
def sortRowWise(m): 

    # One by one sort individual rows. 
    for i in range(len(m)):  
        m[i].sort() 

    # printing the sorted matrix 
    for i in range(len(m)): 
        for j in range(len(m[i])): 
            print(m[i][j], end=" ") 
        print() 

    return 0

# Driver code 
m = [[9, 8, 7, 1 ],[7, 3, 0, 2],[9, 5, 3, 2 ],[ 6, 3, 1, 2]] 

sortRowWise(m) 

# This code is contributed by shubhamsingh10 

```

Output

```
1 7 8 9 
0 2 3 7 
2 3 5 9 
1 2 3 6

```



* * *

* * *



