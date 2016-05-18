---
title: 后序序列可以构成BST？
date: 2016-04-30 20:35:43
tags:
---

    //判断一个后序序列是不是二叉搜索树的后序遍历序列
    //二叉搜索树的左子树＜根节点；右子树大于根节点
    #include <iostream>
    
    using namespace std;
    bool SequenceIsBST(int *sequence, int length){
        if(sequence==NULL || length<=0)
            return false;
        int root=sequence[length-1];
        int i=0;
        for(;i<length-1;i++)
        {
            if(sequence[i]>root)
                break;
        }
        int j=i;
        for(;j<length-1;j++){
            if(sequence[j]<root)
                return false;
        }
        //上面的过程找到了左右子树
        bool left=true;//左子树是BST吗？
        if(i>0)//左子树存在
            left=SequenceIsBST(sequence,i);
        bool right=true;
        if(i<length-1)//存在右子树
            right=SequenceIsBST(sequence+i,j);
        return (left&&right);
    }
    int main()
    {
        int a[]={5,7,6,9,11,10,8};
        cout<<SequenceIsBST(a,7);
        return 0;
    }

