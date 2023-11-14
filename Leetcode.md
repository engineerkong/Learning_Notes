### Time Complexity

f(n) <= c*g(n) --> f(n) = O(g(n))

O(1) < O(logn) < O(n) < O(nlogn) < O(n^2) < O(n^3) < O(2^n) < O(n!) < O(n^n)

1. Basic Operation 基础操作 (constant)

2. Sequential Operation 顺序操作 (addition)

3. Loop Operation 循环操作 (multiplication)

4. Branch Operation 分支操作 (maximum)

`timeit.Timer` - calculate the time consumption

## Programm = Data Structure + Algorithm

### Data Structure

**List 表** 
list, tuple:

sequential list (sequential storage)

linked list (non-sequential storage)

SortedList() automatically sort the elements in list - `sorted(list)`

operation: `append()`, `count()`, `index()`, `insert(0,'a')`, `pop()`, `remove()`, `reverse()`, `sort()`

**Stack 栈**

`push()`: add the tail

`pop()`: remove the tail

**Queue 队列**

`enqueue()`: add the tail

`dequeue()`: remove the head

**Tree 树**

Depth-First Search:

1. Preorder Traversal 前序: root, left, right

2. Inorder Traversal 中序: left, root, right

3. Postorder Traversal 后序: left, right, root

Bread-First Search:

Level-Order Traversal 遍历

**Logical Operation 逻辑运算符**

&, |, ^ (异或), ~ (反), << (乘2), >> (除2)

**HashTable 哈希表**

Mapping key and value

`.keys()`, `.values()`, `.items()`

`dic = {}` -> `dic[i]=xx`

`for j,k in enumerate(nums)`

`for i,(j,k) in enumerate(dict.items())`

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

### Notes

* str and list switch:

`set()`: Change str to list

`s = ''.join(s)`: Change list to str

`s = ''.join(filter(str.isalnum,s))`: filter everything except alphabet and number to build str

`str.lower()`: change all alphabet to lowercase or uppercase

`str_list = str.split()`: Delete space and change to list

* double pointer:

slow and fast

* binary, decimal and logic:

`int(a,2)` binary to decimal

`bin(a)` decimal to binary

`x & -x` sequentially get the element of x (1,2,4,8,...)

`num + 4294967296` (32bit): reverse interger

* value switch:

queue sequence switch p->c->t --- p<-c<-t:

`
while cur:
   tmp = cur.next
   cur.next = pre
   pre = cur
   cur = tmp
`

`f(n) = f(n-1) + f(n-2)`

`a, b = b, a+b`

* Boolen:

`.all()`, `.any()`: determine if all True or one True

* variable:

`nonlocal res` - define res as nonlocal variable in the external function

* algorithm:

`min(enumerate(list),key=lambda x:x[1])[0]`: find the index of minimum

`(s+s)[1:-1].find(s) != -1`: remove match

prefix table and suffix table -> langest equal prefix and suffix -> next array: KMP

* list reverse (541):

`s_list[xx][::-1]`

also str can not be assigned directly, need to be switched to list and switched back `s_list=list(s) s=''.join(s_list)`
