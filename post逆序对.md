---
title: 逆序对
date: 2016-05-07 17:00:04
tags:
---
//一个数组中的元素构成的逆序对数目
//分治法，递归，类似于堆排序

    #include <iostream>
    
    using namespace std;
    int InversePairsCore(int* data, int* cpy,int start, int endd){
        if(start==endd){
            cpy[start]=data[start];
            return 0;
        }
        int half_len=(endd-start)/2;
        int left=InversePairsCore(cpy,data,start,start+half_len);//子数组内部构成的逆序对,有两步操作：1是统计逆序对数目；2是排序（方便计算子数组间的逆序数数目）
        int right=InversePairsCore(cpy,data,start+half_len+1,endd);//注意前两个参数的顺序。第一个参数代表的是排好序的数组。
    
        int i=start+half_len;//子数组之间的逆序对,子数组是有序的
        int j=endd;
        int cpyIndex=endd;
        int countt=0;
        while(i>=start && j>=start+half_len+1){
             if(data[i]>data[j]){
                cpy[cpyIndex--]=data[i--];//从右往左，从大往小放进辅助数组中
                countt+=j-start-half_len;//j代表的右边子数组中大的那个数字,所以它之前的数字均能与左边子数组构成逆序对
             }
             else{
                cpy[cpyIndex--]=data[j--];
             }
        }
        for(;i>=start;i--){//j到头了，终止退出循环
            cpy[cpyIndex--]=data[i];
        }
        for(;j>=start+half_len+1;j--)
            cpy[cpyIndex--]=data[j];
        return left+right+countt;
    }
    int InversePairs(int *data,int length){
        if(data==NULL||length<=0)
            return 0;
        int *cpy=new int [length];//辅助数组
        for(int i=0;i<length;i++){
            cpy[i]=data[i];
        }
        int countt=InversePairsCore(data,cpy,0,length-1);
        delete[] cpy;
        return countt;
    }
    int main()
    {
        int a[]={7,5,6,4};
        cout << InversePairs(a,4)<< endl;
        return 0;
    }

