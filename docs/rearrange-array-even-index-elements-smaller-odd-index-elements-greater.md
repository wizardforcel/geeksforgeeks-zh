# 重新排列数组，使偶数索引元素较小而奇数索引元素较大

> 原文： [https://www.geeksforgeeks.org/rearrange-array-even-index-elements-smaller-odd-index-elements-greater/](https://www.geeksforgeeks.org/rearrange-array-even-index-elements-smaller-odd-index-elements-greater/)

给定一个数组，重新排列数组，使得：

1.  如果索引`i`为偶数，则`arr[i] <= arr[i + 1]`

2.  如果索引`i`为奇数，则`arr[i] >= arr[i + 1]`

**注意**：可以有多个答案。

**示例**：

```
Input  : arr[] = {2, 3, 4, 5} 
Output : arr[] = {2, 4, 3, 5}
Explanation : Elements at even indexes are
smaller and elements at odd indexes are greater
than their next elements

Note : Another valid answer
is arr[] = {3, 4, 2, 5}

Input  :arr[] = {6, 4, 2, 1, 8, 3}
Output :arr[] = {4, 6, 1, 8, 2, 3}

```



此问题类似于[以波形](https://www.geeksforgeeks.org/sort-array-wave-form-2/)对数组进行排序。

**简单解决方案**是按降序对数组进行排序，然后从第二个元素开始，交换相邻元素。

一种有效的**解决方案**是根据给定条件遍历数组并交换元素。如果我们有一个长度为`n`的数组，那么我们将从索引 0 迭代到`n-2`并检查给定条件。在任何时间点，如果`i`为偶数且`arr[i] > arr[i + 1]`，则我们交换`arr[i]`和`arr[i + 1]`。 类似地，如果`i`为奇数并且`arr[i] < arr[i + 1]`，则我们交换`arr[i]`和`arr[i + 1]`。

对于给定的示例：重排之前，`arr[] = {2, 3, 4, 5}`，开始遍历数组直到索引 2（`n = 4`）

**第一步**：

在`i = 0`时，`arr[i] = 2`且`arr [i + 1] = 3`。当`i`为偶数且`arr[i] < arr[i + 1]`时，无需交换。

**第二步**：

在`i = 1`时，`arr[i] = 3`且`arr[i + 1] = 4`。由于`i`为奇数且`arr[i] < arr[i + 1]`，将它们交换。

现在`arr [] = {2, 4, 3, 5}`。

**第三步**：

在`i = 2`时，`arr[i] = 3`且`arr[i + 1] = 5`。因此，无需交换它们。

重新排列后，`arr[] = {2, 4, 3, 5}`。

## C++ 

```cpp

// CPP code to rearrange an array such that 
// even index elements are smaller and odd 
// index elements are greater than their 
// next. 
#include <iostream> 
using namespace std; 

void rearrange(int* arr, int n) 
{ 
    for (int i = 0; i < n - 1; i++) { 
        if (i % 2 == 0 && arr[i] > arr[i + 1]) 
            swap(arr[i], arr[i + 1]); 

        if (i % 2 != 0 && arr[i] < arr[i + 1]) 
            swap(arr[i], arr[i + 1]); 
    } 
} 

/* Utility that prints out an array in 
   a line */
void printArray(int arr[], int size) 
{ 
    for (int i = 0; i < size; i++) 
        cout << arr[i] << " "; 

    cout << endl; 
} 

/* Driver function to test above functions */
int main() 
{ 
    int arr[] = { 6, 4, 2, 1, 8, 3 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    cout << "Before rearranging: \n"; 
    printArray(arr, n); 

    rearrange(arr, n); 

    cout << "After rearranging: \n"; 
    printArray(arr, n); 

    return 0; 
} 

```

## Java

```java

// Java code to rearrange an array such 
// that even index elements are smaller 
// and odd index elements are greater 
// than their next. 

class GFG { 

    static void rearrange(int arr[], int n) 
    { 

        int temp; 
        for (int i = 0; i < n - 1; i++) { 
            if (i % 2 == 0 && arr[i] > arr[i + 1]) { 
                temp = arr[i]; 
                arr[i] = arr[i + 1]; 
                arr[i + 1] = temp; 
            } 
            if (i % 2 != 0 && arr[i] < arr[i + 1]) { 
                temp = arr[i]; 
                arr[i] = arr[i + 1]; 
                arr[i + 1] = temp; 
            } 
        } 
    } 

    /* Utility that prints out an array in 
    a line */
    static void printArray(int arr[], int size) 
    { 
        for (int i = 0; i < size; i++) 
            System.out.print(arr[i] + " "); 

        System.out.println(); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int arr[] = { 6, 4, 2, 1, 8, 3 }; 
        int n = arr.length; 

        System.out.print("Before rearranging: \n"); 
        printArray(arr, n); 

        rearrange(arr, n); 

        System.out.print("After rearranging: \n"); 
        printArray(arr, n); 
    } 
} 

// This code is contributed by Anant Agarwal. 

```

## Python3

```py

# Python code to rearrange 
# an array such that 
# even index elements 
# are smaller and odd  
# index elements are 
# greater than their  
# next. 

def rearrange(arr, n): 

    for i in range(n - 1): 
        if (i % 2 == 0 and arr[i] > arr[i + 1]): 

            temp = arr[i] 
            arr[i]= arr[i + 1] 
            arr[i + 1]= temp 

        if (i % 2 != 0 and arr[i] < arr[i + 1]): 

            temp = arr[i] 
            arr[i]= arr[i + 1] 
            arr[i + 1]= temp 

# Utility that prints out an array in 
# a line  
def printArray(arr, size): 

    for i in range(size): 
        print(arr[i], " ", end ="") 

    print() 

# Driver code 

arr = [ 6, 4, 2, 1, 8, 3 ] 
n = len(arr) 

print("Before rearranging: ") 
printArray(arr, n) 

rearrange(arr, n) 

print("After rearranging:") 
printArray(arr, n); 

# This code is contributed 
# by Anant Agarwal. 

```

## C# 

```cs

// C# code to rearrange an array such 
// that even index elements are smaller 
// and odd index elements are greater 
// than their next. 
using System; 

class GFG { 

    static void rearrange(int[] arr, int n) 
    { 
        int temp; 
        for (int i = 0; i < n - 1; i++) { 
            if (i % 2 == 0 && arr[i] > arr[i + 1]) 
            { 
                temp = arr[i]; 
                arr[i] = arr[i + 1]; 
                arr[i + 1] = temp; 
            } 

            if (i % 2 != 0 && arr[i] < arr[i + 1]) 
            { 
                temp = arr[i]; 
                arr[i] = arr[i + 1]; 
                arr[i + 1] = temp; 
            } 
        } 
    } 

    /* Utility that prints out an array in 
    a line */
    static void printArray(int[] arr, int size) 
    { 
        for (int i = 0; i < size; i++) 
            Console.Write(arr[i] + " "); 

        Console.WriteLine(); 
    } 

    // Driver code 
    public static void Main() 
    { 
        int[] arr = { 6, 4, 2, 1, 8, 3 }; 
        int n = arr.Length; 

        Console.WriteLine("Before rearranging: "); 
        printArray(arr, n); 

        rearrange(arr, n); 

        Console.WriteLine("After rearranging: "); 
        printArray(arr, n); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php  
// PHP code to rearrange an array such  
// that even index elements are smaller  
// and odd index elements are greater  
// than their next. 

function swap(&$a, &$b) 
{ 
    $temp = $a; 
    $a = $b; 
    $b = $temp; 
} 
function rearrange(&$arr, $n) 
{ 
    for ($i = 0; $i < $n - 1; $i++)  
    { 
        if ($i % 2 == 0 &&  
            $arr[$i] > $arr[$i + 1]) 
            swap($arr[$i], $arr[$i + 1]); 

        if ($i % 2 != 0 &&  
            $arr[$i] < $arr[$i + 1]) 
            swap($arr[$i], $arr[$i + 1]); 
    } 
} 

/* Utility that prints out  
an array in a line */
function printArray(&$arr, $size) 
{ 
    for ($i = 0; $i < $size; $i++) 
        echo $arr[$i] . " "; 

    echo "\n"; 
} 

// Driver Code 
$arr = array(6, 4, 2, 1, 8, 3 ); 
$n = sizeof($arr); 

echo "Before rearranging: \n"; 
printArray($arr, $n); 

rearrange($arr, $n); 

echo "After rearranging: \n"; 
printArray($arr, $n); 

// This code is contributed  
// by ChitraNayal 
?> 

```

**输出**：

```
Before rearranging:
6 4 2 1 8 3
After rearranging:
4 6 1 8 2 3

```

**时间复杂度**：`O(n)`。

**参考**：

[describe.codechef.com/questions/43062/anuund-editorial](http://discuss.codechef.com/questions/43062/anuund-editorial)

