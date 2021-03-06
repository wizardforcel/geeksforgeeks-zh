# Python | 使用双链表实现栈

> 原文：[https://www.geeksforgeeks.org/python-stack-using-doubly-linked-list/](https://www.geeksforgeeks.org/python-stack-using-doubly-linked-list/)

栈是使用后进先出原理（LIFO）插入和删除的对象的集合。 用户可以将元素插入栈，并且只能访问或删除栈顶部最近插入的对象。 在数组上使用链表来实现栈的主要优点是**动态分配数据**，而在数组中，栈的大小受到限制，并且当栈的大小超出最大大小时出现栈溢出错误。

### 栈操作：

1. `push()`：将元素插入栈，并将顶部指针分配给该元素。
2. `pop()`：从栈返回顶部元素，并将顶部指针移到栈的第二个元素。
3. `top()`：返回顶部元素。
4. `size()`：返回栈的大小。
5. `isEmpty()`：如果栈为空，则返回`True`，否则返回`False`。
6. `printstack()`：打印栈中的所有元素。

### 以下是在 Python 中使用双链表实现上述栈操作的方法：

```

# A complete working Python program to demonstrate all  
# stack operations using a doubly linked list  

# Node class  
class Node: 

# Function to initialise the node object 
    def __init__(self, data): 
        self.data = data # Assign data 
        self.next = None # Initialize next as null 
        self.prev = None # Initialize prev as null         

# Stack class contains a Node object 
class Stack: 
    # Function to initialize head  
    def __init__(self): 
        self.head = None

# Function to add an element data in the stack  
    def push(self, data): 

        if self.head is None: 
            self.head = Node(data) 
        else: 
            new_node = Node(data) 
            self.head.prev = new_node 
            new_node.next = self.head 
            new_node.prev = None
            self.head = new_node 

# Function to pop top element and return the element from the stack  
    def pop(self): 

        if self.head is None: 
            return None
        elif self.head.next is None: 
            temp = self.head.data 
            self.head = None
            return temp 
        else: 
            temp = self.head.data 
            self.head = self.head.next
            self.head.prev = None
            return temp 

# Function to return top element in the stack  
    def top(self): 

        return self.head.data 

# Function to return the size of the stack  
    def size(self): 

        temp = self.head 
        count = 0
        while temp is not None: 
            count = count + 1
            temp = temp.next
        return count 

# Function to check if the stack is empty or not   
    def isEmpty(self): 

        if self.head is None: 
           return True
        else: 
           return False

# Function to print the stack 
    def printstack(self): 

        print("stack elements are:") 
        temp = self.head 
        while temp is not None: 
            print(temp.data, end ="->") 
            temp = temp.next           

# Code execution starts here          
if __name__=='__main__':  

# Start with the empty stack 
  stack = Stack() 

# Insert 4 at the beginning. So stack becomes 4->None  
  print("Stack operations using Doubly LinkedList") 
  stack.push(4) 

# Insert 5 at the beginning. So stack becomes 4->5->None  
  stack.push(5) 

# Insert 6 at the beginning. So stack becomes 4->5->6->None  
  stack.push(6) 

# Insert 7 at the beginning. So stack becomes 4->5->6->7->None  
  stack.push(7) 

# Print the stack 
  stack.printstack() 

# Print the top element 
  print("\nTop element is ", stack.top()) 

# Print the stack size 
  print("Size of the stack is ", stack.size()) 

# pop the top element 
  stack.pop() 

# pop the top element 
  stack.pop() 

# two elements are popped 
# Print the stack 
  stack.printstack() 

# Print True if the stack is empty else False 
  print("\nstack is empty:", stack.isEmpty()) 

#This code is added by Suparna Raut 

```

**输出**：

```
Stack operations using Doubly LinkedList
stack elements are:
7->6->5->4->
Top element is  7
Size of the stack is  4
stack elements are:
5->4->
stack is empty: False

```


* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。