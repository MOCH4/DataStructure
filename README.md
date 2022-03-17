## 基本概念 
###  1. 数据结构
* 数据结构是相互之间存在一种或多种特定关系的数据元素的集合
* 数据结构三要素：逻辑结构、存储结构、数据的运算
### 2. 抽象数据类型
* 抽象数据类型：一个数学模型以及定义在该模型上的一组操作
* 抽象数据类型定义只取决于一组逻辑特性，与如何实现无关
### 3. 算法
* 算法的特性
    + 有穷性、确定性、可行性、输入、输出
* 好算法的目标
    + 正确性、可读性、健壮性、效率与低存储要求
* __时间复杂度__：所有语句重复次数的最高阶
* __空间复杂度__：额外占用的存储空间大小规模
## C++语法
### 1. 结构体
```cpp
struct StructName{
    ElemType elem1;
    ElemType elem2;
    ...;
}StructName;
```

## 线性表
### 1. 定义及概念
* 线性表是n个相同数据类型的数据元素的有限序列，表示元素间一对一的关系（逻辑结构）
* 线性表有两种储存方式：顺序表、链表（存储结构）

### 2. 链表
* __单链表__
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
* __双链表__
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

//删除结点*p
ListNode *ListDelete(ListNode*p) {
    ListNode *q = p->next;
    p->data = p->next->data; //将后继结点的值赋给p
    p->next = q->next;       //删除后继结点
    delete(q);
    return p;
}
```

* __遍历输出__
```cpp

```

* __交换元素位置__
```cpp

```
### 4. 链表插入与删除的复杂度  
|        |  时间复杂度  |  空间复杂度  |
|  :---  |  :--:  |  :--:  |
|  前插  | O(n)  |  O(1)  |
|  后插  | O(n)  |  O(1)  |
|  删除第i个结点  |  O(n)  |  O(1)  |
|  删除给定结点p  |  O(1)  |  O(1)  |

### 5. 其他链表
* 循环链表

* 双向链表

* 静态链表

## 栈与队列
### 1. 概念
* 
### 2.顺序栈
* 出入栈指针变化
### 3. 共享栈
* 指针初始位置
* 指针变化模式
### 4. 循环队列
* 指针初始位置
* 指针变化模式
### 5. 栈与队列算法应用
	
## 串
### 1. 定义及概念
### 2. 先、中、后（波兰）表达式转换
### 3. 模式匹配（KMP）
* next数组
* nextval数组
	
## 数组与广义表
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

## 数与二叉树
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
	
## 图
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
* 最小生成树
* 拓扑排序
* 关键路径
	
## 查找与排序
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