# 矩阵的按行遍历与按列遍历

> 原文： [https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)

遍历矩阵的两种常见方式是行优先级和列优先级。

**行主要顺序**：当逐行访问矩阵时。

**列主要顺序**：当逐列访问矩阵时。

例子：

```
Input : mat[][] = {{1, 2, 3}, 
                  {4, 5, 6}, 
                  {7, 8, 9}}
Output : Row-wise: 1 2 3 4 5 6 7 8 9
         Col-wise : 1 4 7 2 5 8 3 6 9

```



**差异**：如果根据时间复杂度来看，两者都导致`O(n^2)`，但是当涉及到缓存级别时，顺序访问之一与其他人相比将更快，这取决于我们使用的语言。 像在 **C** 中一样，以行主格式存储矩阵，因此在第`i`个之后访问第`i + 1`个元素时，很可能会导致命中， 这将进一步减少编程时间。

以下代码显示行主访问和列主访问的时间差。

## C++ 

```cpp

// C program showing time difference 
// in row major and column major access 
#include <stdio.h> 
#include <time.h> 

// taking MAX 10000 so that time difference 
// can be shown 
#define MAX 10000 

int arr[MAX][MAX] = {0}; 

void rowMajor() { 

  int i, j; 

  // accessing element row wise 
  for (i = 0; i < MAX; i++) { 
    for (j = 0; j < MAX; j++) { 
      arr[i][j]++; 
    } 
  } 
} 

void colMajor() { 

  int i, j; 

  // accessing element column wise 
  for (i = 0; i < MAX; i++) { 
    for (j = 0; j < MAX; j++) { 
      arr[j][i]++; 
    } 
  } 
} 

// driver code 
int main() { 
  int i, j; 

  // Time taken by row major order 
  clock_t t = clock(); 
  rowMajor(); 
  t = clock() - t; 
  printf("Row major access time :%f s\n",  
                t / (float)CLOCKS_PER_SEC); 

  // Time taken by column major order 
  t = clock(); 
  colMajor(); 
  t = clock() - t; 
  printf("Column major access time :%f s\n",  
               t / (float)CLOCKS_PER_SEC); 
  return 0; 
} 

```

## Java

```java
// Java program showing time difference 
// in row major and column major access 
import java.time.Duration; 
import java.time.Instant; 
import java.util.*; 
  
class GFG  
{ 
  
// taking MAX 10000 so that time difference 
// can be shown 
static int MAX= 10000; 
  
static int [][]arr = new int[MAX][MAX]; 
  
static void rowMajor()  
{ 
  
    int i, j; 
      
    // accessing element row wise 
    for (i = 0; i < MAX; i++)  
    { 
        for (j = 0; j < MAX; j++)  
        { 
        arr[i][j]++; 
        } 
    } 
} 
  
static void colMajor()  
{ 
  
    int i, j; 
      
    // accessing element column wise 
    for (i = 0; i < MAX; i++)  
    { 
        for (j = 0; j < MAX; j++) 
        { 
        arr[j][i]++; 
        } 
    } 
} 
  
// Driver code 
public static void main(String[] args)  
{ 
  
    // Time taken by row major order 
    Instant start = Instant.now(); 
    rowMajor(); 
    Instant end = Instant.now(); 
        System.out.println("Row major access time : "+  
                    Duration.between(start, end)); 
      
    // Time taken by column major order 
    start = Instant.now(); 
    colMajor(); 
    end = Instant.now(); 
    System.out.printf("Column major access time : "+  
                    Duration.between(start, end)); 
} 
} 
  
// This code is contributed by 29AjayKumar
```

输出：

```
Row major access time :0.492000 s
Column major access time :1.621000 s
```

