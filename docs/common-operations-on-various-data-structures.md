# 对各种数据结构的通用操作

> 原文：[https://www.geeksforgeeks.org/common-operations-on-various-data-structures/](https://www.geeksforgeeks.org/common-operations-on-various-data-structures/)

[数据结构](https://www.geeksforgeeks.org/data-structures/)是一种将数据存储在计算机内存中的方式，以便可以轻松，高效地使用它。 有用于存储数据的不同数据结构。 也可以将其定义为数据项特定组织的数学或逻辑模型。 计算机主存储器中特定数据结构的表示称为存储结构。 **例如**：[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，[栈](http://www.geeksforgeeks.org/stack-data-structure/)，[队列](http://www.geeksforgeeks.org/queue-data-structure/)，[树](https://www.geeksforgeeks.org/binary-tree-data-structure/)，[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)等 。

**对不同数据结构的操作**：

对于每种数据结构中的数据操作，可以执行不同类型的操作。 一些操作的解释和说明如下：

*   **遍历**：遍历数据结构意味着访问存储在其中的元素。 可以使用任何类型的 DS 来完成。

    下面是演示数组遍历的程序：

    ## 数组

    ```

    // C++ program to traversal in an array 
    #include <iostream> 
    using namespace std; 

    // Driver Code 
    int main() 
    { 
        // Initialise array 
        int arr[] = { 1, 2, 3, 4 }; 

        // size of array 
        int N = sizeof(arr) / sizeof(arr[0]); 

        // Traverse the element of arr[] 
        for (int i = 0; i < N; i++) { 

            // Print the element 
            cout << arr[i] << ' '; 
        } 

        return 0; 
    } 

    ```

    ## 栈

    ```

    // C++ program to traversal in an stack 
    #include <bits/stdc++.h> 
    using namespace std; 

    // Function to print the elemen in stack 
    void printStack(stack<int>& St) 
    { 

        // Traverse the stack 
        while (!St.empty()) { 

            // Print top element 
            cout << St.top() << ' '; 

            // Pop top element 
            St.pop(); 
        } 
    } 

    // Driver Code 
    int main() 
    { 
        // Initialise stack 
        stack<int> St; 

        // Insert Element in stack 
        St.push(4); 
        St.push(3); 
        St.push(2); 
        St.push(1); 

        // Print elements in stack 
        printStack(St); 
        return 0; 
    } 

    ```

    ## 队列

    ```

    // C++ program to traversal 
    // in an queue 
    #include <bits/stdc++.h> 
    using namespace std; 

    // Function to print the 
    // element in queue 
    void printQueue(queue<int>& Q) 
    { 
        // Traverse the stack 
        while (!Q.empty()) { 

            // Print top element 
            cout << Q.front() << ' '; 

            // Pop top element 
            Q.pop(); 
        } 
    } 

    // Driver Code 
    int main() 
    { 
        // Initialise queue 
        queue<int> Q; 

        // Insert element 
        Q.push(1); 
        Q.push(2); 
        Q.push(3); 
        Q.push(4); 

        // Print elements 
        printQueue(Q); 
        return 0; 
    } 

    ```

    ## 链表

    ```

    // C++ program to traverse the 
    // given linked list 
    #include <bits/stdc++.h> 
    using namespace std; 
    struct Node { 
        int data; 
        Node* next; 
    }; 

    // Function that allocates a new 
    // node with given data 
    Node* newNode(int data) 
    { 
        Node* new_node = new Node; 
        new_node->data = data; 
        new_node->next = NULL; 
        return new_node; 
    } 

    // Function to insert a new node 
    // at the end of linked list 
    Node* insertEnd(Node* head, int data) 
    { 
        // If linked list is empty, 
        // Create a new node 
        if (head == NULL) 
            return newNode(data); 

        // If we have not reached the end 
        // Keep traversing recursively 
        else
            head->next = insertEnd(head->next, data); 
        return head; 
    } 

    /// Function to traverse given LL 
    void traverse(Node* head) 
    { 
        if (head == NULL) 
            return; 

        // If head is not NULL, 
        // print current node and 
        // recur for remaining list 
        cout << head->data << " "; 

        traverse(head->next); 
    } 

    // Driver Code 
    int main() 
    { 
        // Given Linked List 
        Node* head = NULL; 
        head = insertEnd(head, 1); 
        head = insertEnd(head, 2); 
        head = insertEnd(head, 3); 
        head = insertEnd(head, 4); 

        // Function Call to traverse LL 
        traverse(head); 
    } 

    ```

    **输出**：

    ```
    1 2 3 4

    ```

*   [**搜索**](https://www.geeksforgeeks.org/searching-algorithms/)：搜索意味着在给定的数据结构中找到特定的元素。 找到所需元素后，它被认为是成功的。 搜索是我们可以对数据结构（如数组，链表，树，图等）执行的操作。

    下面是说明在数组中搜索元素的程序：

    ## 数组

    ```

    // C++ program to searching in an array 
    #include <iostream> 
    using namespace std; 

    // Function that finds element K in the 
    // array 
    void findElement(int arr[], int N, int K) 
    { 

        // Traverse the element of arr[] 
        // to find element K 
        for (int i = 0; i < N; i++) { 

            // If Element is present then 
            // print the index and return 
            if (arr[i] == K) { 
                cout << "Element found!"; 
                return; 
            } 
        } 

        cout << "Element Not found!"; 
    } 

    // Driver Code 
    int main() 
    { 
        // Initialise array 
        int arr[] = { 1, 2, 3, 4 }; 

        // Element to be found 
        int K = 3; 

        // size of array 
        int N = sizeof(arr) / sizeof(arr[0]); 

        // Function Call 
        findElement(arr, N, K); 
        return 0; 
    } 

    ```

    ## 栈

    ```

    // C++ program to find element in stack 
    #include <bits/stdc++.h> 
    using namespace std; 

    // Function to find element in stack 
    void findElement(stack<int>& St, int K) 
    { 

        // Traverse the stack 
        while (!St.empty()) { 

            // Check if top is K 
            if (St.top() == K) { 
                cout << "Element found!"; 
                return; 
            } 

            // Pop top element 
            St.pop(); 
        } 

        cout << "Element Not found!"; 
    } 

    // Driver Code 
    int main() 
    { 
        // Initialise stack 
        stack<int> St; 

        // Insert Element in stack 
        St.push(4); 
        St.push(3); 
        St.push(2); 
        St.push(1); 

        // Element to be found 
        int K = 3; 

        // Function Call 
        findElement(St, K); 
        return 0; 
    } 

    ```

    ## 队列

    ```

    // C++ program to find given element 
    // in an queue 
    #include <bits/stdc++.h> 
    using namespace std; 

    // Function to find element in queue 
    void findElement(queue<int>& Q, int K) 
    { 

        // Traverse the stack 
        while (!Q.empty()) { 

            // Check if top is K 
            if (Q.front() == K) { 
                cout << "Element found!"; 
                return; 
            } 

            // Pop top element 
            Q.pop(); 
        } 

        cout << "Element Not found!"; 
    } 

    // Driver Code 
    int main() 
    { 
        // Initialise queue 
        queue<int> Q; 

        // Insert element 
        Q.push(1); 
        Q.push(2); 
        Q.push(3); 
        Q.push(4); 

        // Element to be found 
        int K = 3; 

        // Print elements 
        findElement(Q, K); 
        return 0; 
    } 

    ```

    ## 链表

    ```

    // C++ program to traverse the 
    // given linked list 
    #include <bits/stdc++.h> 
    using namespace std; 
    struct Node { 
        int data; 
        Node* next; 
    }; 

    // Function that allocates a new 
    // node with given data 
    Node* newNode(int data) 
    { 
        Node* new_node = new Node; 
        new_node->data = data; 
        new_node->next = NULL; 
        return new_node; 
    } 

    // Function to insert a new node 
    // at the end of linked list 
    Node* insertEnd(Node* head, int data) 
    { 
        // If linked list is empty, 
        // Create a new node 
        if (head == NULL) 
            return newNode(data); 

        // If we have not reached the end 
        // Keep traversing recursively 
        else
            head->next = insertEnd(head->next, data); 
        return head; 
    } 

    /// Function to traverse given LL 
    bool traverse(Node* head, int K) 
    { 
        if (head == NULL) 
            return false; 

        // If node with value K is found 
        // return true 
        if (head->data == K) 
            return true; 

        return traverse(head->next, K); 
    } 

    // Driver Code 
    int main() 
    { 
        // Given Linked List 
        Node* head = NULL; 
        head = insertEnd(head, 1); 
        head = insertEnd(head, 2); 
        head = insertEnd(head, 3); 
        head = insertEnd(head, 4); 

        // Element to be found 
        int K = 3; 

        // Function Call to traverse LL 
        if (traverse(head, K)) { 
            cout << "Element found!"; 
        } 
        else { 
            cout << "Element Not found!"; 
        } 
    } 

    ```

    **输出**：

    ```
    Element found!

    ```

*   **插入**：这是我们应用于所有数据结构的操作。 插入是指在给定的数据结构中添加元素。 当将所需元素添加到所需数据结构中时，插入操作成功。 在某些情况下，如果数据结构的大小已满，并且数据结构中没有空间可添加任何其他元素，则此操作将不成功。 插入与数组，链表，图，树中的数据结构中的插入同名。 在栈中，此操作称为“推入”。 在队列中，此操作称为入队。

    下面是说明插入栈的程序：

    ## 数组

    ```

    // C++ program for insertion in array 
    #include <iostream> 
    using namespace std; 

    // Function to print the array element 
    void printArray(int arr[], int N) 
    { 
        // Traverse the element of arr[] 
        for (int i = 0; i < N; i++) { 

            // Print the element 
            cout << arr[i] << ' '; 
        } 
    } 

    // Driver Code 
    int main() 
    { 
        // Initialise array 
        int arr[4]; 

        // size of array 
        int N = 4; 

        // Insert elements in array 
        for (int i = 1; i < 5; i++) { 
            arr[i - 1] = i; 
        } 

        // Print array element 
        printArray(arr, N); 
        return 0; 
    } 

    ```

    ## 栈

    ```

    // C++ program for insertion in array 
    #include <bits/stdc++.h> 
    using namespace std; 

    // Function to print the element in stack 
    void printStack(stack<int>& St) 
    { 

        // Traverse the stack 
        while (!St.empty()) { 

            // Print top element 
            cout << St.top() << ' '; 

            // Pop top element 
            St.pop(); 
        } 
    } 

    // Driver Code 
    int main() 
    { 
        // Initialise stack 
        stack<int> St; 

        // Insert Element in stack 
        St.push(4); 
        St.push(3); 
        St.push(2); 
        St.push(1); 

        // Print elements in stack 
        printStack(St); 
        return 0; 
    } 

    ```

    ## 队列

    ```

    // C++ program for insertion in queue 
    #include <bits/stdc++.h> 
    using namespace std; 

    // Function to print the 
    // element in queue 
    void printQueue(queue<int>& Q) 
    { 
        // Traverse the stack 
        while (!Q.empty()) { 

            // Print top element 
            cout << Q.front() << ' '; 

            // Pop top element 
            Q.pop(); 
        } 
    } 

    // Driver Code 
    int main() 
    { 
        // Initialise queue 
        queue<int> Q; 

        // Insert element 
        Q.push(1); 
        Q.push(2); 
        Q.push(3); 
        Q.push(4); 

        // Print elements 
        printQueue(Q); 
        return 0; 
    } 

    ```

    ## 链表

    ```

    // C++ program for insertion in LL 
    #include <bits/stdc++.h> 
    using namespace std; 
    struct Node { 
        int data; 
        Node* next; 
    }; 

    // Function that allocates a new 
    // node with given data 
    Node* newNode(int data) 
    { 
        Node* new_node = new Node; 
        new_node->data = data; 
        new_node->next = NULL; 
        return new_node; 
    } 

    // Function to insert a new node 
    // at the end of linked list 
    Node* insertEnd(Node* head, int data) 
    { 
        // If linked list is empty, 
        // Create a new node 
        if (head == NULL) 
            return newNode(data); 

        // If we have not reached the end 
        // Keep traversing recursively 
        else
            head->next = insertEnd(head->next, data); 
        return head; 
    } 

    /// Function to traverse given LL 
    void traverse(Node* head) 
    { 
        if (head == NULL) 
            return; 

        // If head is not NULL, 
        // print current node and 
        // recur for remaining list 
        cout << head->data << " "; 

        traverse(head->next); 
    } 

    // Driver Code 
    int main() 
    { 
        // Given Linked List 
        Node* head = NULL; 
        head = insertEnd(head, 1); 
        head = insertEnd(head, 2); 
        head = insertEnd(head, 3); 
        head = insertEnd(head, 4); 

        // Function Call to traverse LL 
        traverse(head); 
    } 

    ```

    **输出**：

    ```
    1 2 3 4

    ```

*   **删除**：这是我们应用于所有数据结构的操作。 删除意味着删除给定数据结构中的元素。 从数据结构中删除所需元素时，删除操作成功。 删除与数组，链表，图形，树等数据结构中的删除具有相同的名称。在栈中，此操作称为“弹出”。 在队列中，此操作称为出队。

    下面是说明队列中出队的程序：

    ## 栈

    ```

    // C++ program for insertion in array 
    #include <bits/stdc++.h> 
    using namespace std; 

    // Function to print the element in stack 
    void printStack(stack<int> St) 
    { 
        // Traverse the stack 
        while (!St.empty()) { 

            // Print top element 
            cout << St.top() << ' '; 

            // Pop top element 
            St.pop(); 
        } 
    } 

    // Driver Code 
    int main() 
    { 
        // Initialise stack 
        stack<int> St; 

        // Insert Element in stack 
        St.push(4); 
        St.push(3); 
        St.push(2); 
        St.push(1); 

        // Print elements before pop 
        // operation on stack 
        printStack(St); 

        cout << endl; 

        // Pop the top element 
        St.pop(); 

        // Print elements after pop 
        // operation on stack 
        printStack(St); 
        return 0; 
    } 

    ```

    ## 队列

    ```

    // C++ program to illustrate dequeue 
    // in queue 
    #include <bits/stdc++.h> 
    using namespace std; 

    // Function to print the element 
    // of the queue 
    void printQueue(queue<int> myqueue) 
    { 
        // Traverse the queue and print 
        // element at the front of queue 
        while (!myqueue.empty()) { 

            // Print the first element 
            cout << myqueue.front() << ' '; 

            // Dequeue the element from the 
            // front of the queue 
            myqueue.pop(); 
        } 
    } 

    // Driver Code 
    int main() 
    { 
        // Declare a queue 
        queue<int> myqueue; 

        // Insert element in queue from 
        // 0 to 5 
        for (int i = 1; i < 5; i++) { 

            // Insert element at the 
            // front of the queue 
            myqueue.push(i); 
        } 

        // Print element beforepop 
        // from queue 
        printQueue(myqueue); 

        cout << endl; 

        // Pop the front element 
        myqueue.pop(); 

        // Print element after pop 
        // from queue 
        printQueue(myqueue); 
        return 0; 
    } 

    ```

    ## 链表

    ```

    // C++ program for insertion in LL 
    #include <bits/stdc++.h> 
    using namespace std; 
    struct Node { 
        int data; 
        Node* next; 
    }; 

    // Function that allocates a new 
    // node with given data 
    Node* newNode(int data) 
    { 
        Node* new_node = new Node; 
        new_node->data = data; 
        new_node->next = NULL; 
        return new_node; 
    } 

    // Function to insert a new node 
    // at the end of linked list 
    Node* insertEnd(Node* head, int data) 
    { 
        // If linked list is empty, 
        // Create a new node 
        if (head == NULL) 
            return newNode(data); 

        // If we have not reached the end 
        // Keep traversing recursively 
        else
            head->next = insertEnd(head->next, data); 
        return head; 
    } 

    /// Function to traverse given LL 
    void traverse(Node* head) 
    { 
        if (head == NULL) 
            return; 

        // If head is not NULL, 
        // print current node and 
        // recur for remaining list 
        cout << head->data << " "; 

        traverse(head->next); 
    } 

    // Driver Code 
    int main() 
    { 
        // Given Linked List 
        Node* head = NULL; 
        head = insertEnd(head, 1); 
        head = insertEnd(head, 2); 
        head = insertEnd(head, 3); 
        head = insertEnd(head, 4); 

        // Print before deleting the first 
        // element from LL 
        traverse(head); 

        // Move head pointer to forward 
        // to remove the first element 

        // If LL has more than 1 element 
        if (head->next != NULL) { 
            head = head->next; 
        } 
        else { 
            head = NULL; 
        } 

        cout << endl; 

        // Print after deleting the first 
        // element from LL 
        traverse(head); 
    } 

    ```

    **输出**：

    ```
    1 2 3 4 
    2 3 4

    ```



* * *

* * *



