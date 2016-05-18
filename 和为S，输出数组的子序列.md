---
title: 和为S，输出数组的子序列
date: 2016-05-09 10:57:04
tags:
---

    //数组已经排好序，假设升序。
    //当给定和为S,返回数组中两个数使得他们和为s
    
    
    #include <iostream>
    
    using namespace std;
    //找到排序数组和为S的两个数
    //void FindNumbersWithSum(int *data,int length,int s){
    //    bool flag=false;
    //    if(data==NULL ||length<1)
    //        return;
    //    int ahead=0;
    //    int behind=length-1;
    //    while(ahead<behind){
    //        if(data[ahead]+data[behind]==s){
    //            flag=true;
    //            break;//找到就跳出循环，不然就死了
    //        }
    //        else if(data[ahead]+data[behind]>s)
    //            behind--;
    //        else
    //            ahead++;
    //    }
    //    if(flag){
    //        cout<<data[ahead]<<" "<<data[behind];
    //    }
    //    else
    //        cout<<"not found"<<endl;
    //}
    //************拓展*********************************8
    //找到连续正数序列（1,2,3.。。。。S）中和为S的序列，打印出来,至少为3
    void PrintContinueSequence(int small, int big){
        for(int i=small;i<=big;i++)
            cout<<i<<" ";
        cout<<endl;
    }
    void FindContinueSequence(int sum){
        if(sum<3)
            return ;
        int small=1;
        int big=2;
        int mid=(sum+1)/2;//因为是递增，所以最小的数不可能超过中间值
        int curSum=small+big;
        while(small<mid){
            if(curSum==sum){
                PrintContinueSequence(small,big);
            }
            while(curSum>sum && small<mid){
                curSum-=small;//先减去已经在里面的小的数值
                small++;
    
                if(curSum==sum)
                    PrintContinueSequence(small,big);
            }
            big++;
            curSum+=big;//后加上不在里面的大的数值
        }
    }
    int main()
    {
    //    int data[]={1,2,3,7,11,15};
    //    FindNumbersWithSum(data,6,1);
          FindContinueSequence(13);
        return 0;
    }


