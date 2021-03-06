# 替换元素使数组元素连续

> 原文： [https://www.geeksforgeeks.org/replacing-an-element-makes-array-elements-consecutive/](https://www.geeksforgeeks.org/replacing-an-element-makes-array-elements-consecutive/)

给定正整数的数组。 我们需要找到唯一的元素，其任何其他值的替换都会使数组元素变得连续不同。 如果不可能使数组元素连续，则返回 -1。

**示例**：

```
Input : arr[] = {45, 42, 46, 48, 47}
Output : 42
Explanation: We can replace 42 with either
44 or 48 to make array consecutive.

Input : arr[] = {5, 6, 7, 9, 10}
Output : 5 [OR 10]
Explanation: We can either replace 5 with 8
or 10 with 8 to make array elements 
consecutive.

Input : arr[] = {5, 6, 7, 9, 8}
Output : Array elements are already consecutive

```



**朴素的方法**是要检查`arr[]`的每个元素，在替换后使[连续或不连续](https://www.geeksforgeeks.org/check-array-elements-consecutive-time-o1-space-handles-positive-negative-numbers/)。 此方法的时间复杂度`O(n^2)`。

**更好的方法**基于以下重要观察结果：如果存在答案，则最小或最大元素将为答案。 如果存在答案，则有两种情况。

1.  一系列连续元素从数组的最小元素开始，然后通过在前一个元素上加 1 继续。

2.  一系列连续元素从数组的最大元素开始，然后从上一个元素中减去 1 继续。

我们制作两个以上的系列，对于每个系列，我们都在数组中搜索系列元素。 如果两个系列的不匹配数均大于 1，则不存在答案。 如果发现任何一个序列不匹配，那么我们有答案。

## C++ 

```cpp

// CPP program to find an element replacement 
// of which makes the array elements consecutive. 
#include <bits/stdc++.h> 
using namespace std; 

int findElement(int arr[], int n) 
{ 
    sort(arr, arr+n); 

    // Making a series starting from first element 
    // and adding 1 to every element.     
    int mismatch_count1 = 0, res; 
    int next_element = arr[n-1] - n + 1; 
    for (int i=0; i<n-1; i++) { 
       if (binary_search(arr, arr+n, next_element) == 0) 
       { 
          res = arr[0];   
          mismatch_count1++; 
       } 
        next_element++; 
    }    

    // If only one mismatch is found. 
    if (mismatch_count1 == 1) 
        return res; 

    // If no mismatch found, elements are 
    // already consecutive. 
    if (mismatch_count1 == 0)   
        return 0; 

    // Making a series starting from last element 
    // and subtracting 1 to every element.  
    int mismatch_count2 = 0; 
    next_element = arr[0] + n - 1; 
    for (int i=n-1; i>=1; i--) { 
       if (binary_search(arr, arr+n, next_element) == 0) 
       { 
          res = arr[n-1];   
          mismatch_count2++; 
       }       
       next_element--; 
    } 

    // If only one mismatch is found. 
    if (mismatch_count2 == 1) 
      return res; 

    return -1;   
} 

// Driver code 
int main() 
{ 
    int arr[] =  {7, 5, 12, 8} ; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    int res = findElement(arr,n); 
    if (res == -1) 
      cout << "Answer does not exist"; 
    else if (res == 0) 
      cout << "Elements are already consecutive"; 
    else
      cout << res; 
    return 0; 
} 

```

## Java

```java

// Java program to find an element  
// replacement of which makes  
// the array elements consecutive. 
import java.io.*; 
import java.util.Arrays; 

class GFG 
{ 
    static int findElement(int []arr,  
                           int n) 
    { 
        Arrays.sort(arr); 

        // Making a series starting  
        // from first element and  
        // adding 1 to every element.  
        int mismatch_count1 = 0,  
                        res = 0; 
        int next_element = arr[n - 1] -  
                               n + 1; 

        for (int i = 0; i < n - 1; i++)  
        { 
        if (Arrays.binarySearch(arr,  
                            next_element) < 0) 
        { 
            res = arr[0];  
            mismatch_count1++; 
        } 
            next_element++; 
        }  

        // If only one mismatch is found. 
        if (mismatch_count1 == 1) 
            return res; 

        // If no mismatch found, elements  
        // are already consecutive. 
        if (mismatch_count1 == 0)  
            return 0; 

        // Making a series starting 
        // from last element and  
        // subtracting 1 to every element.  
        int mismatch_count2 = 0; 
        next_element = arr[0] + n - 1; 

        for (int i = n - 1; i >= 1; i--)  
        { 
        if (Arrays.binarySearch(arr,  
                            next_element) < 0) 
        { 
            res = arr[n - 1];  
            mismatch_count2++; 
        }      
        next_element--; 
        } 

        // If only one mismatch is found. 
        if (mismatch_count2 == 1) 
        return res; 

        return -1;  
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int []arr = new int[]{7, 5, 12, 8} ; 
        int n = arr.length; 
        int res = findElement(arr,n); 
        if (res == -1) 
        System.out.print("Answer does not exist"); 
        else if (res == 0) 
        System.out.print("Elements are " +  
                         "already consecutive"); 
        else
        System.out.print(res); 
    } 
} 

// This code is contributed by  
// Manish Shaw(manishshaw1) 

```

## C# 

```cs

// C# program to find an element  
// replacement of which makes  
// the array elements consecutive. 
using System; 
using System.Linq; 
using System.Collections.Generic; 

class GFG 
{ 
    static int findElement(int []arr,  
                           int n) 
    { 
        Array.Sort(arr); 

        // Making a series starting  
        // from first element and  
        // adding 1 to every element.  
        int mismatch_count1 = 0, res = 0; 
        int next_element = arr[n - 1] - n + 1; 

        for (int i = 0; i < n - 1; i++)  
        { 
        if (Array.BinarySearch(arr,  
                               next_element) < 0) 
        { 
            res = arr[0];  
            mismatch_count1++; 
        } 
            next_element++; 
        }  

        // If only one mismatch is found. 
        if (mismatch_count1 == 1) 
            return res; 

        // If no mismatch found, elements  
        // are already consecutive. 
        if (mismatch_count1 == 0)  
            return 0; 

        // Making a series starting 
        // from last element and  
        // subtracting 1 to every element.  
        int mismatch_count2 = 0; 
        next_element = arr[0] + n - 1; 

        for (int i = n - 1; i >= 1; i--)  
        { 
        if (Array.BinarySearch(arr,  
                               next_element) < 0) 
        { 
            res = arr[n - 1];  
            mismatch_count2++; 
        }      
        next_element--; 
        } 

        // If only one mismatch is found. 
        if (mismatch_count2 == 1) 
        return res; 

        return -1;  
    } 

    // Driver code 
    static void Main() 
    { 
        int []arr = new int[]{7, 5, 12, 8} ; 
        int n = arr.Length; 
        int res = findElement(arr,n); 
        if (res == -1) 
        Console.Write("Answer does not exist"); 
        else if (res == 0) 
        Console.Write("Elements are " +  
                      "already consecutive"); 
        else
        Console.Write(res); 
    } 
} 

// This code is contributed by  
// Manish Shaw(manishshaw1) 

```

**输出**：

```
12

```

**时间复杂度**：`O(N log N)`。



* * *

* * *



