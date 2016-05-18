---
title: 数组中出现次数超过一半的数字
date: 2016-05-02 20:31:42
tags:
---

    #include <iostream>
    
    using namespace std;
    //是不是有效输入
    bool IsValidMatrix(int * matrix,int length){
        if(matrix==NULL||length<=0)
            return false;
        return  true;
    }
    //如果出现次数最多的也不能达到数组长度的一半怎么办呢
    bool IsMoreThanHalf(int* matrix,int length,int number){//number 是数组中出现次数最大的那个数
        int countt=0;
        for(int i=0;i<length;i++){
            if(matrix[i]==number)
                countt++;
        }
        if(countt*2<length)
            return false;
        return true;
    }
    int MoreThanHalfNum(int *matrix,int length){
        if(IsValidMatrix(matrix,length)){
            int MaxNumber=matrix[0];
            int times=1;
            for(int i=1;i<length;i++){//此后的数字相同的加1，不同的减1，直到times变成0，从下一个数字开始重头开始这个过程。
                if(times==0){
                    MaxNumber=matrix[i];//重新开始  1,2,2
                    times=1;
                }
               else if(MaxNumber==matrix[i])
                    times++;
                else{
    
                    times--;
                }
            }
            if(IsMoreThanHalf(matrix,length,MaxNumber)){
    
                return MaxNumber;
            }
    
    
            else
                cout<<"无效";
        }
    
    }
    int main()
    {
        int a[]={1};
        cout<<MoreThanHalfNum(a,1);
        return 0;
    }

