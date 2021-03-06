# 查找数组中的偶对数量，以使它们的 XOR 为 0

> 原文： [https://www.geeksforgeeks.org/find-number-pairs-array-xor-0/](https://www.geeksforgeeks.org/find-number-pairs-array-xor-0/)

给定大小为`N`的数组`A[]`。求对`(i, j)`的对数，以使`A[i] XOR A[j] = 0`，并且`1 <= i < j <= N`。

**示例**：

```
Input : A[] = {1, 3, 4, 1, 4}
Output : 2
Explanation : Index (0, 3) and (2, 4)

Input : A[] = {2, 2, 2}
Output : 3

```



**第一种方法 - 排序**：

仅当`A[i] = A[j]`时才满足`A[i] XOR A[j] = 0`的要求。 因此，我们将首先对数组进行排序，然后计算每个元素的频率。 通过组合，我们可以观察到，如果某个元素的频率为`count`，那么它将为答案提供`count*(count-1)/2`。

以下是上述方法的实现：

## C++ 

```cpp

// C++ program to find number  
// of pairs in an array such 
// that their XOR is 0 
#include <bits/stdc++.h> 
using namespace std; 

// Function to calculate the 
// count 
int calculate(int a[], int n) 
{ 
    // Sorting the list using 
    // built in function 
    sort(a, a + n); 

    int count = 1; 
    int answer = 0; 

    // Traversing through the 
    // elements 
    for (int i = 1; i < n; i++) { 

        if (a[i] == a[i - 1]){ 

            // Counting frequency of each  
            // elements 
            count += 1; 

        }  
        else 
        { 
            // Adding the contribution of 
            // the frequency to the answer 
            answer = answer + (count * (count - 1)) / 2; 
            count = 1; 
        } 
    } 

    answer = answer + (count * (count - 1)) / 2; 

    return answer; 
} 

// Driver Code 
int main() 
{ 

    int a[] = { 1, 2, 1, 2, 4 }; 
    int n = sizeof(a) / sizeof(a[0]); 

    // Print the count 
    cout << calculate(a, n); 
    return 0; 
} 

// This article is contributed by Sahil_Bansall. 

```

## Java

```java

// Java program to find number  
// of pairs in an array such 
// that their XOR is 0 
import java.util.*; 

class GFG  
{ 
    // Function to calculate  
    // the count 
    static int calculate(int a[], int n) 
    { 
        // Sorting the list using 
        // built in function 
        Arrays.sort(a); 

        int count = 1; 
        int answer = 0; 

        // Traversing through the 
        // elements 
        for (int i = 1; i < n; i++)  
        { 

            if (a[i] == a[i - 1]) 
            { 
                // Counting frequency of each  
                // elements 
                count += 1; 

            }  
            else
            { 
                // Adding the contribution of 
                // the frequency to the answer 
                answer = answer + (count * (count - 1)) / 2; 
                count = 1; 
            } 
        } 

        answer = answer + (count * (count - 1)) / 2; 

        return answer; 
    } 

    // Driver Code 
    public static void main (String[] args)  
    { 
        int a[] = { 1, 2, 1, 2, 4 }; 
        int n = a.length; 

        // Print the count 
        System.out.println(calculate(a, n)); 
    } 
} 

// This code is contributed by Ansu Kumari. 

```

## Python3

```py

# Python3 program to find number of pairs 
# in an array such that their XOR is 0 

# Function to calculate the count 
def calculate(a) : 

    # Sorting the list using 
    # built in function 
    a.sort() 

    count = 1
    answer = 0

    # Traversing through the elements 
    for i in range(1, len(a)) : 

        if a[i] == a[i - 1] : 

            # Counting frequncy of each elements 
            count += 1

        else : 

            # Adding the contribution of 
            # the frequency to the answer 
            answer = answer + count * (count - 1) // 2
            count = 1

    answer = answer + count * (count - 1) // 2

    return answer 

# Driver Code 
if __name__ == '__main__': 

    a = [1, 2, 1, 2, 4] 

    # Print the count 
    print(calculate(a)) 

```

## C# 

```cs

// C# program to find number  
// of pairs in an array such 
// that their XOR is 0 
using System; 

class GFG  
{ 
    // Function to calculate  
    // the count 
    static int calculate(int []a, int n) 
    { 
        // Sorting the list using 
        // built in function 
        Array.Sort(a); 

        int count = 1; 
        int answer = 0; 

        // Traversing through the 
        // elements 
        for (int i = 1; i < n; i++)  
        { 

            if (a[i] == a[i - 1]) 
            { 
                // Counting frequency of each  
                // elements 
                count += 1; 

            }  
            else
            { 
                // Adding the contribution of 
                // the frequency to the answer 
                answer = answer + (count * (count - 1)) / 2; 
                count = 1; 
            } 
        } 

        answer = answer + (count * (count - 1)) / 2; 

        return answer; 
    } 

    // Driver Code 
    public static void Main ()  
    { 
        int []a = { 1, 2, 1, 2, 4 }; 
        int n = a.Length; 

        // Print the count 
        Console.WriteLine(calculate(a, n)); 
    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP program to find number  
// of pairs in an array such 
// that their XOR is 0 

// Function to calculate  
// the count 
function calculate($a, $n) 
{ 

    // Sorting the list using 
    // built in function 
    sort($a); 

    $count = 1; 
    $answer = 0; 

    // Traversing through the 
    // elements 
    for ($i = 1; $i < $n; $i++) 
    { 

        if ($a[$i] == $a[$i - 1]) 
        { 

            // Counting frequency of  
            // each elements 
            $count += 1; 

        }  

        else
        { 

            // Adding the contribution of 
            // the frequency to the answer 
            $answer = $answer + ($count *  
                       ($count - 1)) / 2; 
            $count = 1; 
        } 
    } 

    $answer = $answer + ($count *  
               ($count - 1)) / 2; 

    return $answer; 
} 

    // Driver Code 
    $a = array(1, 2, 1, 2, 4); 
    $n = count($a); 

    // Print the count 
    echo calculate($a, $n); 

// This code is contributed by anuj_67\. 
?> 

```

**输出**：

```
2

```

**时间复杂度**：`O(N log N)`。

，

**第二种方法 - 散列（索引映射）**：

如果我们可以计算数组中每个元素的频率，则解决方案很方便。 索引映射技术可用于计算每个元素的频率。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find number of pairs 
// in an array such that their XOR is 0 
#include <bits/stdc++.h> 
using namespace std; 

// Function to calculate the answer 
int calculate(int a[], int n){ 

    // Finding the maximum of the array 
    int *maximum = max_element(a, a + 5); 

    // Creating frequency array 
    // With initial value 0 
    int frequency[*maximum + 1] = {0}; 

    // Traversing through the array  
    for(int i = 0; i < n; i++) 
    {  
        // Counting frequency 
        frequency[a[i]] += 1; 
    } 
    int answer = 0; 

    // Traversing through the frequency array 
    for(int i = 0; i < (*maximum)+1; i++) 
    {  
        // Calculating answer 
        answer = answer + frequency[i] * (frequency[i] - 1) ; 
    } 
    return answer/2; 
} 

// Driver Code 
int main() 
{ 
   int a[] = {1, 2, 1, 2, 4}; 
   int n = sizeof(a) / sizeof(a[0]);  

   // Function calling 
   cout << (calculate(a,n)); 
} 

// This code is contributed by Smitha 

```

## Java

```java
// Java program to find number of pairs  
// in an array such that their XOR is 0  
import java.util.*; 
  
class GFG  
{ 
  
    // Function to calculate the answer  
    static int calculate(int a[], int n)  
    { 
  
        // Finding the maximum of the array  
        int maximum = Arrays.stream(a).max().getAsInt(); 
  
        // Creating frequency array  
        // With initial value 0  
        int frequency[] = new int[maximum + 1]; 
  
        // Traversing through the array  
        for (int i = 0; i < n; i++)  
        { 
              
            // Counting frequency  
            frequency[a[i]] += 1; 
        } 
        int answer = 0; 
  
        // Traversing through the frequency array  
        for (int i = 0; i < (maximum) + 1; i++)  
        { 
              
            // Calculating answer  
            answer = answer + frequency[i] * (frequency[i] - 1); 
        } 
        return answer / 2; 
    } 
  
    // Driver Code  
    public static void main(String[] args)  
    { 
        int a[] = {1, 2, 1, 2, 4}; 
        int n = a.length; 
  
        // Function calling  
        System.out.println(calculate(a, n)); 
    } 
} 
  
// This code is contributed by 29AjayKumar
```

## Python 3

```
# Python3 program to find number of pairs 
# in an array such that their XOR is 0 
  
# Function to calculate the answer 
def calculate(a) : 
      
    # Finding the maximum of the array 
    maximum = max(a) 
      
    # Creating frequency array 
    # With initial value 0 
    frequency = [0 for x in range(maximum + 1)] 
      
    # Traversing through the array  
    for i in a : 
           
        # Counting frequency 
        frequency[i] += 1
      
    answer = 0
      
    # Traversing through the frequency array 
    for i in frequency : 
          
        # Calculating answer 
        answer = answer + i * (i - 1) // 2
      
    return answer 
  
# Driver Code 
a = [1, 2, 1, 2, 4] 
print(calculate(a))
```

## C#

```cs
// C# program to find number of pairs  
// in an array such that their XOR is 0  
using System; 
using System.Linq; 
class GFG  
{ 
  
    // Function to calculate the answer  
    static int calculate(int []a, int n)  
    { 
  
        // Finding the maximum of the array  
        int maximum = a.Max(); 
  
        // Creating frequency array  
        // With initial value 0  
        int []frequency = new int[maximum + 1]; 
  
        // Traversing through the array  
        for (int i = 0; i < n; i++)  
        { 
              
            // Counting frequency  
            frequency[a[i]] += 1; 
        } 
        int answer = 0; 
  
        // Traversing through the frequency array  
        for (int i = 0; i < (maximum) + 1; i++)  
        { 
              
            // Calculating answer  
            answer = answer + frequency[i] *  
                             (frequency[i] - 1); 
        } 
        return answer / 2; 
    } 
  
    // Driver Code  
    public static void Main(String[] args)  
    { 
        int []a = {1, 2, 1, 2, 4}; 
        int n = a.Length; 
  
        // Function calling  
        Console.WriteLine(calculate(a, n)); 
    } 
} 
  
// This code is contributed by PrinciRaj1992
```

## PHP

```php
<?php 
// PHP program to find number  
// of pairs in an array such  
// that their XOR is 0 
  
// Function to calculate the answer 
function calculate($a, $n) 
{ 
      
    // Finding the maximum of the array 
    $maximum = max($a); 
      
    // Creating frequency array 
    // With initial value 0 
    $frequency = array_fill(0, $maximum + 1, 0); 
      
    // Traversing through the array  
    for($i = 0; $i < $n; $i++) 
    {  
        // Counting frequency 
        $frequency[$a[$i]] += 1; 
    } 
    $answer = 0; 
      
    // Traversing through  
    // the frequency array 
    for($i = 0; $i < ($maximum) + 1; $i++) 
    {  
        // Calculating answer 
        $answer = $answer + $frequency[$i] * 
                        ($frequency[$i] - 1); 
    } 
    return $answer / 2; 
} 
  
// Driver Code 
$a = array(1, 2, 1, 2, 4); 
$n = count($a); 
// Function calling 
echo (calculate($a,$n)); 
  
// This code is contributed by Smitha 
?>
```

输出：

```
2
```

时间复杂度：`O(N)`。

注意：仅当数组中的数字不大时才可以使用索引映射方法。 在这种情况下，可以使用分类方法。