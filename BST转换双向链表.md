---
title: BST转换双向链表
date: 2016-05-02 10:48:02
tags:
---

    //实现二叉搜索树到双向链表的转换
    #include <iostream>
    #include<queue>
    using namespace std;
    struct BinaryTreeNode{
        int m_nValue;
        BinaryTreeNode* m_pLeft;
        BinaryTreeNode* m_pRight;
    };
    void PrintFromTopToBottom(BinaryTreeNode* pTreeRoot){
        if(!pTreeRoot)
            return;
        queue<BinaryTreeNode*> que;
        que.push(pTreeRoot);
        while(que.size()){
            BinaryTreeNode* pNode=que.front();//指向队列的第一个元素，要被弹出的元素
            que.pop();
            cout<<pNode->m_nValue<<" ";
            if(pNode->m_pLeft)//打印节点的左右子节点
                que.push(pNode->m_pLeft);
            if(pNode->m_pRight)
                que.push(pNode->m_pRight);
        }
    }
    void Print(BinaryTreeNode*  &pHead){
        if(pHead==NULL)
            return ;
        BinaryTreeNode* p=pHead;
        while(p){
            cout<<p->m_nValue<<" ";
            p=p->m_pRight;
        }
        cout<<endl;
    }
    BinaryTreeNode* ContrustCore(int* startpreorder,int* endpreorder,int* startinorder,int* endinorder){
        //根据先序确定第一个数值确定根节点
       //BinaryTreeNode *root;
        int rootValue=startpreorder[0];
        BinaryTreeNode* root=new BinaryTreeNode();//为链表申请空间
        root->m_nValue=rootValue;
        root->m_pLeft=root->m_pRight=NULL;
        if(startpreorder==endpreorder){
            if(startinorder==endinorder && *startpreorder==*endpreorder)//z只有一个根节点
                return root;
            else
                throw std::exception();
        }
        //在中序找到根节点所在位置
        int*rootinoder=startinorder;
         while(rootinoder<=endinorder && *rootinoder!=rootValue)
            rootinoder++;
         if(rootinoder==endinorder && *rootinoder!=rootValue)//在中序中没有找到根节点
             throw exception();
         int leftLength=rootinoder-startinorder;
         int* leftPreorderEnd=startpreorder+leftLength;
         if(leftLength>0)//左子树的长度,构建左子树
         {
             root->m_pLeft=ContrustCore(startpreorder+1,leftPreorderEnd,startinorder,rootinoder-1);
         }
        if(leftLength<endpreorder-startpreorder)//存在右子树
            root->m_pRight=ContrustCore(leftPreorderEnd+1,endpreorder,rootinoder+1,endinorder);
        return root;
    }
    BinaryTreeNode* Contrust(int* preorder,int* inorder,int length){
            if(preorder==NULL||inorder==NULL||length<=0)
                return NULL;
            return ContrustCore(preorder,preorder+length-1,inorder,inorder+length-1);
    }
    void CovertNode(BinaryTreeNode* pNode,BinaryTreeNode** pLastNodeInList){
        if(pNode==NULL)
            return;
        BinaryTreeNode* pCurrent=pNode;
        if(pCurrent->m_pLeft!=NULL)//转换左子树为排序的双向链表
            CovertNode(pCurrent->m_pLeft,pLastNodeInList);
        pCurrent->m_pLeft=*pLastNodeInList;//pCurrent指向根节点
        if(*pLastNodeInList!=NULL)
            (*pLastNodeInList)->m_pRight=pCurrent;//连接上根节点
        *pLastNodeInList=pCurrent;//当前双向链表的最后一个几点就是根节点
        if(pCurrent->m_pRight!=NULL)
            CovertNode(pCurrent->m_pRight,pLastNodeInList);
    
    }
    BinaryTreeNode* Covert(BinaryTreeNode* pRootOfTree){
        BinaryTreeNode* pLastNodeInList=NULL;//双向链表为 空
        CovertNode(pRootOfTree,&pLastNodeInList);
        //pLastNodeInList指向双向链表的最后
        //我们需要返回最后结点
        BinaryTreeNode* pHeadOfList=pLastNodeInList;
        while(pHeadOfList!=NULL && pHeadOfList->m_pLeft!=NULL)//最后找到双向链表的头结点
            pHeadOfList=pHeadOfList->m_pLeft;
        return pHeadOfList;
    }
    int main()
    {
        BinaryTreeNode* Btree;
        int preorder[]={10,6,4,8,14,12,16};
        int inorder[]={4,6,8,10,12,14,16};
        Btree= Contrust(preorder,inorder,7);
        PrintFromTopToBottom(Btree);
        cout<<endl;
    
        BinaryTreeNode* L=Covert(Btree);
    
        Print(L);
        return 0;
    }

