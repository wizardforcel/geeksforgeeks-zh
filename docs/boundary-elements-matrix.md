# 矩阵的边界元素

> 原文： [https://www.geeksforgeeks.org/boundary-elements-matrix/](https://www.geeksforgeeks.org/boundary-elements-matrix/)

**打印矩阵的边界元素。**

给定大小为`n x m`的矩阵。 打印矩阵的边界元素。 边界元素是在所有四个方向上都没有被元素包围的元素，即第一行，第一列，最后一行和最后一列中的元素。

**示例**：

```
Input :
        1 2 3 4  
        5 6 7 8
        1 2 3 4
        5 6 7 8
Output : 
         1 2 3 4 
         5     8 
         1     4 
         5 6 7 8
Explanation:The boundary elements of the
matrix is printed.

Input:
        1 2 3   
        5 6 7 
        1 2 3 
Output: 
        1 2 3   
        5   7 
        1 2 3 
Explanation:The boundary elements of the 
matrix is printed.

```



**方法**：这个想法很简单。 遍历矩阵并检查每个元素是否在边界上，如果是，则打印该元素，否则打印空格字符。

*   **算法**：

    1.  从头到尾遍历数组。

    2.  分配外部循环以指向该行，分配内部行以遍历该行的元素。

    3.  如果元素位于矩阵的边界中，则打印该元素，即元素是否位于第一行，第一列，最后一行，最后一列。

    4.  如果元素不是边界元素，则打印空白。

*   **实现**：

    ## C++ 

    ```

    // C++ program to print boundary element of 
    // matrix. 
    #include <bits/stdc++.h> 
    using namespace std; 

    const int MAX = 100; 

    void printBoundary(int a[][MAX], int m, int n) 
    { 
        for (int i = 0; i < m; i++) { 
            for (int j = 0; j < n; j++) { 
                if (i == 0 || j == 0 || i == n - 1 || j == n - 1) 
                    cout << a[i][j] << " "; 
                else
                    cout << " "
                         << " "; 
            } 
            cout << "\n"; 
        } 
    } 

    // Driver code 
    int main() 
    { 
        int a[4][MAX] = { { 1, 2, 3, 4 }, { 5, 6, 7, 8 }, { 1, 2, 3, 4 }, { 5, 6, 7, 8 } }; 
        printBoundary(a, 4, 4); 
        return 0; 
    } 

    ```

    ## Java

    ```

    // JAVA Code for Boundary elements of a Matrix 
    class GFG { 

        public static void printBoundary(int a[][], int m, 
                                         int n) 
        { 
            for (int i = 0; i < m; i++) { 
                for (int j = 0; j < n; j++) { 
                    if (i == 0) 
                        System.out.print(a[i][j] + " "); 
                    else if (i == m - 1) 
                        System.out.print(a[i][j] + " "); 
                    else if (j == 0) 
                        System.out.print(a[i][j] + " "); 
                    else if (j == n - 1) 
                        System.out.print(a[i][j] + " "); 
                    else
                        System.out.print("  "); 
                } 
                System.out.println(""); 
            } 
        } 

        /* Driver program to test above function */
        public static void main(String[] args) 
        { 
            int a[][] = { { 1, 2, 3, 4 }, { 5, 6, 7, 8 }, { 1, 2, 3, 4 }, { 5, 6, 7, 8 } }; 

            printBoundary(a, 4, 4); 
        } 
    } 
    // This code is contributed by Arnav Kr. Mandal. 

    ```

    ## Python

    ```

    # Python program to print boundary element 
    # of the matrix. 

    MAX = 100

    def printBoundary(a, m, n): 
        for i in range(m): 
            for j in range(n): 
                if (i == 0): 
                    print a[i][j], 
                elif (i == m-1): 
                    print a[i][j], 
                elif (j == 0): 
                    print a[i][j], 
                elif (j == n-1): 
                    print a[i][j], 
                else: 
                    print " ", 
            print

    # Driver code 
    a = [ [ 1, 2, 3, 4 ], [ 5, 6, 7, 8 ],  
        [ 1, 2, 3, 4 ], [ 5, 6, 7, 8 ] ] 
    printBoundary(a, 4, 4) 

    # This code is contributed by Sachin Bisht 

    ```

    ## C# 

    ```

    // C# Code for Boundary 
    // elements of a Matrix 
    using System; 

    class GFG { 

        public static void printBoundary(int[, ] a, 
                                         int m, 
                                         int n) 
        { 
            for (int i = 0; i < m; i++) { 
                for (int j = 0; j < n; j++) { 
                    if (i == 0) 
                        Console.Write(a[i, j] + " "); 
                    else if (i == m - 1) 
                        Console.Write(a[i, j] + " "); 
                    else if (j == 0) 
                        Console.Write(a[i, j] + " "); 
                    else if (j == n - 1) 
                        Console.Write(a[i, j] + " "); 
                    else
                        Console.Write("  "); 
                } 
                Console.WriteLine(" "); 
            } 
        } 

        // Driver Code 
        static public void Main() 
        { 
            int[, ] a = { { 1, 2, 3, 4 }, 
                          { 5, 6, 7, 8 }, 
                          { 1, 2, 3, 4 }, 
                          { 5, 6, 7, 8 } }; 

            printBoundary(a, 4, 4); 
        } 
    } 

    // This code is contributed by ajit 

    ```

    ## PHP

    ```

    <?php 
    // PHP program to print  
    // boundary element of  
    // matrix. 
    $MAX = 100; 

    function printBoundary($a, $m, $n) 
    { 
        global $MAX; 
        for ($i = 0; $i < $m; $i++)  
        { 
            for ($j = 0; $j < $n; $j++)  
            { 
                if ($i == 0) 
                    echo $a[$i][$j], " "; 
                else if ($i == $m - 1) 
                    echo $a[$i][$j], " "; 
                else if ($j == 0) 
                    echo $a[$i][$j], " "; 
                else if ($j == $n - 1) 
                    echo $a[$i][$j], " "; 
                else
                    echo " ", " "; 
            } 
            echo "\n"; 
        } 
    } 

    // Driver code 
    $a = array(array( 1, 2, 3, 4 ),  
               array( 5, 6, 7, 8 ),  
               array( 1, 2, 3, 4 ),  
               array( 5, 6, 7, 8 )); 
    printBoundary($a, 4, 4); 

    // This code is contributed  
    // by akt_mit 
    ?> 

    ```

    **输出**：

    ```
    1 2 3 4 
    5     8 
    1     4 
    5 6 7 8

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(n * n)`，其中`n`是数组的大小。

        这是通过矩阵的单次遍历实现的。

    *   **空间复杂度**：`O(1)`。

        由于需要一个恒定的空间。

**查找边界元素的总和**：

给定大小为`n x m`的矩阵。 找到矩阵边界元素的总和。 边界元素是在所有四个方向上都未被元素包围的元素，即第一行，第一列，最后一行和最后一列中的元素。

**示例**：

```
Input :
        1 2 3 4  
        5 6 7 8
        1 2 3 4
        5 6 7 8
Output : 54
Explanation:The boundary elements of the matrix 
         1 2 3 4 
         5     8 
         1     4 
         5 6 7 8
Sum = 1+2+3+4+5+8+1+4+5+6+7+8 =54

Input :
        1 2 3   
        5 6 7 
        1 2 3 
Output : 24
Explanation:The boundary elements of the matrix
        1 2 3   
        5   7 
        1 2 3  
Sum = 1+2+3+5+7+1+2+3 = 24

```

**方法**：这个想法很简单。 遍历矩阵并检查每个元素是否在边界上，如果是，则将它们相加以获得所有边界元素的总和。

*   **算法**：

    1.  创建一个变量来存储总和，并从头到尾遍历数组。

    2.  分配外部循环以指向该行，分配内部行以遍历该行的元素。

    3.  如果元素位于矩阵的边界中，则将第一个元素添加到总和中，即如果元素位于第一行，第一列，最后一行，最后一列。

    4.  打印总和。

*   **实现**：

    ## C++ 

    ```

    // C++ program to find sum of boundary elements 
    // of matrix. 
    #include <bits/stdc++.h> 
    using namespace std; 

    const int MAX = 100; 

    int getBoundarySum(int a[][MAX], int m, int n) 
    { 
        long long int sum = 0; 
        for (int i = 0; i < m; i++) { 
            for (int j = 0; j < n; j++) { 
                if (i == 0) 
                    sum += a[i][j]; 
                else if (i == m - 1) 
                    sum += a[i][j]; 
                else if (j == 0) 
                    sum += a[i][j]; 
                else if (j == n - 1) 
                    sum += a[i][j]; 
            } 
        } 
        return sum; 
    } 

    // Driver code 
    int main() 
    { 
        int a[][MAX] = { { 1, 2, 3, 4 }, { 5, 6, 7, 8 }, { 1, 2, 3, 4 }, { 5, 6, 7, 8 } }; 
        long long int sum = getBoundarySum(a, 4, 4); 
        cout << "Sum of boundary elements is " << sum; 
        return 0; 
    } 

    ```

    ## Java

    ```

    // JAVA Code for Finding sum of boundary elements 
    class GFG { 

        public static long getBoundarySum(int a[][], int m, 
                                          int n) 
        { 
            long sum = 0; 
            for (int i = 0; i < m; i++) { 
                for (int j = 0; j < n; j++) { 
                    if (i == 0) 
                        sum += a[i][j]; 
                    else if (i == m - 1) 
                        sum += a[i][j]; 
                    else if (j == 0) 
                        sum += a[i][j]; 
                    else if (j == n - 1) 
                        sum += a[i][j]; 
                } 
            } 
            return sum; 
        } 

        /* Driver program to test above function */
        public static void main(String[] args) 
        { 
            int a[][] = { { 1, 2, 3, 4 }, { 5, 6, 7, 8 }, { 1, 2, 3, 4 }, { 5, 6, 7, 8 } }; 
            long sum = getBoundarySum(a, 4, 4); 
            System.out.println("Sum of boundary elements"
                               + " is " + sum); 
        } 
    } 
    // This code is contributed by Arnav Kr. Mandal. 

    ```

    ## Python

    ```

    # Python program to print boundary element  
    # of the matrix. 

    MAX = 100

    def printBoundary(a, m, n): 
        sum = 0
        for i in range(m): 
            for j in range(n): 
                if (i == 0): 
                    sum += a[i][j] 
                elif (i == m-1): 
                    sum += a[i][j] 
                elif (j == 0): 
                    sum += a[i][j] 
                elif (j == n-1): 
                    sum += a[i][j] 
        return sum

    # Driver code 
    a = [ [ 1, 2, 3, 4 ], [ 5, 6, 7, 8 ], 
        [ 1, 2, 3, 4 ], [ 5, 6, 7, 8 ] ] 
    sum = printBoundary(a, 4, 4) 
    print "Sum of boundary elements is", sum

    # This code is contributed by Sachin Bisht 

    ```

    ## C# 

    ```

    // C# Code for Finding sum 
    // of boundary elements 
    using System; 

    class GFG { 
        public static long getBoundarySum(int[, ] a, 
                                          int m, int n) 
        { 
            long sum = 0; 
            for (int i = 0; i < m; i++) { 
                for (int j = 0; j < n; j++) { 
                    if (i == 0) 
                        sum += a[i, j]; 
                    else if (i == m - 1) 
                        sum += a[i, j]; 
                    else if (j == 0) 
                        sum += a[i, j]; 
                    else if (j == n - 1) 
                        sum += a[i, j]; 
                } 
            } 
            return sum; 
        } 

        // Driver Code 
        static public void Main() 
        { 
            int[, ] a = { { 1, 2, 3, 4 }, 
                          { 5, 6, 7, 8 }, 
                          { 1, 2, 3, 4 }, 
                          { 5, 6, 7, 8 } }; 
            long sum = getBoundarySum(a, 4, 4); 
            Console.WriteLine("Sum of boundary"
                              + " elements is " + sum); 
        } 
    } 

    // This code is contributed by ajit 

    ```

    ## PHP

    ```

    <?php 
    // PHP program to find  
    // sum of boundary  
    // elements of matrix. 

    function getBoundarySum($a,  
                            $m, $n) 
    { 
        $sum = 0; 
        for ($i = 0; $i < $m; $i++) 
        { 
            for ( $j = 0; $j < $n; $j++) 
            { 
                if ($i == 0) 
                    $sum += $a[$i][$j]; 
                else if ($i == $m - 1) 
                    $sum += $a[$i][$j]; 
                else if ($j == 0) 
                    $sum += $a[$i][$j]; 
                else if ($j == $n - 1) 
                    $sum += $a[$i][$j]; 
            } 
        } 
        return $sum; 
    } 

    // Driver code 
    $a = array(array(1, 2, 3, 4),  
               array(5, 6, 7, 8),  
               array(1, 2, 3, 4),  
               array(5, 6, 7, 8)); 

    $sum = getBoundarySum($a, 4, 4); 
    echo "Sum of boundary elements is ", $sum; 

    // This code is contributed by ajit 
    ?> 

    ```

    **输出**：

    ```
    Sum of boundary elements is 54

    ```

*   **复杂度分析**：

    *   **时间复杂度**：`O(n * n)`，其中`n`是数组的大小。

        这是通过矩阵的单次遍历实现的。

    *   **空间复杂度**：`O(1)`。

        由于需要一个恒定的空间。

