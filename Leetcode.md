### Time Complexity

f(n) <= c*g(n) --> f(n) = O(g(n))
O(1) < O(logn) < O(n) < O(nlogn) < O(n^2) < O(n^3) < O(2^n) < O(n!) < O(n^n)
1. Basic Operation 基础操作 (constant)
2. Sequential Operation 顺序操作 (addition)
3. Loop Operation 循环操作 (multiplication)
4. Branch Operation 分支操作 (maximum)

timeit.Timer - calculate the time consumption

## Programm = Data Structure + Algorithm

### Data Structure

**1. List 表** 
list, tuple:
sequential list (sequential storage)
linked list (non-sequential storage)

**2. Stack 栈**
push(): add the tail
pop(): remove the tail

**3. Queue 队列**
enqueue(): add the tail
dequeue(): remove the head

**4. Tree 树**
Depth-First Search:
1. Preorder Traversal 前序: root, left, right
2. Inorder Traversal 中序: left, root, right
3. Postorder Traversal 后序: left, right, root
Bread-First Search:
Level-Order Traversal 遍历

### Algorithm

**Sorting Algorithm**
1. Bubble Sort 冒泡 bubble
2. Selection Sort 选择 select the max/min in the unsorted list
3. Insertion Sort 插入 poker card
4. Quit Sort 快速 pivot and sort each part
5. Hash Sort 哈希 
6. Merge Sort 归并 merge and start with min and max in a part

**Searching Algorithm**
1. Linear Search 线性
2. Binary Search 二分
3. Binary Search Tree 二叉树 left smaller and right larger and insert
4. Hash Search 哈希
