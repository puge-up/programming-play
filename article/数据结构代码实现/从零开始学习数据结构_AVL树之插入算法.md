- [一、AVL树的插入](#一avl树的插入)
- [二、AVL树的插入算法](#二avl树的插入算法)
- [三、完整代码+测试代码+运行结果](#三完整代码测试代码运行结果)
  - [3.1 完整代码](#31-完整代码)
  - [3.2 测试代码](#32-测试代码)
  - [3.3 测试结果](#33-测试结果)
- [四、说明](#四说明)

## 一、AVL树的插入

1. 必须追踪插入路径，要对bf进行调整，此时不能用递归；
2. 用栈保留路径信息，每次插入均是以叶子结点插入的;
3. **插入一个新结点，自身的 bf 不用调整，其初始化为 0；要调整的是栈中的平衡因子，关键在双旋时，平衡因子的调整要小心，还是调整栈中结点的平衡因子。**

## 二、AVL树的插入算法

思路：

1. 按照二叉搜索树的非递归实现插入数据；
2. 有一个父节点，记录信息，并且入栈；
3. 栈非空，出栈，判断插入是左/右，此时给栈顶的结点平衡因子++/--；
4. 判断bf的值，进行不同情况的处理，针对bf不满足平衡，将根据情况调用4个旋转函数进行调整；
5. 最后实行连接工作，看栈，空的话，直接给root，否则读栈顶，比较数据大小，连接在左/右孩子。

**代码均由 C++ 实现，要记住的是：栈中只保存的是插入结点的路径，其余结点的信息不在保存。**

如何判断写出要用4个旋转函数，并且此时情形如何？

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQADAAicS3iamhwXyDIBc1icF5c3eGUboDuOm73TTwDTJib4nmaby2TSmAjv6eKib3qek6ibBiaNQUSyHtow/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>

以上仅仅是一种情况，但是 parent 和 p 的指向我们已经理解了，其他的情形就可以看出来了。

代码如下：

```cpp
template<typename Type>
bool AVLTree<Type>::insert(AVLNode<Type> *&t, const Type &x){
    AVLNode<Type> *p = t;
    AVLNode<Type> *parent = NULL; // 记录前驱结点，方便连接和调整平衡因子
    stack<AVLNode<Type> *> st; //用栈记录插入的路径，方便调整栈中结点的平衡因子;
    int sign;

    while(p != NULL){
        if(x == p->data){ //要插入的数据和AVL树中的数字相同,则返回失败！
            return false;
        }

        parent = p;
        st.push(parent); //找过的入栈
        if(x < p->data){
            p = p->leftChild;
        }else if(x > p->data){
            p = p->rightChild;
        }
    } // 找插入位置,不用递归，就是为了记录路径信息
    
    p = new AVLNode<Type>(x);
    if(parent == NULL){
        t = p;    //判断是不是第一个结点，进行root的连接;
        return true;
    }

    if(x < parent->data){ //此时通过父节点的数据判断插入的是左还是右
        parent->leftChild = p;
    }else{
        parent->rightChild = p;
    }
    //新插入点的bf为0,关键是栈中的平衡因子的调整
/////////////////////////////////////////////////////// 以上完成插入工作
    while(!st.empty()){  //栈不空，出栈顶元素
        parent = st.top();
        st.pop();

        if(p == parent->leftChild){   //判断插入的是父节点的左/右孩子,
            parent->bf--;           //让其bf++/--;
        }else{
            parent->bf++;
        }

        //以下判断栈中的平衡因子，看是否需要进行旋转调整
        if(parent->bf == 0){  //bf=0，直接跳出循环
            break;
        }
        if(parent->bf==1 || parent->bf==-1){ 
            p = parent;  //此时在向上走，判断bf;
        }else{  //以下的bf为2/-2;利用标志判断左右旋;
            sign = parent->bf > 0 ? 1 : -1;
            if(p->bf == sign){  //符号相同为单旋
                if(sign == 1){  //为1左旋
                    RotateL(parent);  
                }else{
                    RotateR(parent); //右旋
                }
            }else{  //符号不同，为双旋
                if(sign == 1){  
                    RotateRL(parent); //为1右左
                }else{
                    RotateLR(parent);
                }
            }
/*
    以下方法也可以判断左右旋
        else
        {
            if(parent->bf < 0)  //左边
            {
                if(p->bf<0 && p==parent->leftChild)    //    / 只能是左孩子
                {
                    //RotateR(parent);
                }
                else if(p->bf>0 && p == parent->leftChild)  //   <
                {
                    //RotateLR(parent);
                }
            }
            else
            {
                if(p->bf>0 && p==parent->rightChild)   //   \ 
                {
                    //RotateL(parent);
                }
                else if(p->pf<0 && p==parent->rightChild)  //      >
                {
                    //RotateRL(parent);
                }
            }
        }

*/
    break;
        }
    }

    if(st.empty()){  //通过旋转函数，此时parent指向当前根节点;
        t = parent;  //此时调到栈底了，旋转后将更改root的指向
    }else{
        AVLNode<Type> *tmp = st.top();  //当前的栈顶结点
        if(parent->data < tmp->data){  
            tmp->leftChild = parent;
        }else{
            tmp->rightChild = parent;
        }
    }

    return true;
}
```

## 三、完整代码+测试代码+运行结果

### 3.1 完整代码

```cpp
#ifndef _AVL_TREE_H_
#define _AVL_TREE_H_

#include<iostream>  //引入头文件
#include<stack>    //要用栈保存路径信息
using namespace std;

template<typename Type>
class AVLTree;

template<typename Type>
class AVLNode{   //AVL树的结点
    friend class AVLTree<Type>;
public:
    AVLNode() : data(Type()), leftChild(NULL), rightChild(NULL), bf(0){}
    AVLNode(Type d, AVLNode *left = NULL, AVLNode *right = NULL) 
        : data(d), leftChild(left), rightChild(right), bf(0){}
    ~AVLNode(){}
private:
    Type data;
    AVLNode *leftChild;
    AVLNode *rightChild;
    int bf;  //多了一个平衡因子
};

template<typename Type>
class AVLTree{   //AVL树的类型
public:
    AVLTree() : root(NULL){}
public:
    bool insert(const Type &x){
        return insert(root, x);
    }
    void inOrder()const{
        inOrder(root);
    }
protected:
    void inOrder(AVLNode<Type> *t)const{
        if(t != NULL){
            inOrder(t->leftChild);
            cout<<t->data<<" : "<<t->bf<<endl;;
            inOrder(t->rightChild);
        }
    }
    bool insert(AVLNode<Type> *&t, const Type &x); //插入函数
    void RotateR(AVLNode<Type> *&ptr){  //右旋
        AVLNode<Type> *subR = ptr;
        ptr = ptr->leftChild;
        subR->leftChild = ptr->rightChild;
        ptr->rightChild = subR;
        ptr->bf = subR->bf = 0;
    }
    void RotateL(AVLNode<Type> *&ptr){  //左旋
        AVLNode<Type> *subL = ptr;
        ptr = subL->rightChild;
        subL->rightChild = ptr->leftChild;
        ptr->leftChild = subL;
        subL->bf = ptr->bf = 0;
    }
    void RotateLR(AVLNode<Type> *&ptr){  //先左后右旋转
        AVLNode<Type> *subR = ptr;
        AVLNode<Type> *subL = ptr->leftChild;
        ptr = subL->rightChild;

        subL->rightChild = ptr->leftChild;
        ptr->leftChild = subL;
        if(ptr->bf <= 0){
            subL->bf = 0;
        }else{
            subL->bf = -1;
        }

        subR->leftChild = ptr->rightChild;
        ptr->rightChild = subR;
        if(ptr->bf == -1){
            subR->bf = 1;
        }else{
            subR->bf = 0;
        }

        ptr->bf = 0;
    }
    void RotateRL(AVLNode<Type> *&ptr){  //先右后左旋转
        AVLNode<Type> *subL = ptr;
        AVLNode<Type> *subR = ptr->rightChild;
        ptr = subR->leftChild;

        subR->leftChild = ptr->rightChild;
        ptr->rightChild = subR;
        if(ptr->bf >=0){
            subR->bf = 0;
        }else{
            subR->bf = 1;
        }

        subL->rightChild = ptr->leftChild;
        ptr->leftChild = subL;
        if(ptr->bf == 1){
            subL->bf = -1;
        }else{
            subL->bf = 0;
        }
        ptr->bf = 0;
    }
private:
    AVLNode<Type> *root;
};

template<typename Type>
bool AVLTree<Type>::insert(AVLNode<Type> *&t, const Type &x){
    AVLNode<Type> *p = t;
    AVLNode<Type> *parent = NULL; // 记录前驱结点，方便连接和调整平衡因子
    stack<AVLNode<Type> *> st; //用栈记录插入的路径，方便调整栈中结点的平衡因子;
    int sign;

    while(p != NULL){
        if(x == p->data){ //要插入的数据和AVL树中的数字相同,则返回失败！
            return false;
        }

        parent = p;
        st.push(parent); //找过的入栈
        if(x < p->data){
            p = p->leftChild;
        }else if(x > p->data){
            p = p->rightChild;
        }
    } // 找插入位置,不用递归，就是为了记录路径信息
    
    p = new AVLNode<Type>(x);
    if(parent == NULL){
        t = p;    //判断是不是第一个结点，进行root的连接;
        return true;
    }

    if(x < parent->data){ //此时通过父节点的数据判断插入的是左还是右
        parent->leftChild = p;
    }else{
        parent->rightChild = p;
    }
    //新插入点的bf为0,关键是栈中的平衡因子的调整
/////////////////////////////////////////////////////// 以上完成插入工作
    while(!st.empty()){  //栈不空，出栈顶元素
        parent = st.top();
        st.pop();

        if(p == parent->leftChild){   //判断插入的是父节点的左/右孩子,
            parent->bf--;           //让其bf++/--;
        }else{
            parent->bf++;
        }

        //以下判断栈中的平衡因子，看是否需要进行旋转调整
        if(parent->bf == 0){  //bf=0，直接跳出循环
            break;
        }
        if(parent->bf==1 || parent->bf==-1){ 
            p = parent;  //此时在向上走，判断bf;
        }else{  //以下的bf为2/-2;利用标志判断左右旋;
            sign = parent->bf > 0 ? 1 : -1;
            if(p->bf == sign){  //符号相同为单旋
                if(sign == 1){  //为1左旋
                    RotateL(parent);  
                }else{
                    RotateR(parent); //右旋
                }
            }else{  //符号不同，为双旋
                if(sign == 1){  
                    RotateRL(parent); //为1右左
                }else{
                    RotateLR(parent);
                }
            }
/*
    以下方法也可以判断左右旋
        else
        {
            if(parent->bf < 0)  //左边
            {
                if(p->bf<0 && p==parent->leftChild)    //    / 只能是左孩子
                {
                    //RotateR(parent);
                }
                else if(p->bf>0 && p == parent->leftChild)  //   <
                {
                    //RotateLR(parent);
                }
            }
            else
            {
                if(p->bf>0 && p==parent->rightChild)   //   \ 
                {
                    //RotateL(parent);
                }
                else if(p->pf<0 && p==parent->rightChild)  //      >
                {
                    //RotateRL(parent);
                }
            }
        }

*/
    break;
        }
    }

    if(st.empty()){  //通过旋转函数，此时parent指向当前根节点;
        t = parent;  //此时调到栈底了，旋转后将更改root的指向
    }else{
        AVLNode<Type> *tmp = st.top();  //当前的栈顶结点
        if(parent->data < tmp->data){  
            tmp->leftChild = parent;
        }else{
            tmp->rightChild = parent;
        }
    }

    return true;
}
#endif
```

### 3.2 测试代码

```cpp
#include"avlTree.h"

int main(void){
    int ar[] = {16, 3, 7, 11, 9, 26, 18, 14, 15,};
    int n = sizeof(ar) / sizeof(int);
    AVLTree<int> avl;

    for(int i = 0; i < n; i++){
        avl.insert(ar[i]);
    }

    avl.inOrder();
    return 0;
}
```

### 3.3 测试结果

测试最终形成的 AVL 树如下：

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQADAAicS3iamhwXyDIBc1icF5gysCygsS15zmuItr17ycugyodsiadNDnJFJiaopxNwf60kU9c6wKoT4g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQADAAicS3iamhwXyDIBc1icF5R6yCDuqCLQjWiaLsbxsVgpaW6pFcrna8dugozIrHmXuWMFds0qbLTiaw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>

## 四、说明

原创文章链接：[从零开始学习数据结构-->AVL树之插入算法](https://mp.weixin.qq.com/s?__biz=MzU4MjQ3NzEyNA==&mid=2247485445&idx=1&sn=308097bdf1dc20122af766298deded56&chksm=fdb6fc2ecac175384522398f3f2b04be483c47048d56ccf7d08cd0a96e0b45123e0cae269e97&token=1129091266&lang=zh_CN#rd)
