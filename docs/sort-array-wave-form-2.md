# 以波形形式对数组进行排序

> 原文： [https://www.geeksforgeeks.org/sort-array-wave-form-2/](https://www.geeksforgeeks.org/sort-array-wave-form-2/)

给定一个未排序的整数数组，将该数组排序为类似波浪的数组。 如果`arr[0] >= arr[1] <= arr[2] >= arr[3] <= arr [4] >= …`，则数组`arr[0..n-1]`将以波形形式排序。 

例子：

```
 Input:  arr[] = {10, 5, 6, 3, 2, 20, 100, 80}
 Output: arr[] = {10, 5, 6, 2, 20, 3, 100, 80} OR
                 {20, 5, 10, 2, 80, 6, 100, 3} OR
                 any other array that is in wave form

 Input:  arr[] = {20, 10, 8, 6, 4, 2}
 Output: arr[] = {20, 8, 10, 4, 6, 2} OR
                 {10, 8, 20, 2, 6, 4} OR
                 any other array that is in wave form

 Input:  arr[] = {2, 4, 6, 8, 10, 20}
 Output: arr[] = {4, 2, 8, 6, 20, 10} OR
                 any other array that is in wave form

 Input:  arr[] = {3, 6, 5, 10, 7, 20}
 Output: arr[] = {6, 3, 10, 5, 20, 7} OR
                 any other array that is in wave form

```



**简单解决方案**将使用排序。 首先对输入数组进行排序，然后交换所有相邻元素。

例如，让输入数组为`{3, 6, 5, 10, 7, 20}`。 排序后，我们得到`{3, 5, 6, 7, 10, 20}`。 交换相邻元素后，我们得到`{5, 3, 7, 6, 6, 20, 10}`。

以下是此简单方法的实现。

## C++ 

```cpp

// A C++ program to sort an array in wave form using 
// a sorting function 
#include<iostream> 
#include<algorithm> 
using namespace std; 

// A utility method to swap two numbers. 
void swap(int *x, int *y) 
{ 
    int temp = *x; 
    *x = *y; 
    *y = temp; 
} 

// This function sorts arr[0..n-1] in wave form, i.e.,  
// arr[0] >= arr[1] <= arr[2] >= arr[3] <= arr[4] >= arr[5].. 
void sortInWave(int arr[], int n) 
{ 
    // Sort the input array 
    sort(arr, arr+n); 

    // Swap adjacent elements 
    for (int i=0; i<n-1; i += 2) 
        swap(&arr[i], &arr[i+1]); 
} 

// Driver program to test above function 
int main() 
{ 
    int arr[] = {10, 90, 49, 2, 1, 5, 23}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    sortInWave(arr, n); 
    for (int i=0; i<n; i++) 
       cout << arr[i] << " "; 
    return 0; 
} 

```

## Java

```java

// Java implementation of naive method for sorting 
// an array in wave form. 
import java.util.*; 

class SortWave 
{ 
    // A utility method to swap two numbers. 
    void swap(int arr[], int a, int b) 
    { 
        int temp = arr[a]; 
        arr[a] = arr[b]; 
        arr[b] = temp; 
    } 

    // This function sorts arr[0..n-1] in wave form, i.e., 
    // arr[0] >= arr[1] <= arr[2] >= arr[3] <= arr[4].. 
    void sortInWave(int arr[], int n) 
    { 
        // Sort the input array 
        Arrays.sort(arr); 

        // Swap adjacent elements 
        for (int i=0; i<n-1; i += 2) 
            swap(arr, i, i+1); 
    } 

    // Driver method 
    public static void main(String args[]) 
    { 
        SortWave ob = new SortWave(); 
        int arr[] = {10, 90, 49, 2, 1, 5, 23}; 
        int n = arr.length; 
        ob.sortInWave(arr, n); 
        for (int i : arr) 
            System.out.print(i + " "); 
    } 
} 
/*This code is contributed by Rajat Mishra*/

```

## Python

```py

# Python function to sort the array arr[0..n-1] in wave form, 
# i.e., arr[0] >= arr[1] <= arr[2] >= arr[3] <= arr[4] >= arr[5] 
def sortInWave(arr, n): 

    #sort the array 
    arr.sort() 

    # Swap adjacent elements 
    for i in range(0,n-1,2): 
        arr[i], arr[i+1] = arr[i+1], arr[i] 

# Driver progrM 
arr = [10, 90, 49, 2, 1, 5, 23] 
sortInWave(arr, len(arr)) 
for i in range(0,len(arr)): 
    print arr[i], 

# This code is contributed by __Devesh Agrawal__ 

```

## C# 

```cs

// C# implementation of naive method  
// for sorting an array in wave form. 
using System; 

class SortWave { 

    // A utility method to swap two numbers. 
    void swap(int[] arr, int a, int b) 
    { 
        int temp = arr[a]; 
        arr[a] = arr[b]; 
        arr[b] = temp; 
    } 

    // This function sorts arr[0..n-1] in wave form, i.e., 
    // arr[0] >= arr[1] <= arr[2] >= arr[3] <= arr[4].. 
    void sortInWave(int[] arr, int n) 
    { 
        // Sort the input array 
        Array.Sort(arr); 

        // Swap adjacent elements 
        for (int i = 0; i < n - 1; i += 2) 
            swap(arr, i, i + 1); 
    } 

    // Driver method 
    public static void Main() 
    { 
        SortWave ob = new SortWave(); 
        int[] arr = { 10, 90, 49, 2, 1, 5, 23 }; 
        int n = arr.Length; 

        ob.sortInWave(arr, n); 
        for (int i = 0; i < n; i++) 
        Console.Write(arr[i] + " "); 
    } 
} 

// This code is contributed by vt_m. 

```

Output:

```
2 1 10 5 49 23 90
```

如果使用诸如[归并排序](http://geeksquiz.com/merge-sort/)，[堆排序](http://geeksquiz.com/heap-sort/)等的`O(nLogn)`排序算法，则上述解决方案的时间复杂度为`O(nLogn)`。

通过对给定数组进行单次遍历，可以在`O(n)`时间内完成此操作。 这个想法基于这样一个事实：如果我们确保所有偶数定位（在索引 0、2、4，..）的元素都大于其相邻的奇数元素，则无需担心奇数定位的元素。 以下是简单的步骤。

1.  遍历输入数组的所有偶数定位元素，然后执行以下操作。

    1.  如果当前元素小于前一个奇数元素，则交换前一个和当前元素。

    2.  如果当前元素小于下一个奇数元素，则交换下一个和当前。

以下是上述简单算法的实现。

## C++

```cpp

// A O(n) program to sort an input array in wave form 
#include<iostream> 
using namespace std; 

// A utility method to swap two numbers. 
void swap(int *x, int *y) 
{ 
    int temp = *x; 
    *x = *y; 
    *y = temp; 
} 

// This function sorts arr[0..n-1] in wave form, i.e., arr[0] >=  
// arr[1] <= arr[2] >= arr[3] <= arr[4] >= arr[5] .... 
void sortInWave(int arr[], int n) 
{ 
    // Traverse all even elements 
    for (int i = 0; i < n; i+=2) 
    { 
        // If current even element is smaller than previous 
        if (i>0 && arr[i-1] > arr[i] ) 
            swap(&arr[i], &arr[i-1]); 

        // If current even element is smaller than next 
        if (i<n-1 && arr[i] < arr[i+1] ) 
            swap(&arr[i], &arr[i + 1]); 
    } 
} 

// Driver program to test above function 
int main() 
{ 
    int arr[] = {10, 90, 49, 2, 1, 5, 23}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    sortInWave(arr, n); 
    for (int i=0; i<n; i++) 
       cout << arr[i] << " "; 
    return 0; 
} 

```

## Java

```java

// A O(n) Java program to sort an input array in wave form 
class SortWave 
{ 
    // A utility method to swap two numbers. 
    void swap(int arr[], int a, int b) 
    { 
        int temp = arr[a]; 
        arr[a] = arr[b]; 
        arr[b] = temp; 
    } 

    // This function sorts arr[0..n-1] in wave form, i.e., 
    // arr[0] >= arr[1] <= arr[2] >= arr[3] <= arr[4].... 
    void sortInWave(int arr[], int n) 
    { 
        // Traverse all even elements 
        for (int i = 0; i < n; i+=2) 
        { 
            // If current even element is smaller 
            // than previous 
            if (i>0 && arr[i-1] > arr[i] ) 
                swap(arr, i-1, i); 

            // If current even element is smaller 
            // than next 
            if (i<n-1 && arr[i] < arr[i+1] ) 
                swap(arr, i, i + 1); 
        } 
    } 

    // Driver program to test above function 
    public static void main(String args[]) 
    { 
        SortWave ob = new SortWave(); 
        int arr[] = {10, 90, 49, 2, 1, 5, 23}; 
        int n = arr.length; 
        ob.sortInWave(arr, n); 
        for (int i : arr) 
            System.out.print(i+" "); 
    } 
} 
/*This code is contributed by Rajat Mishra*/

```

## Python

```py

# Python function to sort the array arr[0..n-1] in wave form, 
# i.e., arr[0] >= arr[1] <= arr[2] >= arr[3] <= arr[4] >= arr[5] 
def sortInWave(arr, n): 

    # Traverse all even elements 
    for i in range(0, n, 2): 

        # If current even element is smaller than previous 
        if (i> 0 and arr[i] < arr[i-1]): 
            arr[i],arr[i-1] = arr[i-1],arr[i] 

        # If current even element is smaller than next 
        if (i < n-1 and arr[i] < arr[i+1]): 
            arr[i],arr[i+1] = arr[i+1],arr[i] 

# Driver program 
arr = [10, 90, 49, 2, 1, 5, 23] 
sortInWave(arr, len(arr)) 
for i in range(0,len(arr)): 
    print arr[i], 

# This code is contributed by __Devesh Agrawal__ 

```

## C#

```cs

// A O(n) C# program to sort an 
// input array in wave form 
using System; 

class SortWave { 

    // A utility method to swap two numbers. 
    void swap(int[] arr, int a, int b) 
    { 
        int temp = arr[a]; 
        arr[a] = arr[b]; 
        arr[b] = temp; 
    } 

    // This function sorts arr[0..n-1] in wave form, i.e., 
    // arr[0] >= arr[1] <= arr[2] >= arr[3] <= arr[4].... 
    void sortInWave(int[] arr, int n) 
    { 
        // Traverse all even elements 
        for (int i = 0; i < n; i += 2) { 

            // If current even element is smaller 
            // than previous 
            if (i > 0 && arr[i - 1] > arr[i]) 
                swap(arr, i - 1, i); 

            // If current even element is smaller 
            // than next 
            if (i < n - 1 && arr[i] < arr[i + 1]) 
                swap(arr, i, i + 1); 
        } 
    } 

    // Driver program to test above function 
    public static void Main() 
    { 
        SortWave ob = new SortWave(); 
        int[] arr = { 10, 90, 49, 2, 1, 5, 23 }; 
        int n = arr.Length; 

        ob.sortInWave(arr, n); 
        for (int i = 0; i < n; i++) 
        Console.Write(arr[i] + " "); 
    } 
} 

// This code is contributed by vt_m. 

```

输出：

```
90 10 49 1 5 2 23
```

