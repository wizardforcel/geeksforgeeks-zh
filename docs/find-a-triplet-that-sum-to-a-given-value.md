# 查找总和为给定值的三元组

> 原文： [https://www.geeksforgeeks.org/find-a-triplet-that-sum-to-a-given-value/](https://www.geeksforgeeks.org/find-a-triplet-that-sum-to-a-given-value/)

给定一个数组和一个值，查找数组中是否有一个三元组，其和等于给定值。 如果数组中存在此类三元组，则打印该三元组并返回`true`。 否则返回`false`。

**例如**：

```
Input: array = {12, 3, 4, 1, 6, 9}, sum = 24;
Output: 12, 3, 9
Explanation: There is a triplet (12, 3 and 9) present
in the array whose sum is 24\. 

Input: array = {1, 2, 3, 4, 5}, sum = 9
Output: 5, 3, 1
Explanation: There is a triplet (5, 3 and 1) present 
in the array whose sum is 9\. 

```



**方法 1**：这是解决上述问题的朴素方法。

*   **方法**：一种简单的方法是生成所有可能的三元组，并将每个三元组的总和与给定值进行比较。 以下代码使用三个嵌套循环实现此简单方法。

*   **算法**：

    1.  给定长度为`n`且总和为`s`的数组。

    2.  创建三个嵌套循环，第一个循环从开始到结束（循环计数器`i`），第二个循环从`i + 1`到结束（循环计数器`j`），第三个循环从`j + 1`到结束（循环计数器`k`）运行。

    3.  这些循环的计数器表示三元组的 3 个元素的索引。

    4.  求出第`i`，`j`和`k`个元素的总和。 如果总和等于给定的总和。 打印三元组并中断。

    5.  如果没有三元组，则打印不存在三元组。

*   **实现**：

    ## C++ 

    ```

    #include <bits/stdc++.h> 
    using namespace std; 

    // returns true if there is triplet with sum equal  
    // to 'sum' present in A[]. Also, prints the triplet  
    bool find3Numbers(int A[], int arr_size, int sum)  
    {  
        int l, r;  

        // Fix the first element as A[i]  
        for (int i = 0; i < arr_size - 2; i++) 
        {  

            // Fix the second element as A[j]  
            for (int j = i + 1; j < arr_size - 1; j++) 
            {  

                // Now look for the third number  
                for (int k = j + 1; k < arr_size; k++) 
                {  
                    if (A[i] + A[j] + A[k] == sum) 
                    {  
                        cout << "Triplet is " << A[i] << 
                            ", " << A[j] << ", " << A[k];  
                        return true;  
                    }  
                }  
            }  
        }  

        // If we reach here, then no triplet was found  
        return false;  
    }  

    /* Driver code */
    int main()  
    {  
        int A[] = { 1, 4, 45, 6, 10, 8 };  
        int sum = 22;  
        int arr_size = sizeof(A) / sizeof(A[0]);  
        find3Numbers(A, arr_size, sum);  
        return 0;  
    }  

    // This is code is contributed by rathbhupendra 

    ```

    ## C

    ```

    #include <stdio.h> 

    // returns true if there is triplet with sum equal 
    // to 'sum' present in A[]. Also, prints the triplet 
    bool find3Numbers(int A[], int arr_size, int sum) 
    { 
        int l, r; 

        // Fix the first element as A[i] 
        for (int i = 0; i < arr_size - 2; i++) { 

            // Fix the second element as A[j] 
            for (int j = i + 1; j < arr_size - 1; j++) { 

                // Now look for the third number 
                for (int k = j + 1; k < arr_size; k++) { 
                    if (A[i] + A[j] + A[k] == sum) { 
                        printf("Triplet is %d, %d, %d", 
                               A[i], A[j], A[k]); 
                        return true; 
                    } 
                } 
            } 
        } 

        // If we reach here, then no triplet was found 
        return false; 
    } 

    /* Driver program to test above function */
    int main() 
    { 
        int A[] = { 1, 4, 45, 6, 10, 8 }; 
        int sum = 22; 
        int arr_size = sizeof(A) / sizeof(A[0]); 
        find3Numbers(A, arr_size, sum); 
        return 0; 
    } 

    ```

    ## Java

    ```

    // Java program to find a triplet 
    class FindTriplet { 

        // returns true if there is triplet with sum equal 
        // to 'sum' present in A[]. Also, prints the triplet 
        boolean find3Numbers(int A[], int arr_size, int sum) 
        { 
            int l, r; 

            // Fix the first element as A[i] 
            for (int i = 0; i < arr_size - 2; i++) { 

                // Fix the second element as A[j] 
                for (int j = i + 1; j < arr_size - 1; j++) { 

                    // Now look for the third number 
                    for (int k = j + 1; k < arr_size; k++) { 
                        if (A[i] + A[j] + A[k] == sum) { 
                            System.out.print("Triplet is " + A[i] + ", " + A[j] + ", " + A[k]); 
                            return true; 
                        } 
                    } 
                } 
            } 

            // If we reach here, then no triplet was found 
            return false; 
        } 

        // Driver program to test above functions 
        public static void main(String[] args) 
        { 
            FindTriplet triplet = new FindTriplet(); 
            int A[] = { 1, 4, 45, 6, 10, 8 }; 
            int sum = 22; 
            int arr_size = A.length; 

            triplet.find3Numbers(A, arr_size, sum); 
        } 
    } 

    ```

    ## Python3

    ```

    # Python3 program to find a triplet  
    # that sum to a given value 

    # returns true if there is triplet with 
    # sum equal to 'sum' present in A[].  
    # Also, prints the triplet 
    def find3Numbers(A, arr_size, sum): 

        # Fix the first element as A[i] 
        for i in range( 0, arr_size-2): 

            # Fix the second element as A[j] 
            for j in range(i + 1, arr_size-1):  

                # Now look for the third number 
                for k in range(j + 1, arr_size): 
                    if A[i] + A[j] + A[k] == sum: 
                        print("Triplet is", A[i], 
                              ", ", A[j], ", ", A[k]) 
                        return True

        # If we reach here, then no  
        # triplet was found 
        return False

    # Driver program to test above function  
    A = [1, 4, 45, 6, 10, 8] 
    sum = 22
    arr_size = len(A) 
    find3Numbers(A, arr_size, sum) 

    # This code is contributed by Smitha Dinesh Semwal  

    ```

    ## C# 

    ```

    // C# program to find a triplet 
    // that sum to a given value 
    using System; 

    class GFG { 
        // returns true if there is 
        // triplet with sum equal 
        // to 'sum' present in A[]. 
        // Also, prints the triplet 
        static bool find3Numbers(int[] A, 
                                 int arr_size, 
                                 int sum) 
        { 
            // Fix the first 
            // element as A[i] 
            for (int i = 0; 
                 i < arr_size - 2; i++) { 

                // Fix the second 
                // element as A[j] 
                for (int j = i + 1; 
                     j < arr_size - 1; j++) { 

                    // Now look for 
                    // the third number 
                    for (int k = j + 1; 
                         k < arr_size; k++) { 
                        if (A[i] + A[j] + A[k] == sum) { 
                            Console.WriteLine("Triplet is " + A[i] + ", " + A[j] + ", " + A[k]); 
                            return true; 
                        } 
                    } 
                } 
            } 

            // If we reach here, 
            // then no triplet was found 
            return false; 
        } 

        // Driver Code 
        static public void Main() 
        { 
            int[] A = { 1, 4, 45, 6, 10, 8 }; 
            int sum = 22; 
            int arr_size = A.Length; 

            find3Numbers(A, arr_size, sum); 
        } 
    } 

    // This code is contributed by m_kit 

    ```

    ## PHP

    ```

    <?php 
    // PHP program to find a triplet  
    // that sum to a given value 

    // returns true if there is  
    // triplet with sum equal to 
    // 'sum' present in A[]. 
    // Also, prints the triplet 
    function find3Numbers($A, $arr_size, $sum) 
    { 
        $l; $r; 

        // Fix the first 
        // element as A[i] 
        for ($i = 0;  
             $i < $arr_size - 2; $i++) 
        { 
        // Fix the second  
        // element as A[j] 
        for ($j = $i + 1;  
             $j < $arr_size - 1; $j++) 
        { 
            // Now look for the 
            // third number 
            for ($k = $j + 1;  
                 $k < $arr_size; $k++) 
            { 
                if ($A[$i] + $A[$j] +  
                    $A[$k] == $sum) 
                { 
                    echo "Triplet is", " ", $A[$i], 
                                      ", ", $A[$j],  
                                      ", ", $A[$k]; 
                    return true; 
                } 
            } 
        } 
        } 

        // If we reach here, then 
        // no triplet was found 
        return false; 
    } 
    // Driver Code 
    $A = array(1, 4, 45,  
               6, 10, 8); 
    $sum = 22; 
    $arr_size = sizeof($A); 

    find3Numbers($A, $arr_size, $sum); 

    // This code is contributed by ajit 
    ?> 

    ```

    **输出**：

    ```
    Triplet is 4, 10, 8

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(n ^ 3)`。

        数组中遍历了三个嵌套循环，因此时间复杂度为`O(n ^ 3)`。

    *   **空间复杂度**：`O(1)`。

        由于不需要额外的空间。

**方法 2**： 此方法使用排序来提高代码的效率。

*   **方法**：通过对数组进行排序，可以提高算法的效率。 这种有效的方法使用了[双指针技术](https://www.geeksforgeeks.org/given-an-array-a-and-a-number-x-check-for-pair-in-a-with-sum-as-x/)。 遍历数组并修复三元组的第一个元素。 现在，使用“双指针”算法查找是否存在一对总和等于`x – array[i]`的对。 两个指针算法需要线性时间，因此它比嵌套循环更好。

*   **算法**：

    1.  排序给定的数组。

    2.  遍历数组并修复可能的三元组的第一个元素`arr[i]`。

    3.  然后固定两个指针，一个指向`i + 1`，另一个指向`n-1`。然后看一下总和，

        1.  如果总和小于所需总和，则递增第一个指针。

        2.  否则，如果总和较大，请减小结束指针以减少总和。

        3.  否则，如果两个指针处的元素之和等于给定的和，则打印三元组并中断。

*   **实现**：

    ## C++ 

    ```

    // C++ program to find a triplet 
    #include <bits/stdc++.h> 
    using namespace std; 

    // returns true if there is triplet with sum equal 
    // to 'sum' present in A[]. Also, prints the triplet 
    bool find3Numbers(int A[], int arr_size, int sum) 
    { 
        int l, r; 

        /* Sort the elements */
        sort(A, A + arr_size); 

        /* Now fix the first element one by one and find the 
           other two elements */
        for (int i = 0; i < arr_size - 2; i++) { 

            // To find the other two elements, start two index 
            // variables from two corners of the array and move 
            // them toward each other 
            l = i + 1; // index of the first element in the 
            // remaining elements 

            r = arr_size - 1; // index of the last element 
            while (l < r) { 
                if (A[i] + A[l] + A[r] == sum) { 
                    printf("Triplet is %d, %d, %d", A[i], 
                           A[l], A[r]); 
                    return true; 
                } 
                else if (A[i] + A[l] + A[r] < sum) 
                    l++; 
                else // A[i] + A[l] + A[r] > sum 
                    r--; 
            } 
        } 

        // If we reach here, then no triplet was found 
        return false; 
    } 

    /* Driver program to test above function */
    int main() 
    { 
        int A[] = { 1, 4, 45, 6, 10, 8 }; 
        int sum = 22; 
        int arr_size = sizeof(A) / sizeof(A[0]); 

        find3Numbers(A, arr_size, sum); 

        return 0; 
    } 

    ```

    ## Java

    ```

    // Java program to find a triplet 
    class FindTriplet { 

        // returns true if there is triplet with sum equal 
        // to 'sum' present in A[]. Also, prints the triplet 
        boolean find3Numbers(int A[], int arr_size, int sum) 
        { 
            int l, r; 

            /* Sort the elements */
            quickSort(A, 0, arr_size - 1); 

            /* Now fix the first element one by one and find the 
               other two elements */
            for (int i = 0; i < arr_size - 2; i++) { 

                // To find the other two elements, start two index variables 
                // from two corners of the array and move them toward each 
                // other 
                l = i + 1; // index of the first element in the remaining elements 
                r = arr_size - 1; // index of the last element 
                while (l < r) { 
                    if (A[i] + A[l] + A[r] == sum) { 
                        System.out.print("Triplet is " + A[i] + ", " + A[l] + ", " + A[r]); 
                        return true; 
                    } 
                    else if (A[i] + A[l] + A[r] < sum) 
                        l++; 

                    else // A[i] + A[l] + A[r] > sum 
                        r--; 
                } 
            } 

            // If we reach here, then no triplet was found 
            return false; 
        } 

        int partition(int A[], int si, int ei) 
        { 
            int x = A[ei]; 
            int i = (si - 1); 
            int j; 

            for (j = si; j <= ei - 1; j++) { 
                if (A[j] <= x) { 
                    i++; 
                    int temp = A[i]; 
                    A[i] = A[j]; 
                    A[j] = temp; 
                } 
            } 
            int temp = A[i + 1]; 
            A[i + 1] = A[ei]; 
            A[ei] = temp; 
            return (i + 1); 
        } 

        /* Implementation of Quick Sort 
        A[] --> Array to be sorted 
        si  --> Starting index 
        ei  --> Ending index 
         */
        void quickSort(int A[], int si, int ei) 
        { 
            int pi; 

            /* Partitioning index */
            if (si < ei) { 
                pi = partition(A, si, ei); 
                quickSort(A, si, pi - 1); 
                quickSort(A, pi + 1, ei); 
            } 
        } 

        // Driver program to test above functions 
        public static void main(String[] args) 
        { 
            FindTriplet triplet = new FindTriplet(); 
            int A[] = { 1, 4, 45, 6, 10, 8 }; 
            int sum = 22; 
            int arr_size = A.length; 

            triplet.find3Numbers(A, arr_size, sum); 
        } 
    } 

    ```

    ## Python3

    ```

    # Python3 program to find a triplet 

    # returns true if there is triplet 
    # with sum equal to 'sum' present 
    # in A[]. Also, prints the triplet 
    def find3Numbers(A, arr_size, sum): 

        # Sort the elements  
        A.sort() 

        # Now fix the first element  
        # one by one and find the 
        # other two elements  
        for i in range(0, arr_size-2): 

            # To find the other two elements, 
            # start two index variables from 
            # two corners of the array and 
            # move them toward each other 

            # index of the first element 
            # in the remaining elements 
            l = i + 1 

            # index of the last element 
            r = arr_size-1 
            while (l < r): 

                if( A[i] + A[l] + A[r] == sum): 
                    print("Triplet is", A[i],  
                         ', ', A[l], ', ', A[r]); 
                    return True

                elif (A[i] + A[l] + A[r] < sum): 
                    l += 1
                else: # A[i] + A[l] + A[r] > sum 
                    r -= 1

        # If we reach here, then 
        # no triplet was found 
        return False

    # Driver program to test above function  
    A = [1, 4, 45, 6, 10, 8] 
    sum = 22
    arr_size = len(A) 

    find3Numbers(A, arr_size, sum) 

    # This is contributed by Smitha Dinesh Semwal 

    ```

    ## C# 

    ```

    // C# program to find a triplet 
    using System; 

    class GFG { 

        // returns true if there is triplet 
        // with sum equal to 'sum' present 
        // in A[]. Also, prints the triplet 
        bool find3Numbers(int[] A, int arr_size, 
                          int sum) 
        { 
            int l, r; 

            /* Sort the elements */
            quickSort(A, 0, arr_size - 1); 

            /* Now fix the first element  
        one by one and find the 
        other two elements */
            for (int i = 0; i < arr_size - 2; i++) { 

                // To find the other two elements, 
                // start two index variables from 
                // two corners of the array and 
                // move them toward each other 
                l = i + 1; // index of the first element 
                // in the remaining elements 
                r = arr_size - 1; // index of the last element 
                while (l < r) { 
                    if (A[i] + A[l] + A[r] == sum) { 
                        Console.Write("Triplet is " + A[i] + ", " + A[l] + ", " + A[r]); 
                        return true; 
                    } 
                    else if (A[i] + A[l] + A[r] < sum) 
                        l++; 

                    else // A[i] + A[l] + A[r] > sum 
                        r--; 
                } 
            } 

            // If we reach here, then 
            // no triplet was found 
            return false; 
        } 

        int partition(int[] A, int si, int ei) 
        { 
            int x = A[ei]; 
            int i = (si - 1); 
            int j; 

            for (j = si; j <= ei - 1; j++) { 
                if (A[j] <= x) { 
                    i++; 
                    int temp = A[i]; 
                    A[i] = A[j]; 
                    A[j] = temp; 
                } 
            } 
            int temp1 = A[i + 1]; 
            A[i + 1] = A[ei]; 
            A[ei] = temp1; 
            return (i + 1); 
        } 

        /* Implementation of Quick Sort 
    A[] --> Array to be sorted 
    si --> Starting index 
    ei --> Ending index 
    */
        void quickSort(int[] A, int si, int ei) 
        { 
            int pi; 

            /* Partitioning index */
            if (si < ei) { 
                pi = partition(A, si, ei); 
                quickSort(A, si, pi - 1); 
                quickSort(A, pi + 1, ei); 
            } 
        } 

        // Driver Code 
        static void Main() 
        { 
            GFG triplet = new GFG(); 
            int[] A = new int[] { 1, 4, 45, 6, 10, 8 }; 
            int sum = 22; 
            int arr_size = A.Length; 

            triplet.find3Numbers(A, arr_size, sum); 
        } 
    } 

    // This code is contributed by mits 

    ```

    ## PHP

    ```

    <?php 
    // PHP program to find a triplet 

    // returns true if there is  
    // triplet with sum equal to 
    // 'sum' present in A[]. Also, 
    // prints the triplet 
    function find3Numbers($A, $arr_size, $sum) 
    { 
        $l; $r; 

        /* Sort the elements */
        sort($A); 

        /* Now fix the first element  
        one by one and find the 
        other two elements */
        for ($i = 0; $i < $arr_size - 2; $i++)  
        { 

            // To find the other two elements,  
            // start two index variables from  
            // two corners of the array and  
            // move them toward each other 
            $l = $i + 1; // index of the first element  
                         // in the remaining elements 

            // index of the last element 
            $r = $arr_size - 1;  
            while ($l < $r)  
            { 
                if ($A[$i] + $A[$l] +  
                    $A[$r] == $sum) 
                { 
                    echo "Triplet is ", $A[$i], " ", 
                                        $A[$l], " ",  
                                        $A[$r], "\n"; 
                    return true; 
                } 
                else if ($A[$i] + $A[$l] + 
                         $A[$r] < $sum) 
                    $l++; 
                else // A[i] + A[l] + A[r] > sum 
                    $r--; 
            } 
        } 

        // If we reach here, then 
        // no triplet was found 
        return false; 
    } 

    // Driver Code 
    $A = array (1, 4, 45, 6, 10, 8); 
    $sum = 22; 
    $arr_size = sizeof($A); 

    find3Numbers($A, $arr_size, $sum); 

    // This code is contributed by ajit 
    ?> 

    ```

    **输出**：

    ```
    Triplet is 4, 8, 10

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(N ^ 2)`。

        只有两个嵌套循环遍历数组，因此时间复杂度为`O(N ^ 2)`。 两个指针算法需要`O(n)`时间，并且可以使用另一个嵌套遍历来固定第一个元素。

    *   **空间复杂度**：`O(1)`。

        由于不需要额外的空间。

**方法 3**：这是基于哈希的解决方案。

*   **方法**：这种方法使用了额外的空间，但比两个指针方法更简单。 从头到尾运行两个循环，外循环，从`i + 1`到结束运行内循环。 创建一个哈希映射或设置为将元素存储在`i + 1`到`j-1`之间。 因此，如果给定的总和为`x`，请检查集合中是否存在等于`x – arr[i] – arr[j]`的数字。 如果是，请打印三元组。

*   **算法**：

    1.  从头到尾遍历数组。 （循环计数器`i`）

    2.  创建一个哈希映射或集合来存储唯一对。

    3.  从`i + 1`到数组末尾运行另一个循环。 （循环计数器`j`）

    4.  如果集合中有一个元素等于`x - arr[i] – arr[j]`，则打印三元组（`arr[i]`，`arr[j]`，`x-arr[i] - arr[j]`）和跳出。

    5.  将第`j`个元素插入集合中。

*   **实现**：

    ## C++ 

    ```

    // C++ program to find a triplet using Hashing 
    #include <bits/stdc++.h> 
    using namespace std; 

    // returns true if there is triplet with sum equal 
    // to 'sum' present in A[]. Also, prints the triplet 
    bool find3Numbers(int A[], int arr_size, int sum) 
    { 
        // Fix the first element as A[i] 
        for (int i = 0; i < arr_size - 2; i++) { 

            // Find pair in subarray A[i+1..n-1] 
            // with sum equal to sum - A[i] 
            unordered_set<int> s; 
            int curr_sum = sum - A[i]; 
            for (int j = i + 1; j < arr_size; j++) { 
                if (s.find(curr_sum - A[j]) != s.end()) { 
                    printf("Triplet is %d, %d, %d", A[i], 
                           A[j], curr_sum - A[j]); 
                    return true; 
                } 
                s.insert(A[j]); 
            } 
        } 

        // If we reach here, then no triplet was found 
        return false; 
    } 

    /* Driver program to test above function */
    int main() 
    { 
        int A[] = { 1, 4, 45, 6, 10, 8 }; 
        int sum = 22; 
        int arr_size = sizeof(A) / sizeof(A[0]); 

        find3Numbers(A, arr_size, sum); 

        return 0; 
    } 

    ```

    ## Java

    ```

    // Java program to find a triplet using Hashing 
    import java.util.*; 

    class GFG { 

        // returns true if there is triplet 
        // with sum equal to 'sum' present 
        // in A[]. Also, prints the triplet 
        static boolean find3Numbers(int A[], 
                                    int arr_size, int sum) 
        { 
            // Fix the first element as A[i] 
            for (int i = 0; i < arr_size - 2; i++) { 

                // Find pair in subarray A[i+1..n-1] 
                // with sum equal to sum - A[i] 
                HashSet<Integer> s = new HashSet<Integer>(); 
                int curr_sum = sum - A[i]; 
                for (int j = i + 1; j < arr_size; j++) { 
                    if (s.contains(curr_sum - A[j])) { 
                        System.out.printf("Triplet is %d, %d, %d", A[i], 
                                          A[j], curr_sum - A[j]); 
                        return true; 
                    } 
                    s.add(A[j]); 
                } 
            } 

            // If we reach here, then no triplet was found 
            return false; 
        } 

        /* Driver code */
        public static void main(String[] args) 
        { 
            int A[] = { 1, 4, 45, 6, 10, 8 }; 
            int sum = 22; 
            int arr_size = A.length; 

            find3Numbers(A, arr_size, sum); 
        } 
    } 

    // This code has been contributed by 29AjayKumar 

    ```

    ## Python3

    ```

    # Python3 program to find a triplet using Hashing 
    # returns true if there is triplet with sum equal 
    # to 'sum' present in A[]. Also, prints the triplet 
    def find3Numbers(A, arr_size, sum): 
        for i in range(0, arr_size-1): 
            # Find pair in subarray A[i + 1..n-1]  
            # with sum equal to sum - A[i] 
            s = set() 
            curr_sum = sum - A[i] 
            for j in range(i + 1, arr_size): 
                if (curr_sum - A[j]) in s: 
                    print("Triplet is", A[i],  
                            ", ", A[j], ", ", curr_sum-A[j]) 
                    return True
                s.add(A[j]) 

        return False

    # Driver program to test above function  
    A = [1, 4, 45, 6, 10, 8]  
    sum = 22
    arr_size = len(A)  
    find3Numbers(A, arr_size, sum)  

    # This is contributed by Yatin gupta 

    ```

    ## C# 

    ```

    // C# program to find a triplet using Hashing 
    using System; 
    using System.Collections.Generic; 
    public class GFG { 

        // returns true if there is triplet 
        // with sum equal to 'sum' present 
        // in A[]. Also, prints the triplet 
        static bool find3Numbers(int[] A, 
                                 int arr_size, int sum) 
        { 
            // Fix the first element as A[i] 
            for (int i = 0; i < arr_size - 2; i++) { 

                // Find pair in subarray A[i+1..n-1] 
                // with sum equal to sum - A[i] 
                HashSet<int> s = new HashSet<int>(); 
                int curr_sum = sum - A[i]; 
                for (int j = i + 1; j < arr_size; j++) { 
                    if (s.Contains(curr_sum - A[j])) { 
                        Console.Write("Triplet is {0}, {1}, {2}", A[i], 
                                      A[j], curr_sum - A[j]); 
                        return true; 
                    } 
                    s.Add(A[j]); 
                } 
            } 

            // If we reach here, then no triplet was found 
            return false; 
        } 

        /* Driver code */
        public static void Main() 
        { 
            int[] A = { 1, 4, 45, 6, 10, 8 }; 
            int sum = 22; 
            int arr_size = A.Length; 

            find3Numbers(A, arr_size, sum); 
        } 
    } 

    /* This code contributed by PrinciRaj1992 */

    ```

    **输出**：

    ```
    Triplet is 4, 8, 10

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(N ^ 2)`。

        只有两个嵌套循环遍历数组，因此时间复杂度为`O(n ^ 2)`。

    *   **空间复杂度**：`O(1)`。

        由于不需要额外的空间。

**如何打印给定总和的所有三元组？**

请参考[查找所有零和的三元组](https://www.geeksforgeeks.org/find-triplets-array-whose-sum-equal-zero/)

