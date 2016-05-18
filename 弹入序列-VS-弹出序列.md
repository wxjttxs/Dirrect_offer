---
title: 弹入序列 VS 弹出序列
date: 2016-04-30 15:26:15
tags:
---

    //给定输入序列，判断给定的输出序列是不是真的
    #include <iostream>
    #include<stack>
    using namespace std;
    
     bool IsPopOrder(const int* pPush, const int* pPop, int length){
        bool flag=false;
        if(pPush !=NULL  && pPop!=NULL && length>0){
            stack<int> stackData;//存取输入数据的栈,辅助栈
            const int* pNextPush=pPush;
            const int* pNextPop=pPop;
            while(pNextPop-pPop< length){
                while(stackData.empty()|| stackData.top()!=*pNextPop){//辅助栈的元素不等于
                    if(pNextPush-pPush==length)
                        break;
                    stackData.push(*pNextPush);
                    pNextPush++;
                }
                if(stackData.top()!=*pNextPop)//找到最后也没有在 输入栈的栈顶元素找到输出栈的下一个元素,说明输出序列与输入不匹配
                    break;
                stackData.pop();//找到匹配的元素
                pNextPop++;
            }
            if(stackData.empty() && (pNextPop-pPop)==length)
                flag=true;
    
        }
        return flag;
     }
    int main()
    {
        const int push[]={1,2,3,4,5};
        const int pop[]={4,5,3,2,1};
        cout<<IsPopOrder(push,pop,5);
        return 0;
    }

