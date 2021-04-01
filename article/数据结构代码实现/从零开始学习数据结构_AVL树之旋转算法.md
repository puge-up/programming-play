- [一、AVL树](#一avl树)
- [二、四种旋转](#二四种旋转)
  - [2.1 单旋转 --> 直线型](#21-单旋转----直线型)
  - [2.2 双旋转 --> 折线型](#22-双旋转----折线型)
- [三、画平衡树](#三画平衡树)
- [四、四种旋转的实现](#四四种旋转的实现)
  - [4.1 右单旋](#41-右单旋)
  - [4.2 左单旋](#42-左单旋)
  - [4.3 先左后右单旋](#43-先左后右单旋)
  - [4.4 先右后左单旋](#44-先右后左单旋)
- [五、说明](#五说明)

AVL（平衡二叉查找树），其新增/删除核心思路：通过树旋转算法来进行树的平衡，提高查找效率。

## 一、AVL树

AVL树首先是一颗二叉搜索树，满足其所有性质，AVL树又叫做高度平衡的二叉搜索树；

AVL: 动态搜索树；

平衡因子bf: 右树高度 — 左树高度; bf的取值只能是1, 0, -1；

左右子树都得符合平衡因子, 若不符, 的通过旋转来调整平衡因子。

## 二、四种旋转

### 2.1 单旋转 --> 直线型

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQIp2yMxltM0oFHibFI34ibXjMDMg3xOXUA2Z4h3aKw9iciaUWErPt0XcLZ4b0ClMS3ece4DzZyozAqibA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>

### 2.2 双旋转 --> 折线型

**要进行两次旋转的调整，判断折线，看哪边突出(就是三个结点中有一个突出的方向)，就先向哪边旋转。**

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQIp2yMxltM0oFHibFI34ibXjcR42J990QNeAD4boaTfbNPsMY1MNmibgibt16OcveHxED5dZ5QXRVCkw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>

**四种旋转，每次就只针对两个结点(要进行旋转的2个结点)；然后将上面的分支挂到旋转后的L/R上即可。**

## 三、画平衡树

根据一组数字，画出其AVL树：16 3 7 11 9 26 18 14 15。

**画AVL树，首先其实是一颗搜索二叉树; 按照其比左孩子大，比右孩子小画就行; 有了平衡因子，不满足时在旋转调整即可。**

画法三步走：

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQIp2yMxltM0oFHibFI34ibXjGYsTSZKNzibbUFibRFUVa97ibSsJ5vVl4t8uiaCfAyVZSicZ3OzLiasNKiatg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>
<p align=center>(第一步)</p>
<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQIp2yMxltM0oFHibFI34ibXjwWUEouiau0VzZfYAFlM9ZJiankAYqXMUq70gEHY2azxWpwoWuupuCiaYQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>
<p align=center>(第二步)</p>
<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQIp2yMxltM0oFHibFI34ibXjlfmyENz159GngI3yfFQUSy4647MDwKD0eXkqicpqiasQcad9fiaGMCXuA/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>
<p align=center>(第三步)</p>

## 四、四种旋转的实现

**永远只考虑三层以内结点的旋转。**

C++实现其所有代码。

### 4.1 右单旋

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQIp2yMxltM0oFHibFI34ibXjRtFEFuWnb5NnaXMVXk1gOTzdqkk3MTh917VHb3dPq3ictq2jJstAdTw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>

代码如下(**代码中 ptr 代表的是要 bf 不为平衡处，指向要进行旋转的结点**)：

```cpp
void RotateR(AVLNode<Type> *&ptr){
    AVLNode<Type> *subR = ptr;
    ptr = ptr->leftChild;  //通过引用直接修改指向1的指针(可能是上一个的左孩子/右孩子)
    subR->leftChild = ptr->rightChild;
    ptr->rightChild = subR;
    ptr->bf = subR->bf = 0;
}
```

### 4.2 左单旋

左单旋与右单旋的代码是镜像的，并且想法是一致的; 所以代码如下：

```cpp
void RotateL(AVLNode<Type> *&ptr){
    AVLNode<Type> *subL = ptr;
    ptr = subL->rightChild;  //同样是经过引用修改
    subL->rightChild = ptr->leftChild;
    ptr->leftChild = subL;
    subL->bf = ptr->bf = 0;
}
```

**在进行单旋转时，因为是在插入，其自身的 bf 不用调整，初始化为0;修改的是根和另一个结点的 bf。**

### 4.3 先左后右单旋

**在进行双旋转时，首先明确左/右孩子，根结点的最终情况, 在进行调整;并且在双旋转时每个结点的bf都得改变。**

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQIp2yMxltM0oFHibFI34ibXjZzU9AHgIx6Sh1rYjVvjKPBy2njydNHUPE9HOxPPvFBBn1bFLRUk3iag/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>

平衡因子在这不好考虑，有点复杂，具体分析如下：

**平衡因子的考虑关键在：ptr 有左树/右树，对应上去则 subL/sunR 原先必有一个分支结点; ptr 没有孩子结点，对应 subR/subL原先也没有分支结点。**

<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQIp2yMxltM0oFHibFI34ibXj6yqEtwMTGIaZVYrbegZW5AcZg8Cf6ukunZKJDUNRvgwbGRiczfFHsZQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>
<p align=center>(第一种情况)</p>
<div align=center><img src='https://mmbiz.qpic.cn/mmbiz_png/iaumSdLKJXtQIp2yMxltM0oFHibFI34ibXjKKTw6GQt3ic2uMwRN5Q5xbnjSVCyfG1kveNMPK6LoVicQRN0Dic9SKMjg/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1'></div>
<p align=center>(第二种情况)</p>

代码如下：

```cpp
void RotateLR(AVLNode<Type> *&ptr){
    AVLNode<Type> *subR = ptr;    //最终右孩子
    AVLNode<Type> *subL = ptr->leftChild; //最终左孩子
    ptr = subL->rightChild;  //最终根节点,因为引用,最终这个修改了指向根结点，完成了连接;

    subL->rightChild = ptr->leftChild;
    ptr->leftChild = subL;
    if(ptr->bf <= 0){
        subL->bf = 0;  //此时的情况就是,自己ptr原先没有挂结点或者是左树挂上结点，而满足这种情况下，sunL原先必有左树，此时在挂上右树，所以为0;
    }else{
        subL->bf = -1;  //此时的情况是ptr有右孩子，而sunL有左孩子，满足这种情况，所以bf只能是-1;
    }

    subR->leftChild = ptr->rightChild;
    ptr->rightChild = subR;
    if(ptr->bf == -1){  //当结点ptr其只有左孩子时，
        subR->bf = 1;  //sunR必定有右孩子,所以此时为1
    }else{
        subR->bf = 0; //当ptr没有孩子结点或有一个右孩子时(此时subR必有右树)，所以此时为0;
    }

    ptr->bf = 0;   //调整后根的bf永远是0;
}
```

### 4.4 先右后左单旋

与上一个双旋的代码是镜像的, 并且想法是一致的; **平衡因子的修改有点不一样，注意一下就行**，所以代码如下:

```cpp
void RotateRL(AVLNode<Type> *&ptr){
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
```

## 五、说明

原创文章链接：[从零开始学习数据结构-->AVL树之旋转算法](https://mp.weixin.qq.com/s?__biz=MzU4MjQ3NzEyNA==&mid=2247485402&idx=1&sn=a2590144c7cc6f10008056f4ddd0a94f&chksm=fdb6f3f1cac17ae7a1ea1967820f730b3b5edb5465585e308e91f25b59ad611fe1725f452a1a&token=1129091266&lang=zh_CN#rd)
