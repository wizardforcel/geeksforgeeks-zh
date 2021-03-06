# 通过最多买卖两次股份获得的最大利润

> 原文： [https://www.geeksforgeeks.org/maximum-profit-by-buying-and-selling-a-share-at-most-twice/](https://www.geeksforgeeks.org/maximum-profit-by-buying-and-selling-a-share-at-most-twice/)

在每日股票交易中，买主在早上购买股票并在同一天出售。 如果允许交易者一天最多进行两笔交易，而第二笔交易只能在第一笔交易完成后才能开始（卖出->买入->卖出->买入）。 给定全天股价，找出股票交易者可以赚取的最大利润。

**示例**：

```
Input:   price[] = {10, 22, 5, 75, 65, 80}
Output:  87
Trader earns 87 as sum of 12 and 75
Buy at price 10, sell at 22, buy at 5 and sell at 80

Input:   price[] = {2, 30, 15, 10, 8, 25, 80}
Output:  100
Trader earns 100 as sum of 28 and 72
Buy at price 2, sell at 30, buy at 8 and sell at 80

Input:   price[] = {100, 30, 15, 10, 8, 25, 80};
Output:  72
Buy at price 8 and sell at 80.

Input:   price[] = {90, 80, 70, 60, 50}
Output:  0
Not possible to earn.
```



**简单解决方案**是考虑每个索引`i`，然后执行以下操作：

```
Max profit with at most two transactions =
       MAX {max profit with one transaction and subarray price[0..i] +
            max profit with one transaction and aubarray price[i+1..n-1]  }
i varies from 0 to n-1\. 
```

可以使用以下`O(n)`算法计算一次交易的最大可能金额：[两个元素之间的最大差异，使得较大的元素出现在较小的数字之后](https://www.geeksforgeeks.org/maximum-difference-between-two-elements/)。

上述简单解的时间复杂度为 `O(n^2)`。

我们可以使用以下**有效解**来实现`O(n)`。 想法是存储每个子数组的最大可能利润，并在接下来的两个阶段中解决问题。

1.  创建一个表`profit[0..n-1]`并初始化其中的所有值 0。

2.  从右到左遍历`price[]`并更新`profit[i]`，以使`profit[i]`在子数组`price[i..n-1]`中存储可从一次交易获得的最大利润。

3.  从左到右遍历`price[]`并更新`profit[i]`，以使`profit[i]`存储最大利润，从而使`profit[i]`包含子数组`price[0..i]`中两次交易的最大可实现利润。

4.  返回`profit[n-1]`。

要执行步骤 2，我们需要从右到左跟踪最大价格，而要执行步骤 3，我们需要从左到右跟踪最小价格。 为什么我们要反向走？ 这个想法是为了节省空间，在第三步中，我们为两个目的使用相同的数组，最多 1 个事务，最大 2 个事务。 在迭代`i`之后，数组`profit[0..i]`包含 2 个事务的最大利润，而`profit[i + 1..n-1]`包含 2 个事务的利润。

以下是上述想法的实现。

## C++ 

```cpp

// C++ program to find maximum possible profit with at most 
// two transactions 
#include<bits/stdc++.h> 
using namespace std; 

// Returns maximum profit with two transactions on a given 
// list of stock prices, price[0..n-1] 
int maxProfit(int price[], int n) 
{ 
    // Create profit array and initialize it as 0 
    int *profit = new int[n]; 
    for (int i=0; i<n; i++) 
        profit[i] = 0; 

    /* Get the maximum profit with only one transaction 
       allowed. After this loop, profit[i] contains maximum 
       profit from price[i..n-1] using at most one trans. */
    int max_price = price[n-1]; 
    for (int i=n-2;i>=0;i--) 
    { 
        // max_price has maximum of price[i..n-1] 
        if (price[i] > max_price) 
            max_price = price[i]; 

        // we can get profit[i] by taking maximum of: 
        // a) previous maximum, i.e., profit[i+1] 
        // b) profit by buying at price[i] and selling at 
        //    max_price 
        profit[i] = max(profit[i+1], max_price-price[i]); 
    } 

    /* Get the maximum profit with two transactions allowed 
       After this loop, profit[n-1] contains the result */
    int min_price = price[0]; 
    for (int i=1; i<n; i++) 
    { 
        // min_price is minimum price in price[0..i] 
        if (price[i] < min_price) 
            min_price = price[i]; 

        // Maximum profit is maximum of: 
        // a) previous maximum, i.e., profit[i-1] 
        // b) (Buy, Sell) at (min_price, price[i]) and add 
        //    profit of other trans. stored in profit[i] 
        profit[i] = max(profit[i-1], profit[i] + 
                                    (price[i]-min_price) ); 
    } 
    int result = profit[n-1]; 

    delete [] profit; // To avoid memory leak 

    return result; 
} 

// Driver program 
int main() 
{ 
    int price[] = {2, 30, 15, 10, 8, 25, 80}; 
    int n = sizeof(price)/sizeof(price[0]); 
    cout << "Maximum Profit = " << maxProfit(price, n); 
    return 0; 
} 

```

## Java

```java

class Profit 
{ 
    // Returns maximum profit with two transactions on a given 
    // list of stock prices, price[0..n-1] 
    static int maxProfit(int price[], int n) 
    { 
        // Create profit array and initialize it as 0 
        int profit[] = new int[n]; 
        for (int i=0; i<n; i++) 
            profit[i] = 0; 

        /* Get the maximum profit with only one transaction 
           allowed. After this loop, profit[i] contains maximum 
           profit from price[i..n-1] using at most one trans. */
        int max_price = price[n-1]; 
        for (int i=n-2;i>=0;i--) 
        { 
            // max_price has maximum of price[i..n-1] 
            if (price[i] > max_price) 
                max_price = price[i]; 

            // we can get profit[i] by taking maximum of: 
            // a) previous maximum, i.e., profit[i+1] 
            // b) profit by buying at price[i] and selling at 
            //    max_price 
            profit[i] = Math.max(profit[i+1], max_price-price[i]); 
        } 

        /* Get the maximum profit with two transactions allowed 
           After this loop, profit[n-1] contains the result */
        int min_price = price[0]; 
        for (int i=1; i<n; i++) 
        { 
            // min_price is minimum price in price[0..i] 
            if (price[i] < min_price) 
                min_price = price[i]; 

            // Maximum profit is maximum of: 
            // a) previous maximum, i.e., profit[i-1] 
            // b) (Buy, Sell) at (min_price, price[i]) and add 
            //    profit of other trans. stored in profit[i] 
            profit[i] = Math.max(profit[i-1], profit[i] + 
                                        (price[i]-min_price) ); 
        } 
        int result = profit[n-1]; 
        return result; 
    } 

    public static void main(String args[]) 
    { 
        int price[] = {2, 30, 15, 10, 8, 25, 80}; 
        int n = price.length; 
        System.out.println("Maximum Profit = "+ maxProfit(price, n)); 
    } 

}/* This code is contributed by Rajat Mishra */

```

## Python

```py

# Returns maximum profit with two transactions on a given  
# list of stock prices price[0..n-1] 
def maxProfit(price,n): 

    # Create profit array and initialize it as 0 
    profit = [0]*n 

    # Get the maximum profit with only one transaction 
    # allowed. After this loop, profit[i] contains maximum 
    # profit from price[i..n-1] using at most one trans. 
    max_price=price[n-1] 

    for i in range( n-2, 0 ,-1): 

        if price[i]> max_price: 
            max_price = price[i] 

        # we can get profit[i] by taking maximum of: 
        # a) previous maximum, i.e., profit[i+1] 
        # b) profit by buying at price[i] and selling at 
        #    max_price 
        profit[i] = max(profit[i+1], max_price - price[i]) 

    # Get the maximum profit with two transactions allowed 
    # After this loop, profit[n-1] contains the result     
    min_price=price[0] 

    for i in range(1,n): 

        if price[i] < min_price: 
            min_price = price[i] 

        # Maximum profit is maximum of: 
        # a) previous maximum, i.e., profit[i-1] 
        # b) (Buy, Sell) at (min_price, A[i]) and add 
        #    profit of other trans. stored in profit[i]     
        profit[i] = max(profit[i-1], profit[i]+(price[i]-min_price)) 

    result = profit[n-1] 

    return result 

# Driver function 
price = [2, 30, 15, 10, 8, 25, 80] 
print "Maximum profit is", maxProfit(price, len(price)) 

# This code is contributed by __Devesh Agrawal__ 

```

## C# 

```cs

// C# program to find maximum possible profit 
// with at most two transactions 
using System; 

class GFG { 

    // Returns maximum profit with two 
    // transactions on a given list of  
    // stock prices, price[0..n-1] 
    static int maxProfit(int []price, int n) 
    { 

        // Create profit array and initialize 
        // it as 0 
        int []profit = new int[n]; 
        for (int i = 0; i < n; i++) 
            profit[i] = 0; 

        /* Get the maximum profit with only 
        one transaction allowed. After this  
        loop, profit[i] contains maximum 
        profit from price[i..n-1] using at 
        most one trans. */
        int max_price = price[n-1]; 

        for (int i = n-2; i >= 0; i--) 
        { 

            // max_price has maximum of 
            // price[i..n-1] 
            if (price[i] > max_price) 
                max_price = price[i]; 

            // we can get profit[i] by taking  
            // maximum of: 
            // a) previous maximum, i.e.,  
            // profit[i+1] 
            // b) profit by buying at price[i] 
            // and selling at max_price 
            profit[i] = Math.Max(profit[i+1],  
                          max_price - price[i]); 
        } 

        /* Get the maximum profit with two 
        transactions allowed After this loop, 
        profit[n-1] contains the result */
        int min_price = price[0]; 

        for (int i = 1; i < n; i++) 
        { 

            // min_price is minimum price in 
            // price[0..i] 
            if (price[i] < min_price) 
                min_price = price[i]; 

            // Maximum profit is maximum of: 
            // a) previous maximum, i.e., 
            // profit[i-1] 
            // b) (Buy, Sell) at (min_price, 
            // price[i]) and add profit of  
            // other trans. stored in 
            // profit[i] 
            profit[i] = Math.Max(profit[i-1], 
                       profit[i] + (price[i] 
                              - min_price) ); 
        } 
        int result = profit[n-1]; 

        return result; 
    } 

    public static void Main() 
    { 
        int []price = {2, 30, 15, 10, 
                                  8, 25, 80}; 
        int n = price.Length; 

        Console.Write("Maximum Profit = "
                      + maxProfit(price, n)); 
    } 
} 

// This code is contributed by nitin mittal. 

```

## PHP

```php

<?php 
// PHP program to find maximum  
// possible profit with at most  
// two transactions 

// Returns maximum profit with  
// two transactions on a given  
// list of stock prices, price[0..n-1]  
function maxProfit($price, $n)  
{ 
    // Create profit array and 
    // initialize it as 0  
    $profit = array();  
    for ($i = 0; $i < $n; $i++)  
        $profit[$i] = 0;  

    // Get the maximum profit with  
    // only one transaction allowed. 
    // After this loop, profit[i] 
    // contains maximum profit from  
    // price[i..n-1] using at most  
    // one trans.  
    $max_price = $price[$n - 1];  
    for ($i = $n - 2; $i >= 0; $i--)  
    {  
        // max_price has maximum  
        // of price[i..n-1]  
        if ($price[$i] > $max_price)  
            $max_price = $price[$i];  

        // we can get profit[i] by  
        // taking maximum of:  
        // a) previous maximum,  
        //    i.e., profit[i+1]  
        // b) profit by buying at  
        // price[i] and selling at  
        // max_price  
        if($profit[$i + 1] > 
           $max_price-$price[$i]) 
        $profit[$i] = $profit[$i + 1];  
        else
        $profit[$i] = $max_price - 
                      $price[$i]; 
    }  

    // Get the maximum profit with  
    // two transactions allowed.  
    // After this loop, profit[n-1]  
    // contains the result  
    $min_price = $price[0];  
    for ($i = 1; $i < $n; $i++)  
    {  
        // min_price is minimum  
        // price in price[0..i]  
        if ($price[$i] < $min_price)  
            $min_price = $price[$i];  

        // Maximum profit is maximum of:  
        // a) previous maximum,  
        //    i.e., profit[i-1]  
        // b) (Buy, Sell) at (min_price,  
        //     price[i]) and add  
        // profit of other trans.  
        // stored in profit[i]  
        $profit[$i] = max($profit[$i - 1],  
                          $profit[$i] +  
                         ($price[$i] - $min_price));  
    }  
    $result = $profit[$n - 1];  
    return $result;  
} 

// Driver Code  
$price = array(2, 30, 15, 10, 
               8, 25, 80);  
$n = sizeof($price);  
echo "Maximum Profit = ".  
      maxProfit($price, $n);  

// This code is contributed 
// by Arnab Kundu 
?> 

```

**输出**：

```
Maximum Profit = 100
```

上述解决方案的时间复杂度为`O(n)`。

算法范例：动态规划。

