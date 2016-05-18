---
title: 查找倒数第k个节点
date: 2016-04-27 10:51:00
tags:
---
在O(1)时间实现

    #include <iostream>
    
    using namespace std;
    typedef struct ListNode{
        int m_nValue;
        ListNode* m_pNext;
    }ListNode, *List;//必须是一个链表
    
    
    void Insert(List& pHead,int data){
        ListNode* p=new ListNode;
        p->m_nValue=data;
        p->m_pNext=NULL;
        if(pHead==NULL)
            pHead=p;
        else{
            p->m_pNext=pHead;
            pHead=p;
        }
    
    }
    void Print(List& pHead){
        if(pHead==NULL)
            return ;
        ListNode* p=pHead;
        while(p){
            cout<<p->m_nValue<<" ";
            p=p->m_pNext;
        }
        cout<<endl;
    }
    ListNode* FindKthTotail(ListNode* pHead, int k){
        if(pHead==NULL||k<=0)//非法输入
            return NULL;
        ListNode* p1=pHead, *p2=pHead;
    
        for(int i=0;i<k-1;i++){
            if(p1->m_pNext!=NULL){
                p1=p1->m_pNext;//第一个指针走k-1步
            }
            else
                return NULL;//长度不够k个节点
         }
    
    
        while(p1->m_pNext!=NULL){
                p2=p2->m_pNext;
                p1=p1->m_pNext;
        }
        return p2;
    }
    int main()
    {
        ListNode *p;
        ListNode* L=NULL;
        Insert(L,1);
        Insert(L,2);
        Insert(L,3);
        Insert(L,4);
        Print(L);
        p=FindKthTotail(L,4);
        cout<<p->m_nValue<<endl;
        return 0;
    }

