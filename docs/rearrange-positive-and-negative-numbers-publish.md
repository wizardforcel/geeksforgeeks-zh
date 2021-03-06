# 在`O(n)`时间和`O(1)`额外空间中重新排列正数和负数

> 原文： [https://www.geeksforgeeks.org/rearrange-positive-and-negative-numbers-publish/](https://www.geeksforgeeks.org/rearrange-positive-and-negative-numbers-publish/)

数组包含随机顺序的正数和负数。 重新排列数组元素，以便交替放置正数和负数。 正数和负数不必相等。 如果有更多正数，它们将出现在数组的末尾。 如果还有更多负数，它们也会出现在数组的末尾。

例如，如果输入数组为`[-1, 2, -3, 4, 5, 6, -7, 8, 9]`，则输出应为`[9, -7, 8, -3, 5, - 1, 2, 4, 6]`。

**注意**：分区过程会更改元素的相对顺序。 即这种方法不能保持元素外观的顺序。 [请参见这里](https://www.geeksforgeeks.org/rearrange-array-alternating-positive-negative-items-o1-extra-space/)，以维护此问题中元素的出现顺序。

解决方案是先使用快排的分区过程将正数和负数分开。 在分区过程中，将 0 视为枢轴元素的值，以便将所有负数放在正数之前。 一旦负数和正数分开，我们就从第一个负数和第一个正数开始，然后将每个备用负数与下一个正数交换。



## C++ 

```cpp

// A C++ program to put positive 
// numbers at even indexes (0, 2, 4,..)  
// and negative numbers at odd  
// indexes (1, 3, 5, ..) 
#include <iostream> 
using namespace std; 

class GFG 
{ 
    public: 
    void rearrange(int [],int); 
    void swap(int *,int *); 
    void printArray(int [],int); 
}; 

// The main function that rearranges  
// elements of given array. It puts 
// positive elements at even indexes  
// (0, 2, ..) and negative numbers  
// at odd indexes (1, 3, ..). 
void GFG :: rearrange(int arr[], int n) 
{ 
    // The following few lines are  
    // similar to partition process 
    // of QuickSort. The idea is to  
    // consider 0 as pivot and 
    // divide the array around it. 
    int i = -1; 
    for (int j = 0; j < n; j++) 
    { 
        if (arr[j] < 0) 
        { 
            i++; 
            swap(&arr[i], &arr[j]); 
        } 
    } 

    // Now all positive numbers are at  
    // end and negative numbers at the 
    // beginning of array. Initialize  
    // indexes for starting point of 
    // positive and negative numbers  
    // to be swapped 
    int pos = i + 1, neg = 0; 

    // Increment the negative index by  
    // 2 and positive index by 1, 
    // i.e., swap every alternate negative  
    // number with next positive number 
    while (pos < n && neg < pos &&  
                     arr[neg] < 0) 
    { 
        swap(&arr[neg], &arr[pos]); 
        pos++; 
        neg += 2; 
    } 
} 

// A utility function  
// to swap two elements 
void GFG :: swap(int *a, int *b) 
{ 
    int temp = *a; 
    *a = *b; 
    *b = temp; 
} 

// A utility function to print an array 
void GFG :: printArray(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 
} 

// Driver Code 
int main()  
{ 
    int arr[] = {-1, 2, -3, 4,  
                  5, 6, -7, 8, 9}; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    GFG test; 
    test.rearrange(arr, n); 
    test.printArray(arr, n); 
    return 0; 
} 

// This code is contributed  
// by vt_Yogesh Shukla 1 

```

## C

```c

// A C++ program to put positive numbers at even indexes (0,  
// 2, 4,..) and negative numbers at odd indexes (1, 3, 5, ..) 
#include <stdio.h> 

// prototype for swap 
void swap(int *a, int *b); 

// The main function that rearranges elements of given array.  
// It puts  positive elements at even indexes (0, 2, ..) and  
// negative numbers at odd indexes (1, 3, ..). 
void rearrange(int arr[], int n) 
{ 
    // The following few lines are similar to partition process 
    // of QuickSort.  The idea is to consider 0 as pivot and 
    // divide the array around it. 
    int i = -1; 
    for (int j = 0; j < n; j++) 
    { 
        if (arr[j] < 0) 
        { 
            i++; 
            swap(&arr[i], &arr[j]); 
        } 
    } 

    // Now all positive numbers are at end and negative numbers 
    // at the beginning of array. Initialize indexes for starting 
    // point of positive and negative numbers to be swapped 
    int pos = i+1, neg = 0; 

    // Increment the negative index by 2 and positive index by 1, 
    // i.e., swap every alternate negative number with next  
    // positive number 
    while (pos < n && neg < pos && arr[neg] < 0) 
    { 
        swap(&arr[neg], &arr[pos]); 
        pos++; 
        neg += 2; 
    } 
} 

// A utility function to swap two elements 
void swap(int *a, int *b) 
{ 
    int temp = *a; 
    *a = *b; 
    *b = temp; 
} 

// A utility function to print an array 
void printArray(int arr[], int n) 
{ 
    for (int i = 0; i < n; i++) 
        printf("%4d ", arr[i]); 
} 

// Driver program to test above functions 
int main() 
{ 
    int arr[] = {-1, 2, -3, 4, 5, 6, -7, 8, 9}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    rearrange(arr, n); 
    printArray(arr, n); 
    return 0; 
} 

```

## Java

```java

// A JAVA program to put positive numbers at even indexes 
// (0, 2, 4,..) and negative numbers at odd indexes (1, 3, 
// 5, ..) 
import java.io.*; 

class Alternate { 

    // The main function that rearranges elements of given 
    // array.  It puts positive elements at even indexes (0, 
    // 2, ..) and negative numbers at odd indexes (1, 3, ..). 
    static void rearrange(int arr[], int n) 
    { 
        // The following few lines are similar to partition 
        // process of QuickSort.  The idea is to consider 0 
        // as pivot and divide the array around it. 
        int i = -1, temp = 0; 
        for (int j = 0; j < n; j++) 
        { 
            if (arr[j] < 0) 
            { 
                i++; 
                temp = arr[i]; 
                arr[i] = arr[j]; 
                arr[j] = temp; 
            } 
        } 

        // Now all positive numbers are at end and negative numbers at 
        // the beginning of array. Initialize indexes for starting point 
        // of positive and negative numbers to be swapped 
        int pos = i+1, neg = 0; 

        // Increment the negative index by 2 and positive index by 1, i.e., 
        // swap every alternate negative number with next positive number 
        while (pos < n && neg < pos && arr[neg] < 0) 
        { 
            temp = arr[neg]; 
            arr[neg] = arr[pos]; 
            arr[pos] = temp; 
            pos++; 
            neg += 2; 
        } 
    } 

    // A utility function to print an array 
    static void printArray(int arr[], int n) 
    { 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i] + "   "); 
    } 

    /*Driver function to check for above functions*/
    public static void main (String[] args) 
    { 
        int arr[] = {-1, 2, -3, 4, 5, 6, -7, 8, 9}; 
        int n = arr.length; 
        rearrange(arr,n); 
        System.out.println("Array after rearranging: "); 
        printArray(arr,n); 
    } 
} 
/*This code is contributed by Devesh Agrawal*/

```

## Python

```py

#  Python program to put positive numbers at even indexes (0,  // 2, 4,..) and 
#  negative numbers at odd indexes (1, 3, 5, ..) 

# The main function that rearranges elements of given array.  
# It puts  positive elements at even indexes (0, 2, ..) and  
# negative numbers at odd indexes (1, 3, ..). 
def rearrange(arr, n): 
    # The following few lines are similar to partition process 
    # of QuickSort.  The idea is to consider 0 as pivot and 
    # divide the array around it. 
    i = -1
    for j in range(n): 
        if (arr[j] < 0): 
            i += 1
            # swapping of arr 
            arr[i], arr[j] = arr[j], arr[i] 

    # Now all positive numbers are at end and negative numbers 
    # at the beginning of array. Initialize indexes for starting 
    # point of positive and negative numbers to be swapped 
    pos, neg = i+1, 0

    # Increment the negative index by 2 and positive index by 1, 
    # i.e., swap every alternate negative number with next  
    # positive number 
    while (pos < n and neg < pos and arr[neg] < 0): 

        # swapping of arr 
        arr[neg], arr[pos] = arr[pos], arr[neg] 
        pos += 1
        neg += 2

# A utility function to print an array 
def printArray(arr, n): 

    for i in range(n): 
        print arr[i], 

# Driver program to test above functions 
arr = [-1, 2, -3, 4, 5, 6, -7, 8, 9] 
n = len(arr) 
rearrange(arr, n) 
printArray(arr, n) 

# Contributed by Afzal 

```

## C# 

```cs

// A C# program to put positive numbers 
// at even indexes (0, 2, 4, ..) and  
// negative numbers at odd indexes (1, 3, 5, ..) 
using System; 

class Alternate { 

    // The main function that rearranges elements  
    // of given array. It puts positive elements  
    // at even indexes (0, 2, ..) and negative  
    // numbers at odd indexes (1, 3, ..). 
    static void rearrange(int[] arr, int n) 
    { 
        // The following few lines are similar to partition 
        // process of QuickSort. The idea is to consider 0 
        // as pivot and divide the array around it. 
        int i = -1, temp = 0; 
        for (int j = 0; j < n; j++) { 
            if (arr[j] < 0) { 
                i++; 
                temp = arr[i]; 
                arr[i] = arr[j]; 
                arr[j] = temp; 
            } 
        } 

        // Now all positive numbers are at end  
        // and negative numbers at the beginning of  
        // array. Initialize indexes for starting point 
        // of positive and negative numbers to be swapped 
        int pos = i + 1, neg = 0; 

        // Increment the negative index by 2 and 
        // positive index by 1, i.e., swap every  
        // alternate negative number with next positive number 
        while (pos < n && neg < pos && arr[neg] < 0) { 
            temp = arr[neg]; 
            arr[neg] = arr[pos]; 
            arr[pos] = temp; 
            pos++; 
            neg += 2; 
        } 
    } 

    // A utility function to print an array 
    static void printArray(int[] arr, int n) 
    { 
        for (int i = 0; i < n; i++) 
            Console.Write(arr[i] + " "); 
    } 

    /*Driver function to check for above functions*/
    public static void Main() 
    { 
        int[] arr = { -1, 2, -3, 4, 5, 6, -7, 8, 9 }; 
        int n = arr.Length; 
        rearrange(arr, n); 
        printArray(arr, n); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// A PHP program to put positive numbers   
// at even indexes (0, 2, 4,..) and negative  
// numbers at odd indexes (1, 3, 5, ..)  

// The main function that rearranges elements  
// of given array. It puts positive elements  
// at even indexes (0, 2, ..) and negative 
// numbers at odd indexes (1, 3, ..).  
function rearrange(&$arr, $n)  
{  
    // The following few lines are similar  
    // to partition process of QuickSort.  
    // The idea is to consider 0 as pivot  
    // and divide the array around it.  
    $i = -1;  
    for ($j = 0; $j < $n; $j++)  
    {  
        if ($arr[$j] < 0)  
        {  
            $i++;  
            swap($arr[$i], $arr[$j]);  
        }  
    }  

    // Now all positive numbers are at end and  
    // negative numbers at the beginning of array.  
    // Initialize indexes for starting point of  
    // positive and negative numbers to be swapped  
    $pos = $i + 1; 
    $neg = 0;  

    // Increment the negative index by 2 and  
    // positive index by 1, i.e., swap every  
    // alternate negative number with next 
    // positive number  
    while ($pos < $n && $neg < $pos &&  
                        $arr[$neg] < 0)  
    {  
        swap($arr[$neg], $arr[$pos]);  
        $pos++;  
        $neg += 2;  
    }  
}  

// A utility function to swap two elements  
function swap(&$a, &$b)  
{  
    $temp = $a;  
    $a = $b;  
    $b = $temp;  
}  

// A utility function to print an array  
function printArray(&$arr, $n)  
{  
    for ($i = 0; $i < $n; $i++)  
        echo " " . $arr[$i] . " ";  
}  

// Driver Code 
$arr = array(-1, 2, -3, 4, 5, 6, -7, 8, 9);  
$n = count($arr);  
rearrange($arr, $n);  
printArray($arr, $n);  

// This code is contributed 
// by rathbhupendra 
?> 

```

**输出**：

```
    4   -3    5   -1    6   -7    2    8    9
```

**时间复杂度**：`O(n)`，其中`n`是给定数组中的元素数。

**辅助空间**：`O(1)`。

**相关文章**：

[以恒定的额外空间重新排列正数和负数](https://www.geeksforgeeks.org/rearrange-positive-and-negative-numbers/)

[将所有负数元素按顺序移动到末尾，并留出额外的空间](https://www.geeksforgeeks.org/move-ve-elements-end-order-extra-space-allowed/)




