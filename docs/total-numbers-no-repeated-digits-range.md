# 范围内没有重复数字的数字总数

> 原文： [https://www.geeksforgeeks.org/total-numbers-no-repeated-digits-range/](https://www.geeksforgeeks.org/total-numbers-no-repeated-digits-range/)

给定一个范围`L, R`，可以找到给定范围内的总数，以使它们没有重复的数字。

例如：

12 没有重复的数字。

22 具有重复的数字。

102、194 和 213 没有重复的数字。

212、171 和 4004 具有重复的数字。

**示例**：

```
Input : 10 12
Output : 2
Explanation : In the given range 
10 and 12 have no repeated digit 
where as 11 has repeated digit.

Input : 1 100
Output : 90

```



**暴力**：

我们将遍历给定范围内的每个元素，并对没有重复数字的数字进行计数。

## C++ 

```cpp

// C++ implementation of brute 
// force solution. 
#include <bits/stdc++.h> 
using namespace std; 

// Function to check if the given 
// number has repeated digit or not 
int repeated_digit(int n) 
{ 
    unordered_set<int> s; 

    // Traversing through each digit 
    while(n != 0) 
    { 
        int d = n % 10; 

        // if the digit is present 
        // more than once in the 
        // number 
        if(s.find(d) != s.end()) 
        { 
            // return 0 if the number 
            // has repeated digit 
            return 0; 
        } 
        s.insert(d); 
        n = n / 10; 
    } 
    // return 1 if the number has  
    // no repeated digit 
    return 1; 
} 

// Function to find total number 
// in the given range which has 
// no repeated digit 
int calculate(int L,int R) 
{ 
    int answer = 0; 

    // Traversing through the range 
    for(int i = L; i < R + 1; ++i) 
    { 

        // Add 1 to the answer if i has 
        // no repeated digit else 0 
        answer = answer + repeated_digit(i); 
    } 

    return answer ; 
} 

// Driver Code 
int main() 
{ 
    int L = 1, R = 100; 

    // Calling the calculate 
    cout << calculate(L, R); 
    return 0; 
} 

// This code is contributed by 
// Sanjit_Prasad 

```

## Java

```java

// Java implementation of brute  
// force solution.  
import java.util.LinkedHashSet; 

class GFG 
{ 
// Function to check if the given  
// number has repeated digit or not  
static int repeated_digit(int n)  
{ 
    LinkedHashSet<Integer> s = new LinkedHashSet<>(); 

    // Traversing through each digit  
    while (n != 0)  
    { 
        int d = n % 10; 

        // if the digit is present  
        // more than once in the  
        // number  
        if (s.contains(d)) 
        { 
            // return 0 if the number  
            // has repeated digit  
            return 0; 
        } 
        s.add(d); 
        n = n / 10; 
    } 

    // return 1 if the number has  
    // no repeated digit  
    return 1; 
} 

// Function to find total number  
// in the given range which has  
// no repeated digit  
static int calculate(int L, int R)  
{ 
    int answer = 0; 

    // Traversing through the range  
    for (int i = L; i < R + 1; ++i)  
    { 

        // Add 1 to the answer if i has  
        // no repeated digit else 0  
        answer = answer + repeated_digit(i); 
    } 

    return answer; 
} 

// Driver Code  
public static void main(String[] args)  
{ 
    int L = 1, R = 100; 

    // Calling the calculate  
    System.out.println(calculate(L, R)); 
} 
} 

// This code is contributed by RAJPUT-JI 

```

## Python3

```py

# Python implementation of brute  
# force solution. 

# Function to check if the given  
# number has repeated digit or not  
def repeated_digit(n): 
    a = [] 

    # Traversing through each digit 
    while n != 0: 
        d = n%10

        # if the digit is present 
        # more than once in the 
        # number 
        if d in a: 

            # return 0 if the number 
            # has repeated digit 
            return 0
        a.append(d) 
        n = n//10

    # return 1 if the number has no 
    # repeated digit 
    return 1

# Function to find total number 
# in the given range which has  
# no repeated digit 
def calculate(L,R): 
    answer = 0

    # Traversing through the range 
    for i in range(L,R+1): 

        # Add 1 to the answer if i has 
        # no repeated digit else 0 
        answer = answer + repeated_digit(i) 

    # return answer 
    return answer 

# Driver's Code  
L=1
R=100

# Calling the calculate 
print(calculate(L, R)) 

```

## C# 

```cs

// C# implementation of brute  
// force solution.  
using System;  
using System.Collections.Generic;  

class GFG  
{ 

// Function to check if the given  
// number has repeated digit or not  
static int repeated_digit(int n) 
{ 
    var s = new HashSet<int>(); 

    // Traversing through each digit  
    while (n != 0) 
    { 
        int d = n % 10; 

        // if the digit is present  
        // more than once in the  
        // number  
        if (s.Contains(d))  
        { 
            // return 0 if the number  
            // has repeated digit  
            return 0; 
        } 
        s.Add(d); 
        n = n / 10; 
    } 

    // return 1 if the number has  
    // no repeated digit  
    return 1; 
} 

// Function to find total number  
// in the given range which has  
// no repeated digit  
static int calculate(int L, int R)  
{ 
    int answer = 0; 

    // Traversing through the range  
    for (int i = L; i < R + 1; ++i)  
    { 

        // Add 1 to the answer if i has  
        // no repeated digit else 0  
        answer = answer + repeated_digit(i); 
    } 

    return answer; 
} 

// Driver Code  
public static void Main(String[] args) 
{ 
    int L = 1, R = 100; 

    // Calling the calculate  
    Console.WriteLine(calculate(L, R)); 
} 
} 

// This code is contributed by RAJPUT-JI 

```

## PHP

```php

<?php 
// PHP implementation of  
// brute force solution. 

// Function to check if  
// the given number has 
// repeated digit or not  
function repeated_digit($n) 
{ 
    $c = 10; 
    $a = array_fill(0, $c, 0); 

    // Traversing through  
    // each digit 
    while($n > 0) 
    { 
        $d = $n % 10; 

        // if the digit is present 
        // more than once in the 
        // number 
        if ($a[$d] > 0) 
        { 
            // return 0 if the number 
            // has repeated digit 
            return 0; 
        } 
        $a[$d]++; 
        $n = (int)($n / 10); 
    } 

    // return 1 if the number  
    // has no repeated digit 
    return 1; 
} 

// Function to find total  
// number in the given range  
// which has no repeated digit 
function calculate($L, $R) 
{ 
    $answer = 0; 

    // Traversing through 
    // the range 
    for($i = $L; $i <= $R; $i++) 
    { 

        // Add 1 to the answer if  
        // i has no repeated digit 
        // else 0 
        $answer += repeated_digit($i); 
    } 

    // return answer 
    return $answer; 
}  

// Driver Code  
$L = 1; 
$R = 100; 

// Calling the calculate 
echo calculate($L, $R); 

// This code is contributed by mits 
?> 

```

**输出**：

```
90

```

此方法将在 **`O(n)`**时间内回答每个查询。

**有效方法**：

我们将计算没有重复数字的数字的前缀数组。

`Prefix[i] =`没有重复位数小于或等于 1 的总数。

因此，每个查询都可以在`O(1)`时间内解决。

![ Answer = Prefix[R] - Prefix[L-1]](img/3d64608a84a7bfd9da2af1a7422fb968.png "Rendered by QuickLaTeX.com")

**下面是上述想法的实现。**

## C++

```cpp

// C++ implementation of above idea  
#include <bits/stdc++.h>  

using namespace std; 

// Maximum  
int MAX = 1000; 

// Prefix Array  
vector<int> Prefix = {0}; 

// Function to check if the given  
// number has repeated digit or not  
int repeated_digit(int n) 
{ 

    unordered_set<int> a; 
    int d; 

    // Traversing through each digit  
    while (n != 0) 
    { 
        d = n % 10; 

        // if the digit is present  
        // more than once in the  
        // number  
        if (a.find(d) != a.end())  

            // return 0 if the number  
            // has repeated digit  
            return 0; 

        a.insert(d);  
        n = n / 10; 
    } 

    // return 1 if the number has no  
    // repeated digit  
    return 1; 
} 

// Function to pre calculate  
// the Prefix array  
void pre_calculation(int MAX) 
{ 

    Prefix.push_back(repeated_digit(1)); 

    // Traversing through the numbers  
    // from 2 to MAX  
    for (int i = 2; i < MAX + 1; i++)  

        // Generating the Prefix array  
        Prefix.push_back(repeated_digit(i) + Prefix[i-1]); 
} 

// Calclute Function  
int calculate(int L,int R) 
{  

    // Answer  
    return Prefix[R] - Prefix[L-1]; 
} 

// Driver code 
int main() 
{ 
    int L = 1, R = 100; 

    // Pre-calculating the Prefix array.  
    pre_calculation(MAX); 

    // Calling the calculate function  
    // to find the total number of number  
    // which has no repeated digit  
    cout << calculate(L, R) << endl;  

    return 0; 
} 

// This code is contributed by Rituraj Jain 

```

## Java

```java

// Java implementation of above idea 
import java.util.*; 

class GFG  
{ 

    // Maximum 
    static int MAX = 100; 

    // Prefix Array 
    static Vector<Integer> Prefix = new Vector<>(); 

    // Function to check if the given 
    // number has repeated digit or not 
    static int repeated_digit(int n) 
    { 
        HashSet<Integer> a = new HashSet<>(); 
        int d; 

        // Traversing through each digit 
        while (n != 0)  
        { 
            d = n % 10; 

            // if the digit is present 
            // more than once in the 
            // number 
            if (a.contains(d)) 

                // return 0 if the number 
                // has repeated digit 
                return 0; 
            a.add(d); 
            n /= 10; 
        } 

        // return 1 if the number has no 
        // repeated digit 
        return 1; 
    } 

    // Function to pre calculate 
    // the Prefix array 
    static void pre_calculations()  
    { 
        Prefix.add(0); 
        Prefix.add(repeated_digit(1)); 

        // Traversing through the numbers 
        // from 2 to MAX 
        for (int i = 2; i < MAX + 1; i++) 

            // Generating the Prefix array 
            Prefix.add(repeated_digit(i) + Prefix.elementAt(i - 1)); 
    } 

    // Calclute Function 
    static int calculate(int L, int R) 
    { 

        // Answer 
        return Prefix.elementAt(R) - Prefix.elementAt(L - 1); 
    } 

    // Driver Code 
    public static void main(String[] args) 
    { 
        int L = 1, R = 100; 

        // Pre-calculating the Prefix array. 
        pre_calculations(); 

        // Calling the calculate function 
        // to find the total number of number 
        // which has no repeated digit 
        System.out.println(calculate(L, R)); 
    } 
} 

// This code is contributed by 
// sanjeev2552 

```

## Python3

```py

# Python implementation of  
# above idea 

# Prefix Array 
Prefix = [0] 

# Function to check if  
# the given number has  
# repeated digit or not  
def repeated_digit(n): 
    a = [] 

    # Traversing through each digit 
    while n != 0: 
        d = n%10

        # if the digit is present 
        # more than once in the 
        # number 
        if d in a: 

            # return 0 if the number 
            # has repeated digit 
            return 0
        a.append(d) 
        n = n//10

    # return 1 if the number has no 
    # repeated digit 
    return 1

# Function to pre calculate 
# the Prefix array 
def pre_calculation(MAX): 

    # To use to global Prefix array 
    global Prefix 
    Prefix.append(repeated_digit(1)) 

    # Traversing through the numbers 
    # from 2 to MAX 
    for i in range(2,MAX+1): 

        # Generating the Prefix array  
        Prefix.append( repeated_digit(i) +
                       Prefix[i-1] ) 

# Calclute Function 
def calculate(L,R): 

    # Answer 
    return Prefix[R]-Prefix[L-1] 

# Driver Code 

# Maximum  
MAX = 1000

# Pre-calculating the Prefix array. 
pre_calculation(MAX) 

# Range 
L=1
R=100

# Calling the calculate function 
# to find the total number of number 
# which has no repeated digit 
print(calculate(L, R)) 

```

## C#

```cs

// C# implementation of above idea 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

    // Maximum 
    static int MAX = 100; 

    // Prefix Array 
    static List<int> Prefix = new List<int>(); 

    // Function to check if the given 
    // number has repeated digit or not 
    static int repeated_digit(int n) 
    { 
        HashSet<int> a = new HashSet<int>(); 
        int d; 

        // Traversing through each digit 
        while (n != 0)  
        { 
            d = n % 10; 

            // if the digit is present 
            // more than once in the 
            // number 
            if (a.Contains(d)) 

                // return 0 if the number 
                // has repeated digit 
                return 0; 
            a.Add(d); 
            n /= 10; 
        } 

        // return 1 if the number has no 
        // repeated digit 
        return 1; 
    } 

    // Function to pre calculate 
    // the Prefix array 
    static void pre_calculations()  
    { 
        Prefix.Add(0); 
        Prefix.Add(repeated_digit(1)); 

        // Traversing through the numbers 
        // from 2 to MAX 
        for (int i = 2; i < MAX + 1; i++) 

            // Generating the Prefix array 
            Prefix.Add(repeated_digit(i) +  
                           Prefix[i - 1]); 
    } 

    // Calclute Function 
    static int calculate(int L, int R) 
    { 

        // Answer 
        return Prefix[R] - Prefix[L - 1]; 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        int L = 1, R = 100; 

        // Pre-calculating the Prefix array. 
        pre_calculations(); 

        // Calling the calculate function 
        // to find the total number of number 
        // which has no repeated digit 
        Console.WriteLine(calculate(L, R)); 
    } 
} 

// This code is contributed by 29AjayKumar 

```

**输出**：

```
90

```



* * *

* * *



