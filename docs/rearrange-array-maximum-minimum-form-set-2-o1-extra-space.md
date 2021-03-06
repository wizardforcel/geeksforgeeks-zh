# 以最大最小形式重新排列数组 | 系列 2（`O(1)`额外空间）

> 原文： [https://www.geeksforgeeks.org/rearrange-array-maximum-minimum-form-set-2-o1-extra-space/](https://www.geeksforgeeks.org/rearrange-array-maximum-minimum-form-set-2-o1-extra-space/)

给定一个带正整数的排序数组，请交替排列数组，即第一个元素应该是最大值，第二小值，第三秒最大值，第四秒最小值等等。

**示例**：

**输入**：`arr[] = {1, 2, 3, 4, 5, 6, 7}`

**输出**：`arr[] = {7, 1, 6, 2 , 5, 3, 4}`

**输入**：`arr[] = {1, 2, 3, 4, 5, 6}`

**输出**：`arr[] = {6, 1, 5, 2, 4 , 3}`

我们在下面的文章中讨论了一个解决方案：

[**以最大最小值形式重新排列数组 | 系列 1**](https://www.geeksforgeeks.org/rearrange-array-maximum-minimum-form/)：这里讨论的解决方案需要额外的空间，如何使用`O(1)`额外的空间解决此问题。



在本文中，将讨论需要`O(n)`时间和`O(1)`额外空间的解决方案。 想法是使用乘法和模块化技巧在索引处存储两个元素。

```
even index : remaining maximum element.
odd index  : remaining minimum element.

max_index : Index of remaining maximum element
            (Moves from right to left)
min_index : Index of remaining minimum element
            (Moves from left to right)

Initialize: max_index = 'n-1'
            min_index = 0  
            max_element = arr[max_index] + 1 //can be any element which is more than the maximum value in array

For i = 0 to n-1            
    If 'i' is even
       arr[i] += arr[max_index] % max_element * max_element 
       max_index--     
    ELSE // if 'i' is odd
       arr[i] +=  arr[min_index] % max_element * max_element
       min_index++

```

表达式`arr[i] += arr[max_index] % max_element * max_element`如何工作？

此表达式的目的是在索引`arr[i]`中存储两个元素。`arr[max_index]`被存储为乘数，而`arr[i]`则被存储为余数。 例如，在`{1 2 3 4 5 6 7 8 9}`中，`max_element`为 10，我们在索引 0 处存储 91。使用 91，我们可以将原始元素获取为`91 % 10`，将新元素获取为`91/10`。

下面实现以上思路：

## C++ 

```cpp

// C++ program to rearrange an array in minimum 
// maximum form 
#include <bits/stdc++.h> 
using namespace std; 

// Prints max at first position, min at second position 
// second max at third position, second min at fourth 
// position and so on. 
void rearrange(int arr[], int n) 
{ 
    // initialize index of first minimum and first 
    // maximum element 
    int max_idx = n - 1, min_idx = 0; 

    // store maximum element of array 
    int max_elem = arr[n - 1] + 1; 

    // traverse array elements 
    for (int i = 0; i < n; i++) { 
        // at even index : we have to put maximum element 
        if (i % 2 == 0) { 
            arr[i] += (arr[max_idx] % max_elem) * max_elem; 
            max_idx--; 
        } 

        // at odd index : we have to put minimum element 
        else { 
            arr[i] += (arr[min_idx] % max_elem) * max_elem; 
            min_idx++; 
        } 
    } 

    // array elements back to it's original form 
    for (int i = 0; i < n; i++) 
        arr[i] = arr[i] / max_elem; 
} 

// Driver program to test above function 
int main() 
{ 
    int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    cout << "Original Arrayn"; 
    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 

    rearrange(arr, n); 

    cout << "\nModified Array\n"; 
    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 
    return 0; 
} 

```

## Java

```java

// Java program to rearrange an 
// array in minimum maximum form 

public class Main { 

    // Prints max at first position, min at second 
    // position second max at third position, second 
    // min at fourth position and so on. 
    public static void rearrange(int arr[], int n) 
    { 
        // initialize index of first minimum and first 
        // maximum element 
        int max_idx = n - 1, min_idx = 0; 

        // store maximum element of array 
        int max_elem = arr[n - 1] + 1; 

        // traverse array elements 
        for (int i = 0; i < n; i++) { 
            // at even index : we have to put 
            // maximum element 
            if (i % 2 == 0) { 
                arr[i] += (arr[max_idx] % max_elem) * max_elem; 
                max_idx--; 
            } 

            // at odd index : we have to put minimum element 
            else { 
                arr[i] += (arr[min_idx] % max_elem) * max_elem; 
                min_idx++; 
            } 
        } 

        // array elements back to it's original form 
        for (int i = 0; i < n; i++) 
            arr[i] = arr[i] / max_elem; 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9 }; 
        int n = arr.length; 

        System.out.println("Original Array"); 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i] + " "); 

        rearrange(arr, n); 

        System.out.print("\nModified Array\n"); 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i] + " "); 
    } 
} 

// This code is contributed by Swetank Modi 

```

## Python3

```py

# Python3 program to rearrange an  
# array in minimum maximum form 

# Prints max at first position, min at second position 
# second max at third position, second min at fourth 
# position and so on. 
def rearrange(arr, n): 

    # Initialize index of first minimum  
    # and first maximum element 
    max_idx = n - 1
    min_idx = 0

    # Store maximum element of array 
    max_elem = arr[n-1] + 1

    # Traverse array elements 
    for i in range(0, n) : 

        # At even index : we have to put maximum element 
        if i % 2 == 0 : 
            arr[i] += (arr[max_idx] % max_elem ) * max_elem 
            max_idx -= 1

        # At odd index : we have to put minimum element 
        else : 
            arr[i] += (arr[min_idx] % max_elem ) * max_elem 
            min_idx += 1

    # array elements back to it's original form 
    for i in range(0, n) : 
        arr[i] = arr[i] / max_elem  

# Driver Code 
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9] 
n = len(arr) 

print ("Original Array") 

for i in range(0, n): 
    print (arr[i], end = " ") 

rearrange(arr, n) 

print ("\nModified Array") 
for i in range(0, n): 
    print (int(arr[i]), end = " ") 

# This code is contributed by Shreyanshi Arun. 

```

## C# 

```cs

// C# program to rearrange an 
// array in minimum maximum form 
using System; 

class main { 

    // Prints max at first position, min at second 
    // position, second max at third position, second 
    // min at fourth position and so on. 
    public static void rearrange(int[] arr, int n) 
    { 
        // initialize index of first minimum 
        // and first maximum element 
        int max_idx = n - 1, min_idx = 0; 

        // store maximum element of array 
        int max_elem = arr[n - 1] + 1; 

        // traverse array elements 
        for (int i = 0; i < n; i++) { 

            // at even index : we have to put 
            // maximum element 
            if (i % 2 == 0) { 
                arr[i] += (arr[max_idx] % max_elem) * max_elem; 
                max_idx--; 
            } 

            // at odd index : we have to 
            // put minimum element 
            else { 
                arr[i] += (arr[min_idx] % max_elem) * max_elem; 
                min_idx++; 
            } 
        } 

        // array elements back to it's original form 
        for (int i = 0; i < n; i++) 
            arr[i] = arr[i] / max_elem; 
    } 

    // Driver code 
    public static void Main() 
    { 
        int[] arr = { 1, 2, 3, 4, 5, 6, 7, 8, 9 }; 
        int n = arr.Length; 
        Console.WriteLine("Original Array"); 
        for (int i = 0; i < n; i++) 
            Console.Write(arr[i] + " "); 
        Console.WriteLine(); 

        rearrange(arr, n); 

        Console.WriteLine("Modified Array"); 
        for (int i = 0; i < n; i++) 
            Console.Write(arr[i] + " "); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP program to rearrange an  
// array in minimum-maximum form 

// Prints max at first position,  
// min at second position 
// second max at third position,  
// second min at fourth 
// position and so on. 
function rearrange(&$arr, $n) 
{ 
    // initialize index of first 
    // minimum and first maximum element 
    $max_idx = $n - 1; $min_idx = 0; 

    // store maximum element of array 
    $max_elem = $arr[$n - 1] + 1; 

    // traverse array elements 
    for ($i = 0; $i < $n; $i++) 
    { 
        // at even index : we have to 
        // put maximum element 
        if ($i % 2 == 0)  
        { 
            $arr[$i] += ($arr[$max_idx] %  
                         $max_elem) * $max_elem; 
            $max_idx--; 
        } 

        // at odd index : we have to  
        // put minimum element 
        else
        { 
            $arr[$i] += ($arr[$min_idx] %  
                         $max_elem) * $max_elem; 
            $min_idx++; 
        } 
    } 

    // array elements back to  
    // it's original form 
    for ($i = 0; $i < $n; $i++) 
        $arr[$i] = (int)($arr[$i] / $max_elem); 
} 

// Driver Code 
$arr = array(1, 2, 3, 4, 5, 6, 7, 8, 9); 
$n = sizeof($arr); 

echo "Original Array" . "\n"; 
for ($i = 0; $i < $n; $i++) 
    echo $arr[$i] . " "; 

rearrange($arr, $n); 

echo "\nModified Array\n"; 
for ($i = 0; $i < $n; $i++) 
    echo $arr[$i] . " "; 

// This code is contributed 
// by Akanksha Rai(Abby_akku) 

```

**输出**：

```
Original Array
1 2 3 4 5 6 7 8 9 
Modified Array
9 1 8 2 7 3 6 4 5 

```

感谢 Saurabh Srivastava 和 Gaurav Ahirwar 提出了这种方法。

**另一种方法**：一种更简单的方法是观察最大元素和最小元素的索引位置。 偶数索引存储最大元素，奇数索引存储最小元素。 随着索引的增加，最大元素减少一个，最小元素增加一个。 可以完成简单的遍历，并再次填写`arr[]`。

**注意**：仅当给定排序数组的元素是连续的，即相差一个单位时，此方法才有效。

下面是上述方法的实现：

## C++

```cpp

// C++ program to rearrange an array in minimum 
// maximum form 
#include <bits/stdc++.h> 
using namespace std; 

// Prints max at first position, min at second position 
// second max at third position, second min at fourth 
// position and so on. 
void rearrange(int arr[], int n) 
{ 
    // initialize index of first minimum and first 
    // maximum element 
    int max_ele = arr[n - 1]; 
    int min_ele = arr[0]; 
    // traverse array elements 
    for (int i = 0; i < n; i++) { 
        // at even index : we have to put maximum element 
        if (i % 2 == 0) { 
            arr[i] = max_ele; 
            max_ele -= 1; 
        } 

        // at odd index : we have to put minimum element 
        else { 
            arr[i] = min_ele; 
            min_ele += 1; 
        } 
    } 
} 

// Driver program to test above function 
int main() 
{ 
    int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    cout << "Original Array\n"; 
    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 

    rearrange(arr, n); 

    cout << "\nModified Array\n"; 
    for (int i = 0; i < n; i++) 
        cout << arr[i] << " "; 
    return 0; 
} 

```

## Java

```java

// Java program to rearrange an 
// array in minimum maximum form 

public class Main { 

    // Prints max at first position, min at second 
    // position second max at third position, second 
    // min at fourth position and so on. 
    public static void rearrange(int arr[], int n) 
    { 
        // initialize index of first minimum and first 
        // maximum element 
        int max_ele = arr[n - 1]; 
        int min_ele = arr[0]; 
        // traverse array elements 
        for (int i = 0; i < n; i++) { 
            // at even index : we have to put maximum element 
            if (i % 2 == 0) { 
                arr[i] = max_ele; 
                max_ele -= 1; 
            } 

            // at odd index : we have to put minimum element 
            else { 
                arr[i] = min_ele; 
                min_ele += 1; 
            } 
        } 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9 }; 
        int n = arr.length; 

        System.out.println("Original Array"); 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i] + " "); 

        rearrange(arr, n); 

        System.out.print("\nModified Array\n"); 
        for (int i = 0; i < n; i++) 
            System.out.print(arr[i] + " "); 
    } 
} 

```

## Python3

```py

# Python 3 program to rearrange an  
# array in minimum maximum form  

# Prints max at first position, min  
# at second position second max at 
# third position, second min at  
# fourth position and so on.  
def rearrange(arr, n): 

    # initialize index of first minimum  
    # and first maximum element  
    max_ele = arr[n - 1] 
    min_ele = arr[0] 

    # traverse array elements  
    for i in range(n): 

        # at even index : we have to  
        # put maximum element 
        if i % 2 == 0: 
            arr[i] = max_ele 
            max_ele -= 1

        # at odd index : we have to 
        # put minimum element 
        else: 
            arr[i] = min_ele 
            min_ele += 1

# Driver code 
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9] 
n = len(arr) 
print("Origianl Array") 
for i in range(n): 
    print(arr[i], end = " ") 

rearrange(arr, n) 
print("\nModified Array") 
for i in range(n): 
    print(arr[i], end = " ") 

# This code is contributed by Shrikant13  

```

## C#

```cs

// C# program to rearrange  
// an array in minimum  
// maximum form 
using System; 

class GFG 
{ 
    // Prints max at first  
    // position, min at second 
    // position second max at 
    // third position, second 
    // min at fourth position 
    // and so on. 
    public static void rearrange(int []arr, 
                                 int n) 
    { 
        // initialize index of  
        // first minimum and 
        // first maximum element 
        int max_ele = arr[n - 1]; 
        int min_ele = arr[0]; 

        // traverse array elements 
        for (int i = 0; i < n; i++)  
        { 
            // at even index : we have  
            // to put maximum element 
            if (i % 2 == 0)  
            { 
                arr[i] = max_ele; 
                max_ele -= 1; 
            } 

            // at odd index : we have 
            // to put minimum element 
            else 
            { 
                arr[i] = min_ele; 
                min_ele += 1; 
            } 
        } 
    } 

    // Driver code 
    static public void Main () 
    { 
        int []arr = {1, 2, 3, 4,  
                     5, 6, 7, 8, 9}; 
        int n = arr.Length; 

        Console.WriteLine("Original Array"); 
        for (int i = 0; i < n; i++) 
            Console.Write(arr[i] + " "); 

        rearrange(arr, n); 

        Console.Write("\nModified Array\n"); 
        for (int i = 0; i < n; i++) 
            Console.Write(arr[i] + " "); 
    } 
} 

// This code is contributed by ajit 

```

**输出**：

```
Original Array
1 2 3 4 5 6 7 8 9 
Modified Array
9 1 8 2 7 3 6 4 5 

```

感谢 **Apollo Doley** 提出了这种方法。



