- [一、二叉搜索树](#一二叉搜索树)
- [二、为什么叫二叉搜索树](#二为什么叫二叉搜索树)
- [三、小堆](#三小堆)
  - [3.1 怎么实现一次调整？](#31-怎么实现一次调整)
  - [3.2 堆排 --> 优先级队列](#32-堆排----优先级队列)
- [四、线索二叉树的查找父结点图形解释](#四线索二叉树的查找父结点图形解释)
- [五、编程时 const 一些注意](#五编程时-const-一些注意)
- [六、搜索二叉树上的操作](#六搜索二叉树上的操作)
  - [6.1 插入函数](#61-插入函数)
  - [6.2 删除函数](#62-删除函数)
- [七、搜索二叉树的完整代码+测试代码+运行结果](#七搜索二叉树的完整代码测试代码运行结果)
  - [7.1 完整代码](#71-完整代码)
  - [7.2 测试代码](#72-测试代码)
  - [7.3 运行结果](#73-运行结果)
- [八、说明](#八说明)

BST（Binary Search Tree）：核心是为了提高查找性能，其查找时间复杂度在log(N) 级别，接近二分查找，查询效率相当高。

## 一、二叉搜索树

1. 逼近二分查找的查找算法；
2. **一般不允许出现重复数字，不然没法存储；**
3. **满足：左孩子数据 < 根结点数据 < 右孩子数据；根(父)结点比左孩子的大，比右孩子的小；**
4. 左子树和右子树也是二叉搜索树；

## 二、为什么叫二叉搜索树

如果对一颗二叉搜索树进行中序遍历，可以按从小到大的顺序输出，此时又叫做二叉排序树。

如图：

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtTw33h2FXV6FvFKIrWLeO3jVDCx14TQAaxzeniaYeFESAoR8wWQjap1pjUtScibp3MntqPicX8qe2KFA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>

## 三、小堆

堆的构造：

1. 数组直接生成堆(向下调整)；
2. 插入创建堆(向上调整)；

### 3.1 怎么实现一次调整？

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtTw33h2FXV6FvFKIrWLeO3jPSDVwib8JZt5SpUc1lDV8lRYpicp03p5lnb9l44f6HlWbYEgfnYu7D9g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>

找到最后一个非叶子结点，n/2-1；一直往下调整即可！

### 3.2 堆排 --> 优先级队列

**堆的删除，只能是堆顶元素，再拿最后一个元素补充上去。在向下做一次调整。形成新的堆结构(满足堆的性质)，将删除的数字输出就是堆排。**

1. 小堆：根(父)小于左右结点；最小的数字先出；
2. 大堆：根(父)大于左右结点；最大的数字先出；因而，进行堆排序就是优先级队列！


<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtTw33h2FXV6FvFKIrWLeO3jztN4z60NtosPUlrib2ia3zF58975hjkCJiaTicmnj3KYP5bAuVROXUwicKQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>

## 四、线索二叉树的查找父结点图形解释

利用空指针指向前驱、后继结点。

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtTw33h2FXV6FvFKIrWLeO3jianSM4WLNMicBKhJ0ibiazeicbsBiahp7FLkrWFMF9ZFk4zztOgicicyhB3RMg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>

## 五、编程时 const 一些注意

1、

在C++中，当我们传的是常量时，引用接收时，形参必须 const 类型接受，否则出错！

常量必须常引用接受。

```cpp
int find(32)；   

int find(const int &value);
```

2、

typedef void  *IP

const IP m; 这个怎么理解？

**因为IP是数据类型，const和数据类型可以互换位置；const IP m; <==> IP const m; 即 void \*const m; m 是一个指针，其指向不能更改，其指向的空间数据可以更改！**

## 六、搜索二叉树上的操作

全部用 C++ 实现的。

之前学习二叉树，并没有说什么插入，删除操作，那是因为，没有规律而言，怎么进行操作呢？搜索二叉树的规律如此明显，那么插入，删除必是重中之重！

我们输入相同的数字，但是顺序不同的话，生成的搜索二叉树是不一样的！  

例：int ar[] = {3, 7, 9, 1, 0, 6, 4, 2,}; 和int ar[] = {7, 3, 9, 1, 0, 6, 4, 2,}; 生成的搜索二叉树不一样。

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtTw33h2FXV6FvFKIrWLeO3jHfStyfgkBOSlfSCjicOHfVZeWj9QtQEGpDCpRwYicMXrknQ88HJ12hvw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>

### 6.1 插入函数

利用搜索二叉树的性质：

```cpp
void insert(BSTreeNode<Type> *&t, const Type &x){
    if(t == NULL){
        t = new BSTreeNode<Type>(x);
        return;
    }else if(x < t->data){
        insert(t->leftChild, x);
    }else if(x > t->data){
        insert(t->rightChild, x);
    }else{
        return;
    }    
}
```

### 6.2 删除函数

思想：**要删除一个有左孩子或右孩子或是叶子结点，看成一种情况，做法：保存要删除的结点，因为传的是引用，可以直接修改上一个结点的左孩子或右孩子，使其跨过当前的直指下一个结点，在释放当前的结点空间。**

第二种情况：就是要删除的既有左子树，又有右子树，此时可以有两种做法：

1. 找左子树最大的数字，覆盖要删除的数字，在往左子树找这个数字删除 --> 递归！
2. 找右子树最小的数字，覆盖要删除的数字，在往右子树找这个数字删除 --> 递归！

第一种情况图形想法如下：

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtTw33h2FXV6FvFKIrWLeO3jTnBLoIcAQLs67TWRD5mePuEE4jW96vGW6AhfXkvHJspAMU0R5E8pZg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>

删除左边和删除右边，还有是叶子结点，想法一样。

第二种情况图形想法如下：

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtTw33h2FXV6FvFKIrWLeO3jx1VCpT5J69VFqx9zhAuhvjjRJlr2hiaWespZIDrnl1A5LYSO1hl8zzQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>

代码如下：

```cpp
bool remove(BSTreeNode<Type> *&t, const Type &key){
    if(t == NULL){  //t传的是引用，每次可以进行直接更改!
        return false;
    }

    if(key < t->data){
        remove(t->leftChild, key);
    }else if(key > t->data){
        remove(t->rightChild, key);
    }else{
        if(t->leftChild != NULL && t->rightChild != NULL){  //第二种情况
            BSTreeNode<Type> *p = t->rightChild;
            while(p->leftChild != NULL){
                p = p->leftChild;
            }
            t->data = p->data;
            remove(t->rightChild, p->data);  //在右树找p->data的数字进行删除;
            }else{     //第一种情况
            BSTreeNode<Type> *p = t;
            if(t->leftChild == NULL){
                t = t->rightChild; //引用的好处体现出来了;
            }else{ 
                t = t->leftChild;  //引用的好处体现出来了;
            }
                delete p;

        }
    }
        
    return true;
}
/*  以下这个代码是先想到的，比较容易，上面这个是经过思考的，将三种情况看成一种情况来处理。
    bool remove(BSTreeNode<Type> *&t, const Type &key){
        if(t == NULL){
            return false;
        }

        if(key < t->data){
            remove(t->leftChild, key);
        }else if(key > t->data){
            remove(t->rightChild, key);
        }else{  //以下三种情况可以看成一种；
            if(t->leftChild == NULL && t->rightChild == NULL){
                delete t;
                t = NULL;
            }else if(t->leftChild != NULL && t->rightChild == NULL){
                BSTreeNode<Type> *p = t;
                t = t->leftChild;
                delete p;
            }else if(t->leftChild == NULL && t->rightChild != NULL){
                BSTreeNode<Type> *p = t;
                t = t->rightChild;
                delete p;
            }else{
                BSTreeNode<Type> *p = t->rightChild;
                while(p->leftChild != NULL){
                    p = p->leftChild;
                }
                t->data = p->data;
                remove(t->rightChild, p->data);
            }
        }
        
        return true;
    }
*/
```

## 七、搜索二叉树的完整代码+测试代码+运行结果  

### 7.1 完整代码

```cpp
#ifndef _BSTREE_H_
#define _BSTREE_H_

#include<iostream>
using namespace std;

#define MIN_NUMBER    -8937589
#define MAX_NUMBER    99999999


template<typename Type>
class BSTree;

template<typename Type>
class BSTreeNode{
    friend class BSTree<Type>;
public:
    BSTreeNode() : data(Type()), leftChild(NULL), rightChild(NULL){}
    BSTreeNode(Type d, BSTreeNode *left = NULL, BSTreeNode *right = NULL) 
        : data(d), leftChild(left), rightChild(right){}
    ~BSTreeNode(){}
private:
    Type data;
    BSTreeNode *leftChild;
    BSTreeNode *rightChild;
};

template<typename Type>
class BSTree{
public:
    BSTree() : root(NULL){}
    BSTree<Type>& operator=(const BSTree &bst){
        if(this != &bst){
            root = copy(bst.root);
        }

        return *this;
    }
    ~BSTree(){}
public:
    void insert(const Type &x){
        insert(root, x);
    }
    void inOrder()const{
        inOrder(root);
    }
    Type Min()const{
        return Min(root);
    }
    Type Max()const{
        return Max(root);
    }
    BSTreeNode<Type>* find(const Type &key)const{
        return find(root, key);
    }
    BSTreeNode<Type> *copy(const BSTreeNode<Type> *t){
        if(t == NULL){
            return NULL;
        }
        BSTreeNode<Type> *tmp = new BSTreeNode<Type>(t->data);
        tmp->leftChild = copy(t->leftChild);
        tmp->rightChild = copy(t->rightChild);

        return tmp;
    }
    BSTreeNode<Type>* parent(const Type &key)const{
        return parent(root, key);
    }
    bool remove(const Type &key){
        return remove(root, key);
    }
protected:
    bool remove(BSTreeNode<Type> *&t, const Type &key){
        if(t == NULL){     //重点：传的是引用
            return false;
        }

        if(key < t->data){
            remove(t->leftChild, key);
        }else if(key > t->data){
            remove(t->rightChild, key);
        }else{
            if(t->leftChild != NULL && t->rightChild != NULL){
                BSTreeNode<Type> *p = t->rightChild;
                while(p->leftChild != NULL){
                    p = p->leftChild;
                }
                t->data = p->data;
                remove(t->rightChild, p->data);
            }else{
                BSTreeNode<Type> *p = t;
                if(t->leftChild == NULL){
                    t = t->rightChild;  //可以直接更改左右孩子
                }else{
                    t = t->leftChild;   //可以直接更改左右孩子
                }
                    delete p;

            }
        }
        
        return true;
    }
/*  
    bool remove(BSTreeNode<Type> *&t, const Type &key){
        if(t == NULL){
            return false;
        }

        if(key < t->data){
            remove(t->leftChild, key);
        }else if(key > t->data){
            remove(t->rightChild, key);
        }else{  //以下三种情况可以看成一种；
            if(t->leftChild == NULL && t->rightChild == NULL){
                delete t;
                t = NULL;
            }else if(t->leftChild != NULL && t->rightChild == NULL){
                BSTreeNode<Type> *p = t;
                t = t->leftChild;
                delete p;
            }else if(t->leftChild == NULL && t->rightChild != NULL){
                BSTreeNode<Type> *p = t;
                t = t->rightChild;
                delete p;
            }else{
                BSTreeNode<Type> *p = t->rightChild;
                while(p->leftChild != NULL){
                    p = p->leftChild;
                }
                t->data = p->data;
                remove(t->rightChild, p->data);
            }
        }
        
        return true;
    }*/
    BSTreeNode<Type>* parent(BSTreeNode<Type> *t, const Type &key)const{
        if(t == NULL || t->data == key){
            return NULL;
        }
        if(t->leftChild->data == key || t->rightChild->data == key){
            return t;
        }
        if(key < t->data){
            return parent(t->leftChild, key);
        }else{
            return parent(t->rightChild, key);
        }
    }
    BSTreeNode<Type>* find(BSTreeNode<Type> *t, const Type &key)const{
        if(t == NULL){
            return NULL;
        }

        if(t->data == key){
            return t;
        }else if(key < t->data){
            return find(t->leftChild, key);
        }else{
            return find(t->rightChild, key);
        }
    }
    Type Max(BSTreeNode<Type> *t)const{
        if(t != NULL){
            while(t->rightChild){
                t = t->rightChild;
            }

            return t->data;
        }

        return MAX_NUMBER;
    }
    Type Min(BSTreeNode<Type> *t)const{
        if(t != NULL){
            while(t->leftChild){
                t = t->leftChild;
            }

            return t->data;
        }
        return MIN_NUMBER;
    }
    void inOrder(BSTreeNode<Type> *t)const{
        if(t != NULL){
            inOrder(t->leftChild);
            cout<<t->data<<" ";
            inOrder(t->rightChild);
        }
    }
    void insert(BSTreeNode<Type> *&t, const Type &x){
        if(t == NULL){
            t = new BSTreeNode<Type>(x);
            return;
        }else if(x < t->data){
            insert(t->leftChild, x);
        }else if(x > t->data){
            insert(t->rightChild, x);
        }else{
            return;
        }    
    }
private:
    BSTreeNode<Type> *root;
};
#endif
```

### 7.2 测试代码

```cpp
#include"bstree.h"

int main(void){
    int ar[] = {3, 7, 9, 1, 0, 6, 4, 2,};
    int n = sizeof(ar) / sizeof(int);
    BSTree<int> bst;
    for(int i = 0; i < n; i++){
        bst.insert(ar[i]);
    }

    bst.inOrder();
    cout<<endl;
    cout<<bst.Min()<<endl;
    cout<<bst.Max()<<endl;
    BSTreeNode<int> *p = bst.find(6);
    BSTreeNode<int> *q = bst.parent(4);
    printf("%p %p\n", p, q);
    bst.remove(0);
    bst.inOrder();
    cout<<endl;
    return 0;
}
```

### 7.3 运行结果

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtTw33h2FXV6FvFKIrWLeO3jicRO0PsaXc6bCPJB1p39tT4pjWBGWKclG8e95UYP4LbqezcbiaydBVWA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>

## 八、说明

原创文章链接：[从零开始学习数据结构-->二叉搜索树（BST）](https://mp.weixin.qq.com/s?__biz=MzU4MjQ3NzEyNA==&mid=2247485378&idx=1&sn=3f0f1adf8fe7f7a6888926322b2617f1&chksm=fdb6f3e9cac17aff4370b832c5286164d103d66a680b45471c0b6300cc57083a749fbcf9a6e6&token=1129091266&lang=zh_CN#rd)
