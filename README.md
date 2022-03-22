# __数据结构__ 

## __目录__
1. 基本概念
2. C++语法
3. 线性表
4. 栈与队列
5. 串
6. 数组与广义表
7. 树与二叉树
8. 图
9. 查找与排序

## __基本概念__

###  1. 数据结构
* 数据结构是相互之间存在一种或多种特定关系的数据元素的集合
* 数据结构三要素：逻辑结构、存储结构、数据的运算

### 2. 抽象数据类型
* 抽象数据类型：一个数学模型以及定义在该模型上的一组操作
* 抽象数据类型定义只取决于一组逻辑特性，与如何实现无关

### 3. 算法
* 算法的特性：有穷性、确定性、可行性、输入、输出
* 好算法的目标：正确性、可读性、健壮性、效率与低存储要求
* __时间复杂度__：所有语句重复次数的最高阶
* __空间复杂度__：额外占用的存储空间大小规模
## __C++__

### 1. 结构体
```cpp
struct StructName{
    ElemType elem1;
    ElemType elem2;
    ...;
}StructName;
```

### 2. C++标准库STL
* vector 可变数组
* string 字符串
* unordered_map 哈希map
* unordered_set 哈希set
* queue 队列
* stack 栈

## __线性表__

### 1. 定义及性质
* 线性表是n个相同数据类型的数据元素的有限序列，表示元素间一对一的关系（逻辑结构）
* 线性表有两种储存方式：顺序表、链表（存储结构）

### 2. 单链表
|  data   | next  |
|  ----  | ----  |
+ 结点
```cpp
struct ListNode{
    ElemType data;//数据域
    struct ListNode *next;//指针域
}ListNode;  
```
+ 创建
```cpp
ListNode *LinkList = new ListNode();
```
### 3. 链表基本操作
* __按位查找__
```cpp
ListNode *GetElem(ListNode *L, int i) {
    int count = i;           //从1开始计数
    ListNode *p = L->next;   //p指向第一个结点
    if (i == 0) return L;    // i=0，返回头节点
    if (i < 1) return NULL;  //i无效，返回NULL
    while (p && count < i) { //遍历找到第i个结点
        p = p->next;
        j++;
    }
    return p;               //返回指向第i个结点的指针
}
``` 
* __按值查找__
```cpp
ListNode *LocateElem(ListNode *L, ElemType e) {
    ListNode *p = L->next;              
    while (p != NULL && p->data != e) {//从第一个结点查找data等于e的结点
        p = p->next;
    } 
    return p;   //返回指向值为e的指针
}
```
* __插入__
```cpp
//后插法
ListNode *ListInsert_Back(ListNode *L, ListNode *s, int i) {
    ListNode *p = GetElem(L, i-1);//p指向插入位置的前驱结点
    s->next = p->next;            //修改指针域
    p->next = s;
    return L;
}

//前插法
ListNode *ListInsert_front(ListNode *L, LinkList*s, int i) {
    ListNode *p = GetElem(L, i-1);
    s->next = p->next;        //修改指针域
    p->next = s;
    ElemType temp = p->data; //交换数据域
    p->data = s->data;
    s->data = temp; 
    return L;
}
```
* __删除__
```cpp
//删除第i个结点
ListNode *ListDelete(ListNode *L, int i) {
    ListNode *p = GetElem(L, i-1);
    ListNode *q = p->next;
    p->next = q->next; //前驱结点指向后继结点
    delete(q);         //释放内存空间
    return L;
}

//删除给定结点*p
ListNode *ListDelete(ListNode*p) {
    ListNode *q = p->next;
    p->data = p->next->data; //将后继结点的值赋给p
    p->next = q->next;       //删除后继结点
    delete(q);
    return p;
}
```

* 遍历输出
```cpp

```

* 交换元素位置
```cpp

```

### 4. 链表插入与删除的复杂度  
|  操作  |  时间复杂度  |  空间复杂度  |
|  :---  |  :--:  |  :--:  |
|  前插  | O(n)  |  O(1)  |
|  后插  | O(n)  |  O(1)  |
|  删除第i个结点  |  O(n)  |  O(1)  |
|  删除给定结点p  |  O(1)  |  O(1)  |
* 主要的时间耗费是找到第i个结点

### 5. 其他链表
* 循环链表  
    &#8195;&#8195;循环链表最后一个结点的指针不是NULL，而是指向头节点，即tail->next = head
* 双向链表
    |  prior  |  data  |  next  |
    |  ----  |  ----  |  ----  |
    + 结点
    ```cpp
    struct DListNode{
        ElemType data;//数据域
        struct ListNode * prior, *next;//指针域
    }DListNode;  
    ```
    + 创建
    ```cpp
    DListNode *DLinkList = new DListNode();
    ```

* 静态链表  
    &#8195;&#8195;静态链表用数组来描述线性表的链式存储结构
    | index |  data  |  next  |
    | :--:  |  :--:  |  :--:  |
    |0||2|
    |1|b|6|
    |2|a|1|
    |3|d|-1|
    |4|||
    |5|||
    |6|c|3|
    &#8195;&#8195;静态链表对应的单链表a->b->c->d

## __栈与队列__

### 1. 定义及性质
* 栈是只允许在一端进行插入和删除的线性表（FILO）
* 队列是只允许在表的一端进行插入，另一段进行删除的线性表（FIFO）

### 2. 顺序栈
* 结构体 
```cpp
struct SqStack{
    ElemType data[MaxSize];
    int top; 
}SqStack;
```
* 指针初始位置
```cpp
//初始化
void InitStack(SqStack &S) {
    S.top == 0;//栈顶指针(指向栈顶元素的下一个存储单元)
}
```
* 顺序栈的基本操作  

__入栈__（push）
```cpp
bool StackPush(SqStack &S, ElemType x) {
    if (StackFull()) return false;
    S.data[S.top++] == x//先送值到栈顶元素，后移动指针
}
```  
  
__出栈__（pop）
```cpp
bool StackPop(SqStack &S, ElemType &x) {
    if (!StackEmpty()) {
        ElemType x;
        x = S.data[--S.top];//先移动指针，后赋值给x
        return ture;
    }
    return false;
}
```
__取栈顶元素__
```cpp
bool getTop(SqStack S, ElemType &x) {
    if (!StackEmpty()) return false;
    x = S.data[S.top - 1];
    return true;
}
```
判断栈满
```cpp
bool StackFull(SqSatck S){
    return S.top == MaxSize;
}
```
__判断栈空__
```cpp
bool StackEmpty(SqStack S) {
    return S.top == 0;
}
```
求栈长
```cpp
int StackLength(SqStack S) {
    return S.top;
}
```

### 3. 共享栈
&#8195;&#8195;两个栈共享一个一维数组空间，两个栈的栈底分别设置在共享空间的两端，两个栈顶向共享空间中间延伸

* 结构体
```cpp
struct ShareStack{
    ElemType data[MaxSize];
    int top0;
    int top1;
}ShareStack;
```
* 指针初始位置
```cpp
//初始化
S.top0 == 0;//栈顶指针(指向栈顶元素的下一个存储单元)
S.top1 == StackSize - 1;
```
* 指针变化模式
```cpp
//S0入栈
S.data[S.top0++] = x;
//S1入栈
S.data[S.top1--] = x;
//S0出栈
x = S.data[--S.top0];
//S1出栈
x = S.data[++S.top1];
```

### 4. 循环队列
&#8195;&#8195;循环队列是首尾相连的环形顺序队列，通过取余运算实现指针循环
* 存储结构
```cpp
struct SqQueue{
    ElemType data[MaxSize];
    int front, rear;
};
```
* 指针初始位置
```cpp
Q.front = Q.rear = 0;
//队满条件
(Q.rear + 1) & MaxSize == Q.front;
//队空条件
Q.rear == Q.front;
```
* 指针变化模式
```cpp
//队头指针进1
Q.front = (Q.front + 1) % MaxiSize;
//队尾指针进1
Q.rear = (Q.rear + 1) % MaxSize;
//队列长度
(Q.rear + MaxSize - Q.front) % MaxSize;//
```
* 基本操作

入队
```cpp
bool EnQueue(SqQueue &Q) {
    if ((Q.rear + 1) & MaxSize == Q.front) return false;
    Q.data[Q.rear] = x;
    Q.rear = (Q.rear + 1) % MaxSize;
    return true;
}
```
出队
```cpp
bool DeQueue(SqQueue &Q) {
    if ((Q.rear == Q.front) return false;
    x = Q.data[Q.front];
    Q.front = (Q.front + 1) % MaxSize;
    return true;
}
```
### 5. 链队列
* 存储结构
```cpp
struct LinkNode{//链队列结点
    ElemType data;
    struct LinkNode *next;
}LinkNode;
struct {
    LinkNode *front, *rear;//头尾指针
}LinkQueue;
```
* 基本操作

入队
```cpp
void EnQueue(LinkQueue &Q, ElemType x) {
    LinkNode *s = new LinkNode();
    s->data = x;
    s->next = NULL;
    Q.rear->next = s;
    Q.rear = s;
}
```
出队
```cpp
bool deQueue(LinkQueue &Q, ElemType &x) {
    if (Q.rear == Q.front) return false;
    LinkNode *p = Q.front->next;
    x = p->data;
    Q.front->next = p->next;
    free(p);
    return true;
}
```

### 6. 栈与队列算法应用
	
## __串__
### 1. 定义及概念
### 2. 先、中、后（波兰）表达式转换
### 3. 模式匹配（KMP）
* next数组
* nextval数组
	
## __数组与广义表__
### 1. 定义及概念
* 
### 2. 二、三维数组地址求解
* 
### 3. 特殊数组存储方式
* 
### 4. 广义表的长度与深度
* 
### 5. head、tail的操作
* 

## __树与二叉树__
### 1. 定义及概念
* 
### 2. 先中后序遍历（算法）
* 
### 3. 完全二叉树与满二叉树的性质
* 
### 4. 平衡二叉树
* 调整方法
### 5. 二叉排序树
* 与中序遍历结合
* 求前驱后继
* 平均查找长度
### 6. 线索二叉树
* 创建
* 求前驱后继
### 7. 哈夫曼树
* 构建
* 求带权路径长度
	
## __图__
### 1. 定义及概念
* 有向图与无向图存储
* 连通图与连通分量
* 完全图的边数
* 握手定理
### 2. BFS与DFS算法
* BFS
* DFS
### 3. 算法应用
* 最短路径   
    __Dijkstra算法__

    __Floyd算法__  
    动态规划思想  
    A[i][j] = min(A[i][j], A[i][k]+A[k][j])  
    三层for循环，时间复杂度O($|v|^3$)  
    $n*n$矩阵存储路径，空间复杂度O($|v|^2$)
    ```cpp
    vector<vector<int>> A(n, vector<int>(n)) = { };//图的邻接矩阵
    vector<vector<int>> path(n, vector<int>(n, -1));//路径矩阵
    void Floyd(vector<vector<int>> &A, vector<vector<int>> &path) {
        int n = A.size();
        for (int k = 0; k < n; k++) {
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    if (A[i][j] > A[i][k] + A[k][j]) {
                        A[i][j] = A[i][k] + A[k][j];
                        path[i][j] = k;
                    }
                }
            }
        }
    }
    ```  
    
* 最小生成树
* 拓扑排序
* 关键路径
	
## __查找与排序__
### 1. 顺序、折半、分块查找
* 求平均长度
### 2. 散列表与哈希表
* 构造方法
* 求平均长度
### 3. 八大排序
* 插入排序
    * 直接插入排序
    * 折半插入排序
    * 希尔排序
* 交换排序
    * 冒泡排序
    * 快速排序
* 选择排序
    * 简单选择排序
    * 堆排序
* 归并排序
* 基数排序
