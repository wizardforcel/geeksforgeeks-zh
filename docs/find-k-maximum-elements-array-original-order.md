# 以原始顺序查找数组的`k`个最大元素

> 原文： [https://www.geeksforgeeks.org/find-k-maximum-elements-array-original-order/](https://www.geeksforgeeks.org/find-k-maximum-elements-array-original-order/)

给定一个数组`arr[]`和一个整数`k`，我们需要打印给定数组的`k`个最大元素。 元素应按输入顺序打印。

**注意**： `k`始终小于或等于`n`。

例子：

```
Input : arr[] = {10 50 30 60 15}
        k = 2
Output : 50 60
The top 2 elements are printed
as per their appearance in original
array.

Input : arr[] = {50 8 45 12 25 40 84}
            k = 3
Output : 50 45 84

```



**方法 1**：我们在给定数组中搜索最大元素`k`次。 每次找到一个最大元素时，我们都会打印该元素，并在数组中使用负无穷大（在 C 中为`INT_MIN`）重新放置它。 该方法的时间复杂度为`O(n * k)`。

**方法 2**：在此方法中，我们将原始数组存储在一个新数组中，并将按降序对新数组进行排序。 排序后，我们将原始数组从 0 迭代到`n`，并打印出现在新数组的前`k`个元素中的所有那些元素。 对于搜索，我们可以执行[二分搜索](http://www.geeksforgeeks.org/binary-search/)。

## C++ 

```cpp

// CPP program to find k maximum elements  
// of array in original order 
#include <bits/stdc++.h> 
using namespace std; 

// Function to print m Maximum elements 
void printMax(int arr[], int k, int n) 
{ 
    // vector to store the copy of the 
    // original array 
    vector<int> brr(arr, arr + n); 

    // Sorting the vector in descending 
    // order. Please refer below link for 
    // details 
    // https://www.geeksforgeeks.org/sort-c-stl/ 
    sort(brr.begin(), brr.end(), greater<int>()); 

    // Traversing through original array and 
    // printing all those elements that are 
    // in first k of sorted vector. 
    // Please refer https://goo.gl/44Rwgt 
    // for details of binary_search() 
    for (int i = 0; i < n; ++i) 
        if (binary_search(brr.begin(), 
                 brr.begin() + k, arr[i],  
                        greater<int>())) 
            cout << arr[i] << " "; 
} 

// Driver code 
int main() 
{ 
    int arr[] = { 50, 8, 45, 12, 25, 40, 84 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int k = 3; 
    printMax(arr, k, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find k maximum   
// elements of array in original order 
import java.util.Arrays; 
import java.util.Collections; 

public class GfG { 

    // Function to print m Maximum elements 
    public static void printMax(int arr[], int k, int n) 
    { 
        // Array to store the copy  
        // of the original array 
        Integer[] brr = new Integer[n]; 

        for (int i = 0; i < n; i++) 
        brr[i] = arr[i]; 

        // Sorting the array in  
        // descending order 
        Arrays.sort(brr, Collections.reverseOrder()); 

        // Traversing through original array and 
        // printing all those elements that are 
        // in first k of sorted array. 
        // Please refer https://goo.gl/uj5RCD 
        // for details of Arrays.binarySearch() 
        for (int i = 0; i < n; ++i) 
            if (Arrays.binarySearch(brr, arr[i],  
                    Collections.reverseOrder()) >= 0
                 && Arrays.binarySearch(brr, arr[i],  
                    Collections.reverseOrder()) < k) 

                System.out.print(arr[i]+ " "); 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int arr[] = { 50, 8, 45, 12, 25, 40, 84 }; 
        int n = arr.length; 
        int k = 3; 
        printMax(arr, k, n); 
    } 
} 

// This code is contributed by Swetank Modi 

```

Output :

```
50 45 84 

```

时间复杂度：`O(N log N)`用于排序。

辅助空间：`O(n)`。



* * *

* * *



