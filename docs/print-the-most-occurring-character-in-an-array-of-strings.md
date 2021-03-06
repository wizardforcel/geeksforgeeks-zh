# 打印字符串数组中出现次数最多的字符

> 原文：[https://www.geeksforgeeks.org/print-the-most-occurring-character-in-an-array-of-strings/](https://www.geeksforgeeks.org/print-the-most-occurring-character-in-an-array-of-strings/)

给定小写字符串数组`arr[]`，任务是打印字符串集中出现次数最多的字符。

**示例**：

> **输入**：`arr[] = {"animal", "zebra", "lion", "giraffe"}`
>
> **输出**：`a`
>
> **说明**：
> `a`的频率是 4，这是最高的。
> 
> **输入**：`arr[] = {"aa", "bb", "cc", "bde"}`
>
> **输出**：`b`

**方法**：想法是使用大小为 26 的数组实现[哈希数据结构](https://www.geeksforgeeks.org/hashing-data-structure/)。此数组存储从`a`到`z`的每个字符的计数。 可以按照以下步骤计算答案：

1.  遍历数组中的每个字符串。

2.  对于字符串中的每个字符，其值在哈希中均增加 1。

3.  遍历所有字符串之后，将检查字符的最大计数并打印字符。

下面是上述方法的实现：

## CPP

```

// C++ program to print the most occurring 
// character in an array of strings 

#include <bits/stdc++.h> 
using namespace std; 

// Function to print the most occurring character 
void findMostOccurringChar(vector<string> str) 
{ 

    // Creating a hash of size 26 
    int hash[26] = { 0 }; 

    // For loop to iterate through 
    // every string of the array 
    for (int i = 0; i < str.size(); i++) { 

        // For loop to iterate through 
        // every character of the string 
        for (int j = 0; j < str[i].length(); j++) { 

            // Incrementing the count of 
            // the character in the hash 
            hash[str[i][j]]++; 
        } 
    } 

    // Finding the character 
    // with the maximum count 
    int max = 0; 
    for (int i = 0; i < 26; i++) { 
        max = hash[i] > hash[max] ? i : max; 
    } 

    cout << (char)(max + 97) << endl; 
} 

// Driver code 
int main() 
{ 

    // Declaring Vector of String type 
    vector<string> str; 
    str.push_back("animal"); 
    str.push_back("zebra"); 
    str.push_back("lion"); 
    str.push_back("giraffe"); 

    findMostOccurringChar(str); 
    return 0; 
} 

```

## Java

```java

// Java program to print the most occurring 
// character in an array of Strings 
import java.util.*; 

class GFG 
{ 

// Function to print the most occurring character 
static void findMostOccurringChar(Vector<String> str) 
{ 

    // Creating a hash of size 26 
    int []hash = new int[26]; 

    // For loop to iterate through 
    // every String of the array 
    for (int i = 0; i < str.size(); i++) 
    { 

        // For loop to iterate through 
        // every character of the String 
        for (int j = 0; j < str.get(i).length(); j++)  
        { 

            // Incrementing the count of 
            // the character in the hash 
            hash[str.get(i).charAt(j)-97]++; 
        } 
    } 

    // Finding the character 
    // with the maximum count 
    int max = 0; 
    for (int i = 0; i < 26; i++)  
    { 
        max = hash[i] > hash[max] ? i : max; 
    } 

    System.out.print((char)(max + 97) +"\n"); 
} 

// Driver code 
public static void main(String[] args) 
{ 

    // Declaring Vector of String type 
    Vector<String> str = new Vector<String>(); 
    str.add("animal"); 
    str.add("zebra"); 
    str.add("lion"); 
    str.add("giraffe"); 

    findMostOccurringChar(str); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

## Python3

```py

# Python3 program to print the most occurring  
# character in an array of strings  

# Function to print the most occurring character  
def findMostOccurringChar(string) : 

    # Creating a hash of size 26  
    hash = [0]*26;  

    # For loop to iterate through  
    # every string of the array  
    for i in range(len(string)) : 

        # For loop to iterate through  
        # every character of the string  
        for j in range(len(string[i])) : 

            # Incrementing the count of  
            # the character in the hash  
            hash[ord(string[i][j]) - ord('a')] += 1;  

    # Finding the character  
    # with the maximum count  
    max = 0;  
    for i in range(26) : 
        max = i if hash[i] > hash[max] else max;  

    print((chr)(max + 97));  

# Driver code  
if __name__ == "__main__" :  

    # Declaring Vector of String type  
    string = [];  
    string.append("animal");  
    string.append("zebra");  
    string.append("lion");  
    string.append("giraffe");  

    findMostOccurringChar(string);  

# This code is contributed by AnkitRai01 

```

## C#

```cs

// C# program to print the most occurring  
// character in an array of Strings  
using System; 

class GFG  
{  

    // Function to print the most occurring character  
    static void findMostOccurringChar(string []str)  
    {  

        // Creating a hash of size 26  
        int []hash = new int[26];  

        // For loop to iterate through  
        // every String of the array  
        for (int i = 0; i < str.Length; i++)  
        {  

            // For loop to iterate through  
            // every character of the String  
            for (int j = 0; j < str[i].Length; j++)  
            {  

                // Incrementing the count of  
                // the character in the hash  
                hash[str[i][j]-97]++;  
            }  
        }  

        // Finding the character  
        // with the maximum count  
        int max = 0;  
        for (int i = 0; i < 26; i++)  
        {  
            max = hash[i] > hash[max] ? i : max;  
        }  

        Console.Write((char)(max + 97) +"\n");  
    }  

    // Driver code  
    public static void Main(String[] args)  
    {  

        // Declaring Vector of String type  
        string []str = {"animal","zebra","lion","giraffe"};  

        findMostOccurringChar(str);  
    }  
}  

// This code is contributed by AnkitRai01 

```

**输出**：

```
a

```



* * *

* * *



