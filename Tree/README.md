# 树
## 定义

树是n（n>=0）个节点的有限集。当n=0时，称为空树。
在任意一棵非空树中：
* 有且仅有一个特定的称为根(Root)的结点。
* 当n>1时，其余结点可分为m(m>0)个互不相交的有限集T1、T2、...、Tm，其中每一个集合本身又是一棵树，并且称为根的子树(SubTree)

> * 根结点是唯一的
> - 子树可以有无数个，但是一定互不相交

> linux操作系统和家谱，都是很好的“树”结构（1对多的关系）。

## 结点
### 度(Degree)

结点拥有的子树，称为结点的度，树的度取树内各结点的度的最大值。
- 度为0的结点称为叶结点(Leaf)或终端结点
- 度不为0的结点称为分支结点或非终端阶段，除根节点为，分支结点也被称为内部结点

### 关系
- Child(孩子)
- Parent(双亲)
- 兄弟(Sibling) -> 需要是同一双亲的孩子
- 祖先：结点的祖先是指结点的根到该结点所经分支上的所有结点。
- 堂兄弟：双亲在同一层的结点

### 层次
树中结点的最大层次称为树的深度(Depth)或高度。
![e3a6556dcd4a7e5d4cffbd0595deb247.png](evernotecid://4C1CF0FC-6574-4271-8E25-0D6386F782B6/appyinxiangcom/30295208/ENResource/p3)

## 其他概念
有序树和无序树
森林，某个结点的子树的集合，就是这个结点的森林。

## 树的存储结构
### 双亲表示法
双亲表示法，言外之意就是以双亲作为索引的关键词的一种存储方式。
#### 例1:
```javascript
class Node {
    constructor (data, parentIndex) {
        this.data = data
        this.parentIndex = parentIndex
    }
}
```
![ee3558f8b4b69466ff891be981ef6c19.png](evernotecid://4C1CF0FC-6574-4271-8E25-0D6386F782B6/appyinxiangcom/30295208/ENResource/p4)

> 但是这种方式child找parent简单，但是parent找child就很复杂，需要整个遍历一边才知道。
### 孩子表示法
#### 方案1
根据树的的度，声明足够空间存放指针结点。
![25390860c09e68ee683843b2c4b51984.png](evernotecid://4C1CF0FC-6574-4271-8E25-0D6386F782B6/appyinxiangcom/30295208/ENResource/p5)
缺点：浪费内存空间

#### 方案2
遍历整个树，根据树的度提前指定好所需的指针内存空间数。
![bd73db34e3c94955add8513b6babaf95.png](evernotecid://4C1CF0FC-6574-4271-8E25-0D6386F782B6/appyinxiangcom/30295208/ENResource/p21)
缺点：初始化时需要遍历整个树，过于复杂，时间复杂度增加

#### 方案3
![2c01df8b82af04d5c66b32dcf76bf7b0.png](evernotecid://4C1CF0FC-6574-4271-8E25-0D6386F782B6/appyinxiangcom/30295208/ENResource/p7)
左排顺序存储每一个结点的数据和一个指针，然后如果某一结点有子结点，指针就指到他的第一个子结点，子结点如果有兄弟(弟弟)结点，子结点的指针就再指向弟弟结点。
> 孩子表示法寻找子结点容易，寻找双亲结点也不太容易。

### 双亲孩子表示法
一目了然
**顺序存储** + **链式存储**
![7cb174df7f824481663ee54ea1588ceb.png](evernotecid://4C1CF0FC-6574-4271-8E25-0D6386F782B6/appyinxiangcom/30295208/ENResource/p9)

![dba653efdd930108642508af5c2b9cfd.png](evernotecid://4C1CF0FC-6574-4271-8E25-0D6386F782B6/appyinxiangcom/30295208/ENResource/p8)

```javascript
// 结点
class Node {
    constructor (data, parentIndex, firstChild) {
        this.data = data
        this.parentIndex = parentIndex
        this.firstChild = firstChild
    }
}

// 子结点信息
class ChildNode {
    constructor (data, nextChild) {
        this.data = data
        this.nextChild = nextChild
    }
}

const k = new Node('K', '6', null)
const j = new Node('J', '4', null)
const i = new Node('I', '4', null)
const h = new Node('H', '4', null)
const g = new Node('G', '3', k)
const f = new Node('F', '3', null)
const e = new Node('E', '1', H)
const d = new Node('D', '0', F)
const c = new Node('C', '0', null)
const b = new Node('B', '0', b)
const a = new Node('A', '-1', e)

// 树
const tree = [a, b, c, d, e, f, g, h, i, j, k]
```


### 孩子兄弟表示法

？？？

## 二叉树
### 定义
二叉树(Binary Tree)是n(n>=0)个结点的有限集合，该集合或者为空集(空二叉树)，或者由一个根节点和两棵互不相交的、分别称为左子树和右子树的二叉树组成。

![ab193abe1b1f909f51196a5693625620.png](evernotecid://4C1CF0FC-6574-4271-8E25-0D6386F782B6/appyinxiangcom/30295208/ENResource/p10)

> 左子树和右子树是有顺序的，次序不能跌倒

### 二叉树的5种基本形态
- 空二叉树
- 只有一个根结点
- 根结点 + 左子树
- 根结点 + 右子树
- 根结点 + 左、右子树

![4a0d8bf7364f190f116de32656c6685d.png](evernotecid://4C1CF0FC-6574-4271-8E25-0D6386F782B6/appyinxiangcom/30295208/ENResource/p11)

### 特殊二叉树
#### 斜树

![6c803c8b079e834caca8c172ba16d464.png](evernotecid://4C1CF0FC-6574-4271-8E25-0D6386F782B6/appyinxiangcom/30295208/ENResource/p12)

#### 满二叉树
##### 定义
一棵深度为k，且有2^k-1
个节点的二叉树，称为满二叉树（Full Binary Tree）。这种树的特点是每一层上的节点数都是最大节点数。

![668235dc5a6c57540361e85ed2518827.png](evernotecid://4C1CF0FC-6574-4271-8E25-0D6386F782B6/appyinxiangcom/30295208/ENResource/p13)

#### 完全二叉树
##### 定义
在一颗二叉树中，若除最后一层外的其余层都是满的，并且最后一层要么是满的，要么在右边缺少连续若干节点，则此二叉树为完全二叉树（Complete Binary Tree）。


> 满二叉树一定是完全二叉树，完全二叉树不一定是满二分叉树。

> 二叉树第i层最多有2^(i - 1)个结点

### 二叉树的存储结构
树需要用顺序存储 + 链式存储进行存储。
但是二叉树比较特殊，仅用顺序存储或链式存储一种就可以简单实现。

#### 顺序存储
![2fa162869cc5116b9ee1318e214a291d.png](evernotecid://4C1CF0FC-6574-4271-8E25-0D6386F782B6/appyinxiangcom/30295208/ENResource/p15)
![ecda9db10479f240d7c3ec509c1e30b7.png](evernotecid://4C1CF0FC-6574-4271-8E25-0D6386F782B6/appyinxiangcom/30295208/ENResource/p16)

#### 链式存储
二叉链表

![987714822f41006700989ecfb9d36249.png](evernotecid://4C1CF0FC-6574-4271-8E25-0D6386F782B6/appyinxiangcom/30295208/ENResource/p18)

### 二叉树的遍历
#### 定义
二叉树的遍历(traversing binary tree)是指从根结点出发，按照某种**次序**依次**访问**二叉树中所有结点，使得每个结点被访问一次且仅被访问一次。

#### 遍历方式
![43bced42312c239ffd6f6a94dd66b8f7.png](evernotecid://4C1CF0FC-6574-4271-8E25-0D6386F782B6/appyinxiangcom/30295208/ENResource/p19)

- 前序遍历
若二叉树为空，则空操作返回，否则先访问根结点，然后前序遍历左子树，再前序遍历右子树。
```
A -> B -> D -> H -> I -> E -> J -> C -> F -> K -> G
```
- 中序遍历
若树为空，则空操作返回，否则从根结点开始(注意不是先访问根结点)，中序遍历根结点的左子树，然后是访问根结点，最后中序遍历右子树。
```
H -> D -> I -> B -> E -> J -> A -> F -> K -> C -> G
```
- 后序遍历
若树为空，则空操作返回，否则从左到右先叶子后结点的方式遍历访问左右子树，最后访问根结点。
```
H -> I -> D -> J -> E -> B -> K -> F -> G -> C -> A
```
- 层序遍历
若树为空，则空操作返回，否则从树的第一层，也就是根结点开始访问，从上而下逐层遍历，在同一层中，按从左到右的顺序对结点逐个访问。
```
A -> B -> C -> D -> E -> F -> G -> H -> I -> I -> J
```

> 注： 前中后是根据根结点被遍历的次序命名的。

### 二叉树的创建与遍历(代码实现)
二叉树的遍历就是为了把二叉树从一个树结构变成一个线性的序列。
因为计算机内存是线性的，不管顺序存储还是链式存储，都是只能处理线性的序列结构。

> 题：建立二叉树，并输出每个字符所在的层数。

![tree.png](/Tree/images/tree.png)


```javascript
class Node {
    constructor (data, leftChild, rightChild) {
    this.data = data;
    this.leftChild = leftChild;
    this.rightChild = rightChild;
    }
}
// 1:将图中二叉树转变为序列结构，默认前序遍历转化
const _tree = ['A', 'B', null, 'D', null, null, 
'C', 'E', null, null, null]

// 2:根据序列结构，生成树
const createBinaryTree = () => {
    // 
}

```

## 线索二叉树
### 定义
二叉树添加了直接指向节点的前驱和后继的指针的二叉树称为线索二叉树。