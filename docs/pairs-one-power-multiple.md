# 一个元素是另一个的幂倍数的偶对

> 原文： [https://www.geeksforgeeks.org/pairs-one-power-multiple/](https://www.geeksforgeeks.org/pairs-one-power-multiple/)

您会得到`n`个元素的数组`A[]`和一个正整数`k`。 现在，您已经找到了对`Ai`，`Aj`的数量，使得`Ai = Aj * (k ^ x)`，其中`x`是整数。

注意：`(Ai, Aj)`和`(Aj, Ai)`必须计数一次。

**示例**：

```
Input : A[] = {3, 6, 4, 2},  k = 2
Output : 2
Explanation : We have only two pairs 
(4, 2) and (3, 6)

Input : A[] = {2, 2, 2},   k = 2
Output : 3
Explanation : (2, 2), (2, 2), (2, 2) 
that are (A1, A2), (A2, A3) and (A1, A3) are 
total three pairs where Ai = Aj * (k^0) 

```



为了解决这个问题，我们首先对给定的数组进行排序，然后对于每个元素`Ai`，对于`x`的不同值，找到等于值`Ai * k ^ x`的元素数量，直到`Ai * k ^ x`小于或等于元素`Ai`的最大值。

算法：

```
    // sort the given array
    sort(A, A+n);

    // for each A[i] traverse rest array
    for (int i=0; i<n; i++)
    {
        for (int j=i+1; j<n; j++)
        {
            // count Aj such that Ai*k^x = Aj
            int x = 0;

            // increase x till Ai * k^x <= 
            // largest element
            while ((A[i]*pow(k, x)) <= A[j])
            {
                if ((A[i]*pow(k, x)) == A[j])
                {              
                     ans++;
                     break;
                }
                x++;
            }        
        }   
    }
    // return answer
    return ans;

```


## C++ 

```cpp

// Program to find pairs count 
#include <bits/stdc++.h> 
using namespace std; 

// function to count the required pairs 
int countPairs(int A[], int n, int k) { 
  int ans = 0; 
  // sort the given array 
  sort(A, A + n); 

  // for each A[i] traverse rest array 
  for (int i = 0; i < n; i++) { 
    for (int j = i + 1; j < n; j++) { 

      // count Aj such that Ai*k^x = Aj 
      int x = 0; 

      // increase x till Ai * k^x <= largest element 
      while ((A[i] * pow(k, x)) <= A[j]) { 
        if ((A[i] * pow(k, x)) == A[j]) { 
          ans++; 
          break; 
        } 
        x++; 
      } 
    } 
  } 
  return ans; 
} 

// driver program 
int main() { 
  int A[] = {3, 8, 9, 12, 18, 4, 24, 2, 6}; 
  int n = sizeof(A) / sizeof(A[0]); 
  int k = 3; 
  cout << countPairs(A, n, k); 
  return 0; 
} 

```

## Java

```java

// Java program to find pairs count 
import java.io.*; 
import java .util.*; 

class GFG { 

    // function to count the required pairs 
    static int countPairs(int A[], int n, int k)  
    { 
        int ans = 0; 

        // sort the given array 
        Arrays.sort(A); 

        // for each A[i] traverse rest array 
        for (int i = 0; i < n; i++) { 
            for (int j = i + 1; j < n; j++)  
            { 

                // count Aj such that Ai*k^x = Aj 
                int x = 0; 

                // increase x till Ai * k^x <= largest element 
                while ((A[i] * Math.pow(k, x)) <= A[j])  
                { 
                    if ((A[i] * Math.pow(k, x)) == A[j])  
                    { 
                        ans++; 
                        break; 
                    } 
                    x++; 
                } 
            } 
        } 
        return ans; 
    } 

    // Driver program 
    public static void main (String[] args)  
    { 
        int A[] = {3, 8, 9, 12, 18, 4, 24, 2, 6}; 
        int n = A.length; 
        int k = 3; 
        System.out.println (countPairs(A, n, k)); 

    } 
} 

// This code is contributed by vt_m. 

```

## Python3

```py

# Program to find pairs count 
import math 

# function to count the required pairs 
def countPairs(A, n, k):  
    ans = 0

    # sort the given array 
    A.sort() 

    # for each A[i] traverse rest array 
    for i in range(0,n):  

        for j in range(i + 1, n): 

            # count Aj such that Ai*k^x = Aj 
            x = 0

            # increase x till Ai * k^x <= largest element 
            while ((A[i] * math.pow(k, x)) <= A[j]) : 
                if ((A[i] * math.pow(k, x)) == A[j]) : 
                    ans+=1
                    break
                x+=1
    return ans 

# driver program 
A = [3, 8, 9, 12, 18, 4, 24, 2, 6] 
n = len(A) 
k = 3

print(countPairs(A, n, k)) 

# This code is contributed by 
# Smitha Dinesh Semwal 

```

## C# 

```cs

// C# program to find pairs count 
using System; 

class GFG { 

    // function to count the required pairs 
    static int countPairs(int []A, int n, int k)  
    { 
        int ans = 0; 

        // sort the given array 
        Array.Sort(A); 

        // for each A[i] traverse rest array 
        for (int i = 0; i < n; i++)  
        { 
            for (int j = i + 1; j < n; j++)  
            { 

                // count Aj such that Ai*k^x = Aj 
                int x = 0; 

                // increase x till Ai * k^x <= largest element 
                while ((A[i] * Math.Pow(k, x)) <= A[j])  
                { 
                    if ((A[i] * Math.Pow(k, x)) == A[j])  
                    { 
                        ans++; 
                        break; 
                    } 
                    x++; 
                } 
            } 
        } 
        return ans; 
    } 

    // Driver program 
    public static void Main ()  
    { 
        int []A = {3, 8, 9, 12, 18, 4, 24, 2, 6}; 
        int n = A.Length; 
        int k = 3; 
        Console.WriteLine(countPairs(A, n, k)); 

    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP Program to find pairs count 

// function to count 
// the required pairs 
function countPairs($A, $n, $k)  
{ 
$ans = 0; 

// sort the given array 
sort($A); 

// for each A[i]  
// traverse rest array 
for ($i = 0; $i < $n; $i++)  
{ 
    for ($j = $i + 1; $j < $n; $j++)  
    { 

    // count Aj such that Ai*k^x = Aj 
    $x = 0; 

    // increase x till Ai *  
    // k^x <= largest element 
    while (($A[$i] * pow($k, $x)) <= $A[$j])  
    { 
        if (($A[$i] * pow($k, $x)) == $A[$j])  
        { 
        $ans++; 
        break; 
        } 
        $x++; 
    } 
    } 
} 
return $ans; 
} 

// Driver Code 

$A = array(3, 8, 9, 12, 18,  
              4, 24, 2, 6); 
$n = count($A); 
$k = 3; 
echo countPairs($A, $n, $k); 

// This code is contributed by anuj_67\. 
?> 

```

**输出**：

```
6

```



* * *

* * *



