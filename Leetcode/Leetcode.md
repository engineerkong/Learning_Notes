## 算法：搜索，查找，排序，双指针，回溯，分治，动态规划，贪心，位运算，数学

# 数据结构：

### Array 数组

```
array = []
array.append(1)
```

### Linked List 链表

```
n1 = ListNode(4)
n1.next = n2
```

```
dummy = ListNode(0, head) # 设置dummy node便于计算
pre = None # 设置pre，以不将None计算在链表中
dummy = ListNode(0)
...
return dummy.next

```

```
# 倒序
while cur:
    nex = cur.next
    cur.next = pre
    pre = cur
    cur = nex
```

```
# 循环检索
pa,pb = headA,headB
while pa != pb:
    pa = pa.next if pa else headB
    pb = pb.next if pb else headA
return pa
```

### Stack 栈

```
stack = []
stack.append(1) # add the tail
stack.pop() # remove the tail
```

```
# 栈转化为队列
StackA -> StackB
```
### Queue 队列

```
import queue
q = queue.Queue()
d = queue.deque()
q.append(1) # add the tail
q.popleft() # remove the head
```

### String 字符串
```
str.replace('.', ' ') # 用' '代替'.'
str.strip() # 删除首尾空格
str.reverse() # 翻转单词列表
' '.join(str) # 拼接为字符串并返回
```

```
# str and list switch:
list(str) # Change str to list
s = ''.join(s) # Change list to str
s = ''.join(filter(str.isalnum,s)) # filter everything except alphabet and number to build str
str.lower() # change all alphabet to lowercase or uppercase
str_list = str.split() # Delete space and change to list
' '.join(list) is different from ''.join(list) # it will have space split between each element
```

### List 表

```
# list, tuple: sequential list (sequential storage), linked list (non-sequential storage)
# 操作: .append(), .count(), .index(), .insert(0,'a'), .pop(), .remove(), .reverse(), .sort()
list.sort() # 更改原地列表
sorted(list) # 创建新的已排序列表
SortedList(list) # 可变数据结构，更改原地列表
```

### Set 集合

```
# 输出无序且唯一的集合
set(['c','a','b','b','a']) -> {'c','a','b'} # 唯一
{'c','a','b'} == {'a','b','c'} is True # 无序
```

### Tree 树

```
n1 = TreeNode(3)
n1.left = n2
n1.right = n3
```

```
# Depth-First Search:
# 1. Preorder Traversal 前序: root, left, right
# 2. Inorder Traversal 中序: left, root, right
# 3. Postorder Traversal 后序: left, right, root

# Bread-First Search:
# Level-Order Traversal 遍历
if not root: return []
res, queue = [], collections.deque()
queue.append(root)
while queue:
    node = queue.popleft()
    res.append(node.val)
    if node.left: queue.append(node.left)
    if node.right: queue.append(node.right)
return res
```

```
def isSameTree(): # 相同树
    s.val == t.val and self.isSameTree(s.left, t.left) and self.isSameTree(s.right, t.right)
```

```
def isSubTree() # 判断子树 + isSameTree()
    self.isSameTree(s, t) or self.isSubtree(s.left, t) or self.isSubtree(s.right, t)
```


### Graph 图

```
# 由 顶点(vertex) 和 边(edge) 组成
# 分为 有向图 和 无向图
```

```
# 邻接矩阵
vertices = [1, 2, 3, 4, 5]
edges = [[0, 1, 1, 1, 1],
         [1, 0, 0, 1, 0],
         [1, 0, 0, 0, 1],
         [1, 1, 0, 0, 1],
         [1, 0, 1, 1, 0]]
```

```
# 邻接表
vertices = [1, 2, 3, 4, 5]
edges = [[1, 2, 3, 4],
         [0, 3],
         [0, 4],
         [0, 1, 4],
         [0, 2, 3]]
```


### Heap 堆

```
# 基于 完全二叉树，堆排序，优先队列
# 完全二叉树: 设二叉树深度为k，若二叉树除第k层外的其它各层（第1至k-1层）的节点达到最大个数，且处于第k层的节点都连续集中在最左边，则称此二叉树为完全二叉树。
# 分为 大顶堆，小顶堆: 任意节点的值不大于（小于）其父节点的值
```

```
heappush(heap,num)
heappop(heap) # 从小到大出堆
```

```
heap = []
# 元素入堆
heappush(heap, 1)
heappush(heap, 4)
heappush(heap, 2)
heappush(heap, 6)
heappush(heap, 8)
# 元素出堆（从小到大）
heappop(heap) # -> 1
heappop(heap) # -> 2
heappop(heap) # -> 4
heappop(heap) # -> 6
heappop(heap) # -> 8
```

### HashTable 哈希表 (Dict)

```
# Mapping key and value
dic = {}
dic[key] = value
del dic[key]
dic.get(key,0)
```

```
# .keys() .values() .items()
```

```
# enumerate
for j,k in enumerate(nums):
for i,(j,k) in enumerate(dict.items()):
```

```
# sort
sorted(original_dict, reverse=True)
```

# 复杂度

```
# 均摊复杂度 — 分析总体复杂度
1. Basic Operation 基础操作 (constant)
2. Sequential Operation 顺序操作 (addition)
3. Loop Operation 循环操作 (multiplication)
4. Branch Operation 分支操作 (maximum)
timeit.Timer # calculate the time consumption
```

### 时间复杂度

```
# 最差情况
O(1) < O(logn) < O(n) < O(nlogn) < O(n^2) < O(n^3) < O(2^n) < O(n!) < O(n^n)
f(n) <= c*g(n) --> f(n) = O(g(n))
O((1+n)*n/2) = O(n^2) # 取最高此项
```

```
# 解释 O(logN)循环或递归每层排除一半
def algorithm(N):
    count = 0
    i = N
    while i > 1:
        i = i / 2
        count += 1
    return count

def func(n):
    return func(n//2)+1
```

```
# 解释 O(NlogN)循环加循环每层排除一半
def algorithm(N):
    count = 0
    i = N
    while i > 1:
        i = i / 2
        for j in range(N):
            count += 1
```

```
# 解释 O(2^N) 递归每层分裂两倍
def algorithm(N):
    if N <= 0: return 1
    count_1 = algorithm(N - 1)
    count_2 = algorithm(N - 1)
    return count_1 + count_2
```

```
# 解释 O(N!) 递归每层分裂N,N-1倍
def algorithm(N):
    if N <= 0: return 1
    count = 0
    for _ in range(N):
        count += algorithm(N - 1)
    return count
```

### 空间复杂度
```
# 最差情况
# 暂存空间 + 输出空间
# 暴力枚举 - 空间最优，辅助哈希表 - 时间最优
```

## Others
```
return -1  # 如果未找到，返回-1表示失败
```

```
for i in range(3,-1,-1): # 3,2,1,0
```

```
# 找出并用ASCII码获得是数字的字符
'0' <= c <= '9' 
ord(c) - ord('0')
```

```
# 字符的比较是ASCII码的比较
'z' > 'a'
```

```
zip(range(), range()) # 实现滑动窗口的左右边界 i, j 同时遍历
```





**Logical Operation 逻辑运算符**

&, |, ^ (异或), ~ (反), << (乘2), >> (除2)


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

job of future, I am studying and what I want to do in the future.

25 + x = y

2(x+2) = （y +2） 2x + 2 = y

* heapq 最小堆:

`heapq.heappop(heap) 此函数会移除并返回列表（被视为堆）的第一个元素（最小元素），同时确保列表的剩余部分仍然保持堆的特性。这通常通过将最后一个元素移到第一个元素的位置，然后对其进行下沉操作以恢复堆的属性来实现。`

`heapq.heappush(heap, item) 此函数将元素添加到列表的末尾（堆的底部），然后执行上浮操作，以确保新添加的元素如果比它的父节点更小，则移动到堆的更高层。`

在堆数据结构中，上浮（Percolate Up）和下沉（Percolate Down）是两种重要的操作，用于维护堆的性质。这里我们聚焦于最小堆，但这些操作对于最大堆也是相似的，只是比较和交换的条件相反。

1. 上浮（Percolate Up）

上浮操作用于插入新元素时，以维护最小堆的性质。它的步骤如下：

1) **插入新元素**：新元素被添加到堆的末尾（即列表的最后）。
2) **比较与父节点**：比较新元素与其父节点的值。在最小堆中，如果新元素小于其父节点，那么它们的位置需要交换。
3) **递归或迭代**：继续将新元素与其新的父节点进行比较，直到新元素大于其父节点或者它已经移动到堆的顶部（成为根节点）。

2. 下沉（Percolate Down）

下沉操作用于删除元素（通常是根元素）时，以维护最小堆的性质。它的步骤如下：

1) **删除根元素**：通常在最小堆中，我们删除根元素（最小元素）。删除后，通常将堆的最后一个元素移动到根的位置。
2) **比较与子节点**：将新的根元素与其子节点进行比较。在最小堆中，如果根元素大于它的任一子节点，那么它应与其最小的子节点交换位置。
3) **递归或迭代**：继续下沉过程，将元素与其子节点比较并在必要时交换，直到它小于所有子节点或者成为叶节点。

* yield:

```
def preorder(self, root: 'Node') -> List[int]:
  def dfs(node):
      if node:
          yield node.val
          for child in node.children:
              yield from dfs(child)
              
  return [v for v in dfs(root)] 
```

* 数组唯一化(unique)

```
unique_array = []
[unique_array.append(x) for x in array if x not in unique_array]
```

* set(sorted()) -> set, sorted(set()) -> list

* `for x in count(n + 1):`: x不断+1，由原n+1 到原n+2

* `y,v=divmod(y,10)`: 同时取商y和余数v

* 回溯操作

```
def backtrack(index: int):
   if index == len(digits):
       combinations.append("".join(combination))
   else:
       digit = int(digits[index])
       for letter in dic[digit]:
           combination.append(letter)
           backtrack(index + 1)
           combination.pop()
```
