# 检查反转子数组是否使数组有序

> 原文： [https://www.geeksforgeeks.org/check-reversing-sub-array-make-array-sorted/](https://www.geeksforgeeks.org/check-reversing-sub-array-make-array-sorted/)

给定一个由`n`个整数组成的数组。 任务是检查反转一个子数组是否使该数组排序。 如果已对数组进行排序或通过对子数组进行排序后反转该数组，则打印`Yes`，否则打印`No`。

**示例**：

```
Input : arr [] = {1, 2, 5, 4, 3}
Output : Yes
By reversing the subarray {5, 4, 3}, 
the array will be sorted.

Input : arr [] = { 1, 2, 4, 5, 3 }
Output : No

```



**方法 1（简单：`O(n^2)`）**：

一个简单的解决方案是逐个考虑每个子数组，尝试反转每个子数组，并检查反转子数组是否构成整体。如果是，则返回`true`；如果反转任何子数组都不能使数组排序，则返回`false`。

**方法 2（排序：`O(nLogn)`）**：

这个想法是将给定数组与排序数组进行比较。 复制给定数组并将其排序。 现在，找到与排序数组不匹配的第一个索引和最后一个索引。 如果找不到这样的索引，请打印`Yes`。 否则检查索引之间的元素是否按降序排列。

下面是上述方法的实现：

## C++ 

```cpp

// C++ program to check whether reversing a 
// sub array make the array sorted or not 
#include<bits/stdc++.h> 
using namespace std; 

// Return true, if reversing the subarray will 
// sort the array, else return false. 
bool checkReverse(int arr[], int n) 
{ 
    // Copying the array. 
    int temp[n]; 
    for (int i = 0; i < n; i++) 
        temp[i] = arr[i]; 

    // Sort the copied array. 
    sort(temp, temp + n); 

    // Finding the first mismatch. 
    int front; 
    for (front = 0; front < n; front++) 
        if (temp[front] != arr[front]) 
            break; 

    // Finding the last mismatch. 
    int back; 
    for (back = n - 1; back >= 0; back--) 
        if (temp[back] != arr[back]) 
            break; 

    // If whole array is sorted 
    if (front >= back) 
        return true; 

    // Checking subarray is decreasing or not. 
    do
    { 
        front++; 
        if (arr[front - 1] < arr[front]) 
            return false; 
    } while (front != back); 

    return true; 
} 

// Driven Program 
int main() 
{ 
    int arr[] = { 1, 2, 5, 4, 3 }; 
    int n = sizeof(arr)/sizeof(arr[0]); 

    checkReverse(arr, n)? (cout << "Yes" << endl): 
                          (cout << "No" << endl); 
    return 0; 
} 

```

## Java

```java

// Java program to check whether reversing a  
// sub array make the array sorted or not 

import java.util.Arrays; 

class GFG { 

// Return true, if reversing the subarray will  
// sort the array, else return false.  
    static boolean checkReverse(int arr[], int n) { 
        // Copying the array.  
        int temp[] = new int[n]; 
        for (int i = 0; i < n; i++) { 
            temp[i] = arr[i]; 
        } 

        // Sort the copied array.  
        Arrays.sort(temp); 

        // Finding the first mismatch.  
        int front; 
        for (front = 0; front < n; front++) { 
            if (temp[front] != arr[front]) { 
                break; 
            } 
        } 

        // Finding the last mismatch.  
        int back; 
        for (back = n - 1; back >= 0; back--) { 
            if (temp[back] != arr[back]) { 
                break; 
            } 
        } 

        // If whole array is sorted  
        if (front >= back) { 
            return true; 
        } 

        // Checking subarray is decreasing or not.  
        do { 
            front++; 
            if (arr[front - 1] < arr[front]) { 
                return false; 
            } 
        } while (front != back); 

        return true; 
    } 

// Driven Program  
    public static void main(String[] args) { 

        int arr[] = {1, 2, 5, 4, 3}; 
        int n = arr.length; 

        if (checkReverse(arr, n)) { 
            System.out.print("Yes"); 
        } else { 
            System.out.print("No"); 
        } 
    } 

} 
//This code contributed by 29AjayKumar  

```

## Python3

```py

# Python3 program to check whether  
# reversing a sub array make the 
# array sorted or not 

# Return true, if reversing the  
# subarray will sort the array,  
# else return false.  
def checkReverse(arr, n): 

    # Copying the array 
    temp = [0] * n 
    for i in range(n): 
        temp[i] = arr[i] 

    # Sort the copied array.  
    temp.sort() 

    # Finding the first mismatch.  
    for front in range(n): 
        if temp[front] != arr[front]: 
            break

    # Finding the last mismatch.  
    for back in range(n - 1, -1, -1): 
        if temp[back] != arr[back]: 
            break

    #If whole array is sorted 
    if front >= back: 
        return True
    while front != back: 
        front += 1
        if arr[front - 1] < arr[front]: 
            return False
    return True

# Driver code 
arr = [1, 2, 5, 4, 3] 
n = len(arr) 
if checkReverse(arr, n) == True: 
    print("Yes") 
else: 
    print("No") 

# This code is contributed  
# by Shrikant13 

```

## C# 

```cs

// C# program to check whether reversing a  
// sub array make the array sorted or not 
using System; 

class GFG 
{ 

// Return true, if reversing the  
// subarray will sort the array, 
// else return false.  
static bool checkReverse(int []arr, int n)  
{ 
    // Copying the array.  
    int []temp = new int[n]; 
    for (int i = 0; i < n; i++)  
    { 
        temp[i] = arr[i]; 
    } 

    // Sort the copied array.  
    Array.Sort(temp); 

    // Finding the first mismatch.  
    int front; 
    for (front = 0; front < n; front++) 
    { 
        if (temp[front] != arr[front]) 
        { 
            break; 
        } 
    } 

    // Finding the last mismatch.  
    int back; 
    for (back = n - 1; back >= 0; back--)  
    { 
        if (temp[back] != arr[back]) 
        { 
            break; 
        } 
    } 

    // If whole array is sorted  
    if (front >= back) 
    { 
        return true; 
    } 

    // Checking subarray is decreasing 
    // or not.  
    do 
    { 
        front++; 
        if (arr[front - 1] < arr[front]) 
        { 
            return false; 
        } 
    } while (front != back); 

    return true; 
} 

// Driven Program  
public static void Main()  
{ 
    int []arr = {1, 2, 5, 4, 3}; 
    int n = arr.Length; 

    if (checkReverse(arr, n))  
    { 
        Console.Write("Yes"); 
    }  
    else 
    { 
        Console.Write("No"); 
    } 
} 
} 

// This code is contributed 
// by PrinciRaj 

```

## PHP

```php

<?php 
// PHP program to check whether reversing a 
// sub array make the array sorted or not 

// Return true, if reversing the subarray  
// will sort the array, else return false. 
function checkReverse($arr, $n) 
{ 
    // Copying the array. 
    $temp[$n] = array(); 
    for ($i = 0; $i < $n; $i++) 
        $temp[$i] = $arr[$i]; 

    // Sort the copied array. 
    sort($temp, 0); 

    // Finding the first mismatch. 
    $front; 
    for ($front = 0; $front < $n; $front++) 
        if ($temp[$front] != $arr[$front]) 
            break; 

    // Finding the last mismatch. 
    $back; 
    for ($back = $n - 1; $back >= 0; $back--) 
        if ($temp[$back] != $arr[$back]) 
            break; 

    // If whole array is sorted 
    if ($front >= $back) 
        return true; 

    // Checking subarray is decreasing or not. 
    do
    { 
        $front++; 
        if ($arr[$front - 1] < $arr[$front]) 
            return false; 
    } while ($front != $back); 

    return true; 
} 

// Driver Code 
$arr = array( 1, 2, 5, 4, 3 ); 
$n = sizeof($arr); 

if(checkReverse($arr, $n)) 
    echo "Yes" . "\n"; 
else
    echo "No" . "\n"; 

// This code is contributed 
// by Akanksha Rai 
?> 

```

**输出**：

```
Yes

```

**时间复杂度**：`O(nLogn)`。

**方法 3（线性：`O(n)`）**：

观察到，对数组进行排序或数组由三部分组成时，答案为`Yes`。 第一部分是增加子数组，然后减少子数组，然后再次增加子数组。 因此，我们需要检查数组包含递增元素，然后包含递减元素，然后递增元素。 在其他所有情况下，答案均为`No`。

以下是此方法的实现：

## C++

```cpp

// C++ program to check whether reversing a sub array 
// make the array sorted or not 
#include<bits/stdc++.h> 
using namespace std; 

// Return true, if reversing the subarray will sort t 
// he array, else return false. 
bool checkReverse(int arr[], int n) 
{ 
    if (n == 1) 
        return true; 

    // Find first increasing part 
    int i; 
    for (i=1; i < n && arr[i-1] < arr[i]; i++); 
    if (i == n) 
        return true; 

    // Find reversed part 
    int j = i; 
    while (j < n && arr[j] < arr[j-1]) 
    { 
        if (i > 1 && arr[j] < arr[i-2]) 
            return false; 
        j++; 
    } 

    if (j == n) 
        return true; 

    // Find last increasing part 
    int k = j; 

    // To handle cases like {1,2,3,4,20,9,16,17} 
    if (arr[k] < arr[i-1]) 
       return false; 

    while (k > 1 && k < n) 
    { 
        if (arr[k] < arr[k-1]) 
            return false; 
        k++; 
    } 
    return true; 
} 

// Driven Program 
int main() 
{ 
    int arr[] = {1, 3, 4, 10, 9, 8}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    checkReverse(arr, n)? cout << "Yes" : cout << "No"; 
    return 0; 
} 

```

## Java

```java
// Java program to check whether reversing a sub array  
// make the array sorted or not 
  
class GFG { 
  
// Return true, if reversing the subarray will sort t  
// he array, else return false.  
    static boolean checkReverse(int arr[], int n) { 
        if (n == 1) { 
            return true; 
        } 
  
        // Find first increasing part  
        int i; 
        for (i = 1; arr[i - 1] < arr[i] && i < n; i++); 
        if (i == n) { 
            return true; 
        } 
  
        // Find reversed part  
        int j = i; 
        while (j < n && arr[j] < arr[j - 1]) { 
            if (i > 1 && arr[j] < arr[i - 2]) { 
                return false; 
            } 
            j++; 
        } 
  
        if (j == n) { 
            return true; 
        } 
  
        // Find last increasing part  
        int k = j; 
  
        // To handle cases like {1,2,3,4,20,9,16,17}  
        if (arr[k] < arr[i - 1]) { 
            return false; 
        } 
  
        while (k > 1 && k < n) { 
            if (arr[k] < arr[k - 1]) { 
                return false; 
            } 
            k++; 
        } 
        return true; 
    } 
  
// Driven Program  
    public static void main(String[] args) { 
  
        int arr[] = {1, 3, 4, 10, 9, 8}; 
        int n = arr.length; 
  
        if (checkReverse(arr, n)) { 
            System.out.print("Yes"); 
        } else { 
            System.out.print("No"); 
        } 
    } 
  
} 
  
// This code is contributed 
// by Rajput-Ji
```

## Python3

```py
# Python3 program to check whether reversing  
# a sub array make the array sorted or not 
import math as mt 
  
# Return True, if reversing the subarray  
# will sort the array, else return False. 
def checkReverse(arr, n): 
  
    if (n == 1): 
        return True
  
    # Find first increasing part 
    i = 1
    for i in range(1, n): 
        if arr[i - 1] < arr[i] : 
            if (i == n): 
                return True
           
        else:  
            break
  
    # Find reversed part 
    j = i 
    while (j < n and arr[j] < arr[j - 1]): 
       
        if (i > 1 and arr[j] < arr[i - 2]): 
            return False
        j += 1
  
    if (j == n): 
        return True
  
    # Find last increasing part 
    k = j 
  
    # To handle cases like 1,2,3,4,20,9,16,17 
    if (arr[k] < arr[i - 1]): 
        return False
  
    while (k > 1 and k < n): 
      
        if (arr[k] < arr[k - 1]): 
            return False
        k += 1
      
    return True
  
# Driver Code 
arr = [ 1, 3, 4, 10, 9, 8] 
n = len(arr) 
if checkReverse(arr, n): 
    print("Yes") 
else: 
    print("No") 
          
# This code is contributed by  
# Mohit kumar 29
```

## C#

```cs
// C# program to check whether reversing a  
// sub array make the array sorted or not 
   
using System; 
public class GFG{ 
  
// Return true, if reversing the subarray will sort t  
// he array, else return false.  
    static bool checkReverse(int []arr, int n) { 
        if (n == 1) { 
            return true; 
        } 
  
        // Find first increasing part  
        int i; 
        for (i = 1; arr[i - 1] < arr[i] && i < n; i++); 
        if (i == n) { 
            return true; 
        } 
  
        // Find reversed part  
        int j = i; 
        while (j < n && arr[j] < arr[j - 1]) { 
            if (i > 1 && arr[j] < arr[i - 2]) { 
                return false; 
            } 
            j++; 
        } 
  
        if (j == n) { 
            return true; 
        } 
  
        // Find last increasing part  
        int k = j; 
  
        // To handle cases like {1,2,3,4,20,9,16,17}  
        if (arr[k] < arr[i - 1]) { 
            return false; 
        } 
  
        while (k > 1 && k < n) { 
            if (arr[k] < arr[k - 1]) { 
                return false; 
            } 
            k++; 
        } 
        return true; 
    } 
  
  
// Driven Program  
    public static void Main() { 
  
        int []arr = {1, 3, 4, 10, 9, 8}; 
        int n = arr.Length; 
  
        if (checkReverse(arr, n)) { 
            Console.Write("Yes"); 
        } else { 
            Console.Write("No"); 
        } 
    } 
} 
// This code is contributed 
// by 29AjayKumar
```

## PHP

```php
<?php 
// PHP program to check whether reversing  
// a sub array make the array sorted or not 
  
// Return true, if reversing the subarray  
// will sort the array, else return false. 
function checkReverse($arr, $n) 
{ 
    if ($n == 1) 
        return true; 
  
    // Find first increasing part 
    for ($i = 1;  
         $i < $n && $arr[$i - 1] < $arr[$i];  
         $i++); 
    if ($i == $n) 
        return true; 
  
    // Find reversed part 
    $j = $i; 
    while ($arr[$j] < $arr[$j - 1]) 
    { 
        if ($i > 1 && $arr[$j] < $arr[$i - 2]) 
            return false; 
        $j++; 
    } 
  
    if ($j == $n) 
        return true; 
  
    // Find last increasing part 
    $k = $j; 
  
    // To handle cases like {1,2,3,4,20,9,16,17} 
    if ($arr[$k] < $arr[$i - 1]) 
    return false; 
  
    while ($k > 1 && $k < $n) 
    { 
        if ($arr[$k] < $arr[$k - 1]) 
            return false; 
        $k++; 
    } 
    return true; 
} 
  
// Driver Code 
$arr = array(1, 3, 4, 10, 9, 8); 
$n = sizeof($arr); 
if(checkReverse($arr, $n)) 
    echo "Yes"; 
else
    echo "No"; 
  
// This code is contributed 
// by Akanksha Rai(Abby_akku) 
?>
```

输出：

```
Yes
```

时间复杂度：`O(n)`。